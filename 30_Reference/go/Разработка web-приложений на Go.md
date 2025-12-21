---
created: 2025-12-14 14:10
up:
  - "[[Web Development]]"
related:
  - "[[Golang]]"
aliases:
  - Go web development
tags:
  - type/note
summary:
---

## Network address

The TCP network address that you pass to `http.ListenAndServe()` should be in the format "`host:port`". If you omit the host ("`:4000"`) then the <font color="#c0504d">**server will listen on all your computer’s available network interfaces**</font>. Generally, you only need to specify a host in the address if your computer has multiple network interfaces and you want to listen on just one of them.

In other Go projects or documentation you might sometimes see network addresses written using named ports like `":http"` or `":http-alt" `instead of a number. If you use a named port then the `http.ListenAndServe()` function <font color="#c0504d">**will attempt to look up the relevant port number from your `/etc/services` file** </font>when starting the server, returning an error if a match can’t be found.

## Trailing slashes in route patterns

Imagine two route patterns ("`/snippet/view`" and "`/snippet/create`") that don’t end in a trailing slash. 
**When a pattern doesn’t have a trailing slash**, it will **only be matched** (and the corresponding handler called) when the request URL path **exactly matches** the pattern in full.

When a route pattern ends with a trailing slash — like `"/"` or "`/static/`" — it is known as a **subtree path pattern**. 
Subtree path patterns are matched (and the corresponding handler called) whenever the start of a request URL path matches the subtree path. 
If it helps your understanding, you can think of subtree paths as acting a bit like they have a wildcard at the end, like "`/**`" or "`/static/**`".

This helps explain why the "`/"` route pattern acts <font color="#c0504d">like a catch-all</font>. The pattern essentially means match a single slash, followed by anything (or nothing at all).

### Restricting subtree paths

To prevent subtree path patterns from acting like they have a wildcard at the end, you can append the special character sequence `{$}` to the end of the pattern — like "`/{$}`" or  "`/static/{$}`".

So if you have the route pattern "`/{$}`" , it effectively means match a single slash, followed by nothing else. 
It will only match requests where the URL path is exactly `/`.