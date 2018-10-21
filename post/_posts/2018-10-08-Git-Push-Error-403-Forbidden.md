---
layout: post
title: Git Push Error 403 Forbidden
description:
---

Lately, I'm having problems with git push command in the remote access machine at school. In this post, I will provide a solution for you that have the same problem.

Initially, you would clone by using this command:

```
git clone https://github.com/<your.username>/<your.repo>.git
```

Then, you will make change to your file(s) or folder(s). When you're ready to post them in your GitHub, you will do the following:

```
git add <your.FilesOrFolders>
git commit -m 'make change to files'
git push origin master
```

Unfortunately, you will get this error:

```
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/<your.username>/<your.repo>.git/info/refs

fatal: HTTP request failed
```

Here is how you will fix it:

```
git remote set-url origin "https://<your.username>@github.com/<your.username>/<your.repo>.git"
```

Then, you will be prompted to enter your Github password.

Finally, you can do:

```
git push origin master
```
