# Python Style Guide (stricter PEP 8 extension)


## About This Document

This style guide is written with respect and appreciation of [PEP 8](https://www.python.org/dev/peps/pep-0008/) and, basically, is it's stricter extension.

Code, formatted according to PEP 8 recommendations and even someone's good sense, is still ugly and unreadable, line-wise diffs might reveal real changes more clearly. This guide is created for those who need more certainty in code style, who frequently ask themselves how to format their code, who strive for perfection in what they produce.

This document contains only difference from PEP 8. Here are only those requirements that are not mentioned there or those that are stricter or more prohibitive.

Key insigts:
- Code is read much more ofter then written. (Cited from PEP 8.)
- Line-wise diffs are always read and represents logical changes.
- The less you think how to format the code the more you think about your task.
- Formatting is checked or even performed automatically.
- Interactive debugging is used sometimes.
- Immutability is blissful.


## Changes and Contibution

This document is subject to revise, refine and improve. It will not change dramatically.

Everyone who thinks that can make this style guide better, please ask, comment and contribute. You're welcomed.


## Style Guide


### Multiline Statements

If statement can be fit into single line, it must be on single line.  
Otherwise, statement must be cautiously written in several lines.  
In rare cases, it's OK to split statement into multiple lines if it's to complex to understand it at first sight.


#### Sequences, Function Calls and Definitions, Class Parents

- All container elements, parameters, arguments and class parents must be written:
   - one per line,
   - followed by comma,
   - indented by 1 level relative to first line of statement.
- First element must be on its separate line, next to first line of statement.
- Do not group several elements on single line.
- Last element must be followed by comma.
- Closing parenthesis, bracket or brace must be
   - on next line to last element
   - with same indent as first line of statement;
   - if needed, it are immediately followed by one or more colon or comma, parenthesis, bracket or brace.

Yes:
```
def foo(  # No parameter on this line
    a,
    b,
    c,  # Trailing comma
):
    pass

foo(  # No parameter on this line
    ['a', 'b'],  # Argument is one-line.
    2,
    3,  # Trailing comma
)

class Foo(  # No parameter on this line
    Bar,
    Baz,
    Booze,  # Trailing comma
):
    pass
```

If statement is multiline and it's not last element of its parent, parent must also be multiline according to rules above.  
If statement is multiline and it is last element of its parent, statement may start on same line as parent and immediately followed without line break by parents closing parenthesis, bracket or brace.

Yes:

```
foo(
    ['a', 'b'],
    (
        'a',
        'b',
        'c',
    ),
    (
        'd',
        'e',
    ),
)
```
```
bar(
    map(int, (
        '1',
        '2',
        '3',
    )),  # Extra Parethesis because map here is not multiine
    4,
    5,
)
```

It's easy for eye to find element looking from top to bottom. Number of elements is simply number of rows.

Think of diffs. With this style, diff are as clear as possible. Otherwise, how would line-wise diff look like if:
- function name were changed,
- new element were added:
   - before first element,
   - after last element,
- there were removed:
   - first element,
   - last element,
- order of elements were changed, including:
   - first element,
   - last element?


#### List Comprehensions

- `for` clause is written on separate line.
- If `in` clause is not trivial or there is not enough space on line, it's written on separate line.
- `if` clause, if presented, is written on separate line.

Yes:
```
odd_apples = (
    fruit
    for index, fruit in enumerate(fruits)
    if index % 2 == 1 and fruit.name.startswith('apple')
)
```
```
even_oranges = (
    fruit
    for index, fruit 
    in enumerate(fetch_fruits(  # Non-trivial in clause
        'api.example.com/fruits',
        limit=100,
    ))
    if index % 2 == 0 and fruit.name.startswith('orange')
)
```

### Single and Double Quotes

- Use single quotes if string is meant to be read by machine.
- Use double quotes if string is meant to be read by human.

Yes:
```
some_fruit = {
    'type': 'apple',
    'name': 'New Apple 2016",
}
```


### Names

- Abbreviations are discouraged. Use them sparingly.
  - If code readability could benefit from using particular abbreviations,
    - document them well,
    - limit their scope,
    - maintain consistency.
- If specific names are used in document, book, convention, use them.
  - For scientific formulas, it's acceptable to use one-letter names (`P` or `phi`) if they are common.
- Avoid underscore suffix to resolve clashed with built-in names. Use more specific names and synonyms.
- Avoid methods starting methods with `get_` and `set_`. 
  - Use properties or, in case of heavy computation, make name reflect it, e.g. `calculate_`.
- Use consitent prefix for named initializers, e.g. `from_` or `make_`.


### Comments and Docstrings

- Include links to documentation, scientific articles, places that code is taken from.
- Ask yourself if better name can replace comment. If so, rename amd remove comment.


### `with` and `try ... except ... else ... finally ...` Clauses


- Prefer `with` over `try ... finally`.
- Use names defined in `try` clause only in `else` clause.
  - Don't use them after whole `try ... except`, neither in `except` nor `finally` clauses.
- Use `else` clause.
- Use `raise ... from ...` in Python 3.

`with` left no choice for interpreter. `finally` can be forgotten.

Only in `else` those names are guaranteed to be defined.



### Sequences

- Use list unpacking instead of zero element.

Yes:
```
single_result, = results  # Don't use results[0] in code
```
```
first_result, *other_results = results  # Python 3 only
```
