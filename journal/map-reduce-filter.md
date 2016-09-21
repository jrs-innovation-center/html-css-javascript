# Map, Reduce and Filtering in Javascript

Map, reduce and filter are core operations that are performed on collections of data (lists or arrays).
These operations can be combined to create building blocks for applications.



---

## Map

Map is a function that is called as a method on a list (or array) of items.
It walks (iterates) over each item in the list (or array) and calls a function on each item returning a new list (or array) as the result.

In this example, we use map to create a new array that has each element in the original array doubled.

<div class="tonic">
<pre>
const double = function (v) {
  return v * 2
}

Array(1,2,3,4).map(double) // 2, 4, 6, 8
</pre>
</div>

> For more information about map:

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map

---

## Reduce

Reduce is intended to compute a single answer from a list or array.
Reduce takes a function and a seed and invokes the function taking the last returned
value and the value of the current item in the list.

<div class="tonic">
<pre>
const sum = function (a, b) {
  return a + b
}

Array(1,2,3,4).reduce(sum, 0)
</pre>
</div>

> For more information about reduce:

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

---

## Filter

Filter provides a method of selecting a subset of items in a list or array.
Filter takes a predicate function that returns true or false.
The function is called for each item in the list (or array).
A new list or array is returned that comtains only the items for which true was returned by the function.

> A predicate function is a function that takes arguments and always returns a
true or false.
> https://en.wikipedia.org/wiki/Predicate_(mathematical_logic)

In this example, we will only return even numbers:

<div class="tonic">
<pre>
const even = function (v) {
  return (v % 2 === 0)
}

Array(1, 2, 3, 4, 5, 6).filter(even)
</pre>
</div>

---

[Back](.)  | [Prev](databases)
