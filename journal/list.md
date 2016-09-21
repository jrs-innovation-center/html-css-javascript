# List Journal Entries

## DB Changes Feed

Using the database changes feed (the `on` function discussed in the last section), we can get notified when a new article is posted so we can display (pain) the article on the screen.

We can access the changes feed using the `db.changes` function.

```
db.changes({ include_docs: true, live: true })
  .on('change', listItem)

function listItem (doc) {
  // create article view
  // add to articles view
}
```

Now everytime a new article is added the listItem document will be called.

---

## Update the screen with a new article

We need to create a new section in our html document:

```
<section id="articles" class="eight columns">
  <header>
    <h2>Articles</h2>
  </header>
</section>
```

Notice in this section we provided an `id` for the section called articles. We
will use that id to reference the point on the screen where we will add the new articles.

In the `browser.js` file we need to create elements for an article and append them
to the articles section.

To build the article view using the dom directly, you may see some code like this:

```
var titleElement = document.createElement('h3')
titleElement.innerText = doc.title
var headerElement = document.createElement('header')
headerElement.appendChild(titleElement)
var bodyElement = document.createElement('div')
bodyElement.innerText = doc.body

var article = document.createElement('article')
article.appendChild(headerElement)
article.appendChild(bodyElement)

var articles = document.getElementById('articles')
articles.appendChild(article)
```

But you can see this is a lot of redundant code and we can create a very simple
abstraction to make this much easier to read and manage.

We will create a little helper function called `h` this function will make it easier
to create and nest elements.

```
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
}())
```

This function will take a string for a tag and either an array or a string for
content. This enables us to nest functions.

So instead of createElement then innerText, we can compose a view, like this:

```
h('article', [
  h('header', [
    h('h3', doc.title)
  ]),
  h('div', doc.body)
])
```

We can further refine the view by creating alias methods:

```
const article = content => h('article', content)
const header = content => h('header', content)
const h3 = content => h('h3', content)
const div = content => h('div', content)
```

By creating these alias methods we can simplify our code:

```
article([
  header([
    h3(doc.title)
  ]),
  div(doc.body)
])
```

---

Our `listItem` function will look like this:

```
function listItem (chg) {
  var el = article([
      header([
        h3(chg.doc.title)
      ]),
      div(chg.doc.body)
    ])

  var parent = document.getElementById('articles')
  var header = parent.querySelector('header')
  parent.insertBefore(el, header.nextSibling)
}
```

---

Now that we have a nice view, lets abstract out the append process into a simple
append function.

```
(function () {
  window.append = function (id, el) {
    var parent = document.getElementById(id)
    var header = parent.querySelector('header')
    parent.insertBefore(el, header.nextSibling)
  }
}())
```

By creating a generic append function, we can reduce the listItem function into
a clearly nested set of functions that are declarative.

Save the code in a file named `append.j`.

---

When an item is added, we want to list the item by appending the new article to
the articles section. The article has a header and a h3 for the title as well as
a div for the body.

```
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
```

---

[Back](.) | [Prev](create) | [Next](summary)
