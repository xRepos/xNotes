---
title: Heroku Notes
description: Heroku Notes
---

Heroku
======

Deploy A New App
----------------

Step 1: Create a new app in Heroku Dashboard.

Step 2: Create a ``Procfile`` in your app folder, add this line to the file(illustrated as a node app)


    web: node app    


Step 3: Git as usual

    $ git init
    $ git remote add heroku git@heroku.com:<app-name>.git
    $ git add .
    $ git commit -m "init commit"
    $ git push heroku master


**Note**: if you skip the ``Procfile`` you might see the error message in ``heroku logs``
    
    at=error code=H14 desc="No web processes running

And if you call ``$ heroku ps:scale web=1`` it may return:

    !    Resource not found

