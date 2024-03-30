---
title: "Hugo"
weight: 7
# bookFlatSection: false
bookToc: false 
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
---
## Hugo 
---                                                                                                             

Info at [snapcraft](https://gohugo.io/)

Visit [Quickstart](https://gohugo.io/getting-started/quick-start/) to get up to speed.

## Example install

```
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/alex-shpak/hugo-book themes/book
echo "theme = 'hugo-book'" >> hugo.toml
hugo server
```

## Own data

Your own data and configs are normally in:
- hugo.toml
- content/docsd
- static

## create new workdirectory from github to test local

```
git clone <your.github.io>
cd <your.github.io>
git submodule init
git submodule update
```
Can also ne done in one go:

```
git clone --recurse-submodule <your.github.io>
```
