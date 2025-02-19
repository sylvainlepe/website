---
title: default-case - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/default-case.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require Default Case in Switch Statements (default-case)

Some code conventions require that all `switch` statements have a `default` case, even if the default case is empty, such as:

```js
switch (foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomething();
        break;

    default:
        // do nothing
}
```

The thinking is that it's better to always explicitly state what the default behavior should be so that it's clear whether or not the developer forgot to include the default behavior by mistake.

Other code conventions allow you to skip the `default` case so long as there is a comment indicating the omission is intentional, such as:

```js
switch (foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomething();
        break;

    // no default
}
```

Once again, the intent here is to show that the developer intended for there to be no default behavior.

## Rule Details

This rule aims to require `default` case in `switch` statements. You may optionally include a `// no default` after the last `case` if there is no `default` case. The comment may be in any desired case, such as `// No Default`.

Examples of **incorrect** code for this rule:

```js
/*eslint default-case: "error"*/

switch (a) {
    case 1:
        /* code */
        break;
}

```

Examples of **correct** code for this rule:

```js
/*eslint default-case: "error"*/

switch (a) {
    case 1:
        /* code */
        break;

    default:
        /* code */
        break;
}


switch (a) {
    case 1:
        /* code */
        break;

    // no default
}

switch (a) {
    case 1:
        /* code */
        break;

    // No Default
}
```

## Options

This rule accepts a single options argument:

* Set the `commentPattern` option to a regular expression string to change the default `/^no default$/i` comment test pattern

### commentPattern

Examples of **correct** code for the `{ "commentPattern": "^skip\\sdefault" }` option:

```js
/*eslint default-case: ["error", { "commentPattern": "^skip\\sdefault" }]*/

switch(a) {
    case 1:
        /* code */
        break;

    // skip default
}

switch(a) {
    case 1:
        /* code */
        break;

    // skip default case
}
```

## When Not To Use It

If you don't want to enforce a `default` case for `switch` statements, you can safely disable this rule.

## Related Rules

* [no-fallthrough](no-fallthrough)

## Version

This rule was introduced in ESLint 0.6.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/default-case.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/default-case.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/default-case.md)
