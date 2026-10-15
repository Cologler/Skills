---
name: nuget-package-dependencypropertygenerator
description: Use when simplifying dependency-property or attached-property code in C# UI controls and improving its readability with DependencyPropertyGenerator.
metadata:
  homepage: "https://github.com/HavenDV/DependencyPropertyGenerator"
  version: "DependencyPropertyGenerator 1.5.1"
  last-updated: "2026-10-16"
  generated-by: "gpt-6"
---

# DependencyPropertyGenerator

## Prerequisite

For a project-local skill, inspect every project in the consuming repository or solution for `DependencyPropertyGenerator`, including imported package references and resolved dependencies. A central `PackageVersion` entry alone does not prove installation. If no project references it, ask whether to install the package or remove this skill, and wait for the user's choice. Only if installation is chosen, run `dotnet add <project.csproj> package DependencyPropertyGenerator`. This check does not apply to the skill catalog itself.

## When and why

Use this source generator to simplify dependency-property and attached-property code and improve readability. Concise attributes replace handwritten registration fields, CLR wrappers or attached accessors, and change-callback plumbing, making property names, types, defaults, and options easier to read.

The package supports WPF, UWP, WinUI, Uno, Avalonia, and MAUI. The examples below target WPF and C# 11 or later, which supports generic attributes without preview mode. Inspect the consuming project's language version and UI framework before adapting them; platform-specific property APIs and options differ. Non-generic attributes are also available for older language versions.

## Ordinary dependency property

Apply the attribute to a `partial` control class, not to a manually declared property:

```csharp
using DependencyPropertyGenerator;
using System.Windows.Controls;

[DependencyProperty<bool>("IsSpinning", DefaultValue = true)]
public partial class Spinner : UserControl
{
    partial void OnIsSpinningChanged(bool oldValue, bool newValue)
    {
        // React here so changes made through bindings also reach this behavior.
    }
}
```

This generates `IsSpinningProperty` and the `IsSpinning` CLR property. Do not redeclare them. The change callback is optional; implement the generated overload accepting no arguments, the new value, or both old and new values as needed.

Use `DefaultValue` for attribute-compatible constants. `Description` supplies both property documentation and a `Description` attribute; `Category` supplies design-time categorization.

## Attached property

Use a static partial owner class. The generic arguments below are the property value type and the target control type:

```csharp
using DependencyPropertyGenerator;
using System.Windows.Controls;

#nullable enable

[AttachedDependencyProperty<object, TreeView>("SelectedItem",
    DefaultBindingMode = DefaultBindingMode.TwoWay)]
public static partial class TreeViewExtensions
{
    static partial void OnSelectedItemChanged(
        TreeView sender, object? oldValue, object? newValue)
    {
        // Implement selection synchronization here if the behavior requires it.
    }
}
```

This generates `SelectedItemProperty`, `GetSelectedItem`, and `SetSelectedItem`. The attribute creates property storage and callbacks; synchronizing it with the control's actual selection still requires application logic. Match the generated callback signature, including `static`, the sender type, and nullability.

## Further reference

The [project homepage](https://github.com/HavenDV/DependencyPropertyGenerator) and its linked source cover details intentionally omitted here: `DefaultValueExpression`, raw XML documentation, platform detection, event binding, metadata overrides, and additional property and event attributes. Consult them only when the task needs those features or platform-specific signatures. For language compatibility, see Microsoft's [C# 11 generic attributes documentation](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-11#generic-attributes).

Do not fetch the homepage for information already covered here.
