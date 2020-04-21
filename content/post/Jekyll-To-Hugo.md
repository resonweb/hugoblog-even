---
title: "Jekyll to Hugo"
date: 2020-04-13T23:48:40+08:00
lastmod: 2020-04-13T23:48:40+08:00
draft: false
keywords: ["Hugo","Blog"]
description: "Manager my blog with hugo instead of jekyll"
tags: ["Blog","Hugo"]
categories: ["Computer"]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
reward: false
mathjax: true
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

Recently, I read the [zilongshanren's blog](https://www.zilongshanren.com/post/move-from-hexo-to-hugo/). He said the 
hugo native support the org file to generate the blog pages, and it is very fast and easy to install and debug.
So I just want to have a try.

After two days work, finally, I move my blog from jekyll to hugo. In the meantime, I found it was a wise decision
to use hugo.

<!--more-->

---
## Why abandon jekyll

At the beginning, I wrote my blog with [Hexo]({{< ref "/post/2017-11-28-The-First-Blog-Hexo.markdown" >}}).
But github use jekyll for the default backend. For the convenience, I changed the framework of my blog
to jekyll. With the more blogs I wrote, I found its so difficult to debug. Because of the confusing installation
and conceptions of jekyll, I didn't install jekyll in my computer. The blog git repository just contains 
origin markdown files and theme files. So, when I add or fix some contents, I must push the repository
to github and wait for the automatic deployment. It's so nauseating.

## Why use Hugo
As said above, the first reason impressed me is it can support org-mode natively.  
But the reasons really pleased me are the installation and workflow of hugo.  
### Installation
No matter what system you use, you can install hugo in a easy way. It's unlike with
jekyll or hexo needing other modules' supports, hugo is an indenpendent package.
You just need to install a single package "hugo", nothing more.
Then you can start your blogging.
### workflow
Before you start to deploy your work to remote server or just open the local server
service, you'd better to download a theme from https://themes.gohugo.io. I recommend
you a beautiful theme, that is the theme under your eyes.

Then you can deploy your work to the localhost first with command `hugo server --theme=even`.
Under this mode, you can edit your blog file, and the blog html page will be automatically generated
by hugo. At the same time, your web browser refresh dynamically. This is the mode I called it debug.
### The third reason
This reason comes with the even theme and many other special themes. That is the support of math typing.
Like this $$ E^2 = m^2 + p^2 $$
### Fast
As for this reason, I have no comment, Because I never used the other two platforms(Hexo, Jekyll) at local.
The speed of hugo is fast enough for me.

## How to start
I think the even-theme-author's [blog](https://blog.olowolo.com/post/hugo-quick-start/) will be a good
starting point. And you can preview the even theme within that blog.
