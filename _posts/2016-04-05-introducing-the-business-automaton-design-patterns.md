---
layout: post
cover: 'assets/images/cover5.jpg'
title: Introducing the Business Automation Design Patterns
date:   2016-04-05 15:04:00
tags: Business-Automation Design-Patterns BxMS
subclass: 'post tag-blogs tag-content'
categories: 'Justin'
navigation: True
---

Setting up a blog has been on my `TODO` list for several years. I've spent a lot of time over the last few years reading blogs from smart people like [Dan North](http://dannorth.net/blog/), [Martin Fowler](http://www.martinfowler.com/), [Cristian Posta](http://blog.christianposta.com/), [Jeff Patton](http://jpattonassociates.com/blog/), [Eric Schabell](http://www.schabell.org/), [Dean Leffingwell](http://www.scaledagileframework.com/author/deanleffingwell/) and [Maciej Swiderski](http://mswiderski.blogspot.com/) (just to name a few). But sharing my own ideas... Well that has only happened in small and sporadic bits, largely via [whitepapers](https://engage.redhat.com/forms/bdd?sc_cid=70160000000bqcVAAQ&offer_id=70160000000brtPAAQ) and [presentations](https://www.redhat.com/en/about/events/using-bpm-enable-devops-values-enterprise) for Red Hat. So after years of encouragement (thanks Haden), I've decided it's time to make this idea a reality.

### So Where To Start?

It turns out that the blogging platforms are going through a period of rapid innovation. The idea of a database driven, content management approach to blogging (a la WordPress) is being challenged by static site generators, which allow you to hack your blog together using your favorite text editor and a terminal. With a simple `git push`, your blog is now hosted on [GitHub Pages](https://pages.github.com/) for free. I travel a lot for work, so an offline workflow to write blogs just feels natural. Plus, I get to learn some new web tech along the way.

Also, worth noting here that there is a whole new family of social blogging platforms like [Medium](https://medium.com/), but I'll pass on yet another social media platform.

### Which Project To Choose?

If you choose a static site generator, [there are a lot of options](https://www.staticgen.com/). They are pretty much all open source and hosted on GitHub. I chose the most popular project out there, [Jekyll](https://jekyllrb.com/), for a few reasons:

- Markdown support. I really like writing in markdown.
- Hackable. This blog is a sublime project with ruby/html/css/js files and a few ruby gems.
- Large community with [lots of cool templates](http://jekyllthemes.org/)
- Fully offline workflow
- [Natively supported via GitHub Pages](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)

### Next Steps

A few other projects caught my eye, all powered via Node.js, which interests me more than a ruby platform:

- [Ghost](https://ghost.org/)
- [Gitbook](https://www.gitbook.com/)
- [Hexo](https://hexo.io/)

At the moment I'm using the [Jasper Jekyll template](https://github.com/biomadeira/jasper) which doesn't perfectly [integrate with GitHub pages](https://github.com/biomadeira/jasper#deployment) so I may explore other platforms or templates to smooth out the workflow. The beauty of a static site generator is that migrating the content is really just a matter of copying over the markdown files.

Oh, and start writing my ideas down more regularly.

photo credit: [Chambers Street Station](http://www.flickr.com/photos/50204706@N07/25509850966) via [photopin](http://photopin.com/) under [Creative Commons SA-2.0](https://creativecommons.org/licenses/by-sa/2.0/)