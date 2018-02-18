---
title: "I Made a Blog"
date: 2018-02-17
draft: false
---
## Why?

I use open source software every day at work and I really want to learn more about it. In learning about new software or web services, I've learned a lot from other people's blogs and I'd like to pay it forward by using this blog to reflect on some of the things I've learned in trying to teach myself about open source.

Some context: I'm a librarian. I work in a research library where we use open source tools to publish digitized collections and original scholarship to the web. Most of my training and early experience revolved around teaching college students how to navigate very expensive, commercial databases to access scholarly and historical information.

Scholarly information is often walled behind a Kafkaesque entanglement of library catalogs, proxy servers, databases,  licensing restrictions, and messy user interfaces. It can be painfully frustrating to track down the full-text of a citation. This frustration motivated me to learn about [open access](https://en.wikipedia.org/wiki/Open_access), a foundational value for the work I now do in libraries.

Open access is similar to the values driving open source software development. People want to share their work online so that they can collaborate with others and advance their field. The internet and open licenses make both open access and open source possible.

I've been really excited about static site generators for the past few months. I've been using [Jekyll](https://jekyllrb.com/) for some work projects, and I really love it so far. For this blog, I chose to go with [Hugo](https://gohugo.io/) to get a little farther out of my comfort zone.

First impressions: Hugo is very fast. Hugo websites build in microseconds, whereas Jekyll sites build in seconds, maybe longer for really big sites. It's not that disruptive for me but if you're working quickly through a bunch of changes, it can be annoying to wait for the site rebuild on `localhost`, but with Hugo it's basically instantaneous. Another nice feature is that Hugo doesn't require you to restart your server when you update the `config` but Jekyll does. This _probably_ shouldn't matter much since `config` files shouldn't be changed that often, but it's another nice difference I've noticed. I still **love** Jekyll and will continue to use it for work projects, but I'm also really liking Hugo.

## How

I'm always interested in hearing about how people set up their development environment, so here's mine:

- Operating System: Windows 10
- Command Terminal: PowerShell
- Text Editor: [Atom](https://atom.io/)
- Git GUI: [GitHub Desktop](https://desktop.github.com/)
- Package Manager: [Chocolatey](https://chocolatey.org/)

Once I get better at this stuff, I hope to use the command line more and rely less on a Git GUI, though I've heard [Sourcetree](https://www.sourcetreeapp.com/) is really good for projects with several contributors.

### Installing Hugo

If you're on Windows 10, install Hugo with Chocolatey. **Do not use the Ubuntu Linux Subsystem to install Hugo on a Windows 10 computer.** I use the Linux subsystem, [Bash on Ubuntu on Windows](https://docs.microsoft.com/en-us/windows/wsl/about), for my work with Jekyll because [the Jekyll docs tell me to](https://jekyllrb.com/docs/windows/). I just kind of assumed most open source development work **had** to be on Linux or Mac OS, so my first attempt at installing Hugo was to use the subsystem; but, for whatever reason, the `sudo apt-get install hugo` command on Bash downloads a deprecated version of Hugo, which won't work with most free hosting providers or Hugo themes. The [Hugo binary install packages on GitHub](https://github.com/gohugoio/hugo/releases) with [these instructions](https://gohugo.io/getting-started/installing/#for-windows-10-users) work just fine. I also found this step-by-step [video tutorial](https://youtu.be/G7umPCU-8xc) very helpful.   

### Using a Theme

A nice thing about Hugo is the number of [themes](https://themes.gohugo.io) available to use. I was looking for something simple with an emphasis on text over images. I was drawn to [Minimal](https://themes.gohugo.io/minimal/) primarily because I like the splash page, the lightness of the typography, and the navigation bar. Each of these themes has installation instructions, which is simple to do if you use the `git submodule` command.

Once you've got a theme chosen and installed, the most important files are the `config.toml` file and the `content` folder. Edit the `config.toml` file in a text editor with your information and use `content` folder for all your pages and posts. No other files are really needed to have a working blog, but each theme should have documentation to help you make customizations. Really good themes have comments in the code to help guide your customizations. I found it super helpful to use the theme's `exampleSite` for figuring out how the files work together.   

Here's the basic structure for a Hugo site (a more in-depth dive into the structure of a Hugo site is [available here](https://youtu.be/sB0HLHjgQ7E)):

```
├───archetypes
├───content
│   └───posts
├───data
├───layouts
│   └───partials
├───static
│   └───css
└───themes
    └───minimal
        ├───archetypes
        ├───exampleSite
        │   └───content
        │       ├───post
        │       └───project
        ├───images
        └───layouts
            ├───partials
            └───_default
config.toml
```
When you build the site, a new folder will be created called `public`, and this will serve as the publish directory you'll need for hosting the rendered website.

### Hosting: Github Pages vs. Netflify

I've tested [GitHub Pages](https://pages.github.com/) before, and it's super easy to use if you like Jekyll, but I couldn't get it to work that well with Hugo. I know [it's possible](https://gohugo.io/hosting-and-deployment/hosting-on-github/), but I couldn't get this website's CSS to render correctly.

I later learned that this was probably an error I caused by having the wrong `baseURL` in `config.toml` but I can't remember for sure if that was the issue. Hugo on Github Pages also requires you to have two repositories for one website: a repository for the source code and another for the rendered HTML. Again, if I were better at Git and knew how to write a shell script, I could probably make it work, but I failed this time. It's too bad though, because I really wanted a `chrisdaaz.github.io` domain. Oh well.

I heard about Netlify from the [Changelog](https://changelog.com/podcast) podcast, a really good and accessible interview podcast about open source. I'm also a fan of Netlify's [JAMstack Radio](https://www.heavybit.com/library/podcasts/jamstack-radio/) podcast, which focuses on web apps using a JavaScript, API's, and Markup architecture, like static site generators.

Hosting a personal, static site on [Netlify](https://www.netlify.com) is free and very easy. You can log in with your GitHub account, point Netlify to a GitHub repository, and Netlify will deploy your site to a `netlify.com` subdomain. Every time you push a commit to your GitHub repository, that will automatically trigger a new build of your site, making your updates live within a few seconds.

I _did_ run into one hiccup when specifying the build settings. I used `hugo` as the build command, because that's the command I use to build the site locally. This won't work on Netlify because they only support certain versions of Hugo, and you will need to specify the Hugo version in the build command. Here are Netlify build settings that worked for this blog:

- Repository: `https://github.com/chrisdaaz/chrisdaaz`
- Build command: `hugo_0.19`
- Publish Directory: `Public`
- Production Branch: `master`

It is nice when computer stuff works.
