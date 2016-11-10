---
layout: post
title: "Start blogging with jekyll and travis"
permalink: blog/start-blogging-with-jekyll-and-travis
date: 2016-04-02 18:59:21
author: Thomas von Gostomski
comments: true
description: "Not as easy as described, some thing will run different."
keywords: ""
categories:

tags:

---

As I started to think about blogging, every solutions seems to be too big. After several days, I came over an article about jekyll and how easy it is to publish a small blog on github.  
So i decided to give it a try.

Many years ago I was not only a developer, I was a frontend-developer. So I don't want just a simple text-based blog UI. It needs to be, at least, a little cute. The start of a nearly endless story searching 
for the right theme, fitting UI, nice interactions. But overall... who really needs a fantastic webapplication, just to talk about some some ideas and thoughts ?
  
##### You are right... no one!

So I stepped back to my very beginnings in searching a theme and took one of the firsts I liked:

#### [end2end theme]

It looks quite nice and it come along with a pre-configured `.travis.yml` and a `deploy.sh`
This makes it quite easy to deploy the jekyll-based Blog to github, BUT only in a project scope.

So I ended up by a little tweak inside the deployment script:

{% highlight bash %}
#!/usr/bin/env bash
set -e # halt script on error

bundle exec jekyll build
# bundle exec travis-lint
# bundle exec htmlproof ${HTML_FOLDER} --disable-external

cd ${HTML_FOLDER}

# config
git config --global user.email "git-mail"
git config --global user.name "name"

# deploy
git init
git add --all
git commit -m "Deploy to GitHub Pages"
git push --force --quiet "https://${GH_TOKEN}@github.com/${GH_REF}" master
{% endhighlight %}

The original deploy script was build to push to gh-pages branch
{% highlight bash %}
git push --force --quiet "https://${GH_TOKEN}@github.com/${GH_REF}" master:gh-pages
{% endhighlight %}
what doesn't fit my needs. So next step was to do an automated deployment with any ci. why not take travis as ist was already configured.
A couple of clicks later, I were the proud owner of a new travis account. And OMG it is amazing easy to configure!

Deploying this theme needed a little change, for me, to get it working. Simply add the line `gem 'jekyll-sass-converter'` to go on error-free building.
{% highlight bash %}
# If you have OpenSSL installed, we recommend updating
# the following line to use "https"
source 'http://rubygems.org'
gem 'liquid'
gem 'redcarpet'
gem 'jekyll-sass-converter'
gem 'github-pages'
gem 'jekyll'
{% endhighlight %}
[end2end theme]: http://jekyllthemes.org/themes/end2end/