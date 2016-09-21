# Basic Data Structures in Javascript

What is data?

In the abstract, data is componsed of facts and statistics collected for reference and analysis.
Data is often in the form of text, but can also be in other forms as well.
For this discussion, we will reference data in the form of text.
In order for our programs to make sense of data we need to provide some structure to the data that can be understood and shared between the functions in our program.
These structures are called *Data Structures*. One of the most common data structures is the *string* which
is a collection of characters or text that is enclosed by single quotes or double quotes.

<div class="tonic">
<pre>
console.log('A string of characters')
</pre>
</div>

In this example, we are printing a string of characters to the console. This type
of data structure is called a string.

---

A more interesting data structure is a collection. This data structure enables us
to store a group of data items in a group or collection. In JavaScript, we call this
data structure an array.

<div class="tonic">
<pre>
Array(1,2,3,4,5) // array of numbers
</pre>
</div>

<div class="tonic">
<pre>
Array('array', 'of', 'characters')
</pre>
</div>

---

With collection data structures such as arrays we can perform actions on these
structures.

<div class="tonic">
<pre>
Array(1,2,3,4,5).reverse()
</pre>
</div>

<div class="tonic">
<pre>
Array('array', 'of', 'characters').join('-')
</pre>
</div>

---

## Getting data in and out of arrays.

To get a specific element of data out of an array you can reference the index
of the element. Indexes are 0 based, which means the first item in the array is
index 0, the next is 1 and so forth.

<div class="tonic">
<pre>
Array(1,2,3)[1] // will return 2
</pre>
</div>

In this example, we are getting the second index of the array.

---

To change a value in the array we can set the value to the array reference index.

<div class="tonic">
<pre>
var numbers = Array(1,2,3)
numbers[1] = 4 // [1,4,3]
numbers
</pre>
</div>

---

You can iterate through an array using a loop.

<div class="tonic">
<pre>
var numbers = Array(1,2,3)
for (var i = 0; i < numbers.length; i++) {
  numbers[i] = numbers[i] + 2
}
numbers
</pre>
</div>

> For more information on Arrays:

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

---

## Exercises

* Create an array of color names of the rainbow, and reverse and print.
* Create an array of numbers and add 2 to each item in the array.


[Back](.)  | [Next](databases)
