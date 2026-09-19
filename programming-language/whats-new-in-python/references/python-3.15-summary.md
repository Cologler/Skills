# Python 3.15

## Lazy imports

[PEP 810](https://peps.python.org/pep-0810/): Defer module loading until first use. Module scope only; not inside `try` blocks or with star/future imports.

```python
lazy import json
lazy from pathlib import Path

data = json.loads("{}")
path = Path(".")
```

## Unpacking in comprehensions

[PEP 798](https://peps.python.org/pep-0798/): Unpack items in comprehensions and generator expressions.

```python
groups = [[1, 2], [3]]
flat = [*group for group in groups]
unique = {*group for group in groups}
items = (*group for group in groups)
merged = {**mapping for mapping in [{"a": 1}, {"b": 2}]}
```

## frozendict

[PEP 814](https://peps.python.org/pep-0814/): An immutable dictionary.

```python
settings = frozendict(mode="strict")
```

## sentinel

[PEP 661](https://peps.python.org/pep-0661/): Create a unique sentinel, also usable in type annotations.

```python
MISSING = sentinel("MISSING")

def resolve(value: int | MISSING = MISSING) -> int:
    return 0 if value is MISSING else value
```

## TypedDict extra items

[PEP 728](https://peps.python.org/pep-0728/): `closed=True` forbids extra keys; `extra_items` specifies their value type.

```python
from typing import TypedDict

class Point(TypedDict, closed=True):
    x: int

class Scores(TypedDict, extra_items=int):
    name: str
```

## TypeForm

[PEP 747](https://peps.python.org/pep-0747/): Annotate values that represent type expressions.

```python
from typing import TypeForm

value_type: TypeForm[int | str] = int | str
```

## Disjoint bases

[PEP 800](https://peps.python.org/pep-0800/): Type checkers reject multiple inheritance from unrelated disjoint bases.

```python
from typing import disjoint_base

@disjoint_base
class A: ...

@disjoint_base
class B: ...

class C(A, B): ...  # Type checker error.
```

## Source and exclusions

Source: [What's New in Python 3.15](https://docs.python.org/3.15/whatsnew/3.15.html)

Excluded content types: bug fixes, performance improvements, contributor information, and unrelated standard-library, tooling, configuration, or C API changes.
