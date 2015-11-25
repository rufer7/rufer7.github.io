---
layout: post
category: out-of-the-www
title: GitHub Repository creation with PowerShell
date: 25 Nov 2015
tags: PowerShell GitHub automation
---

After a longer period of time without blogging I have something interesting for you. In the last few weeks I had to create several GitHub repositories for my daily work. To simplify the process I automated the creation with PowerShell.


I created and initialized the repositories manually until I recognized that this is a perfect task to automate. First I studied the documentation of the [GitHub API v3](https://developer.github.com/v3/), which is very well documented! Fortunately for me the GitHub API supports all the functions I needed.

The automation contains the following steps:

* Create a new repository
* Initialize with one of the licenses provided by the license endpoint
* Initialize with one of the gitignore files provided by the gitignore endpoint
* Add a NOTICE file based on a predefined template to the repository
* Add the license shield to the readme if `Apache License 2.0` was selected as license
* Add labels `feature`, `onhold` and `task` to the repository


The PowerShell script that performs all the steps described above. The script, the corresponding configuration file and the README and NOTICE template can be found in the GitHub repository [PS.GitHub.RepoCreator](https://github.com/rufer7/PS.GitHub.RepoCreator).
Feel free to use it and to contribute or create issues for desired use cases.


#### How to use

1. Create an access token for command-line use (For details see [here](https://help.github.com/articles/creating-an-access-token-for-command-line-use/))
2. Check out the sources from the [`PS.GitHub.RepoCreator`](https://github.com/rufer7/PS.GitHub.RepoCreator) repository
3. Navigate to the `src` folder
  1. `Config.xml`: Fill in your GitHub username and the access token generated in step 1
  2. `NOTICE_Template`: Adjust the content according your wishes (**IMPORTANT**: The placeholders `REPONAME` and `REPODESCRIPTION` always have to occur at least once in the file)
  3. `README_Template`: Adjust the content according your wishes (**IMPORTANT**: The placeholders `REPONAME`, `LICENSEBADGE` and `REPODESCRIPTION` always have to occur at least once in the file)
4. Now you're ready to execute the script which will do the following
  1. Creation of a new repository with the selected license and the selected gitignore file
  2. In case you selected `Apache 2.0` as license, it will add a license badge to the README file
  3. Creation of a NOTICE file based on the `NOTICE_Template`
  4. Creation of 3 new issue labels: `feature`, `onhold`, `task`

Sample invocation

```
PS C:\PS.GitHub.RepoCreator\src> .\New-GitHubRepo.ps1 -RepoName 'NAME' -RepoDescription 'DESCRIPTION'
```

##### Config.xml

```
<?xml version="1.0"?>
<Configuration>
	<GitHub>
		<Username>USERNAME</Username>
		<Token>TOKEN</Token>
	</GitHub>
</Configuration>
```
