---
layout: default
title: "Meta"
nav_order: 12
permalink: /docs/meta
authors: ['ewpratten']
---

# The webdocs' docs
This page contains the documentation for keeping our documentation updated.

## Updating webdocs
Webdocs is built out of a collection of text files [hosted on GitHub](https://github.com/frc5024/webdocs). To update this site, clone and edit the files in the `docs/` folder. Once your addition is ready for publishing, push to the master branch, and the site will automatically update after a few minutes.

### Formatting
All documents are written in a markup language called [Markdown](https://daringfireball.net/projects/markdown/). Markdown is easy to learn, and a great [guide is available](https://www.markdownguide.org/) to help you learn the syntax.

For members looking to work with some extra features, you should know that we do not use standard Markdown, but instead, [Kramdown](https://kramdown.gettalong.org/) (it has the same syntax) with a bunch of [plugins](#the-sites-plugins).

### File headers
For easy development and parsing, webdocs uses the [liquid parser](https://shopify.github.io/liquid/). This allows for the use of variables and other bits of code to be written directly into our documents. The way out site is set up, every file must start with a liquid header. Note, this must literally be the first thing in the file, line 1 cannot be blank.

Here is a standard header for this page
```markdown
---
layout: default
title: "Meta"
nav_order: 12
permalink: /docs/meta
authors: ['ewpratten']
---
```

The start and end of a header are defined by three dashes.

The layout must be `default`. Title is what shows in the nvigation bar, and permalink is the url for this page. Change these to match the page you are writing. 
The `nav_order` variable is the order this item appears in the navigation bar. Generally, put new pages at the bottom of the list.

To create a folder in the nav bar, create a folder inside of the `docs/` folder, and make a file with the same name inside that folder. This file acts at the table of contents for that folder, and must have an extra line in it's header:
```markdown
---
# <The rest of the header goes here>
has_children: true
---
```

To add children to this sub-section, add new files to it's folder, and give them this extra attribute:
```markdown
---
# <The rest of the header goes here>
parent: "<Title of the index file>"
---
```

The parent must exactly match the title of the index (table of contents) file for that folder.

### The contributors list
Every file also has an `authors` tag in it's header. This is used to keep track of who has worked on each file. To add yourself as an author to the page, add your GitHub username (all lowercase) to the list.
```markdown
---
# Example of only one author
authors: ['slownie']

# Example of two authors
authors: ['retrax24', 'ewpratten']
---
```
This list will be displayed at the bottom of the page.

### Adding new members to the config
The way our contributors list is set up allows for automatically generated profile pages for each member (currently disabled). These pages include the member's name, some information about what they do, and their github account details. This is all configured through the `_data/members.yml` file.

Here is an example entry for one of our graduated members, Matthew Eppel.
```yaml
faceincake:
  name: Matthew Eppel
  is_lead: false
  is_mentor: false
  github: faceincake
```

These variables should be pretty self-explanatory. The key must be the same as the value of `github`. 

To add a new member to the website, add them to this list.

## How webdocs is hosted
Webdocs is hosted on [GitHub pages](https://pages.github.com/) and automatically updated by a CD pipeline. This is all automatically configured.

## Webdocs' backend
The backend of webdocs is [Jekyll](https://jekyllrb.com/). This tool turns some markdown and html into a nice website, automatically. For anyone looking to make majour changes to this site, or the programming homepage, you will need to know how to use Jekyll. Luckily, the [Jekyll Docs](https://jekyllrb.com/docs/) have everything you need to know for this job.

### The site's theme
We are using a modified version of [Just the Docs](https://github.com/pmarsceill/just-the-docs). Their website has some useful information on how to use their theme-specific tools.

### The site's plugins
We have a few plugins installed for this website. They are:

  - jekyll-feed
  - jekyll-redirect-from
  - jemoji
  - jekyll-mentions
  - jekyll-seo-tag

Jekyll-feed automatically generates an RSS feed for this website.

Jekyll-redirect-from allows us to set up link shorteners and redirects.

jemoji enables slack-like emoji. :tada: (That was done by adding `:tada:` to the file)

Jekyll-mentions allows us to automatically link to any github account. @frc5024 (That was done by adding `@frc5024` to the file)

Jekyll-seo-tag automatically handles Search Engine Optimization for this site.


## The difference between homepage and webdocs
The programming team has two different websites. 

The first is our [homepage](/). This is a separate website, also hosted with jekyll, that can be found at the [frc5024.github.io](https://github.com/frc5024/frc5024.github.io) GitHub repo.

Second, is webdocs, which is hosted in the [webdocs](https://github.com/frc5024/webdocs) repo.

For instructions on updating the homepage, take a look at it's repo's README.md file.

## Running a development server locally
To run a development version of this site locally, 
 - [Install Ruby](https://jekyllrb.com/docs/installation/)
 - Install Jekyll with: `gem install jekyll bundler`
 - Then run `bundle exec jekyll serve` in the root of this project
 - The site is now live at [localhost:4000](http://localhost:4000/webdocs)
