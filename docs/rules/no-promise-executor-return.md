---
title: no-promise-executor-return - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-promise-executor-return.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow returning values from Promise executor functions (no-promise-executor-return)

The `new Promise` constructor accepts a single argument, called an *executor*.

```js
const myPromise = new Promise(function executor(resolve, reject) {
    readFile('foo.txt', function(err, result) {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});
```

The executor function usually initiates some asynchronous operation. Once it is finished, the executor should call `resolve` with the result, or `reject` if an error occurred.

The return value of the executor is ignored. Returning a value from an executor function is a possible error because the returned value cannot be used and it doesn't affect the promise in any way.

## Rule Details

This rule disallows returning values from Promise executor functions.

Only `return` without a value is allowed, as it's a control flow statement.

Examples of **incorrect** code for this rule:

```js
/*eslint no-promise-executor-return: "error"*/

new Promise((resolve, reject) => {
    if (someCondition) {
        return defaultResult;
    }
    getSomething((err, result) => {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});

new Promise((resolve, reject) => getSomething((err, data) => {
    if (err) {
        reject(err);
    } else {
        resolve(data);
    }
}));

new Promise(() => {
    return 1;
});
```

Examples of **correct** code for this rule:

```js
/*eslint no-promise-executor-return: "error"*/

new Promise((resolve, reject) => {
    if (someCondition) {
        resolve(defaultResult);
        return;
    }
    getSomething((err, result) => {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});

new Promise((resolve, reject) => {
    getSomething((err, data) => {
        if (err) {
            reject(err);
        } else {
            resolve(data);
        }
    });
});

Promise.resolve(1);
```

## Further Reading

* [MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

## Related Rules

* [no-async-promise-executor](no-async-promise-executor)

## Version

This rule was introduced in ESLint 7.3.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-promise-executor-return.js)
* [Test source](https://github.com/eslint/eslint/tree/HEAD/tests/lib/rules/no-promise-executor-return.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-promise-executor-return.md)
