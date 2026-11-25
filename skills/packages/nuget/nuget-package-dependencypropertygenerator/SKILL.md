---
name: nuget-package-dependencypropertygenerator
description: Use when working with C# dependency properties or attached properties in UI controls.
metadata:
  homepage: "https://github.com/HavenDV/DependencyPropertyGenerator"
  version: "DependencyPropertyGenerator 1.5.1"
  last-updated: "2026-11-25"
  generated-by: "gpt-6.1-terra"
---

# DependencyPropertyGenerator

## Why this package is useful

Attributes replace handwritten dependency-property registration fields, CLR wrappers or attached accessors, and change-callback plumbing with a single declaration. This keeps property declarations shorter and easier to read, and prevents mismatches between property names, value types, owner types, and callbacks that might otherwise fail only at runtime.

## Usage

Apply the attribute to a `partial` control class. This WPF example generates `IsSpinningProperty` and the `IsSpinning` CLR property:

```csharp
using DependencyPropertyGenerator;
using System.Windows.Controls;

[DependencyProperty<bool>("IsSpinning", DefaultValue = true)]
public partial class Spinner : UserControl
{
}
```

Do not redeclare the generated members. Use `DefaultValue` for attribute-compatible constants. Optionally implement `OnIsSpinningChanged` as a partial method accepting no arguments, the new value, or both old and new values. `Description` supplies property documentation and a `Description` attribute; `Category` supplies design-time categorization.

### Attached properties

Apply `AttachedDependencyProperty<TValue, TTarget>` to a static partial owner class. For example, in WPF:

```csharp
using DependencyPropertyGenerator;
using System.Windows.Controls;

[AttachedDependencyProperty<object, TreeView>("SelectedItem",
    DefaultBindingMode = DefaultBindingMode.TwoWay)]
public static partial class TreeViewExtensions
{
    static partial void OnSelectedItemChanged(TreeView sender, object? oldValue, object? newValue)
    {
        // Synchronize selection here if the control's selection must follow this property.
    }
}
```

This generates `SelectedItemProperty`, `GetSelectedItem`, and `SetSelectedItem`. An optional change callback must be static and match a generated signature, including the target type and nullability. The generated property does not synchronize the control's selection by itself; add application logic if needed.

## Notes

The package supports WPF, UWP, WinUI, Uno, Avalonia, and MAUI; property APIs and options vary by platform.

Assume the project already references the `DependencyPropertyGenerator` NuGet package. Only check the affected project's dependencies if a compiler error suggests it is missing, and ask the user for approval before adding it.

## Further reference

The [project homepage](https://github.com/HavenDV/DependencyPropertyGenerator) and its linked source cover details intentionally omitted here, including `DefaultValueExpression`, raw XML documentation, platform detection, event binding, metadata overrides, and additional property and event attributes. Consult them only when those features or platform-specific signatures are needed.

Do not fetch the homepage for information already covered here.
