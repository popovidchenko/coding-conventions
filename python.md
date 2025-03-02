# Introduction

The point of this coding convention is to have a common coding vocabulary to focus on **what** is written, **not how** it is written.

It's designed for Python 3.10+ and is based on the [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html) dated February 13, 2024.

The global rules are given here, but the local style of each specific project is also important. The code you add should not be different from the existing code. Be consistent!

This coding convention uses [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119) terminology when using the phrases *must*, *must not*, *should*, *should not*, and *may*:

- **MUST** This word, or the terms "REQUIRED" or "SHALL", means that the definition is an absolute requirement of the specification.
- **MUST NOT** This phrase, or the phrase "SHALL NOT", means that the definition is an absolute prohibition of the specification.
- **SHOULD** This word, or the adjective "RECOMMENDED", means that there may exist valid reasons in particular circumstances to ignore a particular item, but the full implications must be understood and carefully weighed before choosing a different course.
- **SHOULD NOT** This phrase, or the phrase "NOT RECOMMENDED" means that there may exist valid reasons in particular circumstances when the particular behavior is acceptable or even useful, but the full implications should be understood and the case carefully weighed before implementing any behavior described with this label.
- **MAY** This word, or the adjective "OPTIONAL", means that an item is truly optional.

The following notations are used in code examples:

- **EXAMPLE** An example of code demonstrating what is written. This code does not contradict this coding convention.
- **GOOD** An example of code that demonstrates what should be done according to this coding convention.
- **BAD** An example of code that demonstrates what should not be done. This code contradicts this coding convention.

The current version of the document is not final and may be updated as necessary.

# Table of Contents

- [Introduction](#introduction)
- [Table of Contents](#table-of-contents)
- [1 Naming](#1-naming)
  - [1.1 File Naming](#11-file-naming)
  - [1.2 Naming Conventions](#12-naming-conventions)
  - [1.3 Names to Avoid](#13-names-to-avoid)
  - [1.4 Mathematical Notation](#14-mathematical-notation)
  - [1.5 Placeholder Variable](#15-placeholder-variable)
- [2 Сode structure](#2-сode-structure)
  - [2.1 Shebang Line](#21-shebang-line)
  - [2.2 Imports](#22-imports)
    - [2.2.1 Import from Packages](#221-import-from-packages)
    - [2.2.2 Imports formatting](#222-imports-formatting)
  - [2.3 Main](#23-main)
  - [2.4 Function length](#24-function-length)
- [3 Code Style](#3-code-style)
  - [3.1 Semicolons](#31-semicolons)
  - [3.2 Line length](#32-line-length)
  - [3.3 Parentheses](#33-parentheses)
  - [3.4 Indentation](#34-indentation)
  - [3.5 Blank Lines](#35-blank-lines)
  - [3.6 Whitespace](#36-whitespace)
  - [3.7 Statements](#37-statements)
- [4 Comments and Docstrings](#4-comments-and-docstrings)
  - [4.1 Docstrings](#41-docstrings)
  - [4.2 Modules](#42-modules)
    - [4.2.1 Test modules](#421-test-modules)
  - [4.3 Functions and Methods](#43-functions-and-methods)
    - [4.3.1 Overridden Methods](#431-overridden-methods)
  - [4.4 Classes](#44-classes)
  - [4.5 Block and Inline Comments](#45-block-and-inline-comments)
  - [4.6 TODO Comments](#46-todo-comments)
  - [4.7 Punctuation, Spelling, and Grammar](#47-punctuation-spelling-and-grammar)
- [5 Language Rules](#5-language-rules)
  - [5.1 Exceptions](#51-exceptions)
  - [5.2 Mutable Global State](#52-mutable-global-state)
  - [5.3 Nested/Local/Inner Classes and Functions](#53-nestedlocalinner-classes-and-functions)
  - [5.4 Default Iterators and Operators](#54-default-iterators-and-operators)
  - [5.5 Comprehensions Expressions](#55-comprehensions-expressions)
  - [5.6 Generators](#56-generators)
  - [5.7 Lambda Functions](#57-lambda-functions)
  - [5.8 Conditional Expressions](#58-conditional-expressions)
  - [5.9 Default Argument Values](#59-default-argument-values)
  - [5.10 Properties](#510-properties)
  - [5.11 Getters and Setters](#511-getters-and-setters)
  - [5.12 Strings](#512-strings)
    - [5.12.1 Logging](#5121-logging)
    - [5.12.2 Error Messages](#5122-error-messages)
  - [5.13 True/False Evaluations](#513-truefalse-evaluations)
  - [5.14 Lexical Scoping](#514-lexical-scoping)
  - [5.15 Function and Method Decorators](#515-function-and-method-decorators)
  - [5.16 Threading](#516-threading)
  - [5.17 Power Features](#517-power-features)
  - [5.18 Modern Python: from \_\_future\_\_ imports](#518-modern-python-from-__future__-imports)
  - [5.19 Files, Sockets, and similar Stateful Resources](#519-files-sockets-and-similar-stateful-resources)
  - [5.20 Type Annotations](#520-type-annotations)
    - [5.20.1 General Rules](#5201-general-rules)
    - [5.20.2 Line Breaking](#5202-line-breaking)
    - [5.20.3 Forward Declarations](#5203-forward-declarations)
    - [5.20.4 NoneType](#5204-nonetype)
    - [5.20.5 Type Aliases](#5205-type-aliases)
    - [5.20.6 Typing Variables](#5206-typing-variables)
    - [5.20.7 Tuples vs Lists](#5207-tuples-vs-lists)
    - [5.20.8 Type variables](#5208-type-variables)
    - [5.20.9 String types](#5209-string-types)
    - [5.20.10 Imports For Typing](#52010-imports-for-typing)
    - [5.20.11 Conditional Imports](#52011-conditional-imports)
    - [5.20.12 Circular Dependencies](#52012-circular-dependencies)
    - [5.20.13 Generics](#52013-generics)

# 1 Naming

Names *must* be descriptive.

Avoid abbreviation. In particular, do not use abbreviations that are ambiguous or unfamiliar to readers outside the project, and do not abbreviate by deleting letters within a word.

## 1.1 File Naming

Python filenames *must* have a `.py` extension and *must not* contain dashes `-`.

This allows them to be imported and unittested. If you want an executable to be accessible without the extension, use a symbolic link or a simple bash wrapper containing `exec "$0.py" "$@"`.

If it's necessary to make the executable accessible without an extension, use a symbolic link or a simple bash wrapper containing `exec "$0.py" "$@"`.

## 1.2 Naming Conventions

| **Type** | **Public** | **Internal** |
| --- | --- | --- |
| Packages | lower_with_under | |
| Modules | lower_with_under | _lower_with_under |
| Classes | CapWords | _CapWords |
| Exceptions | CapWords | |
| Functions | lower_with_under() | _lower_with_under() |
| Global/Class Constants | CAPS_WITH_UNDER | _CAPS_WITH_UNDER |
| Global/Class Variables | lower_with_under | _lower_with_under |
| Instance Variables | lower_with_under | _lower_with_under (protected) |
| Method Names | lower_with_under() | _lower_with_under() (protected) |
| Function/Method Parameters | lower_with_under | |
| Local Variables | lower_with_under | |

Note: “Internal” means internal to a module, or protected or private within a class.

**Briefly:** `module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`, `query_proper_noun_for_thing`, `send_acronym_via_https`.

Prepending a single underscore `_` has some support for protecting module variables and functions[linters will flag protected member access]. Note that it is okay for unit tests to access protected constants from the modules under test.

Prepending a double underscore `__` [aka “dunder”] to an instance variable or method effectively makes the variable or method private to its class [using name mangling]. It *should not* be used as it impacts readability and testability, and isn't private. Prefer a single underscore.

## 1.3 Names to Avoid

1. Single character names, except for specifically allowed cases:
   - counters or iterators [e.g. `i`, `j`, `k`, `v`, et al.];
   - `e` as an exception identifier in `try/except` statements;
   - `f` as a file handle in `with` statements;
   - private [type variables](#5208-type-variables) with no constraints [e.g. `_T = TypeVar("_T")`, `_P = ParamSpec("_P")`].

    Please be mindful not to abuse single-character naming. Generally speaking, descriptiveness should be proportional to the name's scope of visibility. For example, `i` might be a fine name for 5-line code block but within multiple nested scopes, it is likely too vague.

2. `__double_leading_and_trailing_underscore__` names [reserved by Python].

3. Offensive terms.

4. Names that needlessly include the type of the variable [for example: `id_to_name_dict`].

## 1.4 Mathematical Notation

For mathematically heavy code, short variable names that would otherwise violate the style guide are preferred when they match established notation in a reference paper or algorithm. When doing so, reference the source of all naming conventions in a comment or docstring or, if the source is not accessible, clearly document the naming conventions. Prefer [PEP8](https://peps.python.org/pep-0008/)-compliant `descriptive_names` for public APIs, which are much more likely to be encountered out of context.

## 1.5 Placeholder Variable

The underscore `_` *should* be used as a placeholder variable when a value is required syntactically but is not used in the logic of your code. This makes it clear to readers that the variable is intentionally unused.

```python
# GOOD: Looping through a list without using the index or value.
for _ in range(10):
    ...

# GOOD: Unpacking values and ignoring certain elements.
_, value, _ = get_values()
```

Avoid using `_` for any variable that will be referenced or manipulated in the code. Reserve its use strictly for cases where the value is irrelevant and unused.

# 2 Сode structure

Related classes and top-level functions *should* be placed together in a module [unlike Java, there is no need to be limited to one class per module].

## 2.1 Shebang Line

The Shebang line *should* be used in a file intended for direct execution. It is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules.

Start the main file of a program with `#!/usr/bin/env python3` [to support virtualenvs], `#!/usr/bin/python3` per [PEP-394](https://peps.python.org/pep-0394/). Other `.py` files *should not* start with the line `#!`.

## 2.2 Imports

The `import` operators *must* only be used for packages and modules, *not* for individual types, classes or functions.

- Use `import x` for importing packages and modules.
- Use `from x import y` where `x` is the package prefix and `y` is the module name with no prefix.
- Use `from x import y as z` in any of the following circumstances:
    - Two modules named `y` are to be imported.
    - `y` conflicts with a top-level name defined in the current module.
    - `y` conflicts with a common parameter name that is part of the public API [e.g., `features`].
    - `y` is an inconveniently long name.
    - `y` is too generic in the context of your code [e.g., `from storage.file_system import options as fs_options`].
- Use `import y as z` only when `z` is a standard abbreviation [e.g., `import numpy as np`].

```python
# GOOD:
from sound.effects import echo
...
echo.EchoFilter(input, output, delay = 0.7, atten = 4)
```

Relative names *must not* be used in the import. Even if the module is in the same package, use the full package name. This will help avoid inadvertently importing the the package twice.

### 2.2.1 Import from Packages

Importing a module *must* use the full pathname location of the module.

```python
# GOOD:
# Reference absl.flags in code with the complete name (verbose).
import absl.flags
from doctor.who import jodie

_FOO = absl.flags.DEFINE_string(...)
```

```python
# GOOD:
# Reference flags in code with just the module name (common).
from absl import flags
from doctor.who import jodie

_FOO = flags.DEFINE_string(...)
```

```python
# BAD:
# Assume this file lives in `doctor/who/` where `jodie.py` also exists.
# Unclear what module the author wanted and what will be imported. The actual import behavior
# depends on external factors controlling sys.path. Which possible jodie module did the author
# intend to import?
import jodie
```

### 2.2.2 Imports formatting

Imports *must* be on separate lines.

```python
# GOOD:
from collections.abc import Mapping
from collections.abc import Sequence
import os
import sys
from typing import Any, NewType
```

```python
# BAD:
import os, sys
```

Imports are always put at the top of the file, just after any module comments and docstrings and before module globals and constants.

Imports *should* be grouped from most generic to least generic:

1. Python future import statements.

    ```python
    # EXAMPLE:
    from __future__ import annotations
    ```

    See [more information](#518-modern-python-from-__future__-imports).

2.  Python standard library imports.

    ```python
    # EXAMPLE:
    import sys
    ```

3.  [Third-party](https://pypi.org/) module or package imports.

    ```python
    # EXAMPLE:
    import tensorflow as tf
    ```

4.  Code repository sub-package imports.

    ```python
    # EXAMPLE:
    from otherproject.ai import mind
    ```

Within each grouping, imports *should* be sorted alphabetically, in case-insensitive order, according to each module's full package path [the `path` in `from path import ...`].

Code *may* optionally place a blank line between import sections.

```python
# GOOD:
import collections
import queue
import sys

from absl import app, flags
import bs4
import cryptography
import tensorflow as tf

from book.genres import scifi
from myproject.backend import huxley
from myproject.backend.hgwells import time_machine
from myproject.backend.state_machine import main_loop
from otherproject.ai import body, mind, soul
```

## 2.3 Main

Python, `pydoc` as well as unit tests require modules to be importable. If a file is meant to be used as an executable, its main functionality *must* be in a `main()` function, and the code *must* always check `if __name__ == "__main__"` before executing your main program, so that it is not executed when the module is imported.

```python
# GOOD:
def main():
    ...

if __name__ == "__main__":
    main()
```

## 2.4 Function length

Functions *should* be small and focused.

Long functions are sometimes appropriate, so no hard limit is placed on function length. If a function exceeds about 40 lines, think about whether it can be broken up without harming the structure of the program.

# 3 Code Style

The rules for code styling and formatting are listed below. In situations not covered by these rules, generally accepted typographical standards and [PEP8](https://peps.python.org/pep-0008/) *should* be followed.

## 3.1 Semicolons

Semicolons *must not* end lines and *must not* be used to put two statements on the same line.

## 3.2 Line length

Maximum line length *should* be 100 characters.

Explicit exceptions to the 100 character limit:

- Long import statements.
- URLs, pathnames, or long flags in comments.
- Long string module-level constants not containing whitespace that would be inconvenient to split across lines such as URLs or pathnames.
- Pylint disable comments [e.g.: `# pylint: disable=invalid-name`].

A backslash *must not* be used for [explicit line continuation](https://docs.python.org/3/reference/lexical_analysis.html#explicit-line-joining).

Instead, make use of Python's [implicit line joining inside parentheses, brackets and braces](http://docs.python.org/reference/lexical_analysis.html#implicit-line-joining). An extra pair of parentheses may be added around an expression if necessary.

Note that this rule doesn't prohibit backslash-escaped newlines within strings [see [more information](#512-strings)].

```python
# GOOD:
foo_bar(self, width, height, color="black", design=None, x="foo",
        emphasis=None, highlight=0)
```

```python
# GOOD:
if (width == 0 and height == 0 and
    color == "red" and emphasis == "strong"):

(bridge_questions.clarification_on
 .average_airspeed_of.unladen_swallow) = "African or European?"

with (
    very_long_first_expression_function() as spam,
    very_long_second_expression_function() as beans,
    third_thing() as eggs,
):
    place_order(eggs, beans, spam, beans)
```

```python
# BAD:
if width == 0 and height == 0 and \
    color == "red" and emphasis == "strong":

bridge_questions.clarification_on \
    .average_airspeed_of.unladen_swallow = "African or European?"

with very_long_first_expression_function() as spam, \
    very_long_second_expression_function() as beans, \
    third_thing() as eggs:
    place_order(eggs, beans, spam, beans)
```

When a literal string won't fit on a single line, use parentheses for implicit line joining.

```python
# GOOD:
x = ("This will build a very long long "
     "long long long long long long string")
```

Prefer to break lines at the highest possible syntactic level. If it is necessary to break a line twice, it must be broken at the same syntactic level both times.

```python
# GOOD:
bridgekeeper.answer(
    name="Arthur", quest=questlib.find(owner="Arthur", perilous=True))

answer = (a_long_line().of_chained_methods()
          .that_eventually_provides().an_answer())

if (
    config is None
    or "editor.language" not in config
    or config["editor.language"].use_spaces is False
):
    use_tabs()
```

```python
# BAD:
bridgekeeper.answer(name="Arthur", quest=questlib.find(
    owner="Arthur", perilous=True))

answer = a_long_line().of_chained_methods().that_eventually_provides(
    ).an_answer()

if (config is None or "editor.language" not in config or config[
    "editor.language"].use_spaces is False):
  use_tabs()
```

Within comments, put long URLs on their own line if necessary.

```python
# GOOD:
# See details at
# http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
```

```python
# BAD:
# See details at
# http://www.example.com/us/developer/documentation/api/content/\
# v2.0/csv_file_name_extension_full_specification.html
```

Make note of the indentation of the elements in the line continuation examples above; see the [indentation](#34-indentation) section for explanation.

## 3.3 Parentheses

Parentheses *should* be used sparingly.

Parentheses *may* be used around tuples, but not necessarily. Do not use them in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.

Parentheses *must not* be used in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.

```python
# GOOD:
if foo:
    bar()

while x:
    x = bar()

if x and y:
    bar()

if not x:
    bar()

# For a 1 item tuple the ()s are more visually obvious than the comma.
onesie = (foo,)

return foo

return spam, beans

return (spam, beans)

for (x, y) in dict.items():
    ...
```

```python
# BAD:
if (x):
    bar()

if not(x):
    bar()

return (foo)
```

## 3.4 Indentation

Code blocks *must* be indented with 4 spaces.

Tabs *must not* be used.

Implied line continuation *must* align wrapped elements vertically [see [line length examples](#32-line-length)], or use a hanging 4-space indent. Closing [round, square or curly] brackets can be placed at the end of the expression, or on separate lines, but then *must* be indented the same as the line with the corresponding opening bracket.

```python
# GOOD:
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
meal = (spam,
        beans)

# Aligned with opening delimiter in a dictionary.
foo = {
    "long_dictionary_key": value1 +
                           value2,
    ...
}

# 4-space hanging indent; nothing on first line.
foo = long_function_name(
    var_one, var_two, var_three,
    var_four)
meal = (
    spam,
    beans)

# 4-space hanging indent; nothing on first line,
# closing parenthesis on a new line.
foo = long_function_name(
    var_one, var_two, var_three,
    var_four
)
meal = (
    spam,
    beans,
)

# 4-space hanging indent in a dictionary.
foo = {
    "long_dictionary_key":
        long_dictionary_value,
    ...
}
```

```python
# BAD:
# Stuff on first line forbidden.
foo = long_function_name(var_one, var_two,
    var_three, var_four)
meal = (spam,
    beans)

# 2-space hanging indent forbidden.
foo = long_function_name(
  var_one, var_two, var_three,
  var_four)

# No hanging indent in a dictionary.
foo = {
    "long_dictionary_key":
    long_dictionary_value,
    ...
}
```

Trailing commas in sequences of items *may* only be used if the closing container token `]`, `)` or `}` is not on the same line as the last element, and for tuples with a single element.


```python
# EXAMPLE:
golomb3 = [0, 1, 3]
golomb4 = [
    0,
    1,
    4,
    6,
]
```

```python
# BAD:
golomb4 = [
    0,
    1,
    4,
    6,]
```

## 3.5 Blank Lines

Blank lines *must* be used according to the rules below:

1. Two blank lines between top-level definitions, be they function or class definitions.

2. One blank line between method definitions and between the docstring of a `class` and the first method.

3. No blank line following a `def` line.

Single blank lines *may* be used within functions or methods if necessary.

Blank lines need not be anchored to the definition. For example, related comments immediately preceding function, class, and method definitions can make sense.

## 3.6 Whitespace

Whitespace *must* be used according to the rules below:

1. No whitespace inside parentheses, brackets or braces.

    ```python
    # GOOD:
    spam(ham[1], {"eggs": 2}, [])
    ```

    ```python
    # BAD:
    spam( ham[ 1 ], { "eggs": 2 }, [ ] )
    ```

2. No whitespace before a comma, semicolon, or colon.

    ```python
    # GOOD:
    if x == 4:
        print(x, y)
    x, y = y, x
    ```

    ```python
    # BAD:
    if x == 4 :
        print(x , y)
    x , y = y , x
    ```

3. No whitespace before the open paren/bracket that starts an argument list, indexing or slicing.

    ```python
    # GOOD:
    spam(1)
    ```

    ```python
    # BAD:
    spam (1)
    ```

    ```python
    # GOOD:
    dict["key"] = list[index]
    ```

    ```python
    # BAD:
    dict ["key"] = list [index]
    ```

4. No trailing whitespace.

5. Surround binary operators with a single space on either side for assignment [`=`], comparisons [`==, <, >, !=, <>, <=, >=, in, not in, is, is not`], and Booleans [`and, or, not`]. Use common sense when inserting spaces around arithmetic operators [`+`, `-`, `*`, `/`, `//`, `%`, `**`, `@`].

    ```python
    # GOOD:
    x == 1
    ```

    ```python
    # BAD:
    x<1
    ```

6. Don't use spaces around `=` when passing keyword arguments or defining a default parameter value, with one exception: when a type annotation is present, do use spaces around the `=` for the default parameter value.

    ```python
    # GOOD:
    def complex(real, imag=0.0): return Magic(r=real, i=imag)
    def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
    ```

    ```python
    # BAD:
    def complex(real, imag = 0.0): return Magic(r = real, i = imag)
    def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
    ```

7. Don't use spaces to vertically align tokens on consecutive lines, since it becomes a maintenance burden [applies to `:`, `=`, etc.]:

    ```python
    # GOOD:
    foo = 1000
    long_name = 2

    dictionary = {
        "foo": 1,
        "long_name": 2,
    }
    ```

    ```python
    # BAD:
    foo       = 1000
    long_name = 2

    dictionary = {
        "foo"      : 1,
        "long_name": 2,
    }
    ```

## 3.7 Statements

There *should* be one statement per line.

```python
# GOOD:
if foo:
    bar(foo)
```

```python
# BAD:
if foo: bar(foo)
else:   baz(foo)

try:               bar(foo)
except ValueError: baz(foo)

try:
    bar(foo)
except ValueError: baz(foo)
```

# 4 Comments and Docstrings

For dockstrings of modules, functions, methods and inline comments, the style described below *must* be used.

## 4.1 Docstrings

Python uses docstrings to document code. A docstring is a string that is the first statement in a package, module, class or function. These strings can be extracted automatically through the `__doc__` member of the object and are used by `pydoc`.

Always use the three-double-quote `"""` format for docstrings [per [PEP 257](https://peps.python.org/pep-0257/)]. A docstring should be organized as a summary line [one physical line not exceeding 80 characters] terminated by a period, question mark, or exclamation point.

When writing more [encouraged], this must be followed by a blank line, followed by the rest of the docstring starting at the same cursor position as the first quote of the first line. There are more formatting guidelines for docstrings below.

## 4.2 Modules

Files *must* begin with a docstring describing the content of the module.

The module docstring *may* also include usage of the module, author's name, e-mail, file name, file creation date, project name, licence, etc.

```python
# EXAMPLE:
"""A one-line summary of the module or program, terminated by a period.

Leave one blank line.  The rest of this docstring should contain an
overall description of the module or program.  Optionally, it may also
contain a brief description of exported classes and functions and/or usage
examples.

Typical usage example:
  foo = ClassFoo()
  bar = foo.FunctionBar()
"""
```

### 4.2.1 Test modules

Module-level docstrings for test files are not required. They *should* be included only when there is additional information that can be provided.

Examples include some specifics on how the test should be run, an explanation of an unusual setup pattern, dependency on the external environment, and so on.

```python
# GOOD:
"""This blaze test uses golden files.

You can update those files by running
`blaze run //foo/bar:foo_test -- --update_golden_files` from the `google3`
directory.
"""
```

Docstrings that do not provide any new information *should not* be used.

```python
# BAD:
"""Tests for foo.bar."""
```

## 4.3 Functions and Methods

In this section, "function" means a method, function, generator, or property.

A docstring *must* be given for every function that has one or more of the following properties:
   - being part of the public API;
   - nontrivial size;
   - non-obvious logic.

A docstring *should* give enough information to write a call to the function without reading the function's code. The docstring *should* describe the function's calling syntax and its semantics, but generally not its implementation details, unless those details are relevant to how the function is to be used. For example, a function that mutates one of its arguments as a side effect should note that in its docstring. Otherwise, subtle but important details of a function's implementation that are not relevant to the caller are better expressed as comments alongside the code than within the function's docstring.

The docstring may be descriptive-style [`"""Fetches rows from a Bigtable."""`] or imperative-style [`"""Fetch rows from a Bigtable."""`], but the style *should* be consistent within a file. The docstring for a `@property` data descriptor *should* use the same style as the docstring for an attribute or a function argument [`"""The Bigtable path."""`, rather than `"""Returns the Bigtable path."""`].

Certain aspects of a function *should* be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. All sections other than the heading should maintain a hanging indent of 4 spaces. These sections *may* be omitted in cases where the function's name and signature are informative enough that it can be aptly described using a one-line docstring.

**Args:** List each parameter by name. A description *should* follow the name, and be separated by a colon followed by either a space or newline. If the description is too long to fit on a single 80-character line, use a hanging indent of 4 spaces more than the parameter name. The description should include required type(s) if the code does not contain a corresponding type annotation. If a function accepts `*foo` [variable length argument lists] and/or `**bar` [arbitrary keyword arguments], they should be listed as `*foo` and `**bar`.

**Returns [or Yields for generators]:** Describe the semantics of the return value, including any type information that the type annotation does not provide. If the function only returns None, this section is not required. It may also be omitted if the docstring starts with "Return", "Returns", "Yield", or "Yields" [e.g. `"""Returns row from Bigtable as a tuple of strings."""`] and the opening sentence is sufficient to describe the return value. If the return value is a tuple, describe it as: "Returns: tuple [mat_a, mat_b], where mat_a is ..., and ...". If the function uses `yield` [is a generator], the `Yields:` section should document the object returned by `next()`, instead of the generator object itself that the call evaluates to.

**Raises:** List all exceptions that are relevant to the interface followed by a description. Use a similar exception name + colon + space or newline and hanging indent style as described in `Args:`. Exceptions that get raised when violating the API specified in the docstring *should not* be documented [because this would paradoxically make behavior under violation of the API part of the API].

```python
# EXAMPLE:
def fetch_smalltable_rows(
    table_handle: smalltable.Table,
    keys: Sequence[bytes | str],
    require_all_keys: bool = False,
) -> Mapping[bytes, tuple[str, ...]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
        table_handle: An open smalltable.Table instance.
        keys: A sequence of strings representing the key of each table
          row to fetch.  String keys will be UTF-8 encoded.
        require_all_keys: If True only rows with values set for all keys will be
          returned.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {b"Serak": ("Rigel VII", "Preparer"),
         b"Zim": ("Irk", "Invader"),
         b"Lrrr": ("Omicron Persei 8", "Emperor")}

        Returned keys are always bytes.  If a key from the keys argument is
        missing from the dictionary, then that row was not found in the
        table (and require_all_keys must have been False).

    Raises:
        IOError: An error occurred accessing the smalltable.
    """
```

Similarly, this variation on `Args:` with a line break is also allowed:

```python
# EXAMPLE:
def fetch_smalltable_rows(
    table_handle: smalltable.Table,
    keys: Sequence[bytes | str],
    require_all_keys: bool = False,
) -> Mapping[bytes, tuple[str, ...]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
      table_handle:
        An open smalltable.Table instance.
      keys:
        A sequence of strings representing the key of each table row to
        fetch.  String keys will be UTF-8 encoded.
      require_all_keys:
        If True only rows with values set for all keys will be returned.

    Returns:
      A dict mapping keys to the corresponding table row data
      fetched. Each row is represented as a tuple of strings. For
      example:

      {b"Serak": ("Rigel VII", "Preparer"),
       b"Zim": ("Irk", "Invader"),
       b"Lrrr": ("Omicron Persei 8", "Emperor")}

      Returned keys are always bytes.  If a key from the keys argument is
      missing from the dictionary, then that row was not found in the
      table (and require_all_keys must have been False).

    Raises:
      IOError: An error occurred accessing the smalltable.
    """
```

### 4.3.1 Overridden Methods

A method that overrides a method from a base class does not need a docstring if it is explicitly decorated with [`@override`](https://typing-extensions.readthedocs.io/en/latest/#override) [from `typing_extensions` or `typing` modules], unless the overriding method's behavior materially refines the base method's contract, or details need to be provided [e.g., documenting additional side effects], in which case a docstring with at least those differences is required on the overriding method.

```python
# GOOD:
from typing_extensions import override

class Parent:
  def do_something(self):
    """Parent method, includes docstring."""

# Child class, method annotated with override.
class Child(Parent):
  @override
  def do_something(self):
    pass

# Docstring is trivial, @override is sufficient to indicate that docs can be
# found in the base class.
class Child(Parent):
  @override
  def do_something(self):
    """See base class."""
```

```python
# BAD:
# Child class, but without @override decorator, a docstring is required.
class Child(Parent):
  def do_something(self):
    pass

```

## 4.4 Classes

Classes *should* have a docstring below the class definition describing the class. Public attributes, excluding [properties](#510-properties), *should* be documented here in an **Attributes:** section and follow the same formatting as a [function's `Args`](#43-functions-and-methods) section.

```python
# EXAMPLE:
class SampleClass:
    """Summary of class here.

    Longer class information...
    Longer class information...

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam: bool = False):
        """Initializes the instance based on spam preference.

        Args:
          likes_spam: Defines if instance exhibits this preference.
        """
        self.likes_spam = likes_spam
        self.eggs = 0

    @property
    def butter_sticks(self) -> int:
        """The number of butter sticks we have."""
```

All class docstrings *should* start with a one-line summary that describes what the class instance represents. This implies that subclasses of `Exception` *should* also describe what the exception represents, and not the context in which it might occur. The class docstring *should not* repeat unnecessary information, such as that the class is a class.

```python
# GOOD:
class CheeseShopAddress:
    """The address of a cheese shop.

    ...
    """

class OutOfCheeseError(Exception):
    """No more cheese is available."""
```

```python
# BAD:
class CheeseShopAddress:
    """Class that describes the address of a cheese shop.

    ...
    """

class OutOfCheeseError(Exception):
    """Raised when no more cheese is available."""
```

## 4.5 Block and Inline Comments

Complex code sections *should* be commented out with one or few lines of comments before.

Inline comments *should not* be used.

```python
# GOOD:
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

# True if i is 0 or a power of 2.
if i & (i - 1) == 0:
```

Never describe the code.

```python
# BAD:
# Now go through the b array and make sure whenever i occurs
# the next element is i + 1
```
## 4.6 TODO Comments

`TODO` comments *should* be used for code that is temporary, a short-term solution, or good-enough but not perfect.

A `TODO` comment begins with the word `TODO` in all caps, a following colon, and a link to a resource that contains the context, ideally a bug reference. A bug reference is preferable because bugs are tracked and have follow-up comments. Follow this piece of context with an explanatory string introduced with a hyphen `-`. The purpose is to have a consistent `TODO` format that can be searched to find out how to get more details.

```python
# GOOD:
# TODO: crbug.com/192795 — Investigate cpufreq optimizations.
```

Old style, formerly recommended, but discouraged for use in new code.

```python
# BAD:
# TODO(crbug.com/192795): Investigate cpufreq optimizations.
# TODO(yourusername): Use a "\*" here for concatenation operator.
```

Avoid adding TODOs that refer to an individual or team as the context:

```python
# BAD:
# TODO: @yourusername — File an issue and use a "*" for repetition.
```

If the `TODO` is of the form "At a future date do something" make sure to include either a very specific date ["Fix by November 2009"] or a very specific event ["Remove this code when all clients can handle XML responses."] that future code maintainers will comprehend. Issues are ideal for tracking this.

## 4.7 Punctuation, Spelling, and Grammar

Pay attention to punctuation, spelling, and grammar; it is easier to read well-written comments than badly written ones.

Comments *should* be as readable as narrative text, with proper capitalization and punctuation. In many cases, complete sentences are more readable than sentence fragments.

It is very important that source code maintain a high level of clarity and readability. Proper punctuation, spelling, and grammar help with that goal.

# 5 Language Rules

## 5.1 Exceptions

Exceptions *must* follow certain conditions:

1. Make use of built-in exception classes when it makes sense.

2. Do not use `assert` statements in place of conditionals or validating preconditions. They must not be critical to the application logic and they must be able to be removed without breaking the code. `assert` conditionals are [not guaranteed](https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement) to be evaluated.

3. Libraries or packages may define their own exceptions. When doing so they must inherit from an existing exception class. Exception names should end in `Error` and should not introduce repetition [`foo.FooError`].

4. Never use catch-all `except:` statements, or catch `Exception` or `StandardError`, unless you are:
    - re-raising the exception, or
    - creating an isolation point in the program where exceptions are not propagated but are recorded and suppressed instead, such as protecting a thread from crashing by guarding its outermost block.

5. Minimize the amount of code in a `try`/`except` block. The larger the body of the `try`, the more likely that an exception will be raised by a line of code that is not expected to raise an exception. In those cases, the `try`/`except` block hides a real error.

6. Use the `finally` clause to execute code whether or not an exception is raised in the `try` block. This is often useful for cleanup, i.e., closing a file.

## 5.2 Mutable Global State

Mutable global state *should* be avoided.

In those rare cases where using global state is warranted, mutable global entities should be declared at the module level or as a class attribute and made internal by prepending an `_` to the name. If necessary, external access to mutable global state must be done through public functions or class methods [see [Naming](#1-naming)]. Please explain the design reasons why mutable global state is being used in a comment or a doc linked to from a comment.

Module-level constants are permitted and encouraged. For example: `_MAX_HOLY_HANDGRENADE_COUNT = 3` for an internal use constant or `SIR_LANCELOTS_FAVORITE_COLOR = "blue"` for a public API constant. Constants must be named using all caps with underscores [see [Naming](#1-naming)].

## 5.3 Nested/Local/Inner Classes and Functions

Nested local functions or classes *may* be used with some caveats:

1. Avoid nested functions or classes except when closing over a local value other than `self` or `cls`.

2. Do not nest a function just to hide it from users of a module. Instead, prefix its name with an `_` at the module level so that it can still be accessed by tests.

## 5.4 Default Iterators and Operators

Default iterators and operators *must* be used for types that support them, like lists, dictionaries, and files. The built-in types define iterator methods, too. Prefer these methods to methods that return lists, except that you should not mutate a container while iterating over it.

```python
# GOOD:
for key in adict: ...
if obj in alist: ...
for line in afile: ...
for k, v in adict.items(): ...
```

```python
# BAD:
for key in adict.keys(): ...
for line in afile.readlines(): ...
```

## 5.5 Comprehensions Expressions

Comprehensions expressions *may* be used for simple cases. Multiple `for` clauses or filter expressions are not permitted. The text of the expression *must* be optimised for readability, not conciseness.

```python
# GOOD:
result = [mapping_expr for value in iterable if filter_expr]

result = [
    is_valid(metric = {"key": value})
    for value in interesting_iterable
    if a_longer_filter_expression(value)
]

descriptive_name = [
    transform({"key": key, "value": value}, color = "black")
    for key, value in generate_iterable(some_input)
    if complicated_condition_is_met(key, value)
]

result = []
for x in range(10):
    for y in range(5):
        if x * y > 10:
            result.append((x, y))

return {
    x: complicated_transform(x)
    for x in long_generator_function(parameter)
    if x is not None
}

return (x**2 for x in range(10))

unique_names = {user.name for user in users if user is not None}
```

```python
# BAD:
result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

return (
    (x, y, z)
    for x in range(5)
    for y in range(5)
    if x != y
    for z in range(5)
    if y != z
)
```

## 5.6 Generators

Generators *may* be used as needed.

Use "Yields:" rather than "Returns:" in the docstring for generator functions [see [more information](#43-functions-and-methods)].

If the generator manages an expensive resource, make sure to force the clean up. A good way to do the clean up is by wrapping the generator with a context manager [PEP-0533](https://peps.python.org/pep-0533/).

## 5.7 Lambda Functions

Lambda functions *may* be used for one-line expressions. Prefer generator expressions over `map()` or `filter()` with a `lambda`.

If the code inside the lambda function spans multiple lines or is longer than 60-80 chars, it might be better to define it as a regular [nested function](#514-lexical-scoping).

For common operations like multiplication, use the functions from the `operator` module instead of lambda functions. For example, prefer `operator.mul` to `lambda x, y: x * y`.

## 5.8 Conditional Expressions

Conditional expressions [sometimes called a “ternary operator”] *may* be used for simple cases. Each portion must fit on one line: true-expression, if-expression, else-expression. Use a complete if statement when things get more complicated.

```python
# GOOD:
one_line = "yes" if predicate(value) else "no"
slightly_split = ("yes" if predicate(value)
                  else "no, nein, nyet")
the_longest_ternary_style_that_can_be_done = (
    "yes, true, affirmative, confirmed, correct"
    if predicate(value)
    else "no, false, negative, nay")
```

```python
# BAD:
bad_line_breaking = ("yes" if predicate(value) else
                     "no")
portion_too_long = ("yes"
                    if some_long_module.some_long_predicate_function(
                        really_long_variable_name)
                    else "no, false, negative, nay")
```

## 5.9 Default Argument Values

Default argument values *may* be used in most cases.

Mutable objects *must not* be used as default values in a function or method definition.

```python
# GOOD:
def foo(a, b = None):
    if b is None:
        b = []

def foo(a, b: Sequence | None = None):
    if b is None:
        b = []

# Empty tuple OK since tuples are immutable.
def foo(a, b: Sequence = ()):
    ...
```

```python
# BAD:
from absl import flags
_FOO = flags.DEFINE_string(...)

def foo(a, b = []):
    ...

# Is `b` supposed to represent when this module was loaded?
def foo(a, b = time.time()):
    ...

# sys.argv has not yet been parsed...
def foo(a, b = _FOO.value):
    ...

# Could still get passed to unchecked code.
def foo(a, b: Mapping = {}):
    ...
```

## 5.10 Properties

Properties *may* be used to control getting or setting attributes that require trivial computations or logic. Property implementations must match the general expectations of regular attribute access: that they are cheap, straightforward, and unsurprising.

Properties, like operator overloading, *must* be used only when necessary and consistent with the expectations of typical attribute access; otherwise, follow the [getters and setters](#511-getters-and-setters) rules.

For example, using a property to simply both get and set an internal attribute isn't allowed: there is no computation occurring, so the property is unnecessary [[make the attribute public instead](#511-getters-and-setters)]. In comparison, using a property to control attribute access or to calculate a *trivially* derived value is allowed: the logic is simple and unsurprising.

Properties *must* be created with the `@property` [decorator](#515-function-and-method-decorators). Manually implementing a property descriptor is considered a [power feature](#517-power-features).

Inheritance with properties can be non-obvious. Do not use properties to implement computations a subclass may ever want to override and extend.

## 5.11 Getters and Setters

Getter and setter functions [also called accessors and mutators] *should* be used when they provide a meaningful role or behavior for getting or setting a variable's value.

In particular, they *should* be used when getting or setting the variable is complex or the cost is significant, either currently or in a reasonable future.

If, for example, a pair of getters/setters simply read and write an internal attribute, the internal attribute should be made public instead. By comparison, if setting a variable means some state is invalidated or rebuilt, it should be a setter function. The function invocation hints that a potentially non-trivial operation is occurring. Alternatively, [properties](#510-properties) may be an option when simple logic is needed, or refactoring to no longer need getters and setters.

Getters and setters *must* follow the [Naming](#1-naming) guidelines, such as `get_foo()` and `set_foo()`.

## 5.12 Strings

An [f-string](https://docs.python.org/3/reference/lexical_analysis.html#f-strings), the `%` operator, or the `format` method *should* be used to format strings, even when the parameters are all strings.

Avoid the use of `+` to format strings. A single join with `+` is okay but format with `+` *must not* be used.

```python
# GOOD:
x = f"name: {name}; score: {n}"
x = "%s, %s!" % (imperative, expletive)
x = "{}, {}".format(first, second)
x = "name: %s; score: %d" % (name, n)
x = "name: %(name)s; score: %(score)d" % {"name":name, "score":n}
x = "name: {}; score: {}".format(name, n)
```

```python
# BAD:
x = first + ", " + second
x = "name: " + name + "; score: " + str(n)
```

The `+` and `+=` operators *should not* be used to accumulate a string within a loop. In some conditions, accumulating a string with addition can lead to quadratic rather than linear running time. The conditions under which an optimization applies are not easy to predict and may change.

Instead, add each substring to a list and `"".join` the list after the loop terminates, or write each substring to an `io.StringIO` buffer. These techniques consistently have amortized-linear run-time complexity.

```python
# GOOD:
items = ["<table>"]
for last_name, first_name in employee_list:
    items.append("<tr><td>%s, %s</td></tr>" % (last_name, first_name))
items.append("</table>")
employee_table = "".join(items)
```

```python
# BAD:
employee_table = "<table>"
for last_name, first_name in employee_list:
    employee_table += "<tr><td>%s, %s</td></tr>" % (last_name, first_name)
employee_table += "</table>"
```

The `"` symbol *shoud* be used as quote character. It is okay to use the other quote character on a string to avoid the need to backslash-escape quote characters within the string.

```python
# GOOD:
Python("Why are you hiding your eyes?")
Gollum("I'm scared of lint errors.")
Narrator('"Good!" thought a happy Python reviewer.')
```

```python
# BAD:
Python('Why are you hiding your eyes?')
Gollum("The lint. It burns. It burns us.")
Gollum('Always the great lint. Watching. Watching.')
```

The `"""` *must* be used for multi-line strings [and docstrings].

Multi-line strings do not flow with the indentation of the rest of the program. To avoid embedding extra space in the string, use either concatenated single-line strings or a multi-line string with [`textwrap.dedent()`](https://docs.python.org/3/library/textwrap.html#textwrap.dedent) to remove the initial space on each line.

```python
# BAD:
long_string = """This is pretty ugly.
Don't do this.
"""
```

```python
# GOOD:
long_string = """This is fine if your use case can accept
    extraneous leading spaces."""
```

```python
# GOOD:
long_string = ("And this is fine if you cannot accept\n" +
               "extraneous leading spaces.")
```

```python
# GOOD:
long_string = ("And this too is fine if you cannot accept\n"
               "extraneous leading spaces.")
```

```python
# GOOD:
import textwrap

long_string = textwrap.dedent("""\
    This is also fine, because textwrap.dedent()
    will collapse common leading spaces in each line.""")
```

Note that using a backslash here does not violate the prohibition against [explicit line continuation](#32-line-length); in this case, the backslash is [escaping a newline](https://docs.python.org/3/reference/lexical_analysis.html#string-and-bytes-literals) in a string literal.

### 5.12.1 Logging

Logging functions *must* use a pattern-string [with %-placeholders] as the first argument.

Always call them with a string literal [not an f-string!] as their first argument with pattern-parameters as subsequent arguments. Some logging implementations collect the unexpanded pattern-string as a queryable field. It also prevents spending time rendering a message that no logger is configured to output.

```python
# GOOD:
import tensorflow as tf
logger = tf.get_logger()
logger.info("TensorFlow Version is: %s", tf.__version__)
```

```python
# GOOD:
import os
from absl import logging

logging.info("Current $PAGER is: %s", os.getenv("PAGER", default=""))

homedir = os.getenv("HOME")
if homedir is None or not os.access(homedir, os.W_OK):
    logging.error("Cannot write to home directory, $HOME = %r", homedir)
```

```python
# BAD:
import os
from absl import logging

logging.info("Current $PAGER is:")
logging.info(os.getenv("PAGER", default=""))

homedir = os.getenv("HOME")
if homedir is None or not os.access(homedir, os.W_OK):
    logging.error(f"Cannot write to home directory, $HOME = {homedir!r}")
```

### 5.12.2 Error Messages

Error messages [such as: message strings on exceptions like `ValueError`, or messages shown to the user] *must* follow three guidelines:

1. The message needs to precisely match the actual error condition.

2. Interpolated pieces need to always be clearly identifiable as such.

3. They should allow simple automated processing [e.g. grepping].

```python
# GOOD:
if not 0 <= p <= 1:
    raise ValueError(f"Not a probability: {p=}")

try:
    os.rmdir(workdir)
except OSError as error:
    logging.warning("Could not remove directory (reason: %r): %r",
                    error, workdir)
```

```python
# BAD:
# Also false for float("nan")!
if p < 0 or p > 1:
    raise ValueError(f"Not a probability: {p=}")

try:
    os.rmdir(workdir)
except OSError:
    # Message makes an assumption that might not be true:
    # Deletion might have failed for some other reason, misleading
    # whoever has to debug this.
    logging.warning("Directory already was deleted: %s", workdir)

try:
    os.rmdir(workdir)
except OSError:
    # The message is harder to grep for than necessary, and
    # not universally non-confusing for all possible values of `workdir`.
    # Imagine someone calling a library function with such code
    # using a name such as workdir = "deleted". The warning would read:
    # "The deleted directory could not be deleted."
    logging.warning("The %s directory could not be deleted.", workdir)
```

## 5.13 True/False Evaluations

Implicit False *should* be used whenever possible, e.g., `if foo:` rather than `if foo != []:`.

There are a few caveats:

1. Always use `if foo is None:` [or `is not None`] to check for a `None` value. E.g., when testing whether a variable or argument that defaults to `None` was set to some other value. The other value might be a value that's false in a boolean context!

2. Never compare a boolean variable to `False` using `==`. Use `if not x:` instead. In order to distinguish `False` from `None` then chain the expressions, such as `if not x and x is not None:`.

3. For sequences [strings, lists, tuples], use the fact that empty sequences are False, so `if seq:` and `if not seq:` are preferable to `if len(seq):` and `if not len(seq):` respectively.

4. When handling integers, implicit False may involve more risk than benefit [i.e., accidentally handling `None` as 0]. Compare a value which is known to be an integer [and is not the result of `len()`] against the integer 0.

```python
# GOOD:
if not users:
    print("no users")

if i % 10 == 0:
    self.handle_multiple_of_ten()

def f(x=None):
    if x is None:
        x = []
```

```python
# BAD:
if len(users) == 0:
    print("no users")

if not i % 10:
    self.handle_multiple_of_ten()

def f(x=None):
    x = x or []
```

5. Note that `"0"` [i.e., `0` as string] evaluates to True.

## 5.14 Lexical Scoping

Lexical scoping *may* be used as needed.

A nested Python function can refer to variables defined in enclosing functions, but cannot assign to them. Variable bindings are resolved using lexical scoping, that is, based on the static program text. Any assignment to a name in a block will cause Python to treat all references to that name as a local variable, even if the use precedes the assignment. If a global declaration occurs, the name is treated as a global variable.

```python
# EXAMPLE:
def get_adder(summand1: float) -> Callable[[float], float]:
    """Returns a function that adds numbers to a given number."""
    def adder(summand2: float) -> float:
        return summand1 + summand2

    return adder
```

Be careful! Lexical scoping can lead to confusing bugs, such as this example based on [PEP-0227](https://peps.python.org/pep-0227/):

```python
# EXAMPLE:
i = 4
def foo(x: Iterable[int]):
    def bar():
        print(i, end = "")

    # ...
    # A bunch of code here
    # ...

    # Ah, i *is* local to foo, so this is what bar sees
    for i in x:
        print(i, end = "")
    bar()

# `foo([1, 2, 3])` will print `1 2 3 3`, not `1 2 3 4`.
```

## 5.15 Function and Method Decorators

Decorators *may* be used when there is a clear advantage. Decorators *must* follow the same import and naming guidelines as functions. Decorator pydoc should clearly state that the function is a decorator. Write unit tests for decorators.

[Decorators for Functions and Methods](https://docs.python.org/3/glossary.html#term-decorator) [the `@` notation]. One common decorator is `@property`, used for converting ordinary methods into dynamically computed attributes. However, the decorator syntax allows for user-defined decorators as well. Specifically, for some function `my_decorator`, this:

```python
# EXAMPLE:
class C:
    @my_decorator
    def method(self):
        # method body ...
```

is equivalent to:

```python
# EXAMPLE:
class C:
    def method(self):
        # method body ...
    method = my_decorator(method)
```

Avoid external dependencies in the decorator itself [e.g. don't rely on files, sockets, database connections, etc.], since they might not be available when the decorator runs [at import time, perhaps from `pydoc` or other tools]. A decorator that is called with valid parameters should [as much as possible] be guaranteed to succeed in all cases.

Decorators are a special case of "top-level code" — see [main](#23-main) for more discussion.

The `staticmethod` decorator *should not* be used. Only if it is required to integrate with an API defined in an existing library. Instead, write the function at the module level.

The use of the `classmethod` decorator *should* be limited. Use only when writing a named constructor, or a class-specific routine that modifies necessary global state such as a process-wide cache.

## 5.16 Threading

The atomicity of built-in types *must not* be relied on.

While Python's built-in data types such as dictionaries appear to have atomic operations, there are corner cases where they aren't atomic [e.g. if `__hash__` or `__eq__` are implemented as Python methods] and their atomicity should not be relied upon. Neither should you rely on atomic variable assignment [since this in turn depends on dictionaries].

Use the `queue` module's `Queue` data type as the preferred way to communicate data between threads. Otherwise, use the `threading` module and its locking primitives. Prefer condition variables and `threading.Condition` instead of using lower-level locks.

## 5.17 Power Features

Python is an extremely flexible language and provides many fancy features such as custom metaclasses, access to bytecode, on-the-fly compilation, dynamic inheritance, object reparenting, import hacks, reflection [e.g. some uses of `getattr()`], modification of system internals, `__del__` methods implementing customized cleanup, etc.

The use of these features in code *should* be avoided.

Standard library modules and classes that internally use these features are okay to use [e.g. `abc.ABCMeta`, `dataclasses`, and `enum`].

## 5.18 Modern Python: from \_\_future\_\_ imports

The `from __future__ import` statements *may* be used.

It allows a given source file to start using more modern Python syntax features today. Once you no longer need to run on a version where the features are hidden behind a `__future__` import, feel free to remove those lines.

```python
# EXAMPLE:
from __future__ import ...
```

For more information read the [Python future statement definitions](https://docs.python.org/3/library/__future__.html) documentation.

These imports *must not* be removed until it is certain that the code is being used in a sufficiently modern environment.

## 5.19 Files, Sockets, and similar Stateful Resources

Files and sockets *must* be explicitly closed when finished working with them.

This rule naturally extends to closeable resources that internally use sockets, such as database connections, and also other resources that need to be closed down in a similar fashion. To name only a few examples, this also includes [mmap](https://docs.python.org/3/library/mmap.html) mappings, [h5py File objects](https://docs.h5py.org/en/stable/high/file.html), and [matplotlib.pyplot figure windows](https://matplotlib.org/2.1.0/api/_as_gen/matplotlib.pyplot.close.html).

Leaving files, sockets or other such stateful objects open unnecessarily has many downsides:

- They may consume limited system resources, such as file descriptors. Code that deals with many such objects may exhaust those resources unnecessarily if they're not returned to the system promptly after use.
- Holding files open may prevent other actions such as moving or deleting them, or unmounting a filesystem.
- Files and sockets that are shared throughout a program may inadvertently be read from or written to after logically being closed. If they are actually closed, attempts to read or write from them will raise exceptions, making the problem known sooner.

Furthermore, while files and sockets [and some similarly behaving resources] are automatically closed when the object is destructed, coupling the lifetime of the object to the state of the resource is poor practice:

- There are no guarantees as to when the runtime will actually invoke the `__del__` method. Different Python implementations use different memory management techniques, such as delayed garbage collection, which may increase the object's lifetime arbitrarily and indefinitely.
- Unexpected references to the file, e.g. in globals or exception tracebacks, may keep it around longer than intended.

The preferred way to manage files and similar resources is using the [`with` statement](http://docs.python.org/reference/compound_stmts.html#the-with-statement):

```python
# GOOD:
with open("hello.txt") as hello_file:
    for line in hello_file:
        print(line)
```

For file-like objects that do not support the `with` statement, use `contextlib.closing()`:

```python
# GOOD:
import contextlib

with contextlib.closing(urllib.urlopen("http://www.python.org/")) as front_page:
    for line in front_page:
        print(line)
```

In rare cases where context-based resource management is infeasible, code documentation *must* explain clearly how resource lifetime is managed.

## 5.20 Type Annotations

Code *should* be annotated with type hints according to [PEP-484](https://peps.python.org/pep-0484/) and checked at build time using a type checking tool such as [pytype](https://github.com/google/pytype).

Type annotations can be in the source or in a [stub pyi file](https://peps.python.org/pep-0484/#stub-files). Whenever possible, annotations should be in the source. Use pyi files for third-party or extension modules.

As static analysis is relatively new to Python, possible undesired side effects [such as
incorrectly derived types]. In this case, it is recommended to add a comment with a TODO or a bug reference describing the problem(s) preventing type annotations from being accepted to the BUILD file or to the code itself, as appropriate.

### 5.20.1 General Rules

1. Annotating `self` or `cls` is generally not necessary. [`Self`](https://docs.python.org/3/library/typing.html#typing.Self) *may* be used if it is necessary for proper type information, e.g.

    ```python
    # GOOD:
    from typing import Self

    class BaseClass:
      @classmethod
      def create(cls) -> Self:
        ...

      def difference(self, other: Self) -> float:
        ...
    ```

2. The return value `__init__` [where `None` is the only valid option] *should not* be annotated.

3. If any variable or a returned type should not be expressed, use `Any`.

4. There is no need to annotate all the functions in a module.

   - Public APIs *should* be annotated.
   - Code that is prone to type-related errors *should* be annotated.
   - Code that is difficult to understand *should* be annotated.

    Use common sense to achieve a good balance between security and clarity on the one hand, and flexibility on the other.

    Annotate code as it becomes stable from a types perspective. All functions in mature code may be annotated without loss of flexibility.

### 5.20.2 Line Breaking

Follow the [indentation](#34-indentation) rules.

After annotation, function signatures can become “one parameter per”.

```python
# GOOD:
def my_method(
    self,
    first_var: int,
    second_var: Foo,
    third_var: Bar | None
) -> int:
  ...
```

Always prefer breaking between variables, and not, for example, between variable names and type annotations. However, if everything fits on the same line, go for it.

```python
# GOOD:
def my_method(self, first_var: int) -> int:
  ...
```

If the combination of the function name, the last parameter, and the return type is too long, indent by 4 in a new line. When using line breaks, prefer putting each parameter and the return type on their own lines and aligning the closing parenthesis with the `def`:

```python
# GOOD:
def my_method(
    self,
    other_arg: MyLongType | None,
) -> tuple[MyLongType1, MyLongType1]:
  ...
```

```python
# BAD:
def my_method(self,
              other_arg: MyLongType | None,
             ) -> dict[OtherLongType, MyLongType]:
  ...
```

Optionally, the return type may be put on the same line as the last parameter:

```python
# GOOD:
def my_method(
    self,
    first_var: int,
    second_var: int) -> dict[OtherLongType, MyLongType]:
  ...
```

As in the examples above, prefer not to break types. However, sometimes they are too long to be on a single line [try to keep sub-types unbroken].

```python
# GOOD:
def my_method(
    self,
    first_var: tuple[list[MyLongType1],
                     list[MyLongType2]],
    second_var: list[dict[
        MyLongType3, MyLongType4]],
) -> None:
  ...
```

If a single name and type is too long, consider using an [alias](#5205-type-aliases) for the type. The last resort is to break after the colon and indent by 4.

```python
# GOOD:
def my_function(
    long_variable_name:
        long_module_name.LongTypeName,
) -> None:
  ...
```

```python
# BAD:
def my_function(
    long_variable_name: long_module_name.
        LongTypeName,
) -> None:
  ...
```

### 5.20.3 Forward Declarations

`from __future__ import annotations` or string *should* be used to specify the name of a class that is not yet defined [for example, if a class name is needed within the declaration of that class, or a class is used that is defined later in the code].

```python
# GOOD:
from __future__ import annotations

class MyClass:
  def __init__(self, stack: Sequence[MyClass], item: OtherClass) -> None:

class OtherClass:
  ...
```

```python
# GOOD:
class MyClass:
  def __init__(self, stack: Sequence["MyClass"], item: "OtherClass") -> None:

class OtherClass:
  ...
```

### 5.20.4 NoneType

In the Python type system, `NoneType` is a "first class" type, and for typing purposes, `None` is an alias for `NoneType`. If the argument can be `None`, it *should* be declared!

Explicit `X | None` expressions *must* be used.

```python
# GOOD:
def modern_or_union(a: str | int | None, b: str | None = None) -> str:
  ...
def older_union_optional_syntax(a: Union[str, int, None], b: Optional[str] = None) -> str:
  ...
```

```python
# BAD:
def nullable_union(a: Union[None, str]) -> str:
  ...
def implicit_optional(a: str = None) -> str:
  ...
```

### 5.20.5 Type Aliases

Aliases of complex types *may* be declared. The name of the alias *must* be CapWorded. If the alias is to be used only in this module, it *must* be \_Private.

```python
# GOOD:
from typing import TypeAlias

_LossAndGradient: TypeAlias = tuple[tf.Tensor, tf.Tensor]
ComplexTFMap: TypeAlias = Mapping[str, _LossAndGradient]
```

### 5.20.6 Typing Variables

**Annotated Assignments:**
    If an internal variable has a type that is hard or impossible to infer, specify its type with an annotated assignment — use a colon and type between the variable name and value [the same as is done with function arguments that have a default value]:

```python
# GOOD:
a: Foo = SomeUndecoratedFunction()
```

**Type Comments:**
    Comments for specifying the type of a variable *must not* be used.

```python
# BAD:
# type: Foo
a = SomeUndecoratedFunction()
```

### 5.20.7 Tuples vs Lists

Typed lists can only contain objects of a single type. Typed tuples can either have a single repeated type or a set number of elements with different types. The latter is commonly used as the return type from a function.

```python
# GOOD:
a: list[int] = [1, 2, 3]
b: tuple[int, ...] = (1, 2, 3)
c: tuple[int, str, float] = (1, "2", 3.5)
```

### 5.20.8 Type variables

The Python type system has [generics](https://peps.python.org/pep-0484/#generics). A type variable, such as `TypeVar` and `ParamSpec`, is a common way to use them.

```python
# EXAMPLE:
from collections.abc import Callable
from typing import ParamSpec, TypeVar
_P = ParamSpec("_P")
_T = TypeVar("_T")
...

def next(l: list[_T]) -> _T:
    return l.pop()

def print_when_called(f: Callable[_P, _T]) -> Callable[_P, _T]:
    def inner(*args: _P.args, **kwargs: _P.kwargs) -> _T:
        print("Function was called")
        return f(*args, **kwargs)
    return inner
```

A `TypeVar` *may* be constrained.

```python
# EXAMPLE:
AddableType = TypeVar("AddableType", int, float, str)

def add(a: AddableType, b: AddableType) -> AddableType:
    return a + b
```

A common predefined type variable in the `typing` module is `AnyStr`. The `AnyStr` *must* be used for multiple annotations that can be `bytes` or `str` and must all be the same type.

```python
# EXAMPLE
from typing import AnyStr

def check_length(x: AnyStr) -> AnyStr:
    if len(x) <= 42:
      return x
    raise ValueError()
```

A type variable *must* have a descriptive name, unless it meets all of the following criteria:

- not externally visible;
- not constrained.

```python
# GOOD:
_T = TypeVar("_T")
_P = ParamSpec("_P")
AddableType = TypeVar("AddableType", int, float, str)
AnyFunction = TypeVar("AnyFunction", bound=Callable)
```

```python
# BAD:
T = TypeVar("T")
P = ParamSpec("P")
_T = TypeVar("_T", int, float, str)
_F = TypeVar("_F", bound=Callable)
```

### 5.20.9 String types

`str` for string/text data and `bytes` for code that deals with binary data *must* be used.

`typing.Text` *must* not used.

```python
# GOOD:
def deals_with_text_data(x: str) -> str:
  ...

def deals_with_binary_data(x: bytes) -> bytes:
  ...
```

If all the string types of a function are always the same, for example if the return type is the same as the argument type in the code above, use [AnyStr](#5208-type-variables).

### 5.20.10 Imports For Typing

Symbols [including types, functions and constants] from the `typing` or `collections.abc` modules used to support static analysis and type checking *must* always be directly imported. This allows general annotations to be more concise.

```python
# GOOD:
from collections.abc import Mapping
from collections.abc import Sequence
from typing import Any
from typing import cast
from typing import Generic
from typing import TYPE_CHECKING
```

Given that this way of importing adds items to the local namespace, names in `typing` or `collections.abc` should be treated similarly to keywords, and not be defined in code, typed or not.

If there is a collision between a type and an existing name in a module, import it using `import x as y`.

```python
# GOOD:
from typing import Any as AnyType
```

Where possible, built-in types *must* be used as annotations. Python supports type annotations using parametric container types via [PEP-585](https://peps.python.org/pep-0585/)

```python
# GOOD:
def generate_foo_scores(foo: set[str]) -> list[float]:
  ...
```

### 5.20.11 Conditional Imports

Conditional imports *should not* be used.

Use only in exceptional cases where the additional imports needed for type checking must be avoided at runtime. In fact, refactoring code to allow top-level imports *should* be preferred.

Imports that are needed only for type annotations *must* be placed within an `if TYPE_CHECKING:` block.

- Only entities that are used solely for typing should be defined here; this includes aliases. Otherwise it will be a runtime error, as the module will not be imported at runtime.
- The block should be right after all the normal imports.
- There should be no empty lines in the typing imports list.
- Sort this list as if it were a regular imports list.

```python
# GOOD:
import typing
if typing.TYPE_CHECKING:
  import sketch

def f(x: sketch.Sketch): ...
```

### 5.20.12 Circular Dependencies

Cyclic dependencies caused by type annotations indicate flaws in the code. Such code is a good candidate for refactoring.

Replace modules that create circular dependency imports with `Any`. Set an [alias](#5205-type-aliases) with a meaningful name, and use the real type name from this module [any attribute of `Any` is `Any`]. Alias definitions *must* be separated from the last import by one line.

```python
# GOOD:
from typing import Any

# some_mod.py imports this module.
some_mod = Any
...

def my_method(self, var: some_mod.SomeType) -> None:
  ...
```

### 5.20.13 Generics

Type parameters for generic types *should* be specified when annotating; otherwise, [the generics' parameters will be assumed to be `Any`](https://peps.python.org/pep-0484/#the-any-type).

```python
# GOOD:
def get_names(employee_ids: Sequence[int]) -> Mapping[int, str]:
  ...
```

```python
# BAD:
# This is interpreted as get_names(employee_ids: Sequence[Any]) -> Mapping[Any, Any]
def get_names(employee_ids: Sequence) -> Mapping:
  ...
```

If the best type parameter for a generic is `Any`, make it explicit, but remember that in many cases [`TypeVar`](#5208-type-variables) might be more appropriate:

```python
# GOOD:
_T = TypeVar("_T")
def get_names(employee_ids: Sequence[_T]) -> Mapping[_T, str]:
    """Returns a mapping from employee ID to employee name for given IDs."""
```

```python
# BAD:
def get_names(employee_ids: Sequence[Any]) -> Mapping[Any, str]:
    """Returns a mapping from employee ID to employee name for given IDs."""
```
