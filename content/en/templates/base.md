---
title: Base templates
description: The base and block construct allows you to define the outer shell of your master templates (i.e., the chrome of the page).
categories: []
keywords: []
weight: 40
aliases: [/templates/blocks/,/templates/base-templates-and-blocks/]
---

The `block` keyword allows you to define the outer shell of your pages' one or more master template(s) and then fill in or override portions as necessary.

{{< youtube QVOMCYitLEc >}}

## Base template lookup order

The base template lookup order closely follows that of the template it applies to (e.g. `_default/list.html`).

See [Template Lookup Order](/templates/lookup-order/) for details and examples.

## Define the base template

The following defines a simple base template at `_default/baseof.html`. As a default template, it is the shell from which all your pages will be rendered unless you specify another `*baseof.html` closer to the beginning of the lookup order.

```go-html-template {file="layouts/_default/baseof.html"}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ block "title" . }}
      <!-- Blocks may include default content. -->
      {{ .Site.Title }}
    {{ end }}</title>
  </head>
  <body>
    <!-- Code that all your templates share, like a header -->
    {{ block "main" . }}
      <!-- The part of the page that begins to differ between templates -->
    {{ end }}
    {{ block "footer" . }}
    <!-- More shared code, perhaps a footer but that can be overridden if need be in  -->
    {{ end }}
  </body>
</html>
```

## Override the base template

The default list template will inherit all of the code defined above and can then implement its own `"main"` block from:

```go-html-template {file="layouts/_default/list.html"}
{{ define "main" }}
  <h1>Posts</h1>
  {{ range .Pages }}
    <article>
      <h2>{{ .Title }}</h2>
      {{ .Content }}
    </article>
  {{ end }}
{{ end }}
```

This replaces the contents of our (basically empty) "main" block with something useful for the list template. In this case, we didn't define a `"title"` block, so the contents from our base template remain unchanged in lists.

{{< note >}}
Code that you put outside the block definitions *can* break your layout. This even includes HTML comments. For example:

```go-html-template
<!-- Seemingly harmless HTML comment..that will break your layout at build -->
{{ define "main" }}
...your code here
{{ end }}
```
[See this thread from the Hugo discussion forums.](https://discourse.gohugo.io/t/baseof-html-block-templates-and-list-types-results-in-empty-pages/5612/6)
{{< /note >}}

The following shows how you can override both the `"main"` and `"title"` block areas from the base template with code unique to your default [single template]:

```go-html-template {file="layouts/_default/single.html"}
{{ define "title" }}
  <!-- This will override the default value set in baseof.html; i.e., "{{ .Site.Title }}" in the original example-->
  {{ .Title }} &ndash; {{ .Site.Title }}
{{ end }}
{{ define "main" }}
  <h1>{{ .Title }}</h1>
  {{ .Content }}
{{ end }}
```

[single template]: /templates/types/#single
