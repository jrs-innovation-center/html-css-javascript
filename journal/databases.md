# Data Storage using Javascript

Computer data is typically saved in a *database*.
Databases are applications or systems that store data and enables other applications
or systems to retrieve or query that data.

What does *store data* mean?

- It is the act of placing data in a persistent location so that it may be retrieved
later.

What does *retrieve* or *query* mean?

- You may want to take collections of data and pull some or all into an application
to provide value, or you may want to ask a question against your data to arrive at
a conclusion.
For example, you may have students that just took a test. You stored
in a database for record keeping, and you may want to know what the average score,
was for the class. This would be a query against all of the records in the database.
The query would look at each record and calculate the average and return a result
displaying the average score.

We can think of databases in terms of arrays or collections of objects or key/value
pairs.

## What is an object? ##

A object is a data structure that contains a collection of keys and values. The key is a data item like a string that will be used to find the data. The value is the information associated with the key, perhaps another string or another data structure.

```
Object({ 'key': 'value' })
```

For example, a class takes a test, a single record or object could be the name of the
student and their test result.

<div class="tonic">
<pre>
Object({
  name: 'Tom',
  score: 85
})
</pre>
</div>

> For more information on objects:

>  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object

---

If I have a collection or array of students with their test scores, it may look
something like this:

<div class="tonic">
<pre>
Array({
  name: 'Tom',
  score: 85
}, {
  name: 'Trip',
  score: 95
}, {
  name: 'Mary',
  score: 100
}, {
  name: 'Sue',
  score: 82
})
</pre>
</div>

Databases have common functions like `post` or `put` to store records and `get` or `query` to retrieve records.

---

[Back](.)  | [Prev](data-structures) | [Next](map-reduce-filter)
