# C# 12

## Version requirements

C# 12 is supported on .NET 8, using the .NET 8 SDK or a later compatible SDK. This support baseline is distinct from individual features' runtime dependencies. See [language version configuration](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version).

## Primary constructors

[Constructor reference](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/instance-constructors): Classes and structs accept primary constructor parameters; unlike records, they do not automatically expose them as properties.

```csharp
class Person(string name)
{
    public string Name => name;
}
```

## Collection expressions

[Collection expression reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/collection-expressions): Create a target-typed collection with `[]`; spread elements with `..`.

```csharp
int[] first = [1, 2];
int[] all = [..first, 3];
```

## ref readonly parameters

[Specification](https://github.com/dotnet/csharplang/blob/main/proposals/csharp-12.0/ref-readonly-parameters.md): Accept a read-only reference; pass a variable with `in` or `ref`.

```csharp
int value = 42;
int result = Read(in value);

static int Read(ref readonly int value) => value;
```

## Default lambda parameters

[Lambda reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions): Lambda parameters can have default values.

```csharp
var increment = (int value = 1) => value + 1;
int result = increment(); // 2
```

## Type aliases

[Using directive reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive): Alias types such as tuples and arrays.

```csharp
using Point = (int X, int Y);
using Numbers = int[];

Point origin = (0, 0);
Numbers values = [1, 2];
```

## Inline arrays

[Specification](https://github.com/dotnet/csharplang/blob/main/proposals/csharp-12.0/inline-arrays.md): Store a fixed-length inline buffer in a struct. Requires .NET 8 runtime support.

```csharp
using System.Runtime.CompilerServices;

var buffer = new Buffer();
buffer[0] = 42;

[InlineArray(4)]
struct Buffer
{
    private int _element0;
}
```

## Experimental diagnostics

[Specification](https://github.com/dotnet/csharplang/blob/main/proposals/csharp-12.0/experimental-attribute.md): Mark an API so its use produces the specified diagnostic. The attribute is supplied by .NET 8.

```csharp
using System.Diagnostics.CodeAnalysis;

[Experimental("DEMO001")]
class PreviewApi { }
```

## Source and exclusions

Source: [What's new in C# 12](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12)

Excluded content types: bug fixes, performance optimization reports, contributor information, installation instructions, unrelated tooling or configuration changes, and .NET runtime/API release details belonging in separate runtime summaries. Interceptors are excluded because they were experimental preview functionality, not a stable C# 12 feature.
