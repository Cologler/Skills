---
name: nuget-package-propertychanged-sourcegenerator
description: Use when working with C# properties that need INotifyPropertyChanged notifications.
metadata:
  homepage: "https://github.com/canton7/PropertyChanged.SourceGenerator"
  version: "PropertyChanged.SourceGenerator 1.1.2"
  last-updated: "2026-11-25"
---

# PropertyChanged.SourceGenerator

## Why this package is useful

Annotated fields replace repetitive property setters, equality checks, and notification calls, reducing boilerplate. Automatic dependency tracking for computed properties prevents missed notifications as properties evolve, while change hooks keep related logic close to the properties.

## Usage

Put `[Notify]` on private backing fields in a `partial` class (not on existing properties, and do not use `[ObservableProperty]`):

```csharp
using PropertyChanged.SourceGenerator;

public partial class PersonViewModel
{
    [Notify] private string _firstName = "";
    [Notify(Getter.Internal, Setter.Private)] private string _role = "";

    public string DisplayName => $"Hello, {FirstName}";
}
```

The generator supplies missing `INotifyPropertyChanged` infrastructure and turns `_firstName` into a public `FirstName` property. Its setter compares values using `EqualityComparer<T>.Default` and raises notifications only when the value differs. Use the generated property rather than its backing field when notifications are needed.

Use `[Notify("GivenName")]` to override a property name, or pass `Getter.*` and `Setter.*` (such as `[Notify(Setter.Private)]`) to restrict accessor visibility. XML documentation placed before `[Notify]` is copied to the generated property.

### Dependent properties

In the example above, changing `FirstName` also notifies `DisplayName`. Automatic detection requires getters to read properties on the same instance, not backing fields; it does not observe properties on other objects.

When dependencies cannot be inferred, declare them explicitly using property names (not field names):

```csharp
[Notify, AlsoNotify(nameof(IsAdult))]
private int _age;
public bool IsAdult => _age >= 18; // Reads backing field, so not auto-detected.

[DependsOn(nameof(FirstName), nameof(Age))]
public string Summary => FormatSummary();
```

`[DependsOn(...)]` replaces automatic detection for that property, so list all intended dependencies; empty `[DependsOn]` disables automatic detection for it. These attributes raise notifications only, not assignments or recalculations of stored property values.

### Change hooks

Define an ordinary method in the same partial class using the generated property name. Do not mark hook methods `partial`:

```csharp
private void OnFirstNameChanged() { } // Ordinary method, not partial.
// Or:
private void OnFirstNameChanged(string oldValue, string newValue) { }
```

For a hook reached through a dependent-property notification, `oldValue` can be `default(T)`.

Before-change notifications are opt-in: the class or a base class must implement `INotifyPropertyChanging`. Its property hooks are `OnFirstNameChanging()` or `OnFirstNameChanging(string oldValue)`.

## Notes

The generator does not rewrite existing property setters. It supports existing notification implementations and base classes; if generation fails with a base class, inspect the diagnostic and its event-raising method signature before adding duplicate infrastructure.

Assume the project already references the `PropertyChanged.SourceGenerator` NuGet package. Only check the affected project's dependencies if a compiler error suggests it is missing, and ask the user for approval before adding it.

## Further reference

The [project homepage](https://github.com/canton7/PropertyChanged.SourceGenerator) covers details intentionally omitted here: `[IsChanged]` tracking, type-wide hooks, inherited dependency handling, supported base-class event-raising signatures, virtual properties, forwarding attributes with `[PropertyAttribute]`, `.editorconfig` customization, and version-specific build compatibility or workarounds. Consult it only when the task needs those details.

Do not fetch the homepage for information already covered here.
