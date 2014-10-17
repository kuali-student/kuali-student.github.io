---
layout: default
---


# Documentation Site

This documentation site is hosted [on github](https://github.com/kuali-student/kuali-student.github.io)

# Layout

Jekyll is used in by many for blogging.  Its defaults allow for blog posts to be created but this functionality at has been stripped out for our purposes.

Instead Git Flavour Markdown files can be created in subdirectories from the project root and linked to from the main index.md file.

# Install Jekyll

Follow the [installations instructions](http://jekyllrb.com).

Follow the instructions to align with the versions of ruby and jekyll that github is using: [https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll](https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll)

# File Pull Requests to make documentation changes

Changes to the site can be contribed through the Github pull request mechanism.

# Running the site locally

In one command window

{% highlight shell %}

$ git clone https://github.com/kuali-student/kuali-student.github.io

$ cd kuali-student.github.io

$ bundle install

$ bundle exec jekyll serve

{% endhighlight %}

Leave this running and it will pick up any changes you make as you make them available on the [localhost:4000](http://127.0.0.1:4000)


