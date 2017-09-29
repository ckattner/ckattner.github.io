---
title: Setting up a GitHub Pages Blog
layout: post
published: true
tags: github markdown jekyll blog
---

For a while now I've been feeling like I needed to be writing more.  Firstly, it's just satisfying to stretch some new muscles (or the ones that haven't been used since college).  Second, writing things down is a good way to "remember" things you've learned, and lastly, I think I've been delinquent in learning Git and taking advantage of GitHub - I joined GitHub in 2012, but my first commit was when I started playing around with using it as a blogging host.

There are numerous tools which can be used for generating static pages suitable for hosting on GitHub.  You can find an extensive list of static site generators over on [staticgen](https://www.staticgen.com/).  You can choose a generator written in myriad languages, supporting myriad templating languages.  Want to generate a site with Bash?  Go for it.  Are you the biggest Groovy fan in the world?  You can do that too.  Heck, you could just pretend it's 1995 again and write a bunch of static HTML pages.

All that said, I went for the easy solution since I'm not so much interested in learning a bunch of ins and outs to a blogging tool as learning some more portable skills such as Git.  Fortunately GitHub offers a very low impedance solution: [Github Pages](https://pages.github.com/).  GitHub Pages uses [Jekyll](https://jekyllrb.com/) so I'm also going to use that as my tool of choice.

## First Things First
If you don't already have one, create yourself a GitHub account.  From there the simplest path forward is to simply clone an existing repository.  You can join the legions of others who have created a GitHub Pages site by forking the [jekyll-now](https://github.com/barryclark/jekyll-now) repository.  In the upper right corner of the page you'll see a Fork button.  Hit it and in a few seconds you'll have yourself a fork of the jekyll-now repository.

Once the cloning is finished hit the Settings link in the tab bar along the top.  On the Options page which comes up you'll see an input for Repository Name.  GitHub Pages requires the repository to be named \<username>.github.io.  In my case that means the repo will be named [ckattner.github.io](https://github.com/ckattner/ckattner.github.io).

Congratulations, you now have a blog live at [http://\<username>github.io](http://ckattner.github.io/)!  (Note that while this link points to github.io (go head, mouse over and look at your status bar), it's gonna bounce you to the canonical host I've chosen instead, which is [blog.kattner.us](http://blog.kattner.us/).)

## Now What?
You probably want to set up a few customizations.  Jekyll configuration is done through the `_config.yml` file, so find it in the list, click on it, and hit the pencil icon on the right side of the content window to put the file into edit mode.  I suggest the following settings off the bat:
1. Set `name` to your name
2. Add a new setting named `future` with value `false`.  When this is set to 'false' you can create posts with a future date and they _won't_ be published until that date.
3. Find the `footer-links` section and put in values to any you think relevant.
4. In `url` you can either put `\<username>.github.io` if you're not going to be using a custom URL, or the URL you plan on using if you will be using a custom URL.

## You're a Blogger Now
Once you’re done configuring things you can navigate to the `\_posts` directory.  This is where all the blog posts you'll write will be stored.  The files are named in a `YYYY-M-D-Words-In-Url.md` format, so if you have a file named `2017-9-9-My-First-Post.md` then the post will be generated at address `/My-First-Post` (e.g. _without_ the date or the .md extension).

Posts are written in Markdown, hence the `.md` file extension.  There are a million Markdown references out there, but I like the [WordPress](https://en.support.wordpress.com/markdown-quick-reference/) one.

Go ahead and create a new file using the convention above, then edit it.  You should start the file like so:
```
---
layout: post
title: <Your page title>
---
```

The triple dash lines `---` denote the start and end of the so-called front matter.  The `layout` line tells Jekyll to render the contents using the post layout, while the `title` provides the page title.  You write your page contents below the second dashed line.

Once you save a file GitHub Pages will regenerate your site usually within a few seconds.

## A Place to Call Home
So you've got your blog setup and you've written your first post, but you're not satisfied with your hostname.  You can customize the hostname for your site, but there is a slight downside: as it stands today, when hosting under the GitHub provided address you can also access the site using HTTPS.  If you switch to a custom hostname, then you won't be able to provide SSL protection to your visitors.  (It is possible to use a Cloudflare service to provide SSL for a custom named site, but that is beyond the scope of this article.)
