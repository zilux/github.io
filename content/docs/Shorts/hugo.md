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
