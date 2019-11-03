# GitHub tutorial (for RStudio)

## Contents

* [Setup Git on RStudio](#setup-git-on-rstudio)
* [Create a new GitHub repository](#create-a-new-github-repository)
* [Create a new RStudio project](#create-a-new-rstudio-project)
* [Using Git in RStudio](#using-git-in-rstudio)
* [Useful resources](#useful-resources)



## Setup Git on RStudio

In RStudio, click on the 
**RStudio** menu bar and go to **Preferences**

<img src="https://github.com/mysteryduck/github/blob/master/img/0-1.png" height="200">

Go down to the **GIT/SVN** tab and ensure **Enable version control interface for RStudio projects** is checked.
 
Note that clicking on the **Using Version Control with RStudio** link will take 
you to a site that describes how to set up Git and lists some excellent 
resources to help you learn more about Git. Ignore this for now. 

Instead, we're now going to encrypt communication between our laptops and GitHub. 
To do this we need to generate a certificate. Click on **Create RSA Key...**

<img src="https://github.com/mysteryduck/github/blob/master/img/0-2.png" height="500">

Now, click **Create** to generate your RSA key

<img src="https://github.com/mysteryduck/github/blob/master/img/0-3.png" height="500">

It should look like this

<img src="https://github.com/mysteryduck/github/blob/master/img/0-4.png" height="500">

Now you need to copy your public key and register it with GitHub. Click on **View public key**

<img src="https://github.com/mysteryduck/github/blob/master/img/0-5.png" height="500">

Copy the key to your clipboard

<img src="https://github.com/mysteryduck/github/blob/master/img/0-6.png" height="500">

Then in GitHub, in your **Personal settings**, open the **SSH and GPG keys** tab 

<img src="https://github.com/mysteryduck/github/blob/master/img/0-7.png" height="500">

Create a **New SSH key**

<img src="https://github.com/mysteryduck/github/blob/master/img/0-8.png" height="500">

Paste the public key that you copied from RStudio into the box and click
**Add SSH key** 

<img src="https://github.com/mysteryduck/github/blob/master/img/0-9.png" height="500">

Now back in RStudio, tell Git your user name and email address (these are used 
to label each commit to GitHub). Make sure the email address you enter here is the
same as the one you registered on GitHub.

```{r}
install(usethis)
library(usethis)

use_git_config(
  scope = "user",
  user.name = "insert_github_username_here",
  user.email = "insert_email_address_here"
)
```

RStudio will now remember your details, so don't worry about having to enter 
them again in the future. You should, however, check that your username and 
email address was entered correctly!

```{r}
system("git config --global --list")
```



## Create a new GitHub repository

It's important that you use version control in your project workflow, so let's 
set up a new GitHub repository (you should make a new repository for each
project you're working on). To do this, click **New**

<img src="https://github.com/mysteryduck/github/blob/master/img/1-1.png" height="500">

Choose a short, descriptive name for your repository and 
**Initialize this repository with a README**. Since this is a tutorial and not
a real project, this repository has been named `test`.

<img src="https://github.com/mysteryduck/github/blob/master/img/1-2.png" height="500">

Congratulations! You have successfully created a new GitHub repository, 
containing a single `README.md` file. Remember this for later.

Now **copy** the URL associated with your GitHub repository to your clipboard

<img src="https://github.com/mysteryduck/github/blob/master/img/1-3.png" height="500">



## Create a new RStudio project
In RStudio, click **File** > **New project...**

<img src="https://github.com/mysteryduck/github/blob/master/img/2-1.png" height="300">

Since we're integrating version control into this project workflow, click **Version Control**

<img src="https://github.com/mysteryduck/github/blob/master/img/2-2.png" height="500">

Select the option to clone a project from a **Git** repository

<img src="https://github.com/mysteryduck/github/blob/master/img/2-3.png" height="500">

**Paste** your **Repository URL** into the first box, then click **Browse...** 
and navigate to the git folder on your desktop. If you don't have a git folder 
on your desktop then make one, as it's good practice to keep all of your 
projects together and well organised. RStudio will create a new subdirectory 
that will mirror the contents of your Git repository (so make sure you 
don't already have a folder with the same name as the repository you created, 
as this will cause problems). Now click **Create Project**

<img src="https://github.com/mysteryduck/github/blob/master/img/2-4.png" height="500">

Congratulations! You have successfully created a new RStudio project (now with
added version control). In the example below, the RStudio project is called 
`test`. A new directory, `test`, has been created inside the git folder on your 
desktop (this is now your working directory). Inside this directory are three 
files, including a GitHub `README.md` file (imported from your GitHub 
repository), an RStudio project file (`test.Rproj`), and an invisible 
`.gitignore` file (created by RStudio). 

Note the appearance of a new **Git** tab next to **Connections**. This is 
important.

<img src="https://github.com/mysteryduck/github/blob/master/img/2-5.png" height="500">


## Using Git in RStudio

Compare the contents of your working directory to the files listed in the
**Git** tab. The **Git** tab is a useful tool that shows you how your remote
directory (your GitHub repository) differs from your local directory 
(in this case `~Desktop/Git/test`). Currently, the `README.md` file in your 
local directory is identical to the one in your remote directory. That's why 
you can't see it in the **Git** tab. Instead, `.gitignore` and `test.Rproj`
are listed with yellow **Status** question marks. What do these icons mean?

* "?" - Files or directories that don't currently exist in the git repository 
(you either want to commit these or add them to `.gitignore`)
* "A" - Files that have been staged and are ready to commit (you're in the 
process of committing these)
* "M" - Files that are modified versions of those in the repository (you 
definately want to commit these)

Open the `README.md` file by clicking on its filename in the **Files** tab. 
Does this look familiar? (Compare the contents of this file to your
repository on GitHub)

<img src="https://github.com/mysteryduck/github/blob/master/img/2-6.png" height="500">

Usually a GitHub README (written in GitHub Flavored Markdown) will describe the 
contents of the GitHub repository or give an example of how to use the contents 
of said repository, so let's do that now. Note that when we make edits to the 
README file, its **Status** changes to "M". This means that the file in your 
local directory is no longer identical to the file in your remote directory 
(on GitHub).

Click **Commit** to upload these changes to GitHub.

<img src="https://github.com/mysteryduck/github/blob/master/img/2-7.png" height="500">

The **RStudio: Review Changes** window has opened. Click on the **Staged** 
checkbox next to `README.md` and enter a **Commit message**. Your message 
should describe the changes you've made to the file you're uploading (in this
case, an initial commit). These changes are shown in the lower half of the 
screen, with deletions and insertions highlighted in red and green, 
respectively. Click **Commit** to continue.

<img src="https://github.com/mysteryduck/github/blob/master/img/3-1.png" height="500">

Congratulations! `README.md` is now staged, with 7 insertions and 1 deletion. 
**Close** this window.

<img src="https://github.com/mysteryduck/github/blob/master/img/3-2.png" height="500">

Then **Push** all staged files (at the moment, just `README.md`) to GitHub.

<img src="https://github.com/mysteryduck/github/blob/master/img/3-3.png" height="500">

You'll need to enter your password..

<img src="https://github.com/mysteryduck/github/blob/master/img/3-4.png" height="500">

Congratulations again! You've successfully pushed these changes to GitHub.

<img src="https://github.com/mysteryduck/github/blob/master/img/3-5.png" height="500">

Note that `README.md` is no longer listed in the **Git** tab (because both the
local and remote versions are identical).

<img src="https://github.com/mysteryduck/github/blob/master/img/4-1.png" height="500">

... and the GitHub README is immediately updated. 

<img src="https://github.com/mysteryduck/github/blob/master/img/4-2.png" height="500">

## Useful resources

* https://learngitbranching.js.org

