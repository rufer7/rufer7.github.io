blog
====

This is my personal blog based on GitHub Pages. Here I publish blog posts about different topics concerning computer science.

[visit](http://rufer7.github.io/)


[Information about GitHub Pages](https://help.github.com/categories/github-pages-basics/)


License
===
The following directories and their contents are Copyright Marc Rufer. You may not reuse anything therein without my permission:

* _posts/
* images/

All other directories and files are MIT Licensed. Feel free to use the HTML and CSS as you please.


Local Jenkyll setup
===

Follow this [guide](https://help.github.com/articles/using-jekyll-with-pages/)

### Run configuration in IntelliJ

Install the following IntelliJ plugins

* Batch Scripts Support

Create new run configuration of type `Batch` with the following settings

    Name:               Serve blog
    Script:             ${PROJECT_ROOT}/jekyll_serve.bat
    Working directory:  ${PROJECT_ROOT}


If you execute this run configuration you can then access the blog over `localhost:4000`