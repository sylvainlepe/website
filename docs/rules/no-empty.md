---
title: no-empty - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-empty.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow empty block statements (no-empty)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

Empty block statements, while not technically errors, usually occur due to refactoring that wasn't completed. They can cause confusion when reading code.

## Rule Details

This rule disallows empty block statements. This rule ignores block statements which contain a comment (for example, in an empty `catch` or `finally` block of a `try` statement to indicate that execution should continue regardless of errors).

Examples of **incorrect** code for this rule:

```js
/*eslint no-empty: "error"*/

if (foo) {
}

while (foo) {
}

switch(foo) {
}

try {
    doSomething();
} catch(ex) {

} finally {

}
```

Examples of **correct** code for this rule:

```js
/*eslint no-empty: "error"*/

if (foo) {
    // empty
}

while (foo) {
    /* empty */
}

try {
    doSomething();
} catch (ex) {
    // continue regardless of error
}

try {
    doSomething();
} finally {
    /* continue regardless of error */
}
```

## Options

This rule has an object option for exceptions:

* `"allowEmptyCatch": true` allows empty `catch` clauses (that is, which do not contain a comment)

### allowEmptyCatch

Examples of additional **correct** code for this rule with the `{ "allowEmptyCatch": true }` option:

```js
/* eslint no-empty: ["error", { "allowEmptyCatch": true }] */
try {
    doSomething();
} catch (ex) {}

try {
    doSomething();
}
catch (ex) {}
finally {
    /* continue regardless of error */
}
```

## When Not To Use It

If you intentionally use empty block statements then you can disable this rule.

## Related Rules

* [no-empty-function](./no-empty-function)

## Version

This rule was introduced in ESLint 0.0.2.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-empty.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/no-empty.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-empty.md)
