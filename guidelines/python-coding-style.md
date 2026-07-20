---
summary: "Python coding style and formatting guidelines"
---

# Python coding style and formatting guidelines

We aim to follow the style standards most widely shared in the
Python community such as [PEP8][1] and the [Google style guide][2]. 

As we mentioned we follow the standards, we have
exceptions in a few points. In the document below we only discuss these
alterations and additional rules. For general guidelines you can refer to the
[PEP8][1] and the [Google style guide][2].

## Ruff for code linting

Ruff should be used within all python projects for linting. After finishing every function
Ruff should be run the code to ensure that linting is correct and all errors should be fixed.
This should also occur again at the end of a file.

## Names

- Class names should be `PascalCase` (camel case with first letter capital),
  however resource names should be shown like a single word, e.g. a class
  of annotation from Protein Atlas is `ProteinatlasAnnotation`
- Function, method and variable names should follow `snake_case`, resource
  names typically shown as a single word, e.g. a function yielding annotations
  from Protein Atlas should be `proteinatlas_annotations`

## Function Naming

Avoid redundant prefixes in function names. Common prefixes to avoid:

- `get_` - omit when the function simply returns data
- `load_` - omit when the function reads from a file/source
- `parse_` - omit when the function transforms input data
- `create_` - omit when the function constructs an object
- `add_` - consider omitting when the action is implied by context

### Examples

```python
# Avoid
def get_uniprot_locations(): ...
def load_tcdb_locations(): ...
def parse_equation(): ...
def create_node_mappings(): ...

# Prefer
def uniprot_locations(): ...
def tcdb_locations(): ...
def equation(): ...
def node_mappings(): ...
```

Exceptions: Keep prefixes when they disambiguate or add meaning:

```python
# Keep: 'strip' describes the transformation
def strip_prefix(): ...

# Keep: distinguishes from related function
def add_reverse(): ...  # if there's also remove_reverse()
```

## Function Length

All functions should be shorter than 50 lines.

## Blank lines

Vertical empty space does not cost anything and helps a lot with readability.
We use it extensively. Between, before and after methods and classes we leave
2 empty lines. Before and after blocks we leave an empty line. Inside blocks
we add blank lines between short segments of logically strongly connected
elements (usually one or a few lines).

```python

def function1(a = 1, b = 2):

    a = a + 1
    b = b - 1

    return a * b


def function2(a, b):

    for i in a:

        if i // b:

            yield i

```

## Indentation of argument lists

If the list of arguments or anything inside parentheses needs to be broken to
multiple lines we start newline after the opening parenthese and each element
should have its own line one level deeper indented than the opening line.
We add commas after each element including the last one, except if it is
`**kwargs` because comma after `**kwargs` is syntax error in Python 2.
If the elements are statements separated by operators (e.g. `+` or `and`)
we leave the operator at the end of the line and start the next statement
in a new line. The closing parenthesis returns to the upper indentation level
and left hanging in its own line.

```python

a = function(
    foo = 'foo',
    bar = 'bar',
    baz = 'baz',
)

a = function(
    foo = 'foo',
    bar = 'bar',
    **kwargs
)

if (
    condition1 and
    condition2
):

    do_something()

```

Anywhere else if the vertical alignment helps readability is good to use line
breaks. For example when similar statements are repeated.

```python

a = (
    record[i],
    record[i + 7],
)

```

## Long comprehensions

If the contents of a list or other comprehension does not fit into one line
or even if it fits but looks better if broken into multiple pieces, we start
the value, each `for` and `if` statements in a new line. The closing
parenthesis has the original indentation level in a new line.

```python

foo = [
    bar
    for bar in baz
    if bar[0]
]

```

## Docstrings

After the triple double quotes the docstring starts in a new line and also
the closing quotes have their own line. For docstrings we follow the
[Napoleon (Google) standard][17].

Thanks to type hints we don't have to add the type of arguments and return
values in parentheses (enough to write `arg:` instead of `arg (int):`).

```python

def function(a: int) -> List[int]:
    """
    Does something.

    Args:
        a: A number. I just make this sentence longer, hopefully
            enough long to show how to make a line break: indent the rest
            of the lines, so the argument name itself sticks out.

    Returns:
        A list of integers. I just make this sentence longer,
        hopefully enough long to show how to make a line break.
    """

    return [a, a + 1, a + 2]

```

## Spaces around operators

Operators never stick to the operands, always surrounded by spaces.
Also there is a space after the comma when listing elements of tuples and
lists within a line.

```python

def function(a = 1):

    a = a * 4 + 3
    a = (1, 2, 3)

```

## Quotes

We use single quotes unless there is any strong reason to use double.

## Imports

We group imports the following way:

- Compatibility imports (e.g. `future.utils.iteritems`; not used any more)
- Standard library imports
- Typing imports
- Imports from other third party dependencies (e.g. `numpy`)
- Imports from our current package itself

Between these sections we leave an empty line

Use lazy imports for heavy dependencies inside functions
rather than at module level. This allows importing lighter parts of the
package without triggering the full dependency chain.

## Data Structures

Return the most appropriate data structure for the use case:

- Use `dict` when data will be used for lookups
- Use `list[tuple]` for pairs/relationships
- Reserve `DataFrame` for tabular data that benefits from pandas operations

```python
# Return dict for lookup tables
def tcdb_locations() -> dict[str, str]:
    df = pd.read_csv(data_path('tcdb_locations.csv'))
    return {loc: abbrev for loc, abbrev in zip(df['location'], df['abbreviation'])}

# Return list of tuples for routes/pairs
def tcdb_routes() -> list[tuple[str, str]]:
    df = pd.read_csv(data_path('tcdb_routes.csv'))
    return [(row['from'], row['to']) for _, row in df.iterrows()]

[1]: https://www.python.org/dev/peps/pep-0008/
[2]: https://github.com/google/styleguide/blob/gh-pages/pyguide.md


