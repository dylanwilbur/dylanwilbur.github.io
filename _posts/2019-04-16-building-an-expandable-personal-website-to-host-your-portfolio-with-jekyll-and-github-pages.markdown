---
layout: post
title: "Building an Expandable Personal Website to Host Your Portfolio with Jekyll and Github Pages"
date: "2019-04-16 20:27:59 -0700"
---

## Getting a ruby development environment
  - Setting Up on Windows
    - Link to Ravi's article
  - Setting Up on Mac
    - https://gorails.com/setup/osx/10.14-mojave
    - Use homebrew for everything

## Using Jekyll
  - Using a theme/template
    - http://jekyllthemes.org/
    - https://github.com/mmistakes/
  - Follow the steps given for a specific theme: specific to a theme for many

## Resume creation
- Using json:
  - jsonresume.org
  - must have node installed at v. 8.7(tested at 8.7, broken at 6.9 and 8.0)
  - getting a theme to work:
    - preview the themes on jsonresume.org
    - the links seem to be broken, so googling it and finding the repo link on github might be the best option
    - found little success in trying to download a theme as a node js package, so I opted to clone the repo locally and ran `resume init` from there
    - you can edit the `resume.json` file from there, and preview it using `resume serve`:
      - with resume serve, you should have access to the html file using inspect element
      - you can also download as a pdf by printing the page, then opting to save as pdf
    - you can export your file to html using `resume export resume.html`:
      - only got this to work for the default theme
      - you can then use pandoc to convert to other formats if necessary if you can get it in html form
  - once you have either html file or pdf:
    - you can put it on the site, either by hosting the pdf itself on github pages, or by using the html file as a page on your github pages site

### Resources/References



