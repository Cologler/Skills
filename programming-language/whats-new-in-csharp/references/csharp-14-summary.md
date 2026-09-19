# C# 14

## Version requirements

C# 14 is supported on .NET 10, using the .NET 10 SDK or a later compatible SDK. Using a language version newer than the target framework's supported version is unsupported; this does not mean every feature requires new runtime behavior. See [language version configuration](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version).

## Extension members

[Specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-14.0/extensions): Extension blocks support instance and static methods, properties, and static operators.

```csharp
public static class TextExtensions
{
    extension(string text)
    {
        public bool IsBlank => string.IsNullOrWhiteSpace(text);
        public string Quoted() => $"\"{text}\"";
    }

    extension(string)
    {
        public static string Blank => "";
    }
}
```

Use `" ".IsBlank`, `"hello".Quoted()`, and `string.Blank`.

## Field-backed properties

[`field` reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/field): Access the compiler-generated backing field inside property accessors.

```csharp
class Person
{
    public string Name
    {
        get;
        set => field = value.Trim();
    } = "";
}
```

## Implicit span conversions

[Specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-14.0/first-class-span-types): Span conversions participate in generic inference and extension receiver matching.

```csharp
using System;

int[] values = [1, 2];
int first = values.First();

static class SpanExtensions
{
    public static T First<T>(this ReadOnlySpan<T> values) => values[0];
}
```

Conversions require the corresponding runtime-library helpers; missing helpers cause compilation errors.

## Unbound generics in nameof

[`nameof` reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/nameof): Accept an unbound generic type.

```csharp
using System.Collections.Generic;

string name = nameof(List<>); // "List"
```

## Lambda parameter modifiers

[Lambda reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions): Use parameter modifiers without explicit parameter types. `params` still requires explicit types.

```csharp
TryParse parse = (text, out value) => int.TryParse(text, out value);

delegate bool TryParse(string text, out int value);
```

## Partial constructors and events

[Partial member reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/partial-member): Supply one defining and one implementing declaration. Event implementations require `add` and `remove`.

```csharp
using System;

partial class Counter
{
    public partial Counter();
    public partial event Action Changed;
}

partial class Counter
{
    private Action? _changed;

    public partial Counter() { }
    public partial event Action Changed
    {
        add => _changed += value;
        remove => _changed -= value;
    }
}
```

## Instance assignment and increment operators

[Specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-14.0/user-defined-compound-assignment): Define mutating compound assignment and increment/decrement operators as instance methods returning `void`.

```csharp
class Counter
{
    public int Value;
    public void operator +=(int amount) => Value += amount;
    public void operator ++() => Value++;
}
```

## Null-conditional assignment

[Specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-14.0/null-conditional-assignment): Assign through `?.` or `?[]`; the right side is skipped for a null receiver. Compound assignments work; `++` and `--` do not.

```csharp
int[]? values = null;
values?[0] = 42;
```

## File-based app directives

[File-based app reference](https://learn.microsoft.com/en-us/dotnet/core/sdk/file-based-apps): Source directives select SDK, properties, packages, or project references. Requires the .NET 10 SDK or later.

```csharp
#:property TargetFramework=net10.0

System.Console.WriteLine("Hello");
```

## Source and exclusions

Source: [What's new in C# 14](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-14)

Excluded content types: bug fixes, performance optimization reports, contributor information, installation instructions, unrelated tooling or configuration changes, and .NET runtime/API release details belonging in separate runtime summaries.
