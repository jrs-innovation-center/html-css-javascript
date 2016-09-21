# Setup for the Project

The first thing we want to do is create a form that will take our new article
and add it to a database.

What is a database?

- A database is a container that holds data, in our case articles that we want
to retrieve later. Most databases have a way to create containers,
put things into containers and get things out of containers.

    - create
    - put
    - get

We are going to store and retrieve articles or documents.

This is called a document database. There are several types
of databases, but for this project we only need to think about
document storage databases.

---

## Default HTML

The following is a framework for the journal web page. We will be filling out the page as we build the journal application.


```
<!doctype html>
<html>
<head>
  <title>journal</title>
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
    <h1>Journal</h1>
  </header>
  <main class="row">
    <section id="articles" class="eight columns">
      <header>
        <h2>Articles</h2>
      </header>
      <!-- articles will be injected here -->
    </section>
    <section class="four columns">
      <!-- add form here -->
    </section>
  </main>
  <script src="browser.js"></script>
  </body>
</html>
```

[Back](.)  | [Next](create)
