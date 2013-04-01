---
layout: post
title: "moderncv with GitHub and Linkedin logos"
date: 2013-03-31 23:48
comments: true
categories: [LaTeX, Customization]
---

The [moderncv][] $\rm \LaTeX$ package provides a documentclass for typesetting curriculum vitaes in various formats and styles. With few, very defined commands, you can make a highly professional CV.

Many examples and templates are available out there, as the [examples folder][ex_folder] on CTAN webpage. From there, it can be seen that some commands are used to define the user's personal information, such as the home address (`\address`), email (`\email`), and homepage (`\homepage`). However, in many cases, it is also important to point out other resources such as your [GitHub][] account and your [Linkedin][] page.

<!-- more -->

In order to add such information in `moderncv`, I made some modifications in the source code, and found the logos in this [tex.stackexchange][] thread. Now you can add your GitHub account and Linkedin page with `\github` and `\linkedin` commands from inside your `tex` file. The result should be something like this

![CV exampple](/files/posts/CV_en_example.png)

To use this commands you will have to download the modified files from this [GitHub repository][moderncv_repo], put them in a folder and compile in the usual way. Make sure your source `tex` file is within this folder. In that repository there are template files to get you started (source [here][tex_template] and pdf [here][pdf_template]).

You can download a zipped file with all you need from [here][zip], or you can clone it with `git`

``` bash
git clone git@github.com:fernandomayer/moderncv.git
```

For Brazilian users of `moderncv` I also made the `\lattes` command, so you can add the link for your full "[Currículo Lattes][lattes]" CV, with the [CNPq][] logo. This would look like this

![CV exampple](/files/posts/CV_pt-BR_example.png)

More technical details about these implementations can be found in the [GitHub repository][moderncv_README].

[moderncv]: http://www.ctan.org/tex-archive/macros/latex/contrib/moderncv/
[ex_folder]: http://www.ctan.org/tex-archive/macros/latex/contrib/moderncv/examples
[GitHub]: http://github.com
[Linkedin]: http://linkedin.com
[tex.stackexchange]: http://tex.stackexchange.com/questions/70216/adding-sections-such-as-linkedin-and-github-to-a-moderncv-footer
[moderncv_repo]: https://github.com/fernandomayer/moderncv
[tex_template]: https://github.com/fernandomayer/moderncv/blob/master/template_moderncv.tex
[pdf_template]: https://github.com/fernandomayer/moderncv/blob/master/template_moderncv.pdf
[zip]: https://github.com/fernandomayer/moderncv/archive/master.zip
[lattes]: http://lattes.cnpq.br/
[CNPq]: http://cnpq.br
[moderncv_README]: https://github.com/fernandomayer/moderncv#moderncv