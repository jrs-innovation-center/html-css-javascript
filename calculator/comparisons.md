# Comparison Operators

In order to effectively use the conditional we discussed earlier, you need operators that will enable
you to provide a true or false outcome. These are called comparison operators:

* `===` - equals - The expression is true if the value on the left side of the operator is equal to the value on the right side of the operator.
* `!==` - not equals - The expression if true if the value on the left side of the operator is *not* equal to the value on the right side of the operator.
* `>, <, >=, <=` - Greater Than, Less than, Greater Than or Equal to, Less than or Equal to - These are comparison operators based on the difference between the values on the left and right sides of the operator.

> Note: Comparing numbers works as expected. Comparing strings depends on something called the collating sequence. For example, the string '123' is less than the string 'abc' and the string 'Abc' is greater than the string 'abc' due to how characters are represented in the computer.

Example of a comparison:

```
if (a < b) {
  console.log('a is less than b')
}
```

For more on comparison operators see mozilla developer network:

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators

Often you want the application to only run a set of statements if all
conditional tests pass. And often you want the application to only run a set of
statements if either or any test pass. These are called logical operators.

They use funny symbols in JavaScript:

* && is the `and` operator
* || is the `or` operator


```
if (ONE === 1 && HELLO === 'hello') {
  console.log('all conditional tests pass')
}
```

```
if (ONE === 1 || HELLO === 'hello') {
  console.log('any conditional test passes')
}
```

> Note: The comparison operators are evaluated before the logical operators. You can always use parenthesis to make sure things happen in the order you want them to!

[Back](.) | [Prev](constants)
