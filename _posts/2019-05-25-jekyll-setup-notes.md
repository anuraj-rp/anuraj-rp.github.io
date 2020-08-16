---
title: "Jekyll setup with minimal mistakes theme - Part 1"
date: 2019-05-25
author_profile: true
categories:
  - Notes
tags:
  - technotes
---

[Minimal Mistakes][MinimalMistakes] theme is one of the good jekyll themes for a simple homepage.

I settled on it after a long search for simple theme for my webpage. My current setup is not using the remote jekyll theme. I downloaded a version of the theme and modified it to use it with github pages. I will at some point use the remote theme and host it using something like Netlify. 

I used the following steps to setup the website as it looks now with the splash page as landing page. This method might not work if using remote themes. So the theme will not get updates automatically. With my limited understanding of jekyll, html and css here is how I got it working. I am assuming ruby, Jekyll, bundler and all gems required for the Jekyll website are setup already. 

First of all, download or clone the theme from this link: [Minimal Mistakes][MinimalMistakes]. This [page][MMConfig] provides a good description of the configuration for the the theme.

- *_config.yml* is the yaml file configuration file where a lot of the setup goes. 
- *index.html* is the file that decides the landing page
- The navigation links at the top of the page are set in *_data/navigation.yml*

__Site navigation links at the top of the page__

By default, the only link at the top of the page is the Quick-Start Guide link. Edit *_data/navigation.yml* and uncomment the title and url lines to get more navigation links. The url can be site internal or external. 

__Changing landing page from recent posts to splash page__

The *index.html* file in the root directory has the following contents:
```
---
layout: home
author_profile: true
---
```
Edit *index.html* so that it looks like this:
```
---
layout: splash
permalink: /home/
---
```
Now create a file called home.md in *_pages* directory. Copy the the contents of file *home.md* from the directory *docs/_pages/* to *siteroot/_pages/* directory. Change the permalink in the file to point to the site root.

```
---
layout: splash
permalink: /
pagination: false
...
...
```
Now build the jekyll and serve the jekyll site and view locally.

```
bundle exec jekyll serve
```

Open a browser and go to *http://localhost:4000* to view your freshly made minimal static site with jekyll. I will write the steps to host this on github in Part-2.

[MinimalMistakes]: https://github.com/mmistakes/minimal-mistakes 
[MMConfig]:https://mmistakes.github.io/minimal-mistakes/docs/configuration/ 
