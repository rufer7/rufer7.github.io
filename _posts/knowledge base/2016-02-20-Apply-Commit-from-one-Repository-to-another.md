---
layout: post
category: knowledge-base
title: Apply Commit from one Repository to another
date: 20 Feb 2016
tags: Git
---

Imagine you have several repositories holding more or less the same code base that only differ in some customer specific functionality. At d-fens we had exactly the before described situation. We made some changes (i.e. new features or bugfixes) to one of the repositories and wanted to apply the changes to the second repo. One possibility is to apply all changes made to the first repo manually to the second repository by copying and pasting all the stuff from the first to the second repository. But we found an easier more consistent way to do that by using [`git format-patch`](https://git-scm.com/docs/git-format-patch) and [`git-am`](https://git-scm.com/docs/git-am) commands.

#### Applying the last two commits from `repo1` to `repo2`

The command below will create two patch files for the last two commits from HEAD of `repo1` in the directory `/path/to/repo2`.

```bash
/path/to/repo2 $ git --git-dir=/path/to/repo1/.git format-patch -2 HEAD --stdout
```

To apply them the following commands have to be executed

```bash
/path/to/repo2 $ git am /path/to/1/0001-…-….patch
/path/to/repo2 $ git am /path/to/1/0002-…-….patch
```

If there are conflicts the patches cannot be applied without manual work. In such a case revert the patching by executing `git am --abort` and execute the `git am` command again but this time with the `--reject` switch.

```bash
/path/to/repo2 $ git am /path/to/1/000x-…-….patch --reject
```

When using the reject switch all the changes contained in a patch that could be applied without conflicts will be applied. For every conflicting part a file with ending `.rej` will be created. Now you have to manually apply the changes described in the `.rej` files to your repository (`repo2`). After you applied all the changes add all files to the index by using `git add` command and the you can continue with `git am --continue`.
