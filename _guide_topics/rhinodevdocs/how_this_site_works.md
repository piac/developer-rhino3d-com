---
layout: toc-guide-page
title: How This Site Works
author: dan@mcneel.com
categories: ['General']
platforms: ['Mac', 'Windows']
apis: ['Developer Docs', 'Jekyll', 'Liquid']
languages: ['Markdown', 'Kramdown', 'YAML']
keywords: ['authoring', 'writing', 'editing', 'overview']
TODO: 0
origin: unset
order: 2
---

# How This Site Works

[This site](http://developer.rhino3d.com) is hosted on [GitHub Pages](https://pages.github.com/).  Every time a commit is made to [this git repository](https://github.com/mcneel/developer-rhino3d-com), a static site-generator called [Jekyll](http://jekyllrb.com/) churns through all the markdown content to generate html for the site.  Behind the scenes, Jekyll uses a templating language called [Liquid](https://github.com/Shopify/liquid/wiki), which allows for automatic generation of some content based upon yaml fields or page contents.


## Workflow

The best way to understand how this site works is to make a change to it.  Follow these steps:

1. If you have not already, read the [Getting Started with Dev Docs](https://github.com/mcneel/developer-rhino3d-com/blob/gh-pages/README.md) guide.  This guide will get you setup building the entire site locally on your computer so you can preview changes before making them live (by committing).
1. With the site up and running on your localhost, make a change to one of the pages (find a typo...there are many).  A good editor for Markdown is the [Atom editor](https://atom.io/).  Once you save your changes to the .md file, wait a moment, then refresh the localhost site in your browser to preview your change.
1. If you are satisfied with your change, use git to commit your change to the GitHub repository (or submit a pull-request for review).
1. Wait a couple minutes - this site is large and it may take a minute or two for Jekyll to process all the markdown and render the html contents.  (If you issued a pull-request, your change won't be live until a git administrator accepts it).
1. On the live [developer.rhino3d.com](http://developer.rhino3d.com), you should see your change.

**NOTE**: For those familiar with Google's AppEngine workflow, this workflow should seem similar.

---

## Markdown & Kramdown

Use the [Style Guide]({{ site.baseurl }}/guides/rhinodevdocs/style_guide/) guide as a reference when writing content for this site.

Nearly all content on this site uses [Markdown](http://daringfireball.net/projects/markdown/basics) as the base format.  We are using the [Kramdown](http://kramdown.gettalong.org/quickref.html) markdown parser, which is the default parser with Jekyll.  A complete guide to Markdown and Kramdown is beyond the scope of this guide.  For markdown syntax, refer to the [Kramdown Quick Reference](http://kramdown.gettalong.org/quickref.html) or use other files on this site as examples.

---

## Layout

Each page on this site is generated by Liquid using a layout.  These layouts are found in the `/_layouts/` folder.

You determine which layout should be used by typing the layout's title in the `layout: ` yaml field at the top of the markdown file.

For example, this page uses the `toc-guide-page.html` layout, so you will find...

```yaml
layout: toc-guide-page
```

...at the top of this file.

Layouts can (and do) inherit from each other.  You will notice that the parent layout for all other layouts is `bootstrap.html`.

---

## Types of content

There are 4 types of content on this site:

 1. [Pages](#pages)
 1. [Guides](#guides)
 1. [APIs](#apis)
 1. [Samples](#samples)

All types of content - with the exception of APIs - begin with YAML, which the site uses to categories and sort the content into appropriate areas.


### Pages

Pages are interspersed throughout the site.  The [Welcome page]({{ site.baseurl }}/), the [Guides page]({{ site.baseurl }}/guides), and the [Samples page]({{ site.baseurl }}/samples), are all examples of Pages.

Here is an example of the YAML for [a page]({{ site.baseurl }}/guides/general):

```yaml
---
layout: toc-guide-page
title: General Guides
order: 0
---
```

The YAML fields for Pages determine:

* **layout**: The layout html file used by Liquid (found in `/_layouts/`) on the page.
* **title**: This is the title of the page.  This is the html page title.
* **order**: The relative sort-order of this page in any collection of pages.


### Guides

Guides are contained in the `/_guide_topics/` directory.  This very document you are reading is a Guide.

To create a new guide, simply create a new markdown file and place it in the `/_guide_topics/` folder.  The file must have a `.md` file extension and begin with some YAML that is used to determine what it is and where it should be placed on the site.

Here is an example of the YAML for this guide:

```yaml
---
layout: toc-guide-page
title: Authoring content
author: dan@mcneel.com
categories: ['General']
platforms: ['Mac', 'Windows']
apis: ['Developer Docs', 'Jekyll', 'Liquid']
languages: ['Markdown']
keywords: ['authoring', 'writing', 'editing']
order: 2
---
```

The YAML fields for Guides determine:

* **layout**: The layout html file used by Liquid (found in `/_layouts/`) on the guide.
* **title**: This is the title of the guide.  This is the html page title.
* **author**: The original - or responsible - author.
* **categories**: The category of the guide (General, Overview, Advanced).
* **platforms**: The operating systems this guide is relevant to.
* **apis**: The Rhino APIs that this guide pertains to.
* **languages**: The programming languages this guide references.
* **keywords**: Keywords related to this guide (un-used, as of yet).
* **order**: The relative sort-order of this guide in any list.


### APIs

The [API documentation]({{ site.baseurl }}/api/) is automatically generated from source-code and cannot be edited "by hand."

### Samples

Samples are contained in the `/_samples/` directory.

Here is an example of the YAML for [this sample]({{ site.baseurl }}/samples/rhinocommon/extend_a_curve_object/):

```yaml
---
layout: code-sample
title: Extend a Curve Object
author: dale@mcneel.com
categories: ['Curves']
platforms: ['Cross-Platform']
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
keywords: ['Extend', 'Curve', 'Sample']
order: 1
description: This shows how to extend a curve object
---
```

The YAML fields for Samples determine:

* **layout**: The layout html file used by Liquid (found in `/_layouts/`) on the sample.
* **title**: This is the title of the sample.  This is the html page title.
* **author**: The original - or responsible - author.
* **categories**: The category of the sample (Recipes, Snippet, Boilerplate, etc.).
* **platforms**: The operating systems this sample is relevant to.
* **apis**: The Rhino APIs or SDKs that this sample pertains to.
* **languages**: The programming languages this sample references.
* **keywords**: Keywords related to this sample (un-used, as of yet).
* **order**: The relative sort-order of this sample in any list.
* **description**: A brief description of what the sample does.


## TODO & origin fields

Many of the pages, guides, and samples have a `TODO` and `origin` yaml field.  These fields are used by this site to [report content]({{ site.baseurl }}/admin/index.html#todo-list) that:

- Needs review
- Has not yet been authored
- Needs to be ported from another source

#### TODO

If `TODO` is set to `1` (`TODO: 1`), the site will add this content to the [TODO list]({{ site.baseurl }}/admin/index.html#todo-list).

If the TODO field is not present or is set to `0` (`TODO: 0`), the content will not be on the list.

#### origin

Much of this site is (or was) ported from a previous location.  The `origin` yaml field is reserved for a backlink to the original content.  If the `origin` yaml field is set to a URL - and `TODO` is set to `1` - the content will show up on the [TODO list]({{ site.baseurl }}/admin/index.html#todo-list) as needs porting from the `origin` URL.

---

## Related topics

- [Rhino Developer Docs Style Guide]({{ site.baseurl }}/guides/rhinodevdocs/style_guide/)
- [Jekyll Documentation](http://jekyllrb.com/docs/home/)
- [Liquid Docs](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)
- [Shopify Liquid Cheatsheet](http://cheat.markdunkley.com/)
