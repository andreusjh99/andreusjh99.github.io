---
layout: post
title:  Welcome to Jekyll!
read: 5
post-image: /assets/images/posts/1_jekyll/post.jpg
description: Friendly introduction to Jekyll and how to get started
categories: software development
---

---

![](/assets/images/posts/1_jekyll/post.jpg)

**Jekyll** is a **static site generator**. A static site generator generates a full static HTML website based on raw data and templates. In Jekyll, data is written in **markup**, and templates are known as **layouts**.

## Getting Started

### Installation

The main requirements of Jekyll is <a href="https://www.ruby-lang.org/en/downloads/" target="_blank">**Ruby**</a> (a programming language). Jekyll is written in Ruby and hence you will need Ruby to build Jekyll locally.

For a full guide to install Jekyll and its requirements, you may refer to its official <a href="https://jekyllrb.com/docs/installation/" target="_blank">documentation</a>. In the documentation you will find platform-based instructions, for eg. <a href="https://jekyllrb.com/docs/installation/windows/" target="_blank">Windows</a>, <a href="https://jekyllrb.com/docs/installation/macos/" target="_blank">macOS</a> etc.

Jekyll is a **Ruby gem** - think of a gem as equivalent to a library in Java, or a module in Python. 

In the documentation, you will also be instructed to install bundler. **Bundler** is a Ruby gem that installs all gems required in your project.

Once installed, remember to check your installation by running

    $ jekyll --version
    $ bundler --version
    $ ruby --version

### Create a new project
To create a new project for your website, go to the directory where you would like to keep your project files and run the following command in the command prompt or terminal:

    $ jekyll new .

This will create the necessary website files in the directory you ran this command. You will see the following:

    Running bundle install in <your directory>...
      Bundler: Fetching gem metadata from https:rubygems.org/............
      Bundler: Resolving dependencies...
      Bundler: Using public_suffix 5.0.3
      Bundler: Using addressable 2.8.5
      Bundler: Using bundler 2.2.27
      ...

This is running bundler to install the required gems. When this is done, you will know that it has finished initialising a project when you see:

    New jekyll site installed in <your directory>

To build and run the project locally, run this command:

    $ bundle exec jekyll serve

This command will build your website and host it locally. You can then access your local website on your browser with http://localhost:4000/.

## Directory Layout

<div class="float-lg-start">
<figure>
<img src="/assets/images/posts/1_jekyll/files.jpg" alt="files in initial project">
<figcaption>Folder structure of an initial Jekyll project</figcaption>
</figure>
</div>

The image shows the files created in an initial Jekyll project. `_posts` is a folder that contains all the posts of your website. We will talk more about adding a new blog post [below](#addblogpost).

If you built your project locally, you will also see a `_site` folder. This folder is created during the build process and contains the actual website files served. Think of it as equivalent to the `target` folder for Java Maven projects.

- `_config.yml` is a config file which specifies settings for your website.
- `404.html` is the default error page for 404 not found error.
- `Gemfile` is a file specifying the list of gems used by your site. You can modify this file to add or remove gems.
- `Gemfile.lock` is where Bundler records the exact versions of the gems that were installed. You should not change this file.

### Other folders

There are other folders that you may create to include additional functionalities.

You may create templates for your posts, for eg. templates for your headers and footers. These templates are called <a href="https://jekyllrb.com/docs/layouts/" target="_blank">**layouts**</a> in Jekyll, and they are stored in the `_layouts` directory.

Apart from templates, you may also create components, or <a href="https://jekyllrb.com/docs/includes/" target="_blank">**includes**</a>, that you want to include into multiple pages, for instance an icon or the google analytics tag. You can create an `_includes` folder and store your components in there.

## Adding a new blog post {#addblogpost}

Post files are kept in the `_posts` directory.

Jekyll requires blog post files to be named according to the following format: `YEAR-MONTH-DAY-title.MARKUP`, where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file.

A useful format to write posts in is the markdown format as it is simple and easy to read. For markdown, the file extension will then be `.md`.

For instance, the file name of this post is <a href="https://github.com/andreusjh99/andreusjh99.github.io/blob/main/_posts/2021-09-07-welcome-to-jekyll.md" target="_blank">`2021-09-07-welcome-to-jekyll.md`</a>.

To allow Jekyll to process the file, you need to include a front matter as the first thing in the file. The front matter must take the form of a valid YAML set between triple-dashed lines. An example:

{% highlight yaml %}
---
layout: post
title:  Welcome to Jekyll!
---

This is the first sentence of your post...
{% endhighlight %}

### Markdown

With **markdown**, it is simple to include code snippets or mathematical equations in your post.

Jekyll has built in support for syntax highlighting for code snippets. Its default syntax highlighter is <a href="https://github.com/rouge-ruby/rouge" target="_blank">**Rouge**</a>. You can learn more about it <a href="https://jekyllrb.com/docs/liquid/tags/#code-snippet-highlighting" target="_blank">here</a>. The list of languages it supports can be found in the <a href="https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers" target="_blank">Rogue wiki</a>.

To use **LaTeX** math formatting in your posts, you may use <a href="https://www.mathjax.org/" target="_blank">**MathJax**</a>, which is a JavaScript display engine for mathematics. To use MathJax, simply include the following code snippet in your post file after the front matter.

{% highlight html %}
<script
  type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML"
></script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
  tex2jax: {
  inlineMath: [['$','$'], ['\\(','\\)']],
  displayMath: [['\[', '\]'], ['\\[', '\\]']],
  processEscapes: true},
  jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
  extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
  TeX: {
  extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
  equationNumbers: {
  autoNumber: "AMS"
  }
  }
  });
</script>
{% endhighlight %}

Once included, you may use LaTeX code to write Math. The end result looks like this:

<div class="math">
\begin{align} 
    \text{P}(y_t = a|\mathbf{x}_{1:t}) &= \text{P}(y_t = a|\mathbf{h}_{t}) \label{eq: RNN 1}\\ 
    &= \text{softmax}(\mathbf{W}_{hy} \mathbf{h}_t + \mathbf{b}_{hy})_a \label{eq: RNN 2}
\end{align}
</div>

## Conclusion

**Jekyll** is an easy-to-use static site generator for anyone interested to get started with their own website. It is straight-forward to get started and has many useful features. Most importantly, it is hassle-free to add a new blog post. 

This blog site is built using Jekyll.