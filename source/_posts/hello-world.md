---
title: Hello World
date: 2018-05-12 14:15:55
categories:
- Tutorial
tags:
- Hexo
- Meta-Post
- Markdown
---
Hello, er, not world, it's you! Welcome to Alesiong's blog. In this blog, I will mainly post about anything related to computer science, including technical tutorials, code snippets, some ideas and thoughts, and maybe some maths (if I'm feeling good :P).

This first post is about how did I set up this blog (you can call this post a *meta-post*). I will guide you to build up from scratch your blog by [Hexo][hexo] and [GitHub Pages][gh-pages].

## Hexo

My blog is built with Hexo, a easy to use blog framework. As a developer, you may think it cool to build your blog with primitive HTML and CSS; but I think it would be cooler if you use that time to share your broad knowledge. Hexo is just the framework that let you focus on writing and does the tedious things for you. With hexo, the only things you need to know is

    1. Markdown
    2. Knowing how to execute command in command line is better.


### Markdown
Of course, I would not assume that you know Markdown (if you know, skip this section). So I would get you know it in a few minutes (along with how easy is Markdown !).

Markdown is a *markup* language that is designed to let your files look good even if you are using plaintext editors. Markdown files are usually ended with extension `.md`, you can use any text editor you like to open it, and I will recommend some later. Then you can write anything you like in it, with only a few notice:

1. **Bold** and *Italic*

    You can use `**Bold**` or `__Bold__` to make text **bold**. And similarly `*italic*` or `_italic` to make text *italic*.
2. Paragraph

    Maybe annoying, but you have to use a blank line to represent a new paragraph, like this:
    ```
    Paragraph 1
    Still paragraph 1

    Paragraph 2
    ```
3. Hyperlinks and images

    Hyperlinks are like this `[Example](http://example.com)`, which is rendered as [Example](http://example.com).

    Images are like this `![Beautiful Image](path/to/your/image)`.

For more details about Markdown syntax, I would recommend this [cheatsheet][md-cheatsheet].

#### Editors

Many popular text editors have built in markdown support(including syntax highlight and preview), like [Atom][atom] and [Visual Studio Code][vscode]. And if you are used to the WYSIWYG fashion, you can use [Typora][typora].

### Going on with Hexo

Let's back to Hexo. To start with, you will need to first install `Git` and `Node.js`. Actually the official documentation of Hexo provides a [brief guide][hexo-docs]. And I will assume you have installed the two softwares.

Now open your terminal (cmd.exe or powershell.exe on windows, Terminal.app on macOS)[^1], and follow up[^2].

### Install Hexo

```bash
npm install -g hexo-cli
```

### Open your blog and writing

```bash
hexo init awesome-blog-name
cd awesome-blog-name
npm install
```
This will get your blogs ready with all the dependencies, now

Create a new post
``` bash
hexo new "My New Post"
```
The new post is in the `source/_posts/` folder. You can use your favorite (Markdown) editor to edit it.

When you finish writing
``` bash
npm install hexo-server --save
hexo server
```
Then open <http://localhost:4000/> to see your blog.

Looks good, right? But now only you can see the blog, let's **deploy** the blog to the internet so that you can share your ideas with others.

## Deploy (with Github Pages)

You can deploy your Hexo blog to many web services. I recommend [Github Pages][gh-pages] here because
1. It's free
2. Hexo supports it with a plugin
3. You can even bind your custom domain to it

### Github

To use Github Pages, of course you need to have a Github account. Then you can create a repository to hold your Github Pages contents. I recommend you to name your repository as `<your username>.github.io`.

### Install plugins

Hexo provide Github Pages deployment by plugins, so
```bash
npm install hexo-deployer-git --save
```

### Edit config

Edit the `_config.yml` file and modify/add the `deploy` section like this:
```yaml
deploy:
  type: git
  repo: https://github.com/your-username/your-repo-name.git
  branch: master
```

### Ready to go

``` bash
hexo generate
hexo deploy
```
Now go to <https://your-username.github.io/your-repo-name> to see your blog (it's <https://your-username.github.io> if you name your repo as I recommended).

## Custom domain

> If you think the default url is good for you, just skip this section.

It's very easy to link a custom domain to the Github Pages. The only thing you need to do is to have a domain. You can by one or get a free one from [Freenom][freenom].

1. Create a file named `CNAME` under `source/` folder, and paste your custom domain (along with host name, e.g. `www`) into that file.
2. In the DNS settings of your domain provider, add a `CNAME` record with name `www` (or others) with target `<your username>.github.io`.

Now wait a few minutes and your blog will be up on the new domain. If you think HTTPS is important, tick `Enforce HTTPS` in the github repo settings, and github(actually let's encrypt) will issue a certificate for you !

## Afterwards

### Set the url

Now you should have your url to your blog, let's put it into `_config.yml`: modify or add the `url` entry:
```yaml
url: url-to-your-blog
```
Hexo uses **absolute path** to link inside your blog, so you have to set this correct for links in the blog to work.

### Change the theme

You can find many beautiful themes [here][hexo-theme]. When you decide to use one, go to see its github readme, and it should guide you to install and use the theme. Actually, almost every theme has a similar installing process:

1. Install npm packages if needed (readme should tell you).
2. Clone the theme's repo into `themes/` folder:
    ```
    git clone url-of-theme-repo themes/theme-name
    ```
3. Change the `_config.yml`
    ```yml
    theme: theme-name
    ```
    and add other settings related to the theme.
4. Regenerate or restart the server.

### Use git to manage your blog

When you generate a new hexo blog, it is also a git repository with proper `.gitignore` file. So you can just commit your changes and (if you want) push the repo to github or bitbucket or others. Note that if you added a custom theme, it would be better to manage it as a git submodule:
```bash
git submodule add url-of-theme-repo themes/theme-name
```

[^1]: Linux users: I don't think you cannot find your terminal :)
[^2]: I don't add $ before the command, so it is easier to copy.

[gh-pages]: https://github.io
[hexo]: https://hexo.io/
[md-cheatsheet]: https://www.markdownguide.org/cheat-sheet
[atom]: https://atom.io/
[vscode]: https://code.visualstudio.com/
[typora]: https://typora.io
[hexo-docs]: https://hexo.io/docs/index.html#Install-Git
[freenom]: https://freenom.com
[hexo-theme]: https://hexo.io/themes/index.html
