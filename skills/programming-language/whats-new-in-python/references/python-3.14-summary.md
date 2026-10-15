# Python 3.14

## Template strings

[PEP 750](https://peps.python.org/pep-0750/): `t`-strings produce a `Template` preserving text and interpolations for custom processing.

```python
name = "Alice"
template = t"Hello, {name}!"
```

## Deferred annotations

[PEP 649](https://peps.python.org/pep-0649/) and [PEP 749](https://peps.python.org/pep-0749/): Annotations are evaluated on demand; forward references need no quotes.

```python
def make() -> Item:
    return Item()

class Item: ...
```

## Exception types without parentheses

[PEP 758](https://peps.python.org/pep-0758/): Parentheses are optional for multiple types in `except` and `except*`, unless using `as`.

```python
try:
    int("invalid")
except ValueError, TypeError:
    pass

try:
    raise ExceptionGroup("errors", [ValueError()])
except* ValueError, TypeError:
    pass
```

## Unpacking type aliases

[Type alias documentation](https://docs.python.org/3.14/library/typing.html#typing.TypeAliasType): Unpack a tuple type alias with `*`.

```python
type Pair = tuple[int, str]
type Extended = tuple[bool, *Pair]
```

## Generic memoryview

`memoryview` accepts an element type annotation.

```python
data: memoryview[int] = memoryview(b"abc")
```

## Reader and Writer protocols

[I/O typing documentation](https://docs.python.org/3.14/library/io.html#static-typing): Annotate streams by their read or write interface.

```python
from io import Reader, Writer

def copy_text(source: Reader[str], target: Writer[str]) -> None:
    target.write(source.read())
```

## Union runtime checks

[Union documentation](https://docs.python.org/3.14/library/typing.html#typing.Union): Both union spellings share one runtime type; `Union` supports `isinstance`.

```python
from typing import Union

isinstance(int | str, Union)  # True
```

## Fractional digit grouping

[Format specification documentation](https://docs.python.org/3.14/library/string.html#format-specification-mini-language): Group fractional digits.

```python
text = f"{0.123456:.6_f}"  # '0.123_456'
```

## Source and exclusions

Source: [What's New in Python 3.14](https://docs.python.org/3.14/whatsnew/3.14.html)

Excluded content types: bug fixes, performance improvements, contributor information, and unrelated standard-library, tooling, configuration, or C API changes.
