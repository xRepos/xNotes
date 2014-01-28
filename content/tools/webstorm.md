---
title: xNotes - WebStorm
description: WebStorm
---

WebStorm
========

FileWatcher
-----------

Two mistakes:

1. I used ``less`` instead of ``lessc`` to compile ``.less`` files. Then suddenly, suddenly I realized, ``less`` in command line, has nothing to do with CSS… it is just a file viewer like ``more``… that explains why the “compiled” css file looks exactly the same as its origin less file.

2. I saw the error message

    env: node: No such file or directory

The solution is add PATH=/usr/local/bin to ``Environment variables`` in FileWatcher

Extra note about the FileWatcher: in command line we use ``lessc style.less > style.css`` to write to file. In FileWatcher, set only ``style.less`` in Arguments , and leave ``style.css`` in  ``Output paths to refresh``