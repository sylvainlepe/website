---
title: multiline-ternary - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/multiline-ternary.md
rule_type: layout
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Enforce or disallow newlines between operands of ternary expressions (multiline-ternary)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

JavaScript allows operands of ternary expressions to be separated by newlines, which can improve the readability of your program.

For example:

```js
var foo = bar > baz ? value1 : value2;
```

The above can be rewritten as the following to improve readability and more clearly delineate the operands:

```js
var foo = bar > baz ?
    value1 :
    value2;
```

## Rule Details

This rule enforces or disallows newlines between operands of a ternary expression.
Note: The location of the operators is not enforced by this rule. Please see the [operator-linebreak](operator-linebreak) rule if you are interested in enforcing the location of the operators themselves.

## Options

This rule has a string option:

* `"always"` (default) enforces newlines between the operands of a ternary expression.
* `"always-multiline"` enforces newlines between the operands of a ternary expression if the expression spans multiple lines.
* `"never"` disallows newlines between the operands of a ternary expression.

### always

This is the default option.

Examples of **incorrect** code for this rule with the `"always"` option:

```js
/*eslint multiline-ternary: ["error", "always"]*/

foo > bar ? value1 : value2;

foo > bar ? value :
    value2;

foo > bar ?
    value : value2;
```

Examples of **correct** code for this rule with the `"always"` option:

```js
/*eslint multiline-ternary: ["error", "always"]*/

foo > bar ?
    value1 :
    value2;

foo > bar ?
    (baz > qux ?
        value1 :
        value2) :
    value3;
```

### always-multiline

Examples of **incorrect** code for this rule with the `"always-multiline"` option:

```js
/*eslint multiline-ternary: ["error", "always-multiline"]*/

foo > bar ? value1 :
    value2;

foo > bar ?
    value1 : value2;

foo > bar &&
    bar > baz ? value1 : value2;
```

Examples of **correct** code for this rule with the `"always-multiline"` option:

```js
/*eslint multiline-ternary: ["error", "always-multiline"]*/

foo > bar ? value1 : value2;

foo > bar ?
    value1 :
    value2;

foo > bar ?
    (baz > qux ? value1 : value2) :
    value3;

foo > bar ?
    (baz > qux ?
        value1 :
        value2) :
    value3;

foo > bar &&
    bar > baz ?
        value1 :
        value2;
```

### never

Examples of **incorrect** code for this rule with the `"never"` option:

```js
/*eslint multiline-ternary: ["error", "never"]*/

foo > bar ? value :
    value2;

foo > bar ?
    value : value2;

foo >
    bar ?
    value1 :
    value2;
```

Examples of **correct** code for this rule with the `"never"` option:

```js
/*eslint multiline-ternary: ["error", "never"]*/

foo > bar ? value1 : value2;

foo > bar ? (baz > qux ? value1 : value2) : value3;

foo > bar ? (
    baz > qux ? value1 : value2
) : value3;
```

## When Not To Use It

You can safely disable this rule if you do not have any strict conventions about whether the operands of a ternary expression should be separated by newlines.

## Related Rules

* [operator-linebreak](operator-linebreak)

## Compatibility

* **JSCS**: [requireMultiLineTernary](https://jscs-dev.github.io/rule/requireMultiLineTernary)

## Version

This rule was introduced in ESLint 3.1.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/multiline-ternary.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/multiline-ternary.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/multiline-ternary.md)
