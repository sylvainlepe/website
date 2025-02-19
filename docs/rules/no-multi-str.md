---
title: no-multi-str - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-multi-str.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Multiline Strings (no-multi-str)

It's possible to create multiline strings in JavaScript by using a slash before a newline, such as:

```js
var x = "Line 1 \
         Line 2";
```

Some consider this to be a bad practice as it was an undocumented feature of JavaScript that was only formalized later.

## Rule Details

This rule is aimed at preventing the use of multiline strings.

Examples of **incorrect** code for this rule:

```js
/*eslint no-multi-str: "error"*/

var x = "some very \
long text";
```

Examples of **correct** code for this rule:

```js
/*eslint no-multi-str: "error"*/

var x = "some very long text";

var x = "some very " +
        "long text";
```

## Version

This rule was introduced in ESLint 0.0.9.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-multi-str.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/no-multi-str.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-multi-str.md)
