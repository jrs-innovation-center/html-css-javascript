# Conditionals

Conditionals allow you to make decisions in your program.
You can make these decisions depending on the many things including the values of your data or input to the program.
There are four common conditional patterns, we will talk about three of them:

* `if` statement
* `if else` statement
* `if else if` statements

## if statement

The `if` statement will perform actions if the value of the expression following the `if` keyword is true (or non-zero).

The basic form of the `if` statement is:

```
if (expression) {
    actions
}
```

> Note: the parenthesis around the expression and the braces around the actions are important!

For example:

```
const ONE = 1
if (ONE === 1) {
  console.log('The constant ONE is equal to the value 1')
}
```

Another example:

```
const HELLO = 'hello'
if (HELLO === 'hello') {
  console.log('The constant HELLO is equal to the value "hello"')
}
```

## if else statement

Using `if else` allows you to invoke different statements depending on whether the expression if true (non-zero) or false (zero).

```
const ONE = 1
if (ONE === 2) {
  console.log('The constant ONE is equal to the value 2')
} else {
  console.log('The constant ONE is not equal to the value 2')
}
```

# if else if statement #

Using the `else if` statement, you are able to repeat conditional checks in the statement.

```
const HELLO = 'hello'

if (HELLO === 'goodbye') {
  console.log('The constant HELLO is equal to the value "goodbye"')
} else if (HELLO === 'hello') {
  console.log('The constant HELLO is equal to the value 'hello')
} else {
  console.log('The constant HELLO is not equal to the value "goodbye" or "hello"')
}
```

To read more about the if else statements check out the mozilla developer network:

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else


The other conditional is called a switch statement and we will not discuss it here,
but if you want to know more about the switch statement, you can read more here:

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch

[Back](.) | [Next](constants)
