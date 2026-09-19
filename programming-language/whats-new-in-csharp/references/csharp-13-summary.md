# C# 13

## Version requirements

C# 13 is supported on .NET 9, using the .NET 9 SDK or a later compatible SDK. This support baseline is distinct from individual features' runtime dependencies. See [language version configuration](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version).

## params collections

[Parameter reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/method-parameters#params-modifier): `params` accepts supported collection types, including spans.

```csharp
using System;

int count = Count(1, 2, 3);

static int Count(params ReadOnlySpan<int> values) => values.Length;
```

## Lock-aware locking

[`lock` reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/lock): A statically typed `System.Threading.Lock` uses scope-based locking. Requires the .NET 9 `Lock` API.

```csharp
using System.Threading;

class Counter
{
    private readonly Lock _gate = new();
    private int _value;

    public void Increment()
    {
        lock (_gate) { _value++; }
    }
}
```

## Escape character

[Character reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/char): `\e` represents U+001B.

```csharp
char escape = '\e';
```

## Method group natural types

[Specification](https://github.com/dotnet/csharplang/blob/main/proposals/csharp-13.0/method-group-natural-type-improvements.md): Discard inapplicable generic candidates when inferring a method group's delegate type.

```csharp
var action = new Printer().Print; // Action<int>

class Printer
{
    public void Print(int value) { }
    public void Print<T>(T value) { }
}
```

## From-end indices in initializers

[What's New reference](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-13#implicit-index-access): Use `^` in nested collection initializers.

```csharp
var data = new Data { Values = { [^1] = 42 } };

class Data
{
    public int[] Values { get; } = new int[3];
}
```

## Ref locals in async methods and iterators

[Ref struct reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/ref-struct): Ref locals and ref structs are permitted but cannot remain in use across `await` or `yield return`. Iterators may contain unsafe blocks; `yield` must remain in a safe context.

```csharp
using System;
using System.Threading.Tasks;

static async Task<int> ReadAsync(int[] values)
{
    await Task.Yield();
    Span<int> span = values;
    ref int first = ref span[0];
    return first;
}
```

## Ref struct interfaces and generic arguments

[Specification](https://github.com/dotnet/csharplang/blob/main/proposals/csharp-13.0/ref-struct-interfaces.md): Ref structs can implement interfaces without boxing. `allows ref struct` permits ref struct generic arguments and requires .NET 9 runtime support.

```csharp
static int Read<T>(T value) where T : IValue, allows ref struct
    => value.Get();

interface IValue { int Get(); }

ref struct Value : IValue
{
    public int Get() => 42;
}
```

## Partial properties and indexers

[Partial member reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/partial-member): Pair a defining declaration with an implementation containing accessor bodies.

```csharp
partial class Data
{
    public partial int Count { get; }
    public partial int this[int index] { get; }
}

partial class Data
{
    public partial int Count => 3;
    public partial int this[int index] => index;
}
```

## Overload resolution priority

[Attribute reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/attributes/general#overloadresolutionpriority-attribute): Prefer applicable overloads with higher priority. The attribute is supplied by .NET 9.

```csharp
using System.Runtime.CompilerServices;

class Picker
{
    [OverloadResolutionPriority(1)]
    public static string Pick(object value) => "object";
    public static string Pick(string value) => "string";
}
```

`Picker.Pick("hello")` selects the `object` overload.

## Source and exclusions

Source: [What's new in C# 13](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-13)

Excluded content types: bug fixes, performance optimization reports, contributor information, installation instructions, unrelated tooling or configuration changes, and .NET runtime/API release details belonging in separate runtime summaries. The preview `field` keyword is omitted here; its stable form is covered in [C# 14](csharp-14-summary.md).
