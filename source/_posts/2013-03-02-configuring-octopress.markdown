---
layout: post
title: "Configuring Octopress"
date: 2013-03-02 01:45
comments: true
categories: [Basics, Octopress, Jekyll]
---

As you may have noted, this site is built upon [Octopress][]. As its website points out, Octopress

> is a framework designed by Brandon Mathis for Jekyll, the blog aware static site generator powering Github Pages.

[GitHub][] has a very nice feature, that let you build and host your website (for free!). The engine behind this is [Jekyll][], which is "*a simple, blog aware, static site generator*". This means that if you push the right files into a GitHub repository, you'll get your site and/or blog readly available to the world. However, Octopress continues

> To start blogging with Jekyll, you have to write your own HTML templates, CSS, Javascripts and set up your configuration. But with Octopress all of that is already taken care of. Simply clone or fork Octopress, install dependencies and the theme, and you’re set.

And that's true. If you want a pure Jekyll website you may have to write everything from scratch, or fork someone else's files. Unless you are a  HTML/CSS programmer, this may be a very long road. I tell this from my own experience. I've tried Jekyll for building this website, and I've got it. But it was taking me too much time to configure things the way I wanted. So I gave Octopress a try and here we are.

<!-- more -->

Jekyll is a fantastic engine, and Octopress made it more fantastic, configuring the basics, and letting you matter with more important things --- like blogging. However, Octopress also has its own peculiarities, some of them not really very clear to find out, specially if you are not very familiar with Ruby (the language it uses to build and generate pages), like me.

Obviously, Octopress may have some disadvantages. The most clear to me are: (1) as anything that is a little bit automated, you may lack some learning from it (this is very important for the geeks out there), and (2) you will be just one out of thousands (?) with the same site (blog) layout. But, you may also turn this disadvantages on your favor. As you own the source code, you can learn from it and find out how to configure and modify the default theme the way you want. That's up to you to decide what's the best thing to use. For example, a very nice discussion (and introduction to Jekyll) was written by [Carl Boettiger][carl] in this [blog post][carlpost].

Below I'll show the steps I made to put this site up and running. Obviously I followed the steps in the [Octopress setup page][1], but some things are not really obvious, so I'll put them here.

## 0. Install git (and learn how to use it)

First thing is to have some familiarity with [git][], or else we're going nowhere. To install git in Linux, use your package manager, as for example in Ubuntu

``` bash
sudo apt-get install git git-core git-man git-gui git-doc 
```
You may also need `ssh`, `openssh-server`, `openssh-client`, depending on your system. Then configure your [GitHub account][githelp] (if you still didn't).

If you are not very familiar with git, read the [documentation][gitdoc], and learn by doing with [try-git][] at [codeschool][]. It is a very good idea to focus on [git-branching][], since we'll use branches hereafter.

## 1. Install Ruby

Octopress requires [Ruby][] 1.9.3 to run. You can install it with your default package manager (*e.g.* apt, pacman), or with RVM, the Ruby Version Manager.

### 1.1 Install Ruby from a package manager

In Ubuntu $\geq$ 12.04 specifically, there is a package called `ruby1.9.1`, which, despite the name, installs Ruby 1.9.3. Also, there is a package (actually, a metapackage) called `ruby1.9.3`, which is just a symbolic link to install `ruby1.9.1`. As you will need the `-dev` (and others) files too, the best way is to install `ruby1.9.1-full`, in the usual manner:

``` bash
sudo apt-get install ruby1.9.1-full
```

### 1.2 Install Ruby from RVM

To install Ruby with RVM, first we need to install RVM itself. (You will need `curl` installed).

``` bash
curl -L https://get.rvm.io | bash -s stable --ruby
```

<!-- Precisa ver o detalhe do .bashrc aqui -->

And follow the instructions thereafter. Then install Ruby 1.9.3, and make it in use with

``` bash
rvm install 1.9.3
rvm use 1.9.3
```

After that you will need to install [RubyGems][], a package manager used to install Ruby contributed libraries (called gems). It works in a similar way as apt or pacman does for your Linux system. To install its latest version

``` bash
rvm rubygems latest 
```

> NOTE: if you installed via, *e.g.*, apt, rubygems is already there.

## 2. Set up Octopress

After installing Ruby you have to get the basic structure of Octopress from its repository on GitHub. You do this by cloning the repository with

``` bash
git clone git://github.com/imathis/octopress.git octopress
```

This will create a directory called `octopress`, then you `cd` to it and install the dependencies needed with [Bundler][]

``` bash
cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
sudo gem install bundler
sudo bundle install
``` 

What Bundler do is to follow the instructions contained in the files `Gemfile` and `Gemfile.lock`, and install all the gems (the dependencies here) specified there.

Now install tha default Octopress theme by using `rake`

``` bash
rake install
```

[Rake][] is a program similar to the [GNU Make][], but for Ruby. It build things from a `Rakefile`, in the same way that `make` build things from a `makefile`. It's important to be familiar with this concept, since we'll use `rake` tasks for many things in Octopress from now on.

## 3. Publish from GitHub

So far you've just built your Octopress site locally. To publish it from GitHub you have to create a new repository with your username followed by the GitHub domain. For example, my username is `fernandomayer`, so I've created a repository named `fernandomayer.github.com`. GitHub intelligently understands that the contents of this repository should be a website (any other names won't do it), and it will make it available at `http://fernandomayer.github.com`. (You can use [custom domains][2] though).

To finally setup your website to work with GitHub, use this `rake` task

``` bash
rake setup_github_pages
```

and follow the instructions. In summary this will configure everything you need:

* create a `source` branch in which you'll work with the source files for your site
* create a `master` branch inside `_deploy/` directory

**This is very important**: GitHub will publish your site with the contents that are available in the `master` branch **only**. That means that everything under `_deploy/` will be used. All other files, that are in the `source` branch will be used as **working** files, *i.e.*, you will create, write and modify everything in the `source` branch (particularly at the `source/` directory), then Octopress will generate and deploy it to `_deploy/`. This is done with this two `rake` tasks:

``` bash
rake generate
rake deploy
```

This will generate the appropriate files, copy them to `_deploy/` and `add`, `commit` and `push` to its `master` branch (automatically!). So, to keep record of your changes in git you will also have to add-commit-push to the `source` branch

``` bash
git add .
git commit -m 'message'
git push origin source
```
At this point, you'll want to see your website (still with no modifications) at the default adress, e.g., `http://fernandomayer.github.com`. But, as you make changes (shown below), you'll want to see these changes instantly, right? You don't need to make all this process of generating, deploying, $\ldots$, every time you make a minor change. For that you can use this rake task


``` bash
rake preview
```
and then type `localhost:4000` in your browser. This will show your changes locally, before publishing everything, and instantly. To really publish that you'll need always to generate and deploy, and then add-commit-push to `source`, as in this worklow:

``` bash
# modify some files
rake generate
rake deploy
# now keep track of them at source
git add .
git commit -m 'message'
git push origin source
```
## 4. Configure your site

Before anything else, you need to do some basic configuration on your Octoptess site, like change its name, author, $\ldots$. These basic configurations are controled by one only file: `source/_config.yml`. There you will find many things to change and/or to keep as they are. The comments in it makes it easy to know what to do.

Some more settings can be changed, and the definitive reference for that is the [Octopress configuration page][octo-config].

For more options of theming & customization, see the [Octopress template page][octo-template].

## 5. New pages and new posts

To make a new page, you can use the rake task

``` bash
rake new_page[name]
```
This wil create a folder with an index file, e.g., `name/index.markdown`. To make it appear at the navigation bar of your site you'll have to edit `/source/_includes/custom/navigation.html` file.

To make a new blog post, you'll use
``` bash
rake new_post["post title here"]
```
(note the quotes here). At this point, it's important to read Octopress documentation about [Blogging Basics][BB]. As it is well documented I will not repeat it here.

## 6. Managing Octopress

After some time, you may want to make some changes or make a new post on your Octopress site, but from another computer. This may happen even if you, e.g., format your hard-drive or lose your backup, $\ldots$.

To keep blogging with your configured site from another place, just clone it to where you are now. For example, I would clone

``` bash
git clone git@github.com:fernandomayer/fernandomayer.github.com.git
```

This way you will have everything you need again to go on with your site the way you made it. The only detail here is that, after cloning, you will be at the `master` branch, not the `source` branch where you need to be. To see this, enter in the directory and type

``` bash
git branch
# or
git branch -a
```

To go back to your original environment where all your working files are, just switch to the `source` branch with

``` bash
git checkout source
```
and see the change with
``` bash
git branch
```

With these basic instructions, I hope you can use and manage your own Octopress site. Suggestions and other updates may be added here for future reference.


[Octopress]: http://octopress.org
[GitHub]: http://github.com
[Jekyll]: https://github.com/mojombo/jekyll
[Ruby]: http://www.ruby-lang.org/en/
[RubyGems]: http://rubygems.org/
[Bundler]: http://gembundler.com/
[Rake]: http://rake.rubyforge.org/
[GNU Make]: http://www.gnu.org/software/make/
[1]: http://octopress.org/docs/setup/
[2]: http://octopress.org/docs/deploying/github/#custom_domains
[carl]: http://www.carlboettiger.info
[carlpost]: http://www.carlboettiger.info/2012/12/30/learning-jekyll.html
[BB]: http://octopress.org/docs/blogging/
[git]: http://git-scm.com/
[githelp]: https://help.github.com/articles/set-up-git
[gitdoc]: http://git-scm.com/documentation
[try-git]: http://www.codeschool.com/courses/try-git
[codeschool]: http://www.codeschool.com
[git-branching]: http://git-scm.com/book/en/Git-Branching
[octo-config]: http://octopress.org/docs/configuring/
[octo-template]: http://octopress.org/docs/theme/template/