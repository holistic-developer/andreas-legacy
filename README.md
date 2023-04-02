# This is my personal page & blog

It is built with [hugo](https://gohugo.io/) using the theme [LoveIt] (https://hugoloveit.com/)

Some features of this team require **hugo extended** version.

→ DEV container coming soon.

## How to build locally

Hugo has a live development server built in.
To also see drafts when working on them add -D

```bash
hugo serve --disableFastRender -D
```

## How to publish

To publish it, first generate the page again, then push it to the `gh-pages` branch.

```bash
hugo --minify
git subtree push --prefix public origin gh-pages

```
