---
title: operator-assignment - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/operator-assignment.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# require or disallow assignment operator shorthand where possible (operator-assignment)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

JavaScript provides shorthand operators that combine variable assignment and some simple mathematical operations. For example, `x = x + 4` can be shortened to `x += 4`. The supported shorthand forms are as follows:

```text
 Shorthand | Separate
-----------|------------
 x += y    | x = x + y
 x -= y    | x = x - y
 x *= y    | x = x * y
 x /= y    | x = x / y
 x %= y    | x = x % y
 x **= y   | x = x ** y
 x <<= y   | x = x << y
 x >>= y   | x = x >> y
 x >>>= y  | x = x >>> y
 x &= y    | x = x & y
 x ^= y    | x = x ^ y
 x |= y    | x = x | y
```

## Rule Details

This rule requires or disallows assignment operator shorthand where possible.

The rule applies to the operators listed in the above table. It does not report the logical assignment operators `&&=`, `||=`, and `??=` because their short-circuiting behavior is different from the other assignment operators.

## Options

This rule has a single string option:

* `"always"` (default)  requires assignment operator shorthand where possible
* `"never"` disallows assignment operator shorthand

### always

Examples of **incorrect** code for this rule with the default `"always"` option:

```js
/*eslint operator-assignment: ["error", "always"]*/

x = x + y;
x = y * x;
x[0] = x[0] / y;
x.y = x.y << z;
```

Examples of **correct** code for this rule with the default `"always"` option:

```js
/*eslint operator-assignment: ["error", "always"]*/

x = y;
x += y;
x = y * z;
x = (x * y) * z;
x[0] /= y;
x[foo()] = x[foo()] % 2;
x = y + x; // `+` is not always commutative (e.g. x = "abc")
```

### never

Examples of **incorrect** code for this rule with the `"never"` option:

```js
/*eslint operator-assignment: ["error", "never"]*/

x *= y;
x ^= (y + z) / foo();
```

Examples of **correct** code for this rule with the `"never"` option:

```js
/*eslint operator-assignment: ["error", "never"]*/

x = x + y;
x.y = x.y / a.b;
```

## When Not To Use It

Use of operator assignment shorthand is a stylistic choice. Leaving this rule turned off would allow developers to choose which style is more readable on a case-by-case basis.

## Version

This rule was introduced in ESLint 0.10.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/operator-assignment.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/operator-assignment.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/operator-assignment.md)
