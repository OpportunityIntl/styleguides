#HTML Styleguide

Based off [@mdo Code Guide](http://mdo.github.io/code-guide/), which itself is based off of [Idiomatic CSS](https://github.com/necolas/idiomatic-css) and [GitHub Styleguide](http://github.com/styleguide)

##Syntax

- Use soft tabs with two spaces. Soft tabs are the only way to guarantee code renders the same in any environment. Two spaces is a matter of preference, but [I'm the decider](https://i.chzbgr.com/maxW500/1353310976/h52166690/).
- Nested elements should be indented once (two spaces).
- Use double quotes, not single quotes, on attributes. There's no significant advantage of using one over the other, but we need to be consistent.
- Don't omit optional closing tags (e.g. `</li>` or `</body>`).

##HTML5 doctype

Enforce standards mode and more consistent rendering in every browser possible with this simple doctype at the beginning of every HTML page.

```HTML
<!DOCTYPE html>
<html>
  <head>
  </head>
</html>
```

##IE compatibility mode

Internet Explorer supports the use of a document compatibility <meta> tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IE to use the latest supported mode with edge mode.

For more information, read this awesome Stack Overflow article.

```HTML
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

##Character encoding

Quickly and easily ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document (generally UTF-8).

```HTML
<head>
  <meta charset="UTF-8">
</head>
```

##CSS and JavaScript includes
Per HTML5 spec, typically there is no need to specify a type when including CSS and JavaScript files as text/css and text/javascript are their respective defaults.

- HTML5 spec links
- Using link
- Using style
- Using script

```HTML
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

##Paragraphs and Line Breaks

Only use `<br>` tags for soft returns / line breaks. If you're using more than one `<br>` tag consecutively, you should probably be using a `<p>`. If you're using `<br>` tags for spacing, you should probably be using a CSS class to set a margin.

```HTML
<!-- Bad -->
<div>
  If I had a million dollars, well, I'd buy you an exotic pet. Like a llama or an emu.
  <br>
  <br>
  Actually, that would be a terrible gift. I won't do that.
</div>

<!-- Good -->
<div>
  <p>If I had a million dollars, well, I'd buy you an exotic pet. Like a llama or an emu.</p>
  <p>Actually, that would be a terrible gift. I won't do that.</p>
</div>
```

##Practicality over purity

Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible.

##Boolean attributes
A boolean attribute is one that needs no declared value. XHTML required you to declare a value, but HTML5 has no such requirement.

For further reading, consult the [WhatWG section on boolean attributes](http://www.whatwg.org/specs/web-apps/current-work/multipage/common-microsyntaxes.html#boolean-attributes).

```HTML
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

##JavaScript generated markup

Writing markup in a JavaScript file makes the content harder to find, harder to edit, and less performant. **Avoid it whenever possible.**
