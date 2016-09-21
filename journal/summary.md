# Project Summary

Below is a full listing of all the code required to build this application, we have
separated the modules using the `iffe` pattern, this pattern basically helps us
create closures around our variables and enables us to only expose what we want to
expose to the global space.

Putting it all together:

## The `index.html` file

```
<!doctype html>
<html>
<head>
  <title>vanilla-journal</title>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/skeleton/2.0.4/skeleton.min.css">
  <style>
    .header {
      text-align: center;
      background-color: rgba(0,0,0,.8);
      color: whitesmoke;
    }

    header > h2 {
      color: lightgray;
    }
  </style>
</head>
<body>
  <header class="twelve columns header">
    <h1>Vanilla Journal</h1>
  </header>
  <main class="row">
    <section id="articles" class="eight columns">
      <header>
        <h2>Articles</h2>
      </header>
    </section>
    <section class="four columns">
      <header>
        <h2>New Article</h2>
      </header>
      <form>
        <div class="row">
          <label for="title">Title</label>
          <input class="u-full-width" type="text" id="title" name="title">
        </div>
        <div class="row">
          <label for="body">Article</label>
          <textarea class="u-full-width" id="body" name="body"></textarea>
        </div>
        <div class="row">
          <button class="button-primary u-pull-right">Submit</button>
        </div>
      </form>
    </section>
  </main>
  <script src="storageDB.js"></script>
  <script src="app.js"></script>
  </body>
</html>
```

---

## The `app.js` file


```

// value.js
(function () {
  window.value = function (id) {
    return document.getElementById(id).value
  }
} ())


// hscript.js

(function () {
  window.h = function (tag, content) {
    const el = document.createElement(tag)
    if (content) {
      content.map(c =>
        typeof c === 'string' ? el.innerText = c : el.appendChild(c)
      )
    }
    return el
  }
} ())

// prepend.js
(function () {
  window.prepend = function (id, el) {
    const parent = document.getElementById(id)
    parent.insertBefore(el, parent.firstChild.nextSibling)
  }
} ())

// browser.js

(function () {
  const article = content => h('article', content)
  const header = content => h('header', content)
  const h3 = content => h('h3', content)
  const div = content => h('div', content)

  const db = storageDB

  db.changes({ include_docs: true, live: true })
    .on('change', listItem)

  document.querySelector('form').addEventListener('submit', onSubmit)

  function onSubmit (event) {
    event.preventDefault()
    db.post({
      title: value('title'),
      body: value('body')
    })
    event.target.reset()
  }

  function listItem (chg) {
    append('articles',
      article([
        header([
          h3(chg.doc.title)
        ]),
        div(chg.doc.body)
      ])
    )
  }
}())
```

## The `storageDB.js` file

```
(function (window) {
  function makeid() {
    var text = ""
    var possible = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"

    for( var i=0; i < 5; i++ )
        text += possible.charAt(Math.floor(Math.random() * possible.length))

    return text
  }

  function get() {
    return JSON.parse(window.localStorage.getItem('db') || "[]")
  }

  var docs = get()

  function set() {
    window.localStorage.setItem('db', JSON.stringify(docs))
  }

  var listeners = {
    error: [],
    change: [],
    complete: []
  }

  function addListener(ev, fn) {
    listeners[ev].push(fn)
  }

  function changes (options) {
    setTimeout(_ =>
      docs.map(doc => {
        listeners.change.map(fn => fn({doc: doc}))
      })
    , 0)

    return {
      on: (ev, fn) => addListener(ev, fn)
    }
  }

  function _generateRev (old) {
    if (!old) { old = '0-unknown' }
    return parseInt(old.split('-')[0], 10) + 1 + '-' + makeid()
  }

  function _delete (doc) {
    var old = get(doc._id)
    old._deleted = true
  }

  function post (doc) {
    doc._id = makeid()
    doc._rev = _generateRev()
    docs.push(doc)
    set()
    listeners.change.map(fn => fn({doc: doc}))
  }

  function put (doc) {
    _delete(doc)
    doc._rev = _generateRev(doc._rev)
    docs.push(doc)
    set()
    listeners.change.map(fn => fn({doc: doc}))
  }

  function remove (doc) {
    _delete(doc)
    listeners.change.map(fn => fn({doc: null}))
  }

  function get(id) {
    var results = docs.filter(doc => doc._id === id)
    if (!results) { return null }
    return results[0]
  }

  function query(fn) {
    return docs
      .filter(doc => !doc._deleted)
      .map(fn)
  }

  window.storageDB = {
    changes: changes,
    query: query,
    put: put,
    post: post,
    remove: remove
  }
}(window))

```

---

[Back](.) | [Prev](list)
