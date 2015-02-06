Blog
===
[![Build Status](https://travis-ci.org/rufer7/rufer7.github.io.svg?branch=master)](https://travis-ci.org/rufer7/rufer7.github.io) <a href="https://github.com/rufer7/rufer7.github.io/releases"><img src="https://img.shields.io/github/release/rufer7/rufer7.github.io.svg" alt="Latest Version"></img></a>

This is my personal blog hosted by GitHub Pages. Here I publish blog posts about different topics concerning computer science. Furthermore I will use it as a knowledge base.

[visit Blog](http://rufer7.github.io/)


[Information about GitHub Pages](https://help.github.com/categories/github-pages-basics/)


License
===

The following directories and their contents are Copyright Marc Rufer. You may not reuse anything therein without my permission:

* _posts/

All other directories and files are MIT Licensed. Feel free to use the HTML and CSS as you please.


Local Jenkyll setup
===

Follow this [guide](https://help.github.com/articles/using-jekyll-with-pages/)

If ruby is not working on Windows becuase of an ssl connection error try [this](https://gist.github.com/luislavena/f064211759ee0f806c88)

### Run configuration in IntelliJ

Presupposed plugins
* Batch Scripts Support Plugin

Create new run configuration of type `Batch` with the following settings

    Name:               Serve blog
    Script:             ${PROJECT_ROOT}/jekyll_serve.bat
    Working directory:  ${PROJECT_ROOT}


If you execute this run configuration you can then access the blog over `localhost:4000`
