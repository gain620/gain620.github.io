---
published: true
layout: single
title: "Applying gitignore on an existing repository already tracking large number of files!"
category: post
tags: [c++, programming, git, gitignore]
comments: true
---

## "Sometimes, you push a large number of files inadvertently, that were not meant to be pushed to the remote repository. You may try adding a new .gitignore file, but it just won't work. Too late!" :

Since, I myself being a junior programmer and not 100% comfortable using Git yet, I often make these mistakes.

Well, here's a fast and easy solution!

First of all, go to "https://www.gitignore.io/" and create a .gitignore file that will ignore all the undesired files from being pushed to your remote repository. And add that file to the root directory of your project folder.

Now to untrack every file that is now in your .gitignore, follow these steps.

1. "git rm -r --cached ."

This will remove everything from the index, then just run:

2. "git add ."

Commit it:

3. "git commit -m ".gitignore is now working" "

and you are good to go!

4. "git push origin master"

Now you can push to the remote repository with only the necessary files :)



Reference:
[https://stackoverflow.com/questions/1139762/ignore-files-that-have-already-been-committed-to-a-git-repository]
[https://cjh5414.github.io/gitignore-update/]