---
layout: page
title: How to Create a Simple Academic Website
description: How to create a simple academic website for free using Github Pages.
---

#### How to create a simple academic website for free using Github Pages.

##### For those who have never used GitHub or Git:
* Download the [approriate git software](https://git-scm.com/downloads) and install it.
* Create an account at [GitHub](https://github.com).
* Go through the [Hello World tutorial]( https://guides.github.com/activities/hello-world/), which will teach you how to create a repository and change it using the command line.
* [Click here for information on how to clone a repository](https://help.github.com/articles/cloning-a-repository/)
* [Click here for information on creating a new repository](https://help.github.com/articles/creating-a-new-repository/)
* I find this [GitHub cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf) very useful when I forget which commands do what.
<!--
1) Clone my repository ENTER URL HERE (see this page if you don't know how to clone a repository https://help.github.com/articles/cloning-a-repository/)
2) remove the .git directory
3) Edit a bunch of pages
4) Use git init, git add, git commit
5) create a new repository of the form: username.github.io
    So if my username is mbcarlos, then I would create a repository called mbcarlos.github.io
    when you create this repository do not initialize with a readme or add a license - just leave it blank adn we will push all the files to it
    If you've never created a repository see: https://help.github.com/articles/creating-a-new-repository/
6) Push your changes to github using git push -u origin master
-->



##### Creating a Simple Academic Website

In this tutorial we will create a simple academic website with THIS FORMAT (URL HERE)


1) Figure out where you want to store all of the files for your website. When you clone my directory, it will create a folder called "WHATSIT CALLED?" in your current working dirctory. So figure out where you want it to be stored, navigate to that directory, and then clone (you can of course always move the folder to another place if you wish)
2) Navigate to the directory you just cloned:
```bash
cd NAME OF SITE HERE
```
2) Go to the command line and remove the .git directory. use the command rm -rf .git - BE CAREFUL WITH THIS COMMAND AS IT REMOVES A NON-EMPTY DIRECTORY WITHOUT ASKKNG YOU FOR CONFIRMATION AND IT DOESN'T SEND IT TO THE TRASH, IT REMOVES IT FOREVER AND EVER
```bash
rm -rf .git
```
3) Initialize the git repository. This adds a file called .git that tracks all of the changes to the files in the directory and subdirectories.
```bash
git init
```
Use git add to add these files to your next commit:
```bash
git add .
```
Note that git add . will add ALL of the files in your current directory and all subdirectories. It won't add the files in the directory above the one you ar currently in. If you want to add only specific files you can type:
```bash
git add filename.filesuffix
```
NOTE: At any time you can check to see what has been staged for commit, what has changes but isn't yet staged for commit, and which files are untracked using:
```
git status
```
Commit the changes:
```bash
git commit -m "write whatever message you want to describe this commit"
```
NOTE: you have to have a commit message. If you just type `git commit` you will open up the message editor which is confusing and difficult to get out of. If you do get stuck see [this stackexchange thread](https://apple.stackexchange.com/questions/252541/how-do-i-escape-the-git-commit-window-from-os-x-terminal) for Mac or [this one](https://stackoverflow.com/questions/9171356/how-do-i-exit-from-the-text-window-in-git) for Windows.

4) Go to the github website (github.com) and create a new repository. Call this repository username.github.io. If your username is marisabriana it will look like this:
![create_new_repository]({{ BASE_PATH }}/assets/simple_website_tutorial/create_new_repository.png)
[(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/create_new_repository.png)

5) Go back to the command line and push (upload) all of your files in your website folder to github.
```bash
git remote add origin https://github.com/username/username.github.io.git
git push -u origin master
```
You will be prompted to enter your username and password.
NOTE: If you get an error at this point, you might need to configure your github with your username and email address ([see here](https://help.github.com/articles/setting-your-commit-email-address-in-git/) and [here](https://help.github.com/articles/setting-your-username-in-git/)).

6) Your website should now be live at https://username.github.io. You can check to make sure this is the by going to the settings tab:
![github_settings]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings.png)
[(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings.png)
And scrolling down to the GitHub Pages section:
![github_settings_pages]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings_pages.png)
[(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings_pages.png)




#### Things to edit:
* **ReadMe.md**: This is the file you'll see displayed on your github repository page
* **_config.yml**: Edit lines 11-18 (title - production URL) with your info. The "Title" will be what shows up in the top left-hand corner of every page. (Note: I don't fully understand what this file does, so I can't provide much insight on what might happen if you mess with it...)
* **index.md**: This where you will edit the info that shows up on the home page.
  * In the top header (the stuff at the very top between the two sets of dashes) add a title (This), a description of what this website it, and some keywords. Below the header, edit your description.
  * The link curriculum vitae link does not need to be changed (I'll show you where to store your CV below).
  * In the &lt;div class="container"&gt; section change my name to your name and add your email. The email is hidden so that you don't get spam from bots that crawl pages looking for email addresses. Add your email address in pieces between the text "I don't want spam! So please leave me alone!"
  * Change my name to your name in the section  &lt;`img src="../assets/headshot.jpg"`
  * In the &lt;`div class="navbar"`&gt; section you can add or remove things from the footer navigation bar. The link to the CV does not need to be changed, but you can add your github URL and username and twitter URL and username. Alternatively you can remove these if you don't want them, or add an additional field. Note that this footer navigation bar only shows up on the home page.
* **pages/research.md**: This is the page you will get to by clicking the "research" tab in the top navigation bar. You can add descriptions of your research and link to working papers and code (or whatever you want).
  * Edit the description in the header.
  * If you want to link to working papers, you can add them to the folder *pages/working_papers* and link to them from this page. 
* **_includes/themes/twitter/default.html**: This is the page you can update if you want to change the navigation bar at the top. For example, if you wanted to add a "tutorials" link you would add:
  ```html
  <li><a href="{{ BASE_PATH }}/pages/tutorials.html">tutorials</a></li>
  ```
  and then you would create a page called `tutorials.md` and store it in the `pages` directory. The tutorials page would follow the same syntax as `research.md` or `index.md`. 
* Edit 404.md to include your email address
* Replace the CV and headshot with your own. These are stored in the `assets/` folder. Keep the names CV.pdf and headshot.jpg so that the pages that link to them continue to work.


#### Adding a custom domain name (yourname.com)
To add your own custom domain, follow [the instructions on github](https://help.github.com/articles/using-a-custom-domain-with-github-pages/). Note that uou'll first need to purchase the domain name. I purchased mine from [GoDaddy](https://www.godaddy.com), but there are other options. 
