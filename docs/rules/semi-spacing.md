---
title: semi-spacing - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/semi-spacing.md
rule_type: layout
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Enforce spacing before and after semicolons (semi-spacing)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

JavaScript allows you to place unnecessary spaces before or after a semicolon.

Disallowing or enforcing space around a semicolon can improve the readability of your program.

```js
var a = "b" ;

var c = "d";var e = "f";
```

## Rule Details

This rule aims to enforce spacing around a semicolon. This rule prevents the use of spaces before a semicolon in expressions.

This rule doesn't check spacing in the following cases:

* The spacing after the semicolon if it is the first token in the line.

* The spacing before the semicolon if it is after an opening parenthesis (`(` or `{`), or the spacing after the semicolon if it is before a closing parenthesis (`)` or `}`). That spacing is checked by `space-in-parens` or `block-spacing`.

* The spacing around the semicolon in a for loop with an empty condition (`for(;;)`).

## Options

The rule takes one option, an object, which has two keys `before` and `after` having boolean values `true` or `false`.
If `before` is `true`, space is enforced before semicolons and if it's `false`, space is disallowed before semicolons.
If `after` is `true`, space is enforced after semicolons and if it's `false`, space is disallowed after semicolons.
The `after` option will be only applied if a semicolon is not at the end of line.

The default is `{"before": false, "after": true}`.

```json
    "semi-spacing": ["error", {"before": false, "after": true}]
```

### `{"before": false, "after": true}`

This is the default option. It enforces spacing after semicolons and disallows spacing before semicolons.

Examples of **incorrect** code for this rule:

```js
/*eslint semi-spacing: "error"*/

var foo ;
var foo;var bar;
throw new Error("error") ;
while (a) { break ; }
for (i = 0 ; i < 10 ; i++) {}
for (i = 0;i < 10;i++) {}
```

Examples of **correct** code for this rule:

```js
/*eslint semi-spacing: "error"*/

var foo;
var foo; var bar;
throw new Error("error");
while (a) { break; }
for (i = 0; i < 10; i++) {}
for (;;) {}
if (true) {;}
;foo();
```

### `{"before": true, "after": false}`

This option enforces spacing before semicolons and disallows spacing after semicolons.

Examples of **incorrect** code for this rule with the `{"before": true, "after": false}` option:

```js
/*eslint semi-spacing: ["error", { "before": true, "after": false }]*/

var foo;
var foo ; var bar;
throw new Error("error");
while (a) { break; }
for (i = 0;i < 10;i++) {}
for (i = 0; i < 10; i++) {}
```

Examples of **correct** code for this rule with the `{"before": true, "after": false}` option:

```js
/*eslint semi-spacing: ["error", { "before": true, "after": false }]*/

var foo ;
var foo ;var bar ;
throw new Error("error") ;
while (a) {break ;}
for (i = 0 ;i < 10 ;i++) {}
```

## When Not To Use It

You can turn this rule off if you are not concerned with the consistency of spacing before or after semicolons.

## Related Rules

* [semi](semi)
* [no-extra-semi](no-extra-semi)
* [comma-spacing](comma-spacing)
* [block-spacing](block-spacing)
* [space-in-parens](space-in-parens)

## Version

This rule was introduced in ESLint 0.16.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/semi-spacing.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/semi-spacing.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/semi-spacing.md)
