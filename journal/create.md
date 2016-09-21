# Create a Journal Entry

The first thing we need to do is setup the form we'll use to create journal entries.
Our form will look something like this:

```
<section class="four columns">
  <header>
    <h2>New Article</h2>
  </header>
  <form>
    <div class="row">
      <label for="title">Title</label>
      <input class="u-full-width" type="text" id="title">
    </div>
    <div class="row">
      <label for="body">Article</label>
      <textarea class="u-full-width" id="body" id="body"></textarea>
    </div>
    <div class="row">
      <button class="button-primary u-pull-right">Submit</button>
    </div>
  </form>
</section>
```

We will wrap the form in a section and create three rows, a title row, a body row,
and a button row. We will add some classes to decorate the elements with a
nice presentation look and feel.

We will use the id attributes of both the input and textarea elements as unique
identifiers for the form.

---

## Capture form data

Now that we have the form setup, we want to use *javascript* to add an event
listener such that when the form is submitted  we can grab the data from the form
and add it to the database.

This code looks like this:

```
var form = document.querySelector('form')
form.addEventListener('submit', onSubmit)

function onSubmit (event) {
  event.preventDefault()
  var title = document.getElementById('title').value
  var body = document.getElementById('body').value
  var doc = {
    title: title,
    body: body
  }
  // TODO: save document to database
  console.log(doc)
  // reset form
  event.target.reset()

}
```

Save this function in a file in your project named `browser.js`

On the first line we use the `querySelector` function to return the form element
to our application, then we call `addEventListener` to register the submit function.

> Now we could have just added an attribute to the form `onsubmit` and attached
the listener function that way, but this is a bad practice and can result in to
problems. By wrapping the application in a function wrapper which is called an IFFE, it
will protect our functions from being modified or defined else where.

In the onSubmit function we first prevent the default
action (make a call to a remote server) rom happening. We don't want
to do this, we want to handle the processing on the client. Next we get the
title and body values using the `getElementById` function. This function explicitly
finds and element by its id.

We can refactor this into a simple utility function:


```
(function () {
  window.value = function (id) {
   return document.getElementById(id).value
  }
} ())
```

Save this function in a file in your project named `value.js`

---

Then we can add this utility in our index.html as a script

```
  <body>
    ...
    <script src="value.js"></script>
    <script src="browser.js"></script>
  </body>
```

We want to make sure we include it above the browser.js file

---

Lastly, we can modify our `onSubmit` function to take advantage of this refactor.

```

function onSubmit (event) {
  event.preventDefault()
  var doc = {
    title: value('title'),
    body: value('body')
  }

  // TODO: save document to database
  console.log(doc)
  // reset form
  event.target.reset()

}

```

---

## Store data in the database

For this step we are going to use a simple database that uses storage local to the
browser (localstorage).

What is localstorage?

- LocalStorage is an HTML 5 API that enables an application
to persist data locally in the browser. It has two functions: `setItem` and
`getItem`, the `setItem` function takes a string for the key name and a string
for a value. The getItem function takes a string for the key name and returns a
string for the value.

We will use a library called `sdb.js`. This library mimics a popular database API
called `pouchdb`. We need two functions from the db, `changes` and `post`, the
`changes` function returns another functions; an `on` function.
The `on` function enables us to add a listener to the db such that when new documents are added to the database we will know to add them to our list being displayed. The `post` function just adds a document to the database.

So in our `onSubmit` form, we need to add the `db.post` function.

```
function onSubmit (event) {
  event.preventDefault()
  var doc = {
    title: value('title'),
    body: value('body')
  }

  db.post(doc)

  // reset form
  event.target.reset()

}

```

This will post our document to the database, now we need to create a way to list
articles.

---

[Back](.) | [Prev](setup) | [Next](list)
