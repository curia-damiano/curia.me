---
title: "GitHub: how to reset the content of a repository"
slug: "github-how-to-reset-the-content-of-a-repository"
draft: false
date: "2018-06-12T19:14:00Z"
categories:
  - "Software Development"
tags:
  - "GitHub"
author: "Curia Damiano"
image: "img/github.png"
---

Steps to follow in case you want to reset (i.e. empty) the content of a GitHub repository, without deleting the full repository itself:
* in case you don't already have it, create a SSH key and add it to your GitHub profile:  
  [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
* in case you have tags that you want to delete as well, if you have a clone of the repository, you have to delete them locally and then push the changes to the remote:

  ```git
  git tag -d "TagToDelete"
  git push --delete origin "TagToDelete"
  ```
  
  if you don't have them on your local copy, you need to create them to then be able to delete them on the remote:
  
  ```git
  git tag "TagToDelete"
  git push origin "TagToDelete"
  git tag -d "TagToDelete"
  git push --delete origin "TagToDelete"
  ```

* now that your session is authenticated and authorized, you can proceed with [https://gist.github.com/stephenhardy/5470814](https://gist.github.com/stephenhardy/5470814):  

  ```git
  -- Remove the history from 
  rm -rf .git

  -- recreate the repos from the current content only
  git init -b main
  git add .
  git commit -m "Initial commit"

  -- push to the github remote repos ensuring you overwrite history
  git remote add origin git@github.com:<YOUR ACCOUNT>/<YOUR REPOS>.git
  git push -u --force origin main
  ```
