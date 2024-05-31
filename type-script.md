# Introduction

This code convention is based on the [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html) (GTSSG) dated October 21, 2023, taking into account the project's historical code style.

Like GTSSG this code convention uses [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119) terminology when using the phrases *must*, *must not*, *should*, *should not*, and *may*:
   - **MUST** This word, or the terms "REQUIRED" or "SHALL", mean that the definition is an absolute requirement of the specification.
   - **MUST NOT** This phrase, or the phrase "SHALL NOT", mean that the definition is an absolute prohibition of the specification.
   - **SHOULD** This word, or the adjective "RECOMMENDED", mean that there may exist valid reasons in particular circumstances to ignore a particular item, but the full implications must be understood and carefully weighed before choosing a different course.
   - **SHOULD NOT** This phrase, or the phrase "NOT RECOMMENDED" mean that there may exist valid reasons in particular circumstances when the particular behavior is acceptable or even useful, but the full implications should be understood and the case carefully weighed before implementing any behavior described with this label.
   - **MAY** This word, or the adjective "OPTIONAL", mean that an item is truly optional.

The following notations are used in code examples:

- **EXAMPLE** An example of code demonstrating what is written. This code does not contradict this coding convention.
- **GOOD** An example of code that demonstrates what should be done according to this coding convention.
- **ACCEPTABLE** A code example demonstrating the code acceptable by this coding convention.
- **BAD** An example of code that demonstrates what should not be done. This code contradicts this coding convention.

The current version of the document is not final and may be updated as necessary.

# Table of Contents

- [Introduction](#introduction)
- [Table of Contents](#table-of-contents)
- [1 Source file basics](#1-source-file-basics)
  - [1.1 Language](#11-language)
  - [1.2 Encoding](#12-encoding)
- [2 Source file structure](#2-source-file-structure)
  - [2.1 File header](#21-file-header)
  - [2.2 `@fileoverview` JSDoc](#22-fileoverview-jsdoc)
  - [2.3 Imports](#23-imports)
    - [2.3.1 Import paths](#231-import-paths)
    - [2.3.2 Namespace vs Named imports](#232-namespace-vs-named-imports)
    - [2.3.3 Renaming imports](#233-renaming-imports)
  - [2.4 Exports](#24-exports)
    - [2.4.1 Export visibility](#241-export-visibility)
    - [2.4.2 Mutable exports](#242-mutable-exports)
    - [2.4.3 Container classes](#243-container-classes)
  - [2.5 Import and export type](#25-import-and-export-type)
    - [2.5.1 Import type](#251-import-type)
    - [2.5.2 Export type](#252-export-type)
  - [2.6 Use modules not namespaces](#26-use-modules-not-namespaces)
- [3 Naming](#3-naming)
  - [3.1 Files](#31-files)
  - [3.2 Identifiers](#32-identifiers)
  - [3.2.1 Naming style](#321-naming-style)
    - [3.2.2 Descriptive names](#322-descriptive-names)
  - [3.3 Rules by identifier type](#33-rules-by-identifier-type)
    - [3.3.1 Abbreviations](#331-abbreviations)
    - [3.3.2 Type parameters](#332-type-parameters)
    - [3.3.3 `_` prefix/suffix](#333-_-prefixsuffix)
    - [3.3.4 Constants](#334-constants)
    - [3.3.5 Aliases](#335-aliases)
- [4 Language feature](#4-language-feature)
  - [4.1 Local variable declarations](#41-local-variable-declarations)
    - [4.1.1 Use const and let](#411-use-const-and-let)
    - [4.1.2 One variable per declaration](#412-one-variable-per-declaration)
  - [4.2 Array literals](#42-array-literals)
    - [4.2.1 Do not use the Array constructor](#421-do-not-use-the-array-constructor)
    - [4.2.2 Do not define properties on arrays](#422-do-not-define-properties-on-arrays)
    - [4.2.3 Using spread syntax](#423-using-spread-syntax)
    - [4.2.4 Array destructuring](#424-array-destructuring)
  - [4.3 Object literals](#43-object-literals)
    - [4.3.1 Do not use the Object constructor](#431-do-not-use-the-object-constructor)
    - [4.3.2 Iterating objects](#432-iterating-objects)
    - [4.3.3 Using spread syntax](#433-using-spread-syntax)
    - [4.3.4 Computed property names](#434-computed-property-names)
    - [4.3.5 Object destructuring](#435-object-destructuring)
  - [4.4 Classes](#44-classes)
    - [4.4.1 Class declarations](#441-class-declarations)
    - [4.4.2 Class method declarations](#442-class-method-declarations)
      - [4.4.2.1 Overriding `toString`](#4421-overriding-tostring)
    - [4.4.3 Static methods](#443-static-methods)
      - [4.4.3.1 Avoid private static methods](#4431-avoid-private-static-methods)
      - [4.4.3.2 Do not rely on dynamic dispatch](#4432-do-not-rely-on-dynamic-dispatch)
      - [4.4.3.3 Avoid static `this` references](#4433-avoid-static-this-references)
    - [4.4.4 Constructors](#444-constructors)
    - [4.4.5 Class members](#445-class-members)
      - [4.4.5.1 Do not use `#private` fields](#4451-do-not-use-private-fields)
      - [4.4.5.2 Use readonly](#4452-use-readonly)
      - [4.4.5.3 Parameter properties](#4453-parameter-properties)
      - [4.4.5.4 Field initializers](#4454-field-initializers)
      - [4.4.5.5 Properties used outside of class lexical scope](#4455-properties-used-outside-of-class-lexical-scope)
      - [4.4.5.6 Getters and setters](#4456-getters-and-setters)
      - [4.4.5.7 Computed properties](#4457-computed-properties)
    - [4.4.6. Visibility](#446-visibility)
    - [4.4.7 Disallowed class patterns](#447-disallowed-class-patterns)
      - [4.4.7.1 Do not manipulate `prototypes` directly](#4471-do-not-manipulate-prototypes-directly)
  - [4.5 Functions](#45-functions)
    - [4.5.1 Terminology](#451-terminology)
    - [4.5.2 Prefer function declarations for named functions](#452-prefer-function-declarations-for-named-functions)
    - [4.5.3 Nested functions](#453-nested-functions)
    - [4.5.4 Do not use function expressions](#454-do-not-use-function-expressions)
    - [4.5.5 Arrow function bodies](#455-arrow-function-bodies)
    - [4.5.6 Rebinding `this`](#456-rebinding-this)
    - [4.5.7 Prefer passing arrow functions as callbacks](#457-prefer-passing-arrow-functions-as-callbacks)
    - [4.5.8 Arrow functions as properties](#458-arrow-functions-as-properties)
    - [4.5.9 Event handlers](#459-event-handlers)
    - [4.5.10 Parameter initializers](#4510-parameter-initializers)
    - [4.5.11 Prefer rest and spread when appropriate](#4511-prefer-rest-and-spread-when-appropriate)
    - [4.5.12 Formatting functions](#4512-formatting-functions)
  - [4.6 `this`](#46-this)
  - [4.7 Primitive literals](#47-primitive-literals)
    - [4.7.1 String literals](#471-string-literals)
      - [4.7.1.1 Use single quotes](#4711-use-single-quotes)
      - [4.7.1.2 No line continuations](#4712-no-line-continuations)
      - [4.7.1.3. Template literals](#4713-template-literals)
    - [4.7.2. Number literals](#472-number-literals)
    - [4.7.3. Type coercion](#473-type-coercion)
    - [4.7.3.1. Explicit coercion](#4731-explicit-coercion)
      - [4.7.3.2. Implicit coercion](#4732-implicit-coercion)
- [TODO: Возможно это \[то что ниже\] имеет смысл вынести отсюда.](#todo-возможно-это-то-что-ниже-имеет-смысл-вынести-отсюда)
  - [4.8. Control structures](#48-control-structures)
    - [4.8.1. Control flow statements and blocks](#481-control-flow-statements-and-blocks)
      - [4.8.1.2. Assignment in control statements](#4812-assignment-in-control-statements)
      - [4.8.1.3. Iterating containers](#4813-iterating-containers)
    - [4.8.2. Grouping parentheses](#482-grouping-parentheses)
    - [4.8.3. Exception handling](#483-exception-handling)
      - [4.8.3.1. Instantiate errors using `new`](#4831-instantiate-errors-using-new)
      - [4.8.3.2. Only throw errors](#4832-only-throw-errors)
      - [4.8.3.3. Catching and rethrowing](#4833-catching-and-rethrowing)
      - [4.8.3.4. Empty catch blocks](#4834-empty-catch-blocks)
    - [4.8.4. Switch statements](#484-switch-statements)
    - [4.8.5. Equality checks](#485-equality-checks)
- [4.8.6. Type and non-nullability assertions](#486-type-and-non-nullability-assertions)
      - [4.8.6.1. Type assertion syntax](#4861-type-assertion-syntax)
      - [4.8.6.2. Double assertions](#4862-double-assertions)
      - [4.8.6.3. Type assertions and object literals](#4863-type-assertions-and-object-literals)
    - [4.8.7. Keep try blocks focused](#487-keep-try-blocks-focused)
- [4.9. Disallowed features](#49-disallowed-features)
    - [4.9.1. Wrapper objects for primitive types](#491-wrapper-objects-for-primitive-types)
    - [4.9.2. Automatic Semicolon Insertion](#492-automatic-semicolon-insertion)
    - [4.9.3. Const enums](#493-const-enums)
    - [4.9.4. Debugger statements](#494-debugger-statements)
    - [4.9.5. Do not use `with`](#495-do-not-use-with)
    - [4.9.6. Dynamic code evaluation](#496-dynamic-code-evaluation)
    - [4.9.7. Non-standard features](#497-non-standard-features)
    - [4.9.8. Modifying builtin objects](#498-modifying-builtin-objects)
- [5. Type system](#5-type-system)
  - [5.1. Type inference](#51-type-inference)
    - [5.1.1. Return types](#511-return-types)
  - [5.2. Undefined and null](#52-undefined-and-null)
    - [5.2.1. Nullable/undefined type aliases](#521-nullableundefined-type-aliases)
    - [5.2.2. Prefer optional over `|undefined`](#522-prefer-optional-over-undefined)
  - [5.3. Use structural types](#53-use-structural-types)
  - [5.4. Prefer interfaces over type literal aliases](#54-prefer-interfaces-over-type-literal-aliases)
  - [5.5. `Array<T>` Type](#55-arrayt-type)
  - [5.6. Indexable types / index signatures (`{[key: string]: T}`)](#56-indexable-types--index-signatures-key-string-t)
  - [5.7. Mapped and conditional types](#57-mapped-and-conditional-types)
- [TODO: Возможно имеет смысл все это сделать ссылкой.](#todo-возможно-имеет-смысл-все-это-сделать-ссылкой)
  - [5.8. `any` Type](#58-any-type)
    - [5.8.1. Providing a more specific type](#581-providing-a-more-specific-type)
    - [5.8.2. Using `unknown` over `any`](#582-using-unknown-over-any)
    - [5.8.3. Suppressing `any` lint warnings](#583-suppressing-any-lint-warnings)
  - [5.9. `{}` Type](#59--type)
  - [5.10. Tuple types](#510-tuple-types)
  - [5.11. Wrapper types](#511-wrapper-types)
- [6. Comments and documentation](#6-comments-and-documentation)
  - [6.1. JSDoc versus comments](#61-jsdoc-versus-comments)
  - [6.2. Multi-line comments](#62-multi-line-comments)
  - [6.3. JSDoc general form](#63-jsdoc-general-form)
  - [6.4. Markdown](#64-markdown)
  - [6.5. JSDoc tags](#65-jsdoc-tags)
  - [6.6. Line wrapping](#66-line-wrapping)
  - [6.7. Document all top-level exports of modules](#67-document-all-top-level-exports-of-modules)
  - [6.8. Class comments](#68-class-comments)
  - [6.9. Method and function comments](#69-method-and-function-comments)
  - [6.10. Parameter property comments](#610-parameter-property-comments)
  - [6.11. JSDoc type annotations](#611-jsdoc-type-annotations)
  - [6.12. Make comments that actually add information](#612-make-comments-that-actually-add-information)
- [TODO](#todo)
- [Syntax](#syntax)

# 1 Source file basics

## 1.1 Language

Only the US English language *must* be used in the code.

```typescript
// GOOD:
// Color name.
const colorName: string = 'white';

// BAD:
// Имя цвета.
const colourName: string = 'white';
```

## 1.2 Encoding

Source files *must* be encoded in UTF-8.

# 2 Source file structure

Files *should* consist of the following, in order:
1. File header;
2. JSDoc with @fileoverview [if present];
3. Imports [if present];
4. The file’s implementation.

Exactly one blank line separates each section that is present.

## 2.1 File header

The file header is located at the beginning of the file and must have the following structure:

```typescript
/*
 * File: <file-name>
 * Project: cdm-audio-platform-api
 * File Created: <date-time-in-format dddd, Do MMMM YYYY, h:mm:ss a>
 * Author: <user-name> (<user-email>)
 * -----
 * Last Modified: <date-time-in-format dddd, Do MMMM YYYY, h:mm:ss a>
 * Modified By: <user-name> (<user-email>)
 * -----
 * Copyright 2019 - 2024, General Harmonics Corporation. All Rights Reserved.
 * Unauthorized copying of this file, via any medium is strictly prohibited
 * Proprietary and confidential.
 */
```

The file header of the specified format is automatically generated and updated by the [Psioniq File Header](https://github.com/davidquinn/psi-header) Visual Studio Code extension.

<!-- TODO: Add info about creating a file header — "To install and configure this extension, refer to [link]()." -->


## 2.2 `@fileoverview` JSDoc

A file *may* have a top-level `@fileoverview` JSDoc. If present, it may provide a description of the file's content, its uses, or information about its dependencies. Wrapped lines are not indented.

```typescript
/**
 * @fileoverview Description of file. Lorem ipsum dolor sit amet, consectetur
 * adipiscing elit, sed do eiusmod tempor incididunt.
 */
```

## 2.3 Imports

Code *must* use only ES6 module import syntax. It's not allowed to use `require` (as in `import x = require('...');`) to import.

There are four variants of import statements:

| Import type | Example | Use for |
| --- | --- | --- |
| module | `import * as foo from '...';` | TypeScript imports |
| named | `import { SomeThing } from '...';` | TypeScript imports |
| default | `import SomeThing from '...';` | Only for other external code that requires them |
| side-effect | `import '...';` | Only to import libraries for their side-effects on load (such as custom elements) |

```typescript
// GOOD: Choose between two options as appropriate (see below).
import * as ng from '@angular/core';
import { Foo } from './foo';

// ACCEPTABLE: Only when needed: default imports.
import Button from 'Button';

// ACCEPTABLE: Sometimes needed to import libraries for their side effects.
import 'jasmine';
import '@polymer/paper-button';

// BAD: Do not use require().
import x = require('mydep');
```

### 2.3.1 Import paths

TypeScript code *must* use paths to import other TypeScript code. Paths *may* be relative, i.e. starting with `.` or `..`, or rooted at the base directory, e.g. `root/path/to/file`.

Code *should* use relative imports (`./foo`) rather than absolute imports `path/to/foo` when referring to files within the same (logical) project as this allows to move the project around without introducing changes in these imports.

Consider limiting the number of parent steps (`../../../`) as those can make module and path structures hard to understand.

```typescript
import { Symbol1 } from 'path/from/root';
import { Symbol2 } from '../parent/file';
import { Symbol3 } from './sibling';
```

### 2.3.2 Namespace vs Named imports

Both namespace and named imports *may* be used.

Prefer named imports for symbols used frequently in a file or for symbols that have clear names. Named imports can be aliased to clearer names as needed with `as`.

Prefer namespace imports when using many different symbols from large APIs. A namespace import, despite using the `*` character, is not comparable to a wildcard import as seen in other languages. Instead, namespace imports give a name to all the exports of a module, and each exported symbol from the module becomes a property on the module name. Namespace imports can aid readability for exported symbols that have common names like `Model` or `Controller` without the need to declare aliases.

```typescript
// GOOD: Use the module for namespacing.
import * as tableview from './tableview';

let item: tableview.Item|undefined;

// BAD: Overlong import statement of needlessly namespaced names.
import { Item as TableviewItem, Header as TableviewHeader, Row as TableviewRow,
  Model as TableviewModel, Renderer as TableviewRenderer } from './tableview';

let item: TableviewItem|undefined;
```
```typescript
// GOOD: Give local names for these common functions.
import { describe, it, expect } from './testing';

describe('foo', () => {
  it('bar', () => {
    expect(null).toBeNull();
    expect(undefined).toBeUndefined();
  });
});

// BAD: The module name does not improve readability.
import * as testing from './testing';

testing.describe('foo', () => {
  testing.it('bar', () => {
    testing.expect(null).toBeNull();
    testing.expect(undefined).toBeUndefined();
  });
});
```

### 2.3.3 Renaming imports

Code *should* fix name collisions by using a namespace import or renaming the exports themselves. Code *may* rename imports [`import { SomeThing as SomeOtherThing }`] if needed.

Three examples where renaming can be helpful:
1. If it's necessary to avoid collisions with other imported symbols.
2. If the imported symbol name is generated.
3. If importing symbols whose names are unclear by themselves, renaming can improve code clarity.

## 2.4 Exports

Named exports *must* be used in all code.

Do not use default exports. This ensures that all imports follow a uniform pattern.

```typescript
// GOOD:
export class Foo { ... }

// BAD:
export default class Foo { ... }
```

[More information](https://google.github.io/styleguide/tsguide.html#exports).

### 2.4.1 Export visibility

TypeScript does not support restricting the visibility for exported symbols. Only export symbols that are used outside of the module. Generally minimize the exported API surface of modules.

### 2.4.2 Mutable exports

*Must not* use `export let`.

Regardless of technical support, mutable exports can create hard to understand and debug code, in particular with re-exports across multiple modules.

```typescript
// BAD:
export let foo = 3;

window.setTimeout(() => {
  foo = 4;
}, 1000 /* ms */);
```

### 2.4.3 Container classes

Сontainer classes *must not* be created with static methods or properties for the sake of namespacing.

```typescript
// BAD:
export class Container {
  static FOO = 1;
  static bar() { return 1; }
}
```

Instead, export individual constants and functions.

```typescript
// GOOD:
export const FOO = 1;
export function bar() { return 1; }
```

## 2.5 Import and export type

### 2.5.1 Import type

You *may* use `import type { ... }` when you use the imported symbol only as a type. Use regular imports for values.

```typescript
// GOOD:
import type { Foo } from './foo';
import { Bar } from './foo';

import { type Foo, Bar } from './foo';
```

[More information](https://google.github.io/styleguide/tsguide.html#import-type).

### 2.5.2 Export type

`export type` *must* be used when re-exporting a type.

```typescript
// GOOD:
export type { AnInterface } from './foo';
```

[More information](https://google.github.io/styleguide/tsguide.html#export-type).

## 2.6 Use modules not namespaces

Code *must not* use the `namespace Foo { ... }` construct. `namespaces` may only be used when required to interface with external, third party code (see [para. 2.3.2.](#2-3-2-namespace-vs-named-imports)). To semantically namespace your code, use separate files.

```typescript
// BAD: do not use namespaces.
namespace Rocket {
  function launch() { ... }
}
```

# 3 Naming

## 3.1 Files

File names *must* use only ASCII letters, digits and underscores.

The `snake_case` *should* be used in file names.

## 3.2 Identifiers

Identifiers *must* use only ASCII letters, digits and underscores (only in constant names).

## 3.2.1 Naming style

TypeScript expresses information in types, so names *should not* be decorated with information that is included in the type.

Some concrete examples of this rule:

  - Do not use trailing or leading underscores for private properties or methods.
  - Do not use the `opt_` prefix for optional parameters (for accessors, see [accessor rules]() below).
  - Do not mark interfaces specially (`IMyInterface` or `MyFooInterface`). When introducing an interface for a class, give it a name that expresses why the interface exists in the first place (e.g. `class TodoItem` and `interface TodoItemStorage` if the interface expresses the format used for storage/serialization in JSON).

### 3.2.2 Descriptive names

Names *must* be descriptive and clear to a new reader. Do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

**Exception:** Variables that are in scope for 10 lines or fewer, including arguments that are not part of an exported API, *may* use short (e.g. single letter) variable names.

```typescript
// GOOD:
errorCount          // No abbreviation.
dnsConnectionIndex  // Most people know what "DNS" stands for.
referrerUrl         // Ditto for "URL".
customerId          // "Id" is both ubiquitous and unlikely to be misunderstood.

// BAD:
n                   // Meaningless.
nErr                // Ambiguous abbreviation.
nCompConns          // Ambiguous abbreviation.
wgcConnections      // Only your group knows what this stands for.
pcReader            // Lots of things can be abbreviated "pc".
cstmrId             // Deletes internal letters.
kSecondsPerDay      // Do not use Hungarian notation.
customerID          // Incorrect camelcase of "ID".
```

## 3.3 Rules by identifier type

Most identifier names *should* follow the casing in the table below, based on the identifier's type.

| Style	| Category |
|---|---|
| UpperCamelCase | Class, interface, type, enum, decorator, type parameters. |
| lowerCamelCase | Variable, parameter, function, method, property, module alias. |
| CONSTANT_CASE | Global constant values (including enum values). See [para. 3.2.4.](#3-2-4-constants) below. |
| #ident | Private identifiers are never used. |

### 3.3.1 Abbreviations

Treat abbreviations like acronyms in names as whole words, i.e. use `loadHttpUrl`, not `loadHTTPURL`.

### 3.3.2 Type parameters

Type parameters, like in `Array<T>`, *may* use a single upper case character (`T`) or UpperCamelCase.

### 3.3.3 `_` prefix/suffix

Identifiers *must not* use `_` as a prefix or suffix.

This also means that `_` *must not* be used as an identifier by itself (e.g. to indicate a parameter is unused).

### 3.3.4 Constants

**Immutable:** CONSTANT_CASE indicates that a value is intended to not be changed, and may be used for values that can technically be modified (i.e. values that are not deeply frozen) to indicate to users that they *must not* be modified.

```typescript
// EXAMPLE:
const UNIT_SUFFIXES = {
  'milliseconds': 'ms',
  'seconds': 's',
};
// Even though per the rules of JavaScript UNIT_SUFFIXES is
// mutable, the uppercase shows users to not modify it.
```

A constant can also be a `static readonly` property of a class.

```typescript
// EXAMPLE:
class Foo {
  private static readonly MY_SPECIAL_NUMBER = 5;

  bar() {
    return 2 * Foo.MY_SPECIAL_NUMBER;
  }
}
```

**Global:** Only symbols declared on the module level, static fields of module level classes, and values of module level enums, *may* use `CONST_CASE`. If a value can be instantiated more than once over the lifetime of the program (e.g. a local variable declared within a function, or a static field on a class nested in a function) then it *must* use `lowerCamelCase`.

If a value is an arrow function that implements an interface, then it may be declared `lowerCamelCase`.

### 3.3.5 Aliases

When creating a local-scope alias of an existing symbol, use the format of the existing identifier. The local alias *must* match the existing naming and format of the source. For variables use `const` for your local aliases, and for class fields use the `readonly` attribute.

**Note:** If you're creating an alias just to expose it to a template in your framework of choice, remember to also apply the proper [access modifiers](...).

```typescript
// EXAMPLE
const {BrewStateEnum} = SomeType;
const CAPACITY = 5;

class Teapot {
  readonly BrewStateEnum = BrewStateEnum;
  readonly CAPACITY = CAPACITY;
}
```

# 4 Language feature

This section delineates which features may or may not be used, and any additional constraints on their use.

Language features which are not discussed in this style guide may be used with no recommendations of their usage.

## 4.1 Local variable declarations

### 4.1.1 Use const and let

`const` or `let` *must* always be used to declare variables. Use `const` by default, unless a variable needs to be reassigned. Never use `var`.

`const` and `let` are block scoped, like variables in most other languages. `var` in JavaScript is function scoped, which can cause difficult to understand bugs. Don't use it.

```typescript
// GOOD: Use if "foo" never changes.
const foo = otherValue;

// GOOD: Use if "bar" is ever assigned into later on.
let bar = someValue;

// BAD: Don't use — var scoping is complex and causes bugs.
var foo = someValue;
```

Variables *must not* be used before their declaration.

### 4.1.2 One variable per declaration

Every local variable declaration *must* declare only one variable. Declaring multiple variables at the same time is not used.

```typescript
// GOOD:
let a = 1;
let b = 2;

// BAD:
let a = 1, b = 2;
```

## 4.2 Array literals

### 4.2.1 Do not use the Array constructor

The `Array()` constructor *must not* be used, with or without `new`. It has confusing and contradictory usage:

```typescript
// BAD:
const a = new Array(2); // [undefined, undefined]
const b = new Array(2, 3); // [2, 3];
```

Instead, always use bracket notation to initialize arrays, or `from` to initialize an `Array` with a certain size:

```typescript
// GOOD:
const a = [2];
const b = [2, 3];

// ACCEPTABLE: Equivalent to Array(2):
const c = [];
c.length = 2;

// ACCEPTABLE: [0, 0, 0, 0, 0]
Array.from<number>({length: 5}).fill(0);
```

### 4.2.2 Do not define properties on arrays

Do not define or use non-numeric properties on an array (other than `length`). Use a `Map` (or `Object`) instead.


### 4.2.3 Using spread syntax

Using spread syntax `[...foo];` is a convenient shorthand for shallow-copying or concatenating iterables.

```typescript
// GOOD:
const foo = [
  1,
];

const foo2 = [
  ...foo,
  6,
  7,
];

const foo3 = [
  5,
  ...foo,
];

foo2[1] === 6;
foo3[1] === 1;
```

When using spread syntax, the value being spread *must* match what is being created. When creating an array, only spread iterables. Primitives (including `null` and `undefined`) *must not* be spread.

```typescript
// GOOD:
const foo = shouldUseFoo ? [7] : [];
const bar = [5, ...foo];

// BAD: might be undefined.
const foo = [7];
const bar = [5, ...(shouldUseFoo && foo)];
```

### 4.2.4 Array destructuring

Array literals *may* be used on the left-hand side of an assignment to perform destructuring (such as when unpacking multiple values from a single array or iterable). A final “rest” element may be included (with no space between the `...` and the variable name). Elements should be omitted if they are unused.

```typescript
// EXAMPLE:
const [a, b, c, ...rest] = generateResults();
let [, b,, d] = someArray;
```

Destructuring may also be used for function parameters. Always specify `[]` as the default value if a destructured array parameter is optional, and provide default values on the left hand side:

```typescript
// GOOD:
function destructured([a = 4, b = 2] = []) { … }

// BAD:
function badDestructuring([a, b] = [4, 2]) { … }
```

**Tip:** For (un)packing multiple values into a function’s parameter or return, prefer object destructuring to array destructuring when possible, as it allows naming the individual elements and specifying a different type for each.

## 4.3 Object literals

### 4.3.1 Do not use the Object constructor

The `Object` constructor *must not* be used. Use an object literal (`{}` or `{a: 0, b: 1, c: 2}`) instead.

```typescript
// GOOD:
let myObject = {
  a: 1,
  b: 2,
  c: 3
};

// BAD:
let myObject = new Object();
myObject.a = 1;
myObject.b = 2;
myObject.c = 3;
```

### 4.3.2 Iterating objects

Iterating objects with `for (... in ...)` is error prone. It will include enumerable properties from the prototype chain.

Unfiltered `for (... in ...)` statements must not be used:

```typescript
// BAD: x could come from some parent prototype!
for (const x in someObj) {
  ...
}
```

Either filter values explicitly with an `if` statement, or use `for (... of Object.keys(...))`.

```typescript
// EXAMPLE: now x was definitely defined on someObj.
for (const x in someObj) {
  if (!someObj.hasOwnProperty(x)) continue;
  ...
}

// EXAMPLE: now x was definitely defined on someObj.
for (const x of Object.keys(someObj)) {
  ...
}

// EXAMPLE: now key was definitely defined on someObj.
for (const [key, value] of Object.entries(someObj)) {
  ...
}
```

### 4.3.3 Using spread syntax

Using spread syntax `{...bar}` is a convenient shorthand for creating a shallow copy of an object. When using spread syntax in object initialization, later values replace earlier values at the same key.

```typescript
// EXAMPLE:
const foo = {
  num: 1,
};

const foo2 = {
  ...foo,
  num: 5,
};

const foo3 = {
  num: 5,
  ...foo,
}

foo2.num === 5;
foo3.num === 1;
```

When using spread syntax, the value being spread *must* match what is being created. That is, when creating an object, only objects may be spread; arrays and primitives (including `null` and `undefined`) *must not* be spread. Avoid spreading objects that have prototypes other than the Object prototype (e.g. class definitions, class instances, functions) as the behavior is unintuitive (only enumerable non-prototype properties are shallow-copied).

```typescript
// GOOD:
const foo = shouldUseFoo ? {num: 7} : {};
const bar = {num: 5, ...foo};

// BAD: might be undefined.
const foo = {num: 7};
const bar = {num: 5, ...(shouldUseFoo && foo)};
```

### 4.3.4 Computed property names

Computed property names (e.g. `{['key' + foo()]: 42}`) *may* be used, and are considered dict-style (quoted) keys (i.e., must not be mixed with non-quoted keys) unless the computed property is a [symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (e.g. `[Symbol.iterator]`).

### 4.3.5 Object destructuring

Object destructuring patterns *may* be used on the left-hand side of an assignment to perform destructuring and unpack multiple values from a single object.

Destructured objects *may* also be used as function parameters, but should be kept as simple as possible: a single level of unquoted shorthand properties. Deeper levels of nesting and computed properties may not be used in parameter destructuring. Specify any default values in the left-hand-side of the destructured parameter (`{str = 'some default'} = {}`, rather than `{str} = {str: 'some default'}`), and if a destructured object is itself optional, it must default to `{}`.

```typescript
// EXAMPLE:
interface Options {
  num?: number;
  str?: string;
}

function destructured({num, str = 'default'}: Options = {}) {}

// BAD:
function nestedTooDeeply({x: {num, str}}: {x: Options}) {}
function nontrivialDefault({num, str}: Options = {num: 42, str: 'default'}) {}
```

## 4.4 Classes

### 4.4.1 Class declarations

Class declarations *must not* be terminated with semicolons.

```typescript
// GOOD:
class Foo {
}

// BAD: Unnecessary semicolon.
class Foo {
};
```

In contrast, statements that contain class expressions *must* be terminated with a semicolon.

```typescript
// GOOD: Semicolon here as this is a statement, not a declaration.
export const Baz = class extends Bar {
  method(): number {
    return this.x;
  }
};

// BAD:
exports const Baz = class extends Bar {
  method(): number {
    return this.x;
  }
}
```

Blank lines *should not* separate class declaration braces from other class content.

``` typescript
// GOOD: No spaces around braces.
class Baz {
  method(): number {
    return this.x;
  }
}

// BAD:
class Foo {

  method(): number {
    return this.x;
  }

}
```

### 4.4.2 Class method declarations

Class method declarations *must not* use a semicolon to separate individual method declarations.

```typescript
// GOOD:
class Foo {
  doThing() {
    console.log("A");
  }
}

// BAD: Unnecessary semicolon.
class Foo {
  doThing() {
    console.log("A");
  };
}
```

Method declarations *should* be separated from surrounding code by a single blank line.

```typescript
// GOOD:
class Foo {
  doThing() {
    console.log("A");
  }

  getOtherThing(): number {
    return 4;
  }
}

// BAD:
class Foo {
  doThing() {
    console.log("A");
  }
  getOtherThing(): number {
    return 4;
  }
}
```

#### 4.4.2.1 Overriding `toString`

The `toString` method *may* be overridden, but must always succeed and never have visible side effects.

**Tip:** Beware, in particular, of calling other methods from toString, since exceptional conditions could lead to infinite loops.

### 4.4.3 Static methods

#### 4.4.3.1 Avoid private static methods

Where it does not interfere with readability, prefer module-local functions over private static methods.

#### 4.4.3.2 Do not rely on dynamic dispatch

Code *should not* rely on dynamic dispatch of static methods. Static methods *should* only be called on the base class itself (which defines it directly). Static methods *should not* be called on variables containing a dynamic instance that may be either the constructor or a subclass constructor, and *must not* be called directly on a subclass that doesn’t define the method itself.

```typescript
// Context for the examples below (this class is okay by itself).
class Base {
  static foo() {}
}

class Sub extends Base {}

// BAD: Don't call static methods dynamically.
function callFoo(cls: typeof Base) {
  cls.foo();
}

// BAD: Don't call static methods on subclasses that don't define it themselves.
Sub.foo();

// BAD: Don't access this in static methods.
class MyClass {
  static foo() {
    return this.staticField;
  }
}

MyClass.staticField = 1;
```

#### 4.4.3.3 Avoid static `this` references

Code *must not* use this in a static context.

JavaScript allows accessing static fields through `this`. Different from other languages, static fields are also inherited.

```typescript
class ShoeStore {
  static storage: Storage = ...;

  static isAvailable(s: Shoe) {
    // BAD: Do not use `this` in a static method.
    return this.storage.has(s.id);
  }
}

class EmptyShoeStore extends ShoeStore {
  // Overrides storage from ShoeStore.
  static storage: Storage = EMPTY_STORE;
}
```

This code is generally surprising: authors might not expect that static fields can be accessed through the this pointer, and might be surprised to find that they can be overridden — this feature is not commonly used.

This code also encourages an anti-pattern of having substantial static state, which causes problems with testability.

### 4.4.4 Constructors

Constructor calls *must* use parentheses, even when no arguments are passed.

```typescript
// GOOD:
const x = new Foo();

// BAD:
const x = new Foo;
```

Omitting parentheses can lead to subtle mistakes. These two lines are not equivalent:

```typescript
// EXAMPLE:
new Foo().Bar();
new Foo.Bar();
```

It is unnecessary to provide an empty constructor or one that simply delegates into its parent class because ES2015 provides a default class constructor if one is not specified. However constructors with parameter properties, visibility modifiers or parameter decorators should not be omitted even if the body of the constructor is empty.

```typescript
// GOOD:
class DefaultConstructor {
}

class ParameterProperties {
  constructor(private myService) {}
}

class ParameterDecorators {
  constructor(@SideEffectDecorator myService) {}
}

class NoInstantiation {
  private constructor() {}
}

// BAD:
class UnnecessaryConstructor {
  constructor() {}
}

class UnnecessaryConstructorOverride extends Base {
    constructor(value: number) {
      super(value);
    }
}
```

The constructor *should* be separated from surrounding code both above and below by a single blank line.

```typescript
// GOOD:
class Foo {
  myField = 10;

  constructor(private readonly ctorParam) {}

  doThing() {
    console.log(ctorParam.getThing() + myField);
  }
}

// BAD:
class Foo {
  myField = 10;
  constructor(private readonly ctorParam) {}
  doThing() {
    console.log(ctorParam.getThing() + myField);
  }
}
```

### 4.4.5 Class members

#### 4.4.5.1 Do not use `#private` fields

Private fields (also known as private identifiers) *must not* be used. Instead, use TypeScript's visibility annotations.

```typescript
// GOOD:
class Clazz {
  private ident = 1;
}

//BAD:
class Clazz {
  #ident = 1;
}
```

Private identifiers cause substantial emit size and performance regressions when down-leveled by TypeScript, and are unsupported before ES2015. They can only be downleveled to ES2015, not lower. At the same time, they do not offer substantial benefits when static type checking is used to enforce visibility.

#### 4.4.5.2 Use readonly

Mark properties that are never reassigned outside of the constructor with the `readonly` modifier (these need not be deeply immutable).

#### 4.4.5.3 Parameter properties

The [parameter property](https://www.typescriptlang.org/docs/handbook/2/classes.html#parameter-properties) *must* be used, rather than plumbing an obvious initializer through to a class member.

```typescript
// GOOD:
class Foo {
  constructor(private readonly barService: BarService) {}
}

// BAD:
class Foo {
  private readonly barService: BarService;

  constructor(barService: BarService) {
    this.barService = barService;
  }
}
```

If the parameter property needs documentation, [use an `@param` JSDoc tag](...).

#### 4.4.5.4 Field initializers

If a class member is not a parameter, initialize it where it's declared, which sometimes lets you drop the constructor entirely.

```typescript
// GOOD:
class Foo {
  private readonly userList: string[] = [];
}

// BAD:
class Foo {
  private readonly userList: string[];

  constructor() {
    this.userList = [];
  }
}
```

**Tip:** Properties should never be added to or removed from an instance after the constructor is finished, since it significantly hinders VMs’ ability to optimize classes' “shape”. Optional fields that may be filled in later should be explicitly initialized to `undefined` to prevent later shape changes.

#### 4.4.5.5 Properties used outside of class lexical scope

Properties used from outside the lexical scope of their containing class, *must not* use `private` visibility, as they are used outside of the lexical scope of their containing class.

Use either `protected` or `public` as appropriate to the property in question.

TypeScript code *must not* use `obj['foo']` to bypass the visibility of a property.

When a property is `private`, you are declaring to both automated systems and humans that the property accesses are scoped to the methods of the declaring class, and they will rely on that. For example, a check for unused code will flag a private property that appears to be unused, even if some other file manages to bypass the visibility restriction.

Though it might appear that `obj['foo']` can bypass visibility in the TypeScript compiler, this pattern can be broken by rearranging the build rules, and also violates [optimization compatibility](https://google.github.io/styleguide/tsguide.html#optimization-compatibility).

#### 4.4.5.6 Getters and setters

Getters and setters, also known as accessors, for class members *may* be used. The getter method *must* be a [pure function](https://en.wikipedia.org/wiki/Pure_function) (i.e., result is consistent and has no side effects: getters *must not* change observable state). They are also useful as a means of restricting the visibility of internal or verbose implementation details.

```typescript
// GOOD:
class Foo {
  constructor(private readonly someService: SomeService) {}

  get someMember(): string {
    return this.someService.someVariable;
  }

  set someMember(newValue: string) {
    this.someService.someVariable = newValue;
  }
}

// BAD: Getter changes observable state.
class Foo {
  nextId = 0;
  get next() {
    return this.nextId++;
  }
}
```

If an accessor is used to hide a class property, the hidden property *may* be prefixed or suffixed with any whole word, like `internal` or `wrapped`. When using these private properties, access the value through the accessor whenever possible. At least one accessor for a property *must* be non-trivial: do not define “pass-through” accessors only for the purpose of hiding a property. Instead, make the property public (or consider making it `readonly` rather than just defining a getter with no setter).

```typescript
// GOOD:
class Foo {
  private wrappedBar = '';

  get bar() {
    return this.wrappedBar || 'bar';
  }

  set bar(wrapped: string) {
    this.wrappedBar = wrapped.trim();
  }
}

// BAD: Neither of these accessors have logic, so just make bar public.
class Bar {
  private barInternal = '';

  get bar() {
    return this.barInternal;
  }

  set bar(value: string) {
    this.barInternal = value;
  }
}
```

Getters and setters *must not* be defined using `Object.defineProperty`, since this interferes with property renaming.

#### 4.4.5.7 Computed properties

Computed properties may only be used in classes when the property is a symbol. Dict-style properties (that is, quoted or computed non-symbol keys) are not allowed. A `[Symbol.iterator]` method should be defined for any classes that are logically iterable. Beyond this, `Symbol` should be used sparingly.

**Tip:** Be careful of using any other built-in symbols (e.g. `Symbol.isConcatSpreadable`) as they are not polyfilled by the compiler and will therefore not work in older browsers.

### 4.4.6. Visibility

Restricting visibility of properties, methods, and entire types helps with keeping code decoupled.

- Limit symbol visibility as much as possible.
- Consider converting private methods to non-exported functions within the same file but outside of any class, and moving private properties into a separate, non-exported class.
- TypeScript symbols are public by default. Never use the `public` modifier except when declaring non-readonly public parameter properties (in constructors).

```typescript
class Foo {
  // GOOD: Public modifier not needed.
  bar = new Bar();

  // ACCEPTABLE: Public modifier allowed.
  constructor(public baz: Baz) {}
}

class Foo {
  // BAD: Public modifier not needed.
  public bar = new Bar();

  // BAD: Readonly implies it's a property which defaults to public.
  constructor(public readonly baz: Baz) {}
}
```

See also [export visibility](#241-export-visibility).

### 4.4.7 Disallowed class patterns

#### 4.4.7.1 Do not manipulate `prototypes` directly

The `class` keyword allows clearer and more readable class definitions than defining `prototype` properties. Ordinary implementation code has no business manipulating these objects. Mixins and modifying the prototypes of builtin objects are explicitly forbidden.

## 4.5 Functions

### 4.5.1 Terminology

There are many different types of functions, with subtle distinctions between them. This guide uses the following terminology, which aligns with [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions):

- “function declaration”: a declaration (i.e. not an expression) using the `function` keyword;
- “function expression”: an expression, typically used in an assignment or passed as a parameter, using the `function` keyword;
- “arrow function”: an expression using the `=>` syntax;
- “block body”: right hand side of an arrow function with braces;
- “concise body”: right hand side of an arrow function without braces.

Methods and classes/constructors are not covered in this section.

### 4.5.2 Prefer function declarations for named functions

Prefer function declarations over arrow functions or function expressions when defining named functions.

```typescript
// GOOD:
function foo() {
  return 42;
}

// BAD:
const foo = () => 42;
```

Arrow functions *may* be used, for example, when an explicit type annotation is required.

```typescript
// EXAMPLE:
interface SearchFunction {
  (source: string, subString: string): boolean;
}

const fooSearch: SearchFunction = (source, subString) => { ... };
```

### 4.5.3 Nested functions

Functions nested within other methods or functions *may* use function declarations or arrow functions, as appropriate. In method bodies in particular, arrow functions are preferred because they have access to the outer this.

### 4.5.4 Do not use function expressions

Function expressions *should not* be used. Use arrow functions instead.

```typescript
// GOOD:
bar(() => { this.doSomething(); })

// BAD:
bar(function() { ... })
```

**Exception:** Function expressions *may* be used only if code has to dynamically rebind `this` (but this is [discouraged](#456-rebinding-this)), or for generator functions (which do not have an arrow syntax).

### 4.5.5 Arrow function bodies

Use arrow functions with concise bodies (i.e. expressions) or block bodies as appropriate.

```typescript
// EXAMPLE:
// Top level functions use function declarations.
function someFunction() {
  // Block bodies are fine:
  const receipts = books.map((b: Book) => {
    const receipt = payMoney(b.price);
    recordTransaction(receipt);
    return receipt;
  });

  // Concise bodies are fine, too, if the return value is used:
  const longThings = myValues.filter(v => v.length > 1000).map(v => String(v));

  function payMoney(amount: number) {
    // function declarations are fine, but must not access `this`.
  }

  // Nested arrow functions may be assigned to a const.
  const computeTax = (amount: number) => amount * 0.12;
}
```

Only use a concise body if the return value of the function is actually used. The block body makes sure the return type is `void` then and prevents potential side effects.

```typescript

// GOOD: Return value is unused, use a block body.
myPromise.then(v => {
  console.log(v);
});

// GOOD: Code may use blocks for readability.
const transformed = [1, 2, 3].map(v => {
  const intermediate = someComplicatedExpr(v);
  const more = acrossManyLines(intermediate);
  return worthWrapping(more);
});

// GOOD: explicit `void` ensures no leaked return value
myPromise.then(v => void console.log(v));

// BAD: Use a block body if the return value of the function is not used.
myPromise.then(v => console.log(v));

// BAD: This typechecks, but the return value still leaks.
let f: () => void;
f = () => 1;
```

**Tip:** The `void` operator can be used to ensure an arrow function with an expression body returns `undefined` when the result is unused.

### 4.5.6 Rebinding `this`

Function expressions and function declarations *must not* use `this` unless they specifically exist to rebind the `this` pointer. Rebinding `this` can in most cases be avoided by using arrow functions or explicit parameters.

```typescript
// GOOD: Explicitly reference the object from an arrow function.
document.body.onclick = () => { document.body.textContent = 'hello'; };

// GOOD: Take an explicit parameter
const setTextFn = (e: HTMLElement) => { e.textContent = 'hello'; };
document.body.onclick = setTextFn.bind(null, document.body);

// BAD: What's `this` in this context?
function clickHandler() {
  this.textContent = 'Hello';
}

// BAD: The `this` pointer reference is implicitly set to document.body.
document.body.onclick = clickHandler;
```
Prefer arrow functions over other approaches to binding `this`, such as `f.bind(this)`, `goog.bind(f, this)`, or `const self = this`.

### 4.5.7 Prefer passing arrow functions as callbacks

Callbacks can be invoked with unexpected arguments that can pass a type check but still result in logical errors.

Avoid passing a named callback to a higher-order function, unless you are sure of the stability of both functions' call signatures. Beware, in particular, of less-commonly-used optional parameters.

Instead, prefer passing an arrow-function that explicitly forwards parameters to the named callback.

```typescript
// GOOD: Arguments are explicitly passed to the callback.
const numbers = ['11', '5', '3'].map((n) => parseInt(n));
// > [11, 5, 3]

// GOOD: Function is locally defined and is designed to be used as a callback.
function dayFilter(element: string|null|undefined) {
  return element != null && element.endsWith('day');
}

const days = ['tuesday', undefined, 'juice', 'wednesday'].filter(dayFilter);

// BAD: Arguments are not explicitly passed, leading to unintended behavior
// when the optional `radix` argument gets the array indices 0, 1, and 2.
const numbers = ['11', '5', '10'].map(parseInt);
// > [11, NaN, 2];
```
### 4.5.8 Arrow functions as properties

Classes usually *should not* contain properties initialized to arrow functions. Arrow function properties require the calling function to understand that the callee's `this` is already bound, which increases confusion about what `this` is, and call sites and references using such handlers look broken (i.e. require non-local knowledge to determine that they are correct). Code *should* always use arrow functions to call instance methods (`const handler = (x) => { this.listener(x); };`), and *should not* obtain or pass references to instance methods (~~`const handler = this.listener; handler(x);`~~).

**Note:** In some specific situations, e.g. when binding functions in a template, arrow functions as properties are useful and create much more readable code. Use judgement with this rule. Also, see the [Event Handlers](#459-event-handlers) section below.

```typescript
// GOOD: Explicitly manage `this` at call time.
class DelayHandler {
  constructor() {
    // Use anonymous functions if possible.
    setTimeout(() => {
      this.patienceTracker();
    }, 5000);
  }
  private patienceTracker() {
    this.waitedPatiently = true;
  }
}

// BAD:
class DelayHandler {
  constructor() {
    // Problem: `this` is not preserved in the callback. `this` in the callback
    // will not be an instance of DelayHandler.
    setTimeout(this.patienceTracker, 5000);
  }
  private patienceTracker() {
    this.waitedPatiently = true;
  }
}

// Arrow functions usually should not be properties.
class DelayHandler {
  constructor() {
    // BAD: This code looks like it forgot to bind `this`.
    setTimeout(this.patienceTracker, 5000);
  }
  private patienceTracker = () => {
    this.waitedPatiently = true;
  }
}
```

### 4.5.9 Event handlers

Event handlers *may* use arrow functions when there is no need to uninstall the handler (for example, if the event is emitted by the class itself). If the handler requires uninstallation, arrow function properties are the right approach, because they automatically capture `this` and provide a stable reference to uninstall.

```typescript
// EXAMPLE: Event handlers may be anonymous functions or arrow function properties.
class Component {
  onAttached() {
    // The event is emitted by this class, no need to uninstall.
    this.addEventListener('click', () => {
      this.listener();
    });
    // this.listener is a stable reference, we can uninstall it later.
    window.addEventListener('onbeforeunload', this.listener);
  }
  onDetached() {
    // The event is emitted by window. If we don't uninstall, this.listener will
    // keep a reference to `this` because it's bound, causing a memory leak.
    window.removeEventListener('onbeforeunload', this.listener);
  }
  // An arrow function stored in a property is bound to `this` automatically.
  private listener = () => {
    confirm('Do you want to exit the page?');
  }
}
```

Do not use `bind` in the expression that installs an event handler, because it creates a temporary reference that can't be uninstalled.

```typescript
// BAD: Binding listeners creates a temporary reference that prevents uninstalling.
class Component {
  onAttached() {
    // This creates a temporary reference that we won't be able to uninstall
    window.addEventListener('onbeforeunload', this.listener.bind(this));
  }
  onDetached() {
    // This bind creates a different reference, so this line does nothing.
    window.removeEventListener('onbeforeunload', this.listener.bind(this));
  }
  private listener() {
    confirm('Do you want to exit the page?');
  }
}
```

### 4.5.10 Parameter initializers

Optional function parameters *may* be given a default initializer to use when the argument is omitted.

Initializers *must not* have any observable side effects.

Initializers *should* be kept as simple as possible.

```typescript
// GOOD:
function process(name: string, extraContext: string[] = []) {}
function activate(index = 0) {}

// BAD: Side effect of incrementing the counter.
let globalCounter = 0;
function newId(index = globalCounter++) {}

// BAD: Exposes shared mutable state, which can introduce unintended coupling
// between function calls
class Foo {
  private readonly defaultPaths: string[];
  frobnicate(paths = defaultPaths) {}
}
```

Use default parameters sparingly. Prefer [destructuring](#435-object-destructuring) to create readable APIs when there are more than a small handful of optional parameters that do not have a natural order.

### 4.5.11 Prefer rest and spread when appropriate

Use a rest parameter instead of accessing `arguments`. Never name a local variable or parameter `arguments`, which confusingly shadows the built-in name.

```typescript
// EXAMPLE:
function variadic(array: string[], ...numbers: number[]) {}
```

Use function spread syntax instead of `Function.prototype.apply`.

### 4.5.12 Formatting functions

Blank lines at the start or end of the function body are not allowed.

A single blank line *may* be used within function bodies sparingly to create logical groupings of statements.

Generators should attach the * to the function and yield keywords.

```typescript
// GOOD:
function* foo();
yield* iter;

// BAD:
function *foo();
yield *iter;
```

Parentheses around the left-hand side of a single-argument arrow function are recommended but not required.

Do not put a space after the `...` in rest or spread syntax.

```typescript
// EXAMPLE:
function myFunction(...elements: number[]) {}
myFunction(...array, ...iterable, ...generator());
```

## 4.6 `this`

`this` must only be used in class constructors and methods. Functions that have an explicit `this` type declared (e.g. `function func(this: ThisType, ...)`), or in arrow functions defined in a scope where `this` *may* be used.

Never use `this` to refer to the global object, the context of an `eval`, the target of an event, or unnecessarily `call()`ed or `apply()`ed functions.

```typescript
// BAD:
this.alert('Hello');
```
## 4.7 Primitive literals

### 4.7.1 String literals

#### 4.7.1.1 Use single quotes

Ordinary string literals are delimited with single quotes (`'`), rather than double quotes (`"`).

**Tip:** if a string contains a single quote character, consider using a template string to avoid having to escape the quote.

#### 4.7.1.2 No line continuations

Do not use line continuations (that is, ending a line inside a string literal with a backslash) in either ordinary or template string literals. Even though ES5 allows this, it can lead to tricky errors if any trailing whitespace comes after the slash, and is less obvious to readers.

```typescript
// GOOD:
const LONG_STRING = 'This is a very very very very very very long string. ' +
    'It does not contain long stretches of spaces because it uses ' +
    'concatenated strings.';
const SINGLE_STRING =
    'http://it.is.also/acceptable_to_use_a_single_long_string_when_breaking_would_hinder_search_discoverability';

// BAD:
const LONG_STRING = 'This is a very very very very very very very long string. \
    It inadvertently contains long stretches of spaces due to how the \
    continued lines are indented.';
```

#### 4.7.1.3. Template literals

Use template literals (delimited with ``` ` ```) over complex string concatenation, particularly if multiple string literals are involved. Template literals may span multiple lines.

If a template literal spans multiple lines, it does not need to follow the indentation of the enclosing block, though it may if the added whitespace does not matter.

```typescript
// GOOD:
function arithmetic(a: number, b: number) {
  return `Here is a table of arithmetic operations:
${a} + ${b} = ${a + b}
${a} - ${b} = ${a - b}
${a} * ${b} = ${a * b}
${a} / ${b} = ${a / b}`;
}
```

### 4.7.2. Number literals

Numbers *may* be specified in decimal, hex, octal, or binary. Use exactly `0x`, `0o`, and `0b` prefixes, with lowercase letters, for hex, octal, and binary, respectively. Never include a leading zero unless it is immediately followed by `x`, `o`, or `b`.

### 4.7.3. Type coercion

### 4.7.3.1. Explicit coercion

TypeScript code may use the `String()` and `Boolean()` functions, string template literals, or `!!` to coerce types.

```typescript
// ACCEPTABLE:
const bool = Boolean(false);
const str = String(aNumber);
const bool2 = !!str;
const str2 = `result: ${bool2}`;
```

Values of enum types (including unions of enum types and other types) *must not* be converted to booleans with `Boolean()` or `!!`, and must instead be compared explicitly with comparison operators.

```typescript
// GOOD:
enum SupportLevel {
  NONE,
  BASIC,
  ADVANCED,
}

const level: SupportLevel = ...;
let enabled = level !== SupportLevel.NONE;

const maybeLevel: SupportLevel|undefined = ...;
enabled = level !== undefined && level !== SupportLevel.NONE;

// BAD:
enum SupportLevel {
  NONE,
  BASIC,
  ADVANCED,
}

const level: SupportLevel = ...;
let enabled = Boolean(level);

const maybeLevel: SupportLevel|undefined = ...;
enabled = !!maybeLevel;
```

[Explanation](https://google.github.io/styleguide/tsguide.html#type-coercion).

Using string concatenation to cast to string is discouraged, as we check that operands to the plus operator are of matching types.

Code *must* use `Number()` to parse numeric values, and *must* check its return for `NaN` values explicitly, unless failing to parse is impossible from context.

> **Note:** `Number('')`, `Number(' ')`, and `Number('\t')` would return `0` instead of `NaN`. `Number('Infinity')` and `Number('-Infinity')` would return `Infinity` and `-Infinity` respectively. Additionally, exponential notation such as `Number('1e+309')` and `Number('-1e+309')` can overflow into `Infinity`. These cases may require special handling.

```typescript
// GOOD:
const aNumber = Number('123');
if (!isFinite(aNumber)) throw new Error(...);
```

Code *must not* use unary plus (`+`) to coerce strings to numbers. Parsing numbers can fail, has surprising corner cases, and can be a code smell (parsing at the wrong layer). A unary plus is too easy to miss in code reviews given this.

```typescript
// BAD:
const x = +y;
```

Code also *must not* use `parseInt` or `parseFloat` to parse numbers, except for non-base-10 strings (see below). Both of those functions ignore trailing characters in the string, which can shadow error conditions (e.g. parsing `12 dwarves` as `12`).

```typescript
// BAD: Error prone, regardless of passing a radix.
const n = parseInt(someString, 10);
const f = parseFloat(someString);
```

Code that requires parsing with a radix *must* check that its input contains only appropriate digits for that radix before calling into `parseInt`.

```typescript
// GOOD: Only allowed for radix != 10.
if (!/^[a-fA-F0-9]+$/.test(someString)) throw new Error(...);
// Needed to parse hexadecimal.
// tslint:disable-next-line:ban
const n = parseInt(someString, 16);
```

Use `Number()` followed by `Math.floor` or `Math.trunc` (where available) to parse integer numbers.

```typescript
// GOOD:
let f = Number(someString);
if (isNaN(f)) handleError();
f = Math.floor(f);
```

#### 4.7.3.2. Implicit coercion

Do not use explicit boolean coercions in conditional clauses that have implicit boolean coercion. Those are the conditions in an `if`, `for` and `while` statements.

```typescript
// GOOD:
const foo: MyInterface|null = ...;
if (foo) {...}
while (foo) {...}

// BAD:
const foo: MyInterface|null = ...;
if (!!foo) {...}
while (!!foo) {...}
```
As with [explicit conversions](#4731-explicit-coercion), values of enum types (including unions of enum types and other types) *must not* be implicitly coerced to booleans, and *must* instead be compared explicitly with comparison operators.

```typescript
// GOOD:
enum SupportLevel {
  NONE,
  BASIC,
  ADVANCED,
}

const level: SupportLevel = ...;
if (level !== SupportLevel.NONE) {...}

const maybeLevel: SupportLevel|undefined = ...;
if (level !== undefined && level !== SupportLevel.NONE) {...}

// BAD:
enum SupportLevel {
  NONE,
  BASIC,
  ADVANCED,
}

const level: SupportLevel = ...;
if (level) {...}

const maybeLevel: SupportLevel|undefined = ...;
if (level) {...}
```

# TODO: Возможно это [то что ниже] имеет смысл вынести отсюда.

Other types of values `may` be either implicitly coerced to booleans or compared explicitly with comparison operators:

```typescript
// ACCEPTABLE: Explicitly comparing > 0 is OK.
if (arr.length > 0) {...}
// So is relying on boolean coercion.
if (arr.length) {...}
```

## 4.8. Control structures

### 4.8.1. Control flow statements and blocks

Control flow statements (`if`, `else`, `for`, `do`, `while`, etc) always use braced blocks for the containing code, even if the body contains only a single statement. The first statement of a non-empty block *must* begin on its own line.

```typescript
// GOOD:
for (let i = 0; i < x; i++) {
  doSomethingWith(i);
}

if (x) {
  doSomethingWithALongMethodNameThatForcesANewLine(x);
}

// BAD:
if (x)
  doSomethingWithALongMethodNameThatForcesANewLine(x);

for (let i = 0; i < x; i++) doSomethingWith(i);
```

#### 4.8.1.2. Assignment in control statements

Prefer to avoid assignment of variables inside control statements.

Assignment can be easily mistaken for equality checks inside control statements.

In cases where assignment within a control statement is preferred, add an appropriate comment to indicate that it is intentional.

```typescript
// BAD: Assignment easily mistaken with equality check.
if (x = someFunction()) {
  ...
}

// GOOD:
x = someFunction();
if (x) {
  ...
}

// ACCEPTABLE:
// Assignment is used in this expression because...
if (x = someFunction()) {
  ...
}

```

#### 4.8.1.3. Iterating containers

Prefer `for (... of someArr)` to iterate over arrays.

`Array.prototype.forEach` and for loops are also allowed.

```typescript
// GOOD: x is a value of someArr.
for (const x of someArr) {
  ...
}

// ACCEPTABLE: Explicitly count if the index is needed, otherwise use the for/of form.
for (let i = 0; i < someArr.length; i++) {
  const x = someArr[i];
  ...
}

// ACCEPTABLE: Alternative version of the above.
for (const [i, x] of someArr.entries()) {
  ...
}
```

`for-in` loops *may* only be used on dict-style objects. Do not use `for (... in ...)` to iterate over arrays as it will counterintuitively give the array's indices (as strings!), not values.

```typescript
// BAD: x is the index!
for (const x in someArray) {
  ...
}
```

`Object.prototype.hasOwnProperty` *should* be used in `for-in` loops to exclude unwanted prototype properties. Prefer `for-of` with `Object.keys`, `Object.values`, or `Object.entries` over `for-in` when possible.

```typescript
// GOOD:
for (const key of Object.keys(obj)) {
  doWork(key, obj[key]);
}

// GOOD:
for (const value of Object.values(obj)) {
  doWorkValOnly(value);
}

// GOOD:
for (const [key, value] of Object.entries(obj)) {
  doWork(key, value);
}

// ACCEPTABLE:
for (const key in obj) {
  if (!obj.hasOwnProperty(key)) continue;
  doWork(key, obj[key]);
}
```

### 4.8.2. Grouping parentheses

Optional grouping parentheses *should* be used for clarity and readability of the code, unless it is obvious that omitting them will not lead to misinterpretation.

Do not use unnecessary parentheses around the entire expression following `delete`, `typeof`, `void`, `return`, `throw`, `case`, `in`, `of`, or `yield`.

### 4.8.3. Exception handling

Exceptions are an important part of the language and *should* be used whenever exceptional cases occur.

Custom exceptions provide a great way to convey additional error information from functions. They *should* be defined and used wherever the native `Error` type is insufficient.

Prefer throwing exceptions over ad-hoc error-handling approaches (such as passing an error container reference type, or returning an object with an error property).

#### 4.8.3.1. Instantiate errors using `new`

Always use `new Error()` when instantiating exceptions, instead of just calling `Error()`. Both forms create a new `Error` instance, but using `new` is more consistent with how other objects are instantiated.

```typescript
// BAD:
throw Error('Foo is not a valid bar.');

// GOOD:
throw new Error('Foo is not a valid bar.');
```

#### 4.8.3.2. Only throw errors

TypeScript allow throwing or rejecting a `Promise` with arbitrary values. However if the thrown or rejected value is not an `Error`, it does not populate stack trace information, making debugging hard. This treatment extends to `Promise` rejection values as `Promise.reject(obj)` is equivalent to `throw obj` in async functions.

```typescript
// BAD: Does not get a stack trace.
throw 'oh noes!';

new Promise((resolve, reject) => void reject('oh noes!'));
Promise.reject();
Promise.reject('oh noes!');

// GOOD: Throw only Errors or subtypes of Error.
throw new Error('oh noes!');

class MyError extends Error {}
throw new MyError('my oh noes!');

new Promise((resolve, reject) => void reject(new Error('oh noes!')));
Promise.reject(new Error('oh noes!'));
```

#### 4.8.3.3. Catching and rethrowing

When catching errors, code *should* assume that all thrown errors are instances of `Error`.

```typescript
// GOOD: All thrown errors must be Error subtypes.
// Do not handle other possible values unless you know they are thrown.
function assertIsError(e: unknown): asserts e is Error {
  if (!(e instanceof Error)) throw new Error("e is not an Error");
}

try {
  doSomething();
} catch (e: unknown) {
  assertIsError(e);

  // Handle the exception or rethrow it.
  displayError(e.message);
  throw e;
}
```

Exception handlers *must not* defensively handle non-`Error` types unless the called API is conclusively known to throw non-`Errors` in violation of the above rule. In that case, a comment should be included to specifically identify where the non-`Errors` originate.

```typescript
// GOOD: Bad API throws strings instead of errors.
try {
  badApiThrowingStrings();
} catch (e: unknown) {
  if (typeof e === 'string') { ... }
}
```

> **Why?** Avoid [overly defensive programming](https://en.wikipedia.org/wiki/Defensive_programming#Offensive_programming). Repeating the same defenses against a problem that will not exist in most code leads to boiler-plate code that is not useful.

#### 4.8.3.4. Empty catch blocks

It is very rarely correct to do nothing in response to a caught exception. When it truly is appropriate to take no action whatsoever in a catch block, the reason this is justified is explained in a comment.

```typescript
// BAD:
try {
  shouldFail();
  fail('expected an error');
} catch (expected: unknown) {
}

// GOOD:
try {
  return handleNumericResponse(response);
} catch (e: unknown) {
  // Response is not numeric. Continue to handle as text.
}
return handleTextResponse(response);
```

> **Tip:** For testing code that is expected to throw exceptions, directly using try-catch can lead to incorrect results, as it will catch any exception, not necessarily the ones you intend to test for. Instead, it's recommended to use `assertThrows()` for explicitly verifying that the expected exception is thrown.

### 4.8.4. Switch statements

All `switch` statements *must* contain a `default` statement group, even if it contains no code. The `default` statement group *must* be last.

Within a switch block, each statement group either terminates abruptly with a `break`, a `return` statement, or by throwing an exception. Non-empty statement groups (`case ...`) *must not* fall through (enforced by the compiler).

Empty statement groups are allowed to fall through.

```typescript
// GOOD:
switch (x) {
  case Y:
    doSomethingElse();
    break;
  default:
    // Nothing to do.
}

// ACCEPTABLE:
switch (x) {
  case X:
  case Y:
    doSomething();
    break;
  default:
    // Nothing to do.
}

// BAD: Fall through not allowed!
switch (x) {
  case X:
    doSomething();
  case Y:
    ...
}
```

### 4.8.5. Equality checks

Always use triple equals `===` and not equals `!==`.

The double equality operators cause error prone type coercions that are hard to understand and slower to implement for JavaScript Virtual Machines (see also the [JavaScript equality table](https://dorey.github.io/JavaScript-Equality-Table/)).

> **Exception:** Comparisons to the literal `null` value *may* use the `==` and `!=` operators to cover both `null` and `undefined` values.

```typescript
// BAD: Hard to understand behaviour due to type coercion.
if (foo == 'bar' || baz != bam) {
  ...
}

// GOOD:
if (foo === 'bar' || baz !== bam) {
  ...
}

// ACCEPTABLE: Will trigger when foo is null or undefined.
if (foo == null) {
  ...
}
```

# 4.8.6. Type and non-nullability assertions

Type and non-nullability statements *should not* be used without a clear or obvious reason for doing so.

Type assertions `x as SomeType` and non-nullability assertions `y!` are unsafe. Both only silence the TypeScript compiler, but do not insert any runtime checks to match these assertions, so they can cause your program to crash at runtime.

When you want to assert a type or non-nullability the best answer is to explicitly write a runtime check that performs that check.

```typescript
// BAD:
(x as Foo).foo();

y!.bar();

// GOOD: Assuming Foo is a class.
if (x instanceof Foo) {
  x.foo();
}

// GOOD: Checking for non-nullable.
if (y) {
  y.bar();
}
```

Sometimes due to some local property of your code you can be sure that the assertion form is safe. In those situations, appropriate explanations should be added.

```typescript
// ACCEPTABLE:
// x is a Foo, because ...
(x as Foo).foo();

// y cannot be null, because ...
y!.bar();
```

> **Note:** If the reasoning behind a type or non-nullability assertion is obvious, the comments may not be necessary. Proceed as appropriate.

#### 4.8.6.1. Type assertion syntax

Type assertions *must* use the `as` syntax and not use angle bracket syntax.

This enforces parentheses around the assertion when accessing a member.

```typescript
// BAD:
const x = (<Foo>z).length;
const y = <Foo>z.length;

// ACCEPTABLE:
// z must be Foo because ...
const x = (z as Foo).length;
```

#### 4.8.6.2. Double assertions

From the [TypeScript handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions), TypeScript only allows type assertions which convert to a more specific or less specific version of a type. Adding a type assertion (x as Foo) which does not meet this criteria will give the error: “Conversion of type 'X' to type 'Y' may be a mistake because neither type sufficiently overlaps with the other”.

If you need to convert partially overlapping types and if you are sure that the assertion is safe, you can perform a double assertion. This assumes conversion by `unknown`, since it is less specific than all types.

```typescript
// ACCEPTABLE:
// x is a Foo here, because...
(x as unknown as Foo).fooMethod();
```

Use `unknown` (instead of `any` or `{}`) as the intermediate type.

#### 4.8.6.3. Type assertions and object literals

Use type annotations `: Foo` instead of type assertions `as Foo` to specify the type of an object literal. This allows detecting refactoring bugs when the fields of an interface change over time.

```typescript
interface Foo {
  bar: number;
  // Was "bam", but later renamed to "baz".
  baz?: string;
}

// BAD: No error!
const foo = {
  bar: 123,
  bam: 'abc',
} as Foo;

// BAD: No error!
function func() {
  return {
    bar: 123,
    bam: 'abc',
  } as Foo;
}

// GOOD: Complains about "bam" not being defined on Foo.
const foo: Foo = {
  bar: 123,
  bam: 'abc',
};

// GOOD: Complains about "bam" not being defined on Foo.
function func(): Foo {
  return {
    bar: 123,
    bam: 'abc',
  };
}
```

### 4.8.7. Keep try blocks focused

Limit the amount of code inside a try block, if this can be done without hurting readability.

```typescript
// BAD:
try {
  const result = methodThatMayThrow();
  use(result);
} catch (error: unknown) {
  ...
}

// GOOD:
let result;

try {
  result = methodThatMayThrow();
} catch (error: unknown) {
  ...
}

use(result);
```

Moving the non-throwable lines out of the try/catch block helps the reader learn which method throws exceptions. Some inline calls that do not throw exceptions could stay inside because they might not be worth the extra complication of a temporary variable.

> **Exception:** There may be performance issues if try blocks are inside a loop. Widening try blocks to cover a whole loop is acceptable.

# 4.9. Disallowed features

### 4.9.1. Wrapper objects for primitive types

Code *must not* instantiate the wrapper classes for the primitive types String, Boolean, and Number. Wrapper classes have surprising behavior, such as new Boolean(false) evaluating to true.

```typescript
// BAD:
const s = new String('hello');
const b = new Boolean(false);
const n = new Number(5);
```

The wrappers may be called as functions for coercing (which is preferred over using + or concatenating the empty string) or creating symbols. See [type coercion](#473-type-coercion) for more information.

### 4.9.2. Automatic Semicolon Insertion

Do not rely on Automatic Semicolon Insertion (ASI). Explicitly end all statements using a semicolon. This prevents bugs due to incorrect semicolon insertions and ensures compatibility with tools with limited ASI support (e.g. clang-format).

### 4.9.3. Const enums

Code *must not* use `const enum`. Use plain enum instead.

> **Why?** TypeScript enums already cannot be mutated. `const enum` is a separate language feature related to optimization that makes the enum invisible to JavaScript users of the module.

### 4.9.4. Debugger statements

Debugger statements *must not* be included in production code.

```typescript
// BAD:
function debugMe() {
  debugger;
}
```

### 4.9.5. Do not use `with`

Do not use the `with` keyword. It makes code harder to understand and [has been banned](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with) in strict mode since ES5.


### 4.9.6. Dynamic code evaluation

Do not use `eval` or the `Function(...string)` constructor (except for code loaders). These features are potentially dangerous and do not work in environments using strict [Content Security Policies](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

### 4.9.7. Non-standard features

Do not use non-standard ECMAScript or Web Platform features.

This includes:

- Old features that have been marked deprecated or removed entirely from ECMAScript or the Web Platform (see [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Deprecated_and_obsolete_features)).
- New ECMAScript features that are not yet standardized. Avoid using features that are in current working draft or currently in the proposal process. Use only ECMAScript features defined in the current ECMA-262 specification.
- Proposed but not-yet-complete web standards.
- Non-standard language “extensions” (such as those provided by some external transpilers).

### 4.9.8. Modifying builtin objects

Never modify builtin types, either by adding methods to their constructors or to their prototypes. Avoid depending on libraries that do this.

Do not add symbols to the global object unless absolutely necessary (e.g. required by a third-party API).

# 5. Type system

## 5.1. Type inference

Code *should* rely on type inference as implemented by the compiler for all type expressions (variables, fields, return types, etc). In this case, the type annotations are used for ease of reading the code.

Leave out type annotations for trivially inferred types: variables or parameters initialized to a `string`, `number`, `boolean`, `RegExp` literal or `new` expression.

```typescript
// BAD: `boolean` here does not aid readability.
const x: boolean = true;

// GOOD: Type inferred.
const x = 15;
```

For more complex expressions, type annotations can help with readability of the program:

```typescript
// BAD: Hard to reason about the type of `value` without an annotation.
const value = await rpc.getSomeValue().transform();

// GOOD: Can tell the type of `value` at a glance.
const value: string[] = await rpc.getSomeValue().transform();
```

Explicitly specifying types *should* be required to prevent generic type parameters from being inferred as `unknown`. For example, initializing generic types with no values (e.g. empty arrays, objects, `Map`s, or `Set`s).

```typescript
// BAD: `Set` is trivially inferred from the initialization.
const x: Set<string> = new Set();

// GOOD:
const x = new Set<string>();
```

### 5.1.1. Return types

The types returned by functions or methods always *must* be explicitly specified.

> **Why?**
> There are two benefits to explicitly typing out the implicit return values of functions and methods:
> - More precise documentation to benefit readers of the code.
> - Surface potential type errors faster in the future if there are code changes that change the return type of the function.

## 5.2. Undefined and null

TypeScript supports `undefined` and `null` types. Nullable types can be constructed as a union type `(string|null)`, similarly with `undefined`. There is no special syntax for unions of `undefined` and `null`.

Code can use either undefined or null to denote absence of a value. Use what you think is appropriate.

Many JavaScript APIs use `undefined` (e.g. `Map.get`), while many DOM and Google APIs use `null` (e.g. `Element.getAttribute`), so the appropriate absent value depends on the context.

### 5.2.1. Nullable/undefined type aliases

Type aliases *must not* include `|null` or `|undefined` in a union type. Nullable aliases typically indicate that null values are being passed around through too many layers of an application, and this clouds the source of the original issue that resulted in `null`. They also make it unclear when specific values on a class or interface might be absent.

Instead, code *must* only add `|null` or `|undefined` when the alias is actually used. Code *should* deal with null values close to where they arise, using the above techniques.

```typescript
// BAD:
type CoffeeResponse = Latte|Americano|undefined;

class CoffeeService {
  getLatte(): CoffeeResponse { ... };
}

// GOOD:
type CoffeeResponse = Latte|Americano;

class CoffeeService {
  getLatte(): CoffeeResponse|undefined { ... };
}
```

### 5.2.2. Prefer optional over `|undefined`

In addition, TypeScript supports a special construct for optional parameters and fields, using `?`.

Optional parameters implicitly include `|undefined` in their type. However, they are different in that they can be left out when constructing a value or calling a method. For example, `{sugarCubes: 1}` is a valid `CoffeeOrder` because `milk` is optional.

```typescript
// GOOD:
interface CoffeeOrder {
  sugarCubes: number;
  milk?: Whole|LowFat|HalfHalf;
}

function pourCoffee(volume?: Milliliter) { ... }
```

Use optional fields (on interfaces or classes) and parameters rather than a |undefined type.

> **Note:**
> For classes preferably avoid this pattern altogether and initialize as many fields as possible.

## 5.3. Use structural types

TypeScript's type system is structural, not nominal. That is, a value matches a type if it has at least all the properties the type requires and the properties' types match, recursively.

When providing a structural-based implementation, explicitly include the type at the declaration of the symbol (this allows more precise type checking and error reporting).

```typescript
// BAD:
const badFoo = {
  a: 123,
  b: 'abc',
}

// GOOD:
const foo: Foo = {
  a: 123,
  b: 'abc',
}
```

Use interfaces to define structural types, not classes.

```typescript
// BAD:
class Foo {
  readonly a: number;
  readonly b: number;
}

const foo: Foo = {
  a: 123,
  b: 'abc',
}

// GOOD:
interface Foo {
  a: number;
  b: string;
}

const foo: Foo = {
  a: 123,
  b: 'abc',
}
```

> **Why?**
> The badFoo object above relies on type inference. Additional fields could be added to badFoo and the type is inferred based on the object itself.
>
> When passing a badFoo to a function that takes a Foo, the error will be at the function call site, rather than at the object declaration site. This is also useful when changing the surface of an interface across broad codebases.
>
> ```typescript
> interface Animal {
>   sound: string;
>   name: string;
> }
>
> function makeSound(animal: Animal) {}
>
> /**
>  * 'cat' has an inferred type of '{sound: string}'
>  */
> const cat = {
>   sound: 'meow',
> };
>
> /**
>  * 'cat' does not meet the type contract required for the function, so the
>  * TypeScript compiler errors here, which may be very far from where 'cat' is
>  * defined.
>  */
> makeSound(cat);
>
> /**
>  * Horse has a structural type and the type error shows here rather than the
>  * function call.  'horse' does not meet the type contract of 'Animal'.
>  */
> const horse: Animal = {
>   sound: 'niegh',
> };
>
> const dog: Animal = {
>   sound: 'bark',
>   name: 'MrPickles',
> };
>
> makeSound(dog);
> makeSound(horse);
> ```

## 5.4. Prefer interfaces over type literal aliases

TypeScript supports [type aliases](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases) for naming a type expression. This can be used to name primitives, unions, tuples, and any other types.

However, when declaring types for objects, use interfaces instead of a type alias for the object literal expression.

```typescript
// BAD:
type User = {
  firstName: string,
  lastName: string,
}

// GOOD:
interface User {
  firstName: string;
  lastName: string;
}
```

> **Why?**
> These forms are nearly equivalent, so under the principle of just choosing one out of two forms to prevent variation, we should choose one. Additionally, there are also [interesting technical reasons to prefer interface](https://ncjamieson.com/prefer-interfaces/). That page quotes the TypeScript team lead: Honestly, my take is that it should really just be interfaces for anything that they can model. There is no benefit to type aliases when there are so many issues around display/perf.

## 5.5. `Array<T>` Type

For simple types (containing just alphanumeric characters and dot), use the syntax sugar for arrays, `T[]` or `readonly T[]`, rather than the longer form `Array<T>` or `ReadonlyArray<T>`.

For multi-dimensional non-`readonly` arrays of simple types, use the syntax sugar form `T[][]`, `T[][][]`, and so on, rather than the longer form.

For anything more complex, use the longer form `Array<T>`.

These rules apply at each level of nesting, i.e. a simple `T[]` nested in a more complex type would still be spelled as `T[]`, using the syntax sugar.

```typescript
// BAD:
let a: Array<string>;
let b: ReadonlyArray<string>;
let c: Array<ns.MyObj>;
let d: Array<string[]>;
let e: {n: number, s: string}[];
let f: (string|number)[];
let g: readonly (string | number)[];
let h: InjectionToken<Array<string>>;
let i: readonly string[][];
let j: (readonly string[])[];

// GOOD:
let a: string[];
let b: readonly string[];
let c: ns.MyObj[];
let d: string[][];
let e: Array<{n: number, s: string}>;
let f: Array<string|number>;
let g: ReadonlyArray<string|number>;
let h: InjectionToken<string[]>;
let i: ReadonlyArray<string[]>;
let j: Array<readonly string[]>;
```

## 5.6. Indexable types / index signatures (`{[key: string]: T}`)

In JavaScript, it's common to use an object as an associative array (aka `map`, `hash`, or `dict`). Such objects can be typed using an [index signature](https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures) `[k: string]: T` in TypeScript:

```typescript
// GOOD:
const fileSizes: {[fileName: string]: number} = {};
fileSizes['readme.txt'] = 541;
```

In TypeScript, provide a meaningful label for the key. The label only exists for documentation. It's unused otherwise.

```typescript
// BAD:
const users: {[key: string]: number} = ...;

// GOOD:
const users: {[userName: string]: number} = ...;
```

Rather than using one of these, consider using the ES6 `Map` and `Set` types instead. JavaScript objects have [surprising undesirable behaviors](http://2ality.com/2012/01/objects-as-maps.html) and the ES6 types more explicitly convey your intent. Also, `Map`s can be keyed by — and `Set`s can contain — types other than `string`.

Builtin `Record<Keys, ValueType>` type allows constructing types with a defined set of keys. This is distinct from associative arrays in that the keys are statically known.

## 5.7. Mapped and conditional types

# TODO: Возможно имеет смысл все это сделать ссылкой.

[Mapped types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html) and [conditional types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) allow specifying new types based on other types. TypeScript's standard library includes several type operators based on these (`Record`, `Partial`, `Readonly` etc).

These type system features allow succinctly specifying types and constructing powerful yet type safe abstractions. They come with a number of drawbacks though:

- Compared to explicitly specifying properties and type relations (e.g. using interfaces and extension, see below for an example), type operators require the reader to mentally evaluate the type expression. This can make programs substantially harder to read, in particular combined with type inference and expressions crossing file boundaries.
- Mapped & conditional types' evaluation model, in particular when combined with type inference, is underspecified, not always well understood, and often subject to change in TypeScript compiler versions. Code can accidentally compile or seem to give the right results. This increases future support cost of code using type operators.
- Mapped & conditional types are most powerful when deriving types from complex and/or inferred types. On the flip side, this is also when they are most prone to create hard to understand and maintain programs.
- Some language tooling does not work well with these type system features. E.g. your IDE's find references (and thus rename property refactoring) will not find properties in a Pick<T, Keys> type, and Code Search won't hyperlink them.

The style recommendation is:

- Always use the simplest type construct that can possibly express your code.
- A little bit of repetition or verbosity is often much cheaper than the long term cost of complex type expressions.
- Mapped & conditional types may be used, subject to these considerations.

## 5.8. `any` Type
`any` type is a super and subtype of all other types, and allows dereferencing all properties. As such, `any` is dangerous — it can mask severe programming errors, and its use undermines the value of having static types in the first place.

**Consider *not* to use** `any`. In circumstances where you want to use any, consider one of:

- Provide a more specific type
- Use unknown
- Suppress the lint warning and document why

### 5.8.1. Providing a more specific type

Use interfaces, an inline object type, or a type alias:

```typescript
// Use declared interfaces to represent server-side JSON.
declare interface MyUserJson {
  name: string;
  email: string;
}

// Use type aliases for types that are repetitive to write.
type MyType = number|string;

// Or use inline object types for complex returns.
function getTwoThings(): {something: number, other: string} {
  // ...
  return {something, other};
}

// Use a generic type, where otherwise a library would say `any` to represent
// they don't care what type the user is operating on (but note "Return type
// only generics" below).
function nicestElement<T>(items: T[]): T {
  // Find the nicest element in items.
  // Code can also put constraints on T, e.g. <T extends HTMLElement>.
}
```

### 5.8.2. Using `unknown` over `any`

The `any` type allows assignment into any other type and dereferencing any property off it. Often this behaviour is not necessary or desirable, and code just needs to express that a type is unknown. Use the built-in type `unknown` in that situation — it expresses the concept and is much safer as it does not allow dereferencing arbitrary properties.

```typescript
// BAD:
// Result of an arbitrary expression.
const danger: any = value;
// This access is completely unchecked!
danger.whoops();

// GOOD:
// Can assign any value (including null or undefined) into this but cannot
// use it without narrowing the type or casting.
const val: unknown = value;

```
To safely use `unknown` values, narrow the type using a [type guard](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types).

### 5.8.3. Suppressing `any` lint warnings

Sometimes using `any` is legitimate, for example in tests to construct a mock object. In such cases, add a comment that suppresses the lint warning, and document why it is legitimate.

```typescript
// This test only needs a partial implementation of BookService, and if
// we overlooked something the test will fail in an obvious way.
// This is an intentionally unsafe partial mock
// tslint:disable-next-line:no-any
const mockBookService = ({get() { return mockBook; }} as any) as BookService;

// Shopping cart is not used in this test.
// tslint:disable-next-line:no-any
const component = new MyComponent(mockBookService, /* unused ShoppingCart */ null as any);
```

## 5.9. `{}` Type

The `{}` type, also known as an **empty interface** type, represents a interface with no properties. An empty interface type has no specified properties and therefore any non-nullish value is assignable to it.

```typescript
let player: {};

// Allowed.
player = {
  health: 50,
};

// Property 'health' does not exist on type '{}'.
console.log(player.health);
```
```
function takeAnything(obj:{}) {

}

takeAnything({});
takeAnything({ a: 1, b: 2 });
```

You *should not* use `{}` for most use cases. `{}` represents any non-nullish primitive or object type, which is rarely appropriate. Prefer one of the following more-descriptive types:

- `unknown` can hold any value, including `null` or `undefined`, and is generally more appropriate for opaque values.
- `Record<string, T>` is better for dictionary-like objects, and provides better type safety by being explicit about the type `T` of contained values (which may itself be `unknown`).
- `object` excludes primitives as well, leaving only non-nullish functions and objects, but without any other assumptions about what properties may be available.

## 5.10. Tuple types

You *should* use the tuple type instead of the Pair type.

```typescript
// BAD:
interface Pair {
  first: string;
  second: string;
}
function splitInHalf(input: string): Pair {
  ...
  return {first: x, second: y};
}

// GOOD:
function splitInHalf(input: string): [string, string] {
  ...
  return [x, y];
}

const [leftHalf, rightHalf] = splitInHalf('my string');
```

However, often it's clearer to provide meaningful names for the properties.

If declaring an `interface` is too heavyweight, you can use an inline object literal type:

```typescript
function splitHostPort(address: string): {host: string, port: number} {
  ...
}

const address = splitHostPort(userAddress);
use(address.port);

const {host, port} = splitHostPort(userAddress);
```

## 5.11. Wrapper types

There are a few types related to JavaScript primitives that *should not* ever be used:

- `String`, `Boolean`, and `Number` have slightly different meaning from the corresponding primitive types `string`, `boolean`, and `number`. Always use the lowercase version.
- `Object` has similarities to both `{}` and `object`, but is slightly looser. Use `{}` for a type that include everything except `null` and `undefined`, or lowercase `object` to further exclude the other primitive types (the three mentioned above, plus `symbol` and `bigint`).

Further, never invoke the wrapper types as constructors (with `new`).

# 6. Comments and documentation

## 6.1. JSDoc versus comments

There are two types of comments, JSDoc (`/** ... */`) and non-JSDoc ordinary comments (`// ...` or `/* ... */`).

- Use `/** ... */` comments for documentation, i.e. comments a user of the code should read.
- Use `// ...` for implementation comments, i.e. comments that only concern the implementation of the code itself.

JSDoc comments are understood by tools (such as editors and documentation generators), while ordinary comments are only for other humans.

## 6.2. Multi-line comments

Multi-line comments are indented at the same level as the surrounding code.

They *must* use multiple single-line comments (`// ...`), not block comment style (`/* ... */`).

```typescript
// BAD:
/*
 * This should
 * use multiple
 * single-line comments.
 */

/* This should use //. */

// GOOD:
// This is fine.

// And this is
// fine too.
```
Comments are not enclosed in boxes drawn with asterisks or other characters.

## 6.3. JSDoc general form

The basic formatting of JSDoc comments:

```typescript
/**
 * Multiple lines of JSDoc text are written here,
 * wrapped normally.
 * @param arg A number to do something to.
 */
function doSomething(arg: number) { … }
```

or in this single-line:

```typescript
/** This short jsdoc describes the function. */
function doSomething(arg: number) { … }
```

If a single-line comment overflows into multiple lines, it `must` use the multi-line style with `/**` and `*/` on their own lines.

Many tools extract metadata from JSDoc comments to perform code validation and optimization. As such, these comments `must` be well-formed.

## 6.4. Markdown

JSDoc is written in Markdown, though it `may` include HTML when necessary.

This means that tooling parsing JSDoc will ignore plain text formatting, so if you did this:

```typescript
/**
 * Computes weight based on three factors:
 *   items sent
 *   items received
 *   last timestamp
 */
```

it will be rendered like this:

```text
Computes weight based on three factors: items sent items received last timestamp
```

Instead, write a Markdown list:

```typescript
/**
 * Computes weight based on three factors:
 *
 * - items sent
 * - items received
 * - last timestamp
 */
```

## 6.5. JSDoc tags

It is acceptable to use a subset of JSDoc tags. Most tags *must* occupy their own line, with the tag at the beginning of the line.

```typescript
// BAD:
/**
 * The "param" tag must occupy its own line and may not be combined.
 * @param left @param right
 */
function add(left: number, right: number) { ... }

// GOOD:
/**
 * The "param" tag must occupy its own line and may not be combined.
 * @param left A description of the left param.
 * @param right A description of the right param.
 */
function add(left: number, right: number) { ... }
```

## 6.6. Line wrapping

Line-wrapped block tags are indented four spaces. Wrapped description text *may* be lined up with the description on previous lines, but this horizontal alignment is discouraged.

```typescript
// GOOD:
/**
 * Illustrates line wrapping for long param/return descriptions.
 * @param foo This is a param with a particularly long description that just
 *     doesn't fit on one line.
 * @return This returns something that has a lengthy description too long to fit
 *     in one line.
 */
exports.method = function(foo) {
  return 5;
};
```

## 6.7. Document all top-level exports of modules

Use `/** ... */` comments to communicate information to the users of your code. Avoid merely restating the property or parameter name. You `should` also document all properties and methods (exported/public or not) whose purpose is not immediately obvious from their name.

**Exception**: Symbols that are only exported to be consumed by tooling, such as @NgModule classes, do not require comments.

## 6.8. Class comments

JSDoc comments for classes should provide the reader with enough information to know how and when to use the class, as well as any additional considerations necessary to correctly use the class. Textual descriptions may be omitted on the constructor.

## 6.9. Method and function comments

Method, parameter, and return descriptions may be omitted if they are obvious from the rest of the method’s JSDoc or from the method name and type signature.

Method descriptions begin with a verb phrase that describes what the method does. This phrase is not an imperative sentence, but instead is written in the third person, as if there is an implied “This method ...” before it.

## 6.10. Parameter property comments

A [parameter property](https://www.typescriptlang.org/docs/handbook/2/classes.html#parameter-properties) is a constructor parameter that is prefixed by one of the modifiers `private`, `protected`, `public`, or `readonly`. A parameter property declares both a parameter and an instance property, and implicitly assigns into it. For example, `constructor(private readonly foo: Foo)`, declares that the constructor takes a parameter `foo`, but also declares a private readonly property `foo`, and assigns the parameter into that property before executing the remainder of the constructor.

To document these fields, use JSDoc's `@param` annotation. Editors display the description on constructor calls and property accesses.

```typescript
/** This class demonstrates how parameter properties are documented. */
class ParamProps {
  /**
   * @param percolator The percolator used for brewing.
   * @param beans The beans to brew.
   */
  constructor(
    private readonly percolator: Percolator,
    private readonly beans: CoffeeBean[]) {}
}
```

```typescript
/** This class demonstrates how ordinary fields are documented. */
class OrdinaryClass {
  /** The bean that will be used in the next call to brew(). */
  nextBean: CoffeeBean;

  constructor(initialBean: CoffeeBean) {
    this.nextBean = initialBean;
  }
}
```

## 6.11. JSDoc type annotations

JSDoc type annotations are redundant in TypeScript source code. Do not declare types in `@param` or `@return` blocks, do not write `@implements`, `@enum`, `@private`, `@override` etc. on code that uses the `implements`, `enum`, `private`, `override` etc. keywords.

## 6.12. Make comments that actually add information

For non-exported symbols, sometimes the name and type of the function or parameter is enough. Code will usually benefit from more documentation than just variable names though!

Avoid comments that just restate the parameter name and type, e.g.

```typescript
// BAD:
/** @param fooBarService The Bar service for the Foo application. */
```

Because of this rule, `@param` and `@return` lines are only required when they add information, and `may` otherwise be omitted.

```typescript
// GOOD:
/**
 * POSTs the request to start coffee brewing.
 * @param amountLitres The amount to brew. Must fit the pot size!
 */
brew(amountLitres: number, logger: Logger) {
  // ...
}
```

# TODO

1. Проверить { ... }
2. Проверить '
3. Проверить ссылки
4. Отметить как должны называться файлы
5. Написать про точки с запятыми
6. Проверить комментарии в коде [с большой буквы и точка в конце] // BAD: Getter changes observable state.
7. Возможно имеет смысл выделить отдельный раздел с чисто синтаксисом (в котором давать ссылки на остальные разделы, где эти правила описываются)
8. Возможно имеет смысл переформулировать все правила на термины should, must, may и т.п.
9. Сначала BAD примеры, потом GOOD, потом ACCEPTABLE
10. Оставить блоки Why в рамках данного документа.
11. Проверить чтобы в тексте было поменьше скобок.
12. По возможности убрать упоминание Typescript из текста.
13. Разобраться чем класс отличается от интерфейса.
14. Решить что делать с 7.1.1 @ts-ignore


# Syntax

1. Ограничение строки в 100? символов. Понять какая длинна строки достаточна для современных мониторов и их разрешения.
2. Про отсутпы (tab) и количества пробелов в tab.
3. Всегда используйте точку с запятой на конце, не используйте автоматическую вставку.[4.9.2.]
4. Никогда не называйте локальную переменную или аргументы функции `arguments`, поскольку это сбивает с толку и это встроенное имя [4.5.11].
5. Blank lines at the start or end of the function body are not allowed [4.5.12]
6. A single blank line *may* be used within function bodies sparingly to create logical groupings of statements [4.5.12].
7. Parentheses around the left-hand side of a single-argument arrow function are recommended but not required.[4.5.12]
8. Do not put a space after the `...` in rest or spread syntax.[4.5.12]
9. Ordinary string literals are delimited with single quotes (`'`) [4.7.1.1.]
10. Do not use line continuations [4.7.1.2.]
11. Control flow statements (`if`, `else`, `for`, `do`, `while`, etc) always use braced blocks for the containing code, even if the body contains only a single statement. The first statement of a non-empty block *must* begin on its own line. [4.8.1.]
12. Type assertions *must* use the `as` syntax and not use angle bracket syntax. [4.8.6.1]
13. [5.5.] `Array<T>` Type
14. [6.1] и [6.2.]
