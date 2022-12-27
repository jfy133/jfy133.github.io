---
title: "Updating a Github Pages Theme Through a Repo Merge"
date: 2017-10-08
permalink: /posts/2017/10/updating-github-pages-theme.md/
tags:
  - website
  - github
  - jekyll
  - theme
  - tutorial
  - how-t
layout: post
---

# How-to: Updating a Github Pages Theme Through a Repo Merge

### James A. Fellows Yates

> ⚠️ 2022-12-27: The instructions here do not apply to the current version of the website as this uses a different theme! However the instructions are still a useful example of pulling in changes from an upstream fork.

I am new to Git and Github, and so I am still very much learning on the fly.
Today I noticed the original repository for the theme of this website had added
updates, so I thought to apply them to my own repository.

This wasn't as straightforward as it seemed, so here I have written down
my instructions how to apply the fixes in the future.

The instructions are essentially a merging of what I read on these three pages:

- [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/)
- [https://help.github.com/articles/syncing-a-fork/](https://help.github.com/articles/syncing-a-fork/)
- [http://genomewiki.ucsc.edu/index.php/Resolving_merge_conflicts_in_Git](http://genomewiki.ucsc.edu/index.php/Resolving_merge_conflicts_in_Git)

I assume this is applicable for all Git related repo manipulations, but in this
tutorial I am focusing on updating a Github pages theme.

## Instructions

1. Change into my local repository on my laptop, and initialise

   ```bash
   cd ~/<path>/<to>/<local_repo/
   git init
   ```

2. Check the remote information, and if no upstream branches present - add them. In this case I'm using the repo I used for my website

   ```bash
   git remote -v
   git remote add upstream https://github.com/academicpages/academicpages.github.io.git
   ```

3. Find the changes in the upstream branch

   ```bash
   git fetch upstream
   ```

4. Now check out of branch (not sure if this was needed, but didn't do any harm)

   ```bash
   git checkout master
   ```

5. Now we attempt to merge the changes. Git will take anything in the upstream branch, and if no change has been made on the my personal repo in the past, will make the change. Otherwise, `merge conflict` errors will be printed to screen.

   ```bash
   git merge upstream/master
   ```

6. Take a look at which files have the merge conflicts, and inside each file look at the sections with `<<<<<`, `=====` or `>>>>>` and manually remove the changes (normally the upstream, or one below the `=====`) that you don't want changed. Remove the symbols above as well, save the the file. Add the file to the commit to indicate you've 'fixed'
   the merge conflict, for example:

   ```bash
   git add _config.yml
   ```

7. Once you've fixed all the merge conflicts, you can do a normal git commit and push.

   ```bash
   git commit -m "Merged with <upstream_repo>"
   ```

And with that your website theme should be updated.
