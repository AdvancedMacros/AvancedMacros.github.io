---
title: Editing this site
permalink: "/docs/docs-setup/"
redirect_from:
  - /docs-setup/
  - /docs/docs-setup/
---

## Local Setup
Download the source for [this site](https://github.com/AdvancedMacros/AdvancedMacros.github.io) from github

For installation of Ruby x >= `2.2.7`  and Jekyll, `3.0.0` and up doesn't seem to work though

be in the project folder
Follow instructions [here](https://jekyllrb.com/docs/step-by-step/01-setup/) up until it tells you about setting up files

probably run `bundle install`

then
`bundle exec jekyll build`

finally
`builde exec jekyll serve`

view at [localhost:4000](http://localhost:4000)

## Adding a link to the sidebar

If it's just to the contents, a line like this `## Foo` will show up in contents.<br>
(markdown for &lt;h2&gt;)<br>
<br>
But what if I want to add a link to one of the categories?<br>

Edit `_data/docs_nav.yml` and add the `permalink` in the group. You can even make new categories.<br>

## what's the header in the markdown?
`title` The &lt;h1&gt; title for top of the page<br><br>
`permalink` where the url for the markdown is<br><br>
`redirects_from` if you try to go to one of those links, <br> you go to `permalink` instead<br><br>
`menu_name` if you see this, it changes the title in the side bar<br><br>
`position` pagination

## Do I have to restart the server to see changes?
Nope.

## Tutorial label
Make sure it matches in all steps

I'd make it so as long as they're in the same folder it all counts as one, but `liquid`'s filters are a pain,<br>
who doesn't offer `()` to alter order of operations for filters? `liquid`

