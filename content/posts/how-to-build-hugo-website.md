---
title : 'How to Build Hugo Website'
date : 2024-08-19T14:38:39-04:00
draft : false
author: ["Ozan"]
categories: ["programming"]
tags: ["hugo"]
description: "How to Build Hugo Website"
weight: 1
slug: ""
cover:
    image: /img/posts/how-to-build-hugo-website/hugo.png
    caption: "Edgar Allen Poe develops a Hugo Website"
    alt: "picture of Edgar Allen Poe"
    relative: false
---


## Setting Up Hugo

We need brew, go, git and hugo to build a Hugo website. I assume we already have bre and git are installed in our operating system.

```console
brew install go
go version

brew install hugo
hugo version

hugo new site myspace
code .
```
---

## Create Custom Layout

Create a markdown file named as _index.md under content folder

```markdown
---
title: Home
---

Hello World!!!
```

and about.md with **title:** About then create default layout as **baseof.html** under **/layouts/_default/** folder

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{.Page.Title}}</title>
</head>
<body>
    {{ block "main" . }}
    {{ end }}
</body>
</html>
```
create two more html files under **_default** folder **list.html** for landing page and **single.html** for about page with below content

```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```
---
## Stylesheet

```html
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS | resources.Minify }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```

then create main.scss under assets/sass/ folder

```css
body {
  width: 400px;
  margin: 0 auto;
  font-family: sans-serif;
}
```
---
## Partials

Create a file name as **nav.html** under **/layoutes/partials/** 

```html
<nav>
 <ul>
   <li><a href="/">Home</a></li>
   <li><a href="/about/">About</a></li>
 </ul>
</nav>
```
then add below line in the **baseof.html**
```html
{{ partial "nav.html" }}
```
we can also create meta partial as **meta.html**
```html
<meta charset="utf-8">
<title>{{ print .Page.Title }}</title>
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS | resources.Minify }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```
then add snippet in baseof.html
```html
{{ partial "meta.html" . }}
```
That little . at the end is passing the context of the current page, which allows the partial to print out the current page’s title.

---
## Template
```html
<title>{{ .Params.title }} | {{ .Site.title }}</title>
<p>you can use double curly braces like this: {{ "Hello!" }}.</p>

{{ if isset .Params "title" }}
 <title>{{ .Params.title }}</title>
{{ else }}
 <title>{{ .Site.title }}</title>
{{ end }}

{{ $favorite_food := "Gazelle" }}
{{ $favorite_food }}

{{ $best_friends := slice "pumbaa" "timon" "nala" "rafiki" }}

<ul>
{{ range $best_friends }}
 <li>{{ . }}</li>
{{ end }}
</ul>
```

to create conditiotonal templeting, enter params in config.toml or hugo.toml file

```toml
[params]
name = 'Functor'
```
then create a footer.html partial where footer will only seen if params is exist
```html
{{ with .Params.hide_footer }}
 <!-- No footer here! -->
{{ else }}
 <footer>
   Website made by {{ .Site.Params.name }} in {{ now.Year }}
 </footer>
{{ end }}
```
then add the partial in **baseof.html**

```html
{{ partial "footer.html" . }}
```
we can hide footer in any html page(content) adding hide_footer just below title
```html
hide_footer: true
```
---
## Creating Blog
cretate a file name as  **_index.md** under /content/posts/
```markdown
---
title: Blog
---
```
this markdown file will follow the rules of list.html unde /layouts/_default/ folder
we can create our spesific layout if we also create list.html  under /layout/posts folder
```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```
but we can also create single.html under /layout/posts/ folder so every post will follow the rules of single.html file's rules
```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```

---
## Using Available Layouts

Above we can see basic hugo structure, alternatively we can use a theme to be able to see the site

```console
hugo new site myspace
cd myspace
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
hugo server
```
we can also use git clone instead of fit submodule add

* you can refer from https://gohugo.io/getting-started/quick-start/ 

```console
echo "theme = 'ananke'" >> hugo.toml
```
or directly place below code to hugo.toml before running hugo server
```console
theme: ["PaperMod"]
```
delete draft = true or assign false
to add content and publish it(files in public folder)
```console
hugo new content posts/my-first-post.md
hugo server
hugo
```

when we created new post in terminal, the current time automatically created but if we like to create a file with default **fron matter**, we can add default **fron matter** in **default.md** under **archtypes** folder so next time when we create a file with ***hugo new content*** comment, all the fron matter will be added.
```console
title : '{{ replace .File.ContentBaseName "-" " " | title }}'
date : {{ .Date }}
draft : true
author: ["Ozan"]
```
---
## Hugo.toml

Hugo.toml is a configuration file where we can define navigation, profile module and more. 

---
## Publishing Website

After finishing the development of vebsite we can create public directory with ***hugo*** on terminal. The public directory will contain all the html, css, javascript and static files for the website, however we will upload our files to ***netlify*** so we can delete the public directory.

```console
hugo 
rm -rf ./public/
git init
touch .gitmodules
```

We need to initialize git file to push our filese to github then later we will connect the github repository to netlify. We also need to create a .gitmodules to define the theme for git.

```console
[submodule "themes/PaperMod"]
    path = themes/PaperMod
    url = "htps://github.com/adityatelange/hugo-PaperMod.git"
```

Then we can push our project to github.