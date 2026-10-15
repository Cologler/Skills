---
name: nuget-package-propertychanged-sourcegenerator
description: Use when simplifying C# view-model property-change notification code, keeping computed properties updated, or reacting to property changes with PropertyChanged.SourceGenerator.
metadata:
  homepage: "https://github.com/canton7/PropertyChanged.SourceGenerator"
  version: "PropertyChanged.SourceGenerator 1.1.2"
  last-updated: "2026-10-16"
  generated-by: "gpt-6"
---

# PropertyChanged.SourceGenerator

## Prerequisite

For a project-local skill, inspect every project in the consuming repository or solution for `PropertyChanged.SourceGenerator`, including imported package references and resolved dependencies. A central `PackageVersion` entry alone does not prove installation. If no project references it, ask whether to install the package or remove this skill, and wait for the user's choice. Only if installation is chosen, run `dotnet add <project.csproj> package PropertyChanged.SourceGenerator`. This check does not apply to the skill catalog itself.

## When and why

Use this source generator to simplify `INotifyPropertyChanged` boilerplate and improve readability in C# view models, with or without an MVVM framework. Annotated fields replace repetitive property setters, equality checks, and notification calls; dependency declarations and hooks keep related behavior close to the property definitions.

The generator adds source code during compilation; it does not rewrite existing property setters. Version 1.1.x requires Visual Studio 2022 17.3 or .NET SDK 6.0.304 or later to build, without requiring the application to target .NET 6.

## Generate notifying properties

Use a `partial` class and put `[Notify]` on backing fields:

```csharp
using PropertyChanged.SourceGenerator;

public partial class PersonViewModel
{
    [Notify] private string _firstName = "";
    [Notify] private string _lastName = "";

    public string FullName => $"{FirstName} {LastName}";

    public void Rename(string firstName, string lastName)
    {
        // Use the generated setters so bindings and dependent properties are notified.
        FirstName = firstName;
        LastName = lastName;
    }
}
```

By default, `_firstName` becomes a public `FirstName` property with public accessors. Its setter compares values using `EqualityComparer<T>.Default` and raises notifications only when the value differs. The generator supplies missing `INotifyPropertyChanged` infrastructure. Do not redeclare generated properties or write directly to their backing fields when notifications are required.

Use `[Notify("DisplayName")]` to override a property name, or `[Notify(Setter.Private)]` to restrict its setter. XML documentation placed before `[Notify]` is copied to the generated property.

Existing notification implementations and base classes are supported. When generation fails with an existing base class, inspect the generator diagnostic and its event-raising method signature before adding duplicate infrastructure.

## Dependent properties

In the example, changes to either generated name property also notify `FullName`. Automatic detection requires getters to read properties on the same instance, not backing fields; it does not observe properties on other objects.

When dependencies cannot be inferred, choose the direction that best expresses the relationship:

1. Put `[DependsOn(nameof(FirstName), nameof(LastName))]` on the dependent property, such as `FullName`.
2. Alternatively, put `[Notify, AlsoNotify(nameof(FullName))]` on each source backing field.

Use property names, not field names. `[DependsOn(...)]` replaces automatic detection for that property, so list all intended dependencies; empty `[DependsOn]` disables automatic detection for it. These attributes raise notifications, not assignments or recalculations of stored property values.

## React to changes

Define an ordinary method in the same partial class using the generated property name:

```csharp
using PropertyChanged.SourceGenerator;

public partial class SearchViewModel
{
    [Notify] private string _query = "";
    [Notify(Setter.Private)] private bool _hasResults;

    private void OnQueryChanged(string oldValue, string newValue)
    {
        // Results for the previous query are no longer valid.
        HasResults = false;
    }
}
```

Supported property hooks are `OnQueryChanged()` or `OnQueryChanged(string oldValue, string newValue)`. For a hook reached through a dependent-property notification, the old value can be `default(T)`.

Before-change notifications are opt-in: the class or a base class must implement `INotifyPropertyChanging`. Its property hooks are `OnQueryChanging()` or `OnQueryChanging(string oldValue)`.

## Further reference

The [project homepage](https://github.com/canton7/PropertyChanged.SourceGenerator) covers details intentionally omitted here: `[IsChanged]` tracking, type-wide hooks, inherited dependency handling, supported base-class event-raising signatures, virtual properties, forwarding attributes with `[PropertyAttribute]`, `.editorconfig` customization, and version-specific build compatibility or workarounds. Consult it only when the task needs those details.

Do not fetch the homepage for information already covered here.
