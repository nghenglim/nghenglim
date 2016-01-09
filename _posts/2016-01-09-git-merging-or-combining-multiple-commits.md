---
layout: post
title: Git Merging or Combining Multiple Commits
tags: [Git]
---

![git]({{ site.baseurl }}/images/2016010900.png "git")

### Whats The Problem
- many commits inside a feature branch
    - small enhancement or defect fix
    - not using git stash

### The Solution: Git Rebase
As in my commit message I use issue number such as `#143 fix abc`, therefore I set git config comment character to ";".

```
git config core.commentchar ";"
git log --pretty=oneline
git rebase --interactive HEAD~2
```

in this example, this is what you might see

```
pick abc2345 testing
pick def1234 latest commit
```

edit it to

```
pick abc2345 testing
s def1234 latest commit
```

save it and execute
```
git log --pretty=oneline
```

and you will find that the latest 2 commit has been merged to one

### Conclusion
This is helpful if you are creating a lot of dummy commit due to minor bug fix or not git stashing.
