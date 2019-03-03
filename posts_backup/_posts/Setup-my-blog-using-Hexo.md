title: "Setup my blog using Hexo"
date: 2015-01-17 18:25:21
tags: Hexo
categories: DevOps
---


# Static site generator

When I want to write some technical blogs and publish them online, from programmers' pointer of view, there are many options for static website generator, such as [jekyll](http://jekyllrb.com/), [octopress](http://octopress.org/), [pelican](http://blog.getpelican.com/), [hexo](http://hexo.io/), etc. It is actually not that easy to say which one is the best, depends largely on your needs and background, e.g. jekyll and octopress is ruby based, pelican is powered by python, and hexo is built on nodejs. You can of course pick any one to start with, I did some investigation and comparison and finally end up choosing hexo, simply because it is easy to start with, and I like its simple and clean style.

----------

# Setup hexo

Two depencies need to be installed in advance:
 - [Git](http://git-scm.com/)
 - [Node.js](https://nodejs.org/)

<!--more-->

I am using Ubuntu:

    sudo apt-get update
    sudo apt-get install git-core
    sudo apt-get install nodejs
    sudo npm install -g hexo-cli

Then to create a new blog system:

    hexo init myblog
    cd myblog
    npm install

All the settings could be customized in ***_config.yml***.  Read more at http://hexo.io/docs/index.html

Now the basic setup is done, to serve it locally

    hexo server

----------

# Themes

There are many themes avaialbe at http://hexo.io/themes/ ,  and I like [NexT](https://github.com/iissnan/hexo-theme-next) most.

To install it:

    cd myblog
    git clone https://github.com/iissnan/hexo-theme-next themes/next


From the blog ***_config.yml*** , set language to default (English) and theme to nexT

    language: default
    theme: next

To make *tags* work:

    hexo new page "tags"

A file called ***index.md*** will be created under ***source/tags***, set the ***type*** to **"tags"**

    title: tags
    date: 2015-06-27 11:37:19
    ---

add `type: "tags"` to ***source/categories/index.md***, and enable it form ***_config.yml***


Then enable tag inside ***_config.yml*** located at ***themes/next***, just uncomment it

    menu:
      home: /
      categories: /categories
      archives: /archives
      tags: /tags

Similar procedure for categories

    hexo new page categories

add `type: "categories"` to ***source/categories/index.md***, and enable it form ***_config.yml***.


**Further configs**

 - You may want to create an **images** folder under ***source***, and refer the images from posts by adding: `![](/images/image_name.PNG)` and add your own avatar named "default_avatar.jpg".
 - Set `icon_font: linecons` in ***themes/next/_config.yml*** instead of ***default***
 - Enable `scheme: Mist`


You might want to get the latest feature and bug fix, after a while you need to update under ***themes/next*** folder

    git pull


----------


# Workflow

I am using Github to host the static page, so firstly create a repository called **YOUR_USERNAME.github.io**, then edit the blog ***_confg.yml*** file

    deploy:
      type: git
      repo: https://github.com/chuanjin/chuanjin.github.io.git
      branch: master
      message: hexo deploy

To create a new post:

    hexo new "title"
write the post, update it and view the layout on you local machine

    hexo server

If your post is too long, it is good to insert `<!--more-->` tag in your markdown source file somewhere when it is needed.

To deploy it to Github, install git deployer if you haven't

    npm install hexo-deployer-git --save

And then generate all the files and deploy

    hexo clean
    hexo generate
    hexo deploy

a reference workflow image could be found here: http://jr0cket.co.uk/developer-guides/hexo-workflow.pdf

You may notice after `hexo generate` there will generate a ***public*** folder, and will be pushed to Github by ***hexo deploy***, however it is always good to keep a backup of your original makedown posts somewhere, either push it into a different git repository, or use the script below to backup for you automatically during  deployment.

    #!/bin/bash
    hexo clean
    hexo generate
    if test -d public/posts_backup
    then
        rm -rf public/posts_backup
    fi
    cp -r source/ public/posts_backup
    hexo deploy

To setup custom domain, you need to create a file called **CNAME** under the ***source*** folder, and put your domain into it, then configure the A records from you DNS provider.

refer to
https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/
https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/


Now we are done! Enjoy it and have fun! :)
