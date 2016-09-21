# Using Template Literals

In JavaScript there are four ways to define a string:

```
var x = String('a string of characters')
var y = 'single quotes creates a string'
var z = "double quotes creates a string"
var zz = `back ticks create a string, the neat thing about
back tick strings is that you can create
multi-line strings and template literal`
```

In this lesson, we will learn about the `backtick string` or `template literals`.

The template literal string is created with characters enclosed with a '`'.

<div class="tonic">
<pre>
var template = `I am a template string`
template
</pre>
</div>

The nifty thing about template strings is that you can add placeholders for data
that will be filled in later.

<div class="tonic">
var data = "foo"
var template = `I can inject ${data} using the dollar sign and braces`
</div>

> Detailed documentation on this function is available at: <br>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals

[Back](.) | [Prev](forms)
