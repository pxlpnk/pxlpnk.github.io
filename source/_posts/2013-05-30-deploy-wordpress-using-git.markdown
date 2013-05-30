---
layout: post
title: "Deploy Wordpress using Git"
date: 2013-05-30 11:59
comments: true
author: at
categories:
        - git
        - wordpress
        - deployment
---

A few weeks ago I came into the joy of setting up one or another Wordpress Blog. Copying files around after every change felt so 90ies and also introduced a lot of errors while working on the blog itself.


Being a huge fan of git I found a nice way to deploy any Wordpress blog and any static website using git. First of all you need a server with SSH access and some rights on that machine.

#### The local part
First we create a Git repository in your  Wordpress/Website folder.

``` bash
    cd wordpress_blog
    git init
    git add .
    git commit -m 'Initial commit'
```

#### The remote part

Create bare repository to mirror your local Wordpress source.

``` bash
    mkdir blog.git && cd blog.git
    git init --bare
```

Keep this repository separated from any the webroot and do not make it accessible to the outside world in any way.

Now we need to create the directory where the blog should be deployed to

``` bash
    mkdir /srv/www/blog/
```

and add the ```post-receive``` hook by adding the following to the ```blog.git/hooks/post-receive``` file and making it executable.

``` sh post-receive hook
    #!/bin/sh
    GIT_WORK_TREE=/src/www/blog git checkout -f
    chmod +x blog.git/hooks/post-receive
```

#### The deployment part
Now we need to add the new remote we just created to your repository and push our source code.

``` bash
    git remote add blog ssh://blog.example.com/home/USER/blog.git
    git push blog +master:refs/heads/master
```

To deploy your changes now you need to commit them and then push to your remote.
``` bash
    git push blog
```

After a successfully running the last command your changes should be in ```/srv/www/blog/```.
