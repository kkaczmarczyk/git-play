Git-play
========

Git-play is a custom git command for deploying an application server very easily from remote git repository.
It checks remote git repository every minute and if something has changed, it will restart the application server automatically. 


# Installation

You can simply install git-play from PyPI by using `pip` or `easy_install`:

    $ pip install git-play
    
# Getting started

Git-play is made for people who hate complicated configurations, thus basically it doesn't require you to do much except `.git-play.yml`.

## Configuring your git-play deployment with `.git-play.yml`

Git-play uses `.git-play.yml` file in the root of your repository to learn how you want your application server to be executed.
`.git-play.yml` file has three parts: `app`, `setup`, `teardown`.

For your convenience, there are several examples of `.git-play.yml` file.

### Django
```
app:
  workdir: ./mysite
  respawn: yes
  exec: python manage.py runserver

setup:
  - cd mysite
  - python manage.py syncdb

teardown:
  - echo "The server is going down for maintanance..."
```

### Express
```
app:
  respawn: yes
  exec: node app.js

teardown:
  - echo "The server is going down for maintanance..."
```

## Spray and pray!

Now, all you have to do is just simply type as follows.

    $ git play http://github.com/foo/bar origin master
    