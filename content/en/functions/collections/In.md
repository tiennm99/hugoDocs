---
title: collections.In
description: Reports whether the given value is a member of the given set.
categories: []
keywords: []
params:
  functions_and_methods:
    aliases: [in]
    returnType: bool
    signatures: [collections.In SET VALUE]
aliases: [/functions/in]
---

The `SET` can be an [array](g), [slice](g), or [string](g).

```go-html-template
{{ $s := slice "a" "b" "c" }}
{{ in $s "b" }} → true
```

```go-html-template
{{ $s := slice 1 2 3 }}
{{ in $s 2 }} → true
```

```go-html-template
{{ $s := slice 1.11 2.22 3.33 }}
{{ in $s 2.22 }} → true
```

```go-html-template
{{ $s := "abc" }}
{{ in $s "b" }} → true
```
