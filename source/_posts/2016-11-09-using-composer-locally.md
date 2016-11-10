---
layout: post
title: "Using composer for local development"
permalink: using-composer-locally
date: 2016-11-09 08:34:00
comments: true
description: "no more debug commits in newly created composer package."
keywords: ""
categories:

tags:

---

Creating microservices, packages and smaller libraries to speed up development seems to be normal business.
Some time ago, I created a short wrapper to utilize Redis-Cache inside an oxid eCommerce system.

So I was faced by a structure like:


    /path/to/code   
    └──application
    │    folder1
    │     folder2
    │     folder2
    │     composer.json
    │   
    └──packages
           └── redis-wrapper
                  src
                  tests
                  composer.json

The usual way, as far as I knew, until this moment, the best way to make this work, was following a few simple steps:
  *  create repository
  *  add, commit and push all files
  *  add repository to composer-Repository part
  *  composer install
 
But what happens if you need to change and fix the package itself? Of course, one way could be, to change line right inside the vendor folder.
By changing the code, you probably ran into the Problem or unknown area "What happens if I ran composer install/update again?".
I worried about this and don't want a bunch of "debug"-commits in my package repository, but after googling a bit, composer is quite a fantastic tool. You can also require local Packages without repositories:
Simply add those line to your composer.json and go on developing

{% highlight json %}
{
    "repositories": [
        {
            "type": "path",
            "url": "../../packages/my-package"
        }
    ],
    "require": {
        "my/package": "*"
    }
}
{% endhighlight %}

After finishing development, simply remove those line and add the new package as vcs Type, or add you satis mirror to enable "normal" composer workflow.

I like this way, and I'm glad to learn every day more and more about the things I love to use!
