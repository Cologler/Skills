---
name: nuget-package-injectio
description: Use when registering C# services, modules, or decorators with Microsoft.Extensions.DependencyInjection (IServiceCollection), or when modifying existing Injectio registrations.
metadata:
  homepage: "https://github.com/loresoft/Injectio"
  version: "Injectio 6.3.0"
  last-updated: "2026-11-25"
---

# Injectio

## Why this package is useful

Attributes replace centralized `IServiceCollection` registration lists and runtime assembly scanning. Keeping lifetime and service-contract declarations directly on implementations prevents forgotten or out-of-sync registrations as services evolve, while compile-time generation avoids runtime reflection overhead.

## Usage

Annotate service classes with `[RegisterSingleton]`, `[RegisterScoped]`, or `[RegisterTransient]`. Service classes do not need to be `partial`:

```csharp
using Injectio.Attributes;

[RegisterScoped<IOrderService>]
public class OrderService : IOrderService { }

[RegisterSingleton(
    Registration = RegistrationStrategy.ImplementedInterfaces,
    Duplicate = DuplicateStrategy.Append)]
public class AuditHandler : IOrderHandler { }
```

Use `[Register*<TService>]` (or `ServiceType = typeof(TService)`) to target a specific service contract, or set `Registration` to `Self`, `ImplementedInterfaces`, or `SelfWithInterfaces`. Set `Duplicate` to `Skip` (default), `Replace`, or `Append` (needed for multiple implementations resolved via `IEnumerable<T>`).

Call the generated `IServiceCollection` extension method at startup. By default, its name is `Add<AssemblyName>` with dots removed (for example, `MyCompany.MyApp` generates `AddMyCompanyMyApp`):

```csharp
using Microsoft.Extensions.DependencyInjection;

builder.Services.AddMyCompanyMyApp();
```

### Registration modules

Use `[RegisterServices]` on a `public static` method when registrations require manual logic such as options binding or third-party setup:

```csharp
using Injectio.Attributes;
using Microsoft.Extensions.DependencyInjection;

public static class PersistenceModule
{
    [RegisterServices]
    public static void Register(IServiceCollection services)
    {
        services.AddHttpClient<IPaymentGateway, PaymentGateway>();
    }
}
```

### Keyed services, factories, and decorators

Use `ServiceKey` for .NET keyed services, `Factory` for custom static construction, and `[RegisterDecorator<TService>]` to wrap an existing registration (decorators inherit the wrapped service's lifetime):

```csharp
using Injectio.Attributes;

[RegisterSingleton<ICache>(ServiceKey = "Redis", Factory = nameof(Create))]
public class RedisCache : ICache
{
    public static ICache Create(IServiceProvider sp, object? serviceKey) => new RedisCache();
}

[RegisterDecorator<IOrderService>(Order = 1)] // Lower Order wraps closer to the inner service.
public class LoggingOrderService(IOrderService inner) : IOrderService { }
```

## Notes

Each assembly using Injectio generates its own `Add<AssemblyName>()` method, so the composition root must call the generated method for each relevant assembly. Services can also be filtered at registration time with `Tags = "Client,FrontEnd"` and `services.AddMyCompanyMyApp("Client")` (passing no tags registers all services).

Assume the project already references the `Injectio` NuGet package. Only check the affected project's dependencies if a compiler error suggests it is missing, and ask the user for approval before adding it.

## Further reference

The [project homepage](https://github.com/loresoft/Injectio) covers details intentionally omitted here, including assembly-level registration attributes, `<InjectioName>` MSBuild customization, `IHostApplicationBuilder` and tag-aware `[RegisterServices]` signatures, `ImplementationType`, and open-generic registration rules. Consult it only when those features are needed.

Do not fetch the homepage for information already covered here.
