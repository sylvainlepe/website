---
title: nonblock-statement-body-position - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/nonblock-statement-body-position.md
rule_type: layout
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# enforce the location of single-line statements (nonblock-statement-body-position)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

When writing `if`, `else`, `while`, `do-while`, and `for` statements, the body can be a single statement instead of a block. It can be useful to enforce a consistent location for these single statements.

For example, some developers avoid writing code like this:

```js
if (foo)
  bar();
```

If another developer attempts to add `baz();` to the `if` statement, they might mistakenly change the code to

```js
if (foo)
  bar();
  baz(); // this line is not in the `if` statement!
```

To avoid this issue, one might require all single-line `if` statements to appear directly after the conditional, without a linebreak:

```js
if (foo) bar();
```

## Rule Details

This rule aims to enforce a consistent location for single-line statements.

Note that this rule does not enforce the usage of single-line statements in general. If you would like to disallow single-line statements, use the [`curly`](/docs/rules/curly) rule instead.

### Options

This rule accepts a string option:

* `"beside"` (default) disallows a newline before a single-line statement.
* `"below"` requires a newline before a single-line statement.
* `"any"` does not enforce the position of a single-line statement.

Additionally, the rule accepts an optional object option with an `"overrides"` key. This can be used to specify a location for particular statements that override the default. For example:

* `"beside", { "overrides": { "while": "below" } }` requires all single-line statements to appear on the same line as their parent, unless the parent is a `while` statement, in which case the single-line statement must not be on the same line.
* `"below", { "overrides": { "do": "any" } }` disallows all single-line statements from appearing on the same line as their parent, unless the parent is a `do-while` statement, in which case the position of the single-line statement is not enforced.

Examples of **incorrect** code for this rule with the default `"beside"` option:

```js
/* eslint nonblock-statement-body-position: ["error", "beside"] */

if (foo)
  bar();
else
  baz();

while (foo)
  bar();

for (let i = 1; i < foo; i++)
  bar();

do
  bar();
while (foo)

```

Examples of **correct** code for this rule with the default `"beside"` option:

```js
/* eslint nonblock-statement-body-position: ["error", "beside"] */

if (foo) bar();
else baz();

while (foo) bar();

for (let i = 1; i < foo; i++) bar();

do bar(); while (foo)

if (foo) { // block statements are always allowed with this rule
  bar();
} else {
  baz();
}
```

Examples of **incorrect** code for this rule with the `"below"` option:

```js
/* eslint nonblock-statement-body-position: ["error", "below"] */

if (foo) bar();
else baz();

while (foo) bar();

for (let i = 1; i < foo; i++) bar();

do bar(); while (foo)
```

Examples of **correct** code for this rule with the `"below"` option:

```js
/* eslint nonblock-statement-body-position: ["error", "below"] */

if (foo)
  bar();
else
  baz();

while (foo)
  bar();

for (let i = 1; i < foo; i++)
  bar();

do
  bar();
while (foo)

if (foo) {
  // Although the second `if` statement is on the same line as the `else`, this is a very common
  // pattern, so it's not checked by this rule.
} else if (bar) {
}
```

Examples of **incorrect** code for this rule with the `"beside", { "overrides": { "while": "below" } }` rule:

```js
/* eslint nonblock-statement-body-position: ["error", "beside", { "overrides": { "while": "below" } }] */

if (foo)
  bar();

while (foo) bar();
```

Examples of **correct** code for this rule with the `"beside", { "overrides": { "while": "below" } }` rule:

```js
/* eslint nonblock-statement-body-position: ["error", "beside", { "overrides": { "while": "below" } }] */

if (foo) bar();

while (foo)
  bar();
```

## When Not To Use It

If you're not concerned about consistent locations of single-line statements, you should not turn on this rule. You can also disable this rule if you're using the `"all"` option for the [`curly`](/docs/rules/curly) rule, because this will disallow single-line statements entirely.

## Further Reading

* JSCS: [requireNewlineBeforeSingleStatementsInIf](https://jscs-dev.github.io/rule/requireNewlineBeforeSingleStatementsInIf)

## Version

This rule was introduced in ESLint 3.17.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/nonblock-statement-body-position.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/nonblock-statement-body-position.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/nonblock-statement-body-position.md)
