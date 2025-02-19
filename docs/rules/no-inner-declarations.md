---
title: no-inner-declarations - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-inner-declarations.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow variable or `function` declarations in nested blocks (no-inner-declarations)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

In JavaScript, prior to ES6, a function declaration is only allowed in the first level of a program or the body of another function, though parsers sometimes [erroneously accept them elsewhere](https://code.google.com/p/esprima/issues/detail?id=422). This only applies to function declarations; named or anonymous function expressions can occur anywhere an expression is permitted.

```js
// Good
function doSomething() { }

// Bad
if (test) {
    function doSomethingElse () { }
}

function anotherThing() {
    var fn;

    if (test) {

        // Good
        fn = function expression() { };

        // Bad
        function declaration() { }
    }
}
```

A variable declaration is permitted anywhere a statement can go, even nested deeply inside other blocks. This is often undesirable due to variable hoisting, and moving declarations to the root of the program or function body can increase clarity. Note that [block bindings](https://leanpub.com/understandinges6/read#leanpub-auto-block-bindings) (`let`, `const`) are not hoisted and therefore they are not affected by this rule.

```js
/*eslint-env es6*/

// Good
var foo = 42;

// Good
if (foo) {
    let bar1;
}

// Bad
while (test) {
    var bar2;
}

function doSomething() {
    // Good
    var baz = true;

    // Bad
    if (baz) {
        var quux;
    }
}
```

## Rule Details

This rule requires that function declarations and, optionally, variable declarations be in the root of a program, or in the root of the body of a function, or in the root of the body of a class static block.

## Options

This rule has a string option:

* `"functions"` (default) disallows `function` declarations in nested blocks
* `"both"` disallows `function` and `var` declarations in nested blocks

### functions

Examples of **incorrect** code for this rule with the default `"functions"` option:

```js
/*eslint no-inner-declarations: "error"*/

if (test) {
    function doSomething() { }
}

function doSomethingElse() {
    if (test) {
        function doAnotherThing() { }
    }
}

if (foo) function f(){}

class C {
    static {
        if (test) {
            function doSomething() { }
        }
    }
}
```

Examples of **correct** code for this rule with the default `"functions"` option:

```js
/*eslint no-inner-declarations: "error"*/

function doSomething() { }

function doSomethingElse() {
    function doAnotherThing() { }
}

class C {
    static {
        function doSomething() { }
    }
}

if (test) {
    asyncCall(id, function (err, data) { });
}

var fn;
if (test) {
    fn = function fnExpression() { };
}

if (foo) var a;
```

### both

Examples of **incorrect** code for this rule with the `"both"` option:

```js
/*eslint no-inner-declarations: ["error", "both"]*/

if (test) {
    var foo = 42;
}

function doAnotherThing() {
    if (test) {
        var bar = 81;
    }
}

if (foo) var a;

if (foo) function f(){}

class C {
    static {
        if (test) {
            var something;
        }
    }
}
```

Examples of **correct** code for this rule with the `"both"` option:

```js
/*eslint no-inner-declarations: ["error", "both"]*/

var bar = 42;

if (test) {
    let baz = 43;
}

function doAnotherThing() {
    var baz = 81;
}

class C {
    static {
        var something;
    }
}
```

## When Not To Use It

The function declaration portion rule will be rendered obsolete when [block-scoped functions](https://bugzilla.mozilla.org/show_bug.cgi?id=585536) land in ES6, but until then, it should be left on to enforce valid constructions. Disable checking variable declarations when using [block-scoped-var](block-scoped-var) or if declaring variables in nested blocks is acceptable despite hoisting.

## Version

This rule was introduced in ESLint 0.6.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-inner-declarations.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/no-inner-declarations.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-inner-declarations.md)
