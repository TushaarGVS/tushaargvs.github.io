---
layout: page
title: How to Create a Simple Academic Website
description: How to create a simple academic website for free using Github Pages.
---


This tutorial will teach you how to create a simple and free academic website using GitHub pages. [Click here to see what this website will look like.](http://blueham.github.io)

At the end of the tutorial you will have a website up and running at http://username.github.io (where username is your username). There is a link at the end with instructions for adding a custom domain name (e.g. marisacarlos.com).

<div class="warning">
  <p><strong>Note: </strong> The command line commands are written for Mac users and executed in the Terminal, but they should translate to Windows (Command Prompt) with few or no modifications. If there is something you cannot figure out, email me and I can try to help. </p>
</div>

#### For those who have never used GitHub or Git:
* Download the [approriate git software](https://git-scm.com/downloads) and install it.
* Create an account at [GitHub](https://github.com).
* Go through the [Hello World tutorial]( https://guides.github.com/activities/hello-world/), which will teach you how to create a repository and change it using the command line.
* [Click here for information on how to clone a repository](https://help.github.com/articles/cloning-a-repository/)
* [Click here for information on creating a new repository](https://help.github.com/articles/creating-a-new-repository/)
* I find this [GitHub cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf) very useful when I forget which commands do what.




#### Download the website files and create your repository:

1. Figure out where you want to store all of the files for your website. When you clone my directory, it will create a folder called "simple_academic_website" in your current working dirctory. Navigate to that directory and then clone the repository:
   ```bash
   cd "path to where I want to store the folder"
   git clone https://github.com/mbcarlos/simple_academic_website.git
   ```
   You can of course always move the folder to another place later on if you wish.


2. Navigate to the directory you just cloned:
```bash
cd simple_academic_website
```


3. Go to the command line and remove the .git directory using the command `rm -rf .git`.
   <div class="danger">
     <p><strong>WARNING:</strong> Be careful with this command as it removes a non-empty directory without asking you for confirmation. It will NOT send your files to the trash - it will remove them forever and ever.
     </p>
   </div>
   
   ```bash
   rm -rf .git
   ```
   
   
4. Initialize the git repository. This adds a file called .git that tracks all of the changes to the files in the directory and subdirectories.
   ```bash
   git init
   ```


5. Use git add to add these files to your next commit:
   ```bash
   git add .
   ```
   Note that `git add .` will add ALL of the files in your current directory and all subdirectories. It won't add the files in the directory above the one you ar currently in. If you want to add only specific files you can type:
   ```bash
   git add filename.filesuffix
   ```
   <div class="info">
   <p><strong>Note:</strong> At any time you can check to see what has been staged for commit, what has changes but isn't yet staged for commit, and which files are untracked by typing:</p>
   </div>
   ```
   git status
   ```
   
   
6. Commit the changes:
   ```bash
   git commit -m "write whatever message you want to describe this commit"
   ```
   <div class="info">
     <p><strong>Note 1:</strong> If you get an error at this point, you might need to configure your git with your username and email address. <a href="https://help.github.com/articles/setting-your-commit-email-address-in-git">See here</a> and <a href="https://help.github.com/articles/setting-your-username-in-git/">here</a></p>
   </div>
   
   <div class="info">
     <p><strong>Note 2:</strong> You have to type a commit message. If you just type git commit you will open up the message editor which is confusing and difficult to get out of. If you do get stuck in it, see <a href="https://apple.stackexchange.com/questions/252541/how-do-i-escape-the-git-commit-window-from-os-x-terminal">this Stackexchange thread for mac</a> and <a href="https://stackoverflow.com/questions/9171356/how-do-i-exit-from-the-text-window-in-git">this one for Windows.</a></p>
   </div>


7. Go to the [GitHub website](http://www.github.com) and create a new repository. You must call this repository username.github.io. If your username is marisabriana it will look like this:
   ![create_new_repository]({{ BASE_PATH }}/assets/simple_website_tutorial/create_new_repository.png)
   [(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/create_new_repository.png)

8. Go back to the command line and push (upload) all of your files in your website folder to github.
   ```bash
   git remote add origin https://github.com/username/username.github.io.git
   git push -u origin master
   ```
   You will be prompted to enter your username and password.
   
   <div class="note">
   <p><strong>Note: </strong> You will only have to issue the command <strong>git remote add origin ...</strong> once. This sets the URL for your github repository, which only needs to be done once.</p>
   </div>

9. Your website should now be live at https://username.github.io. You can check to make sure this is the case by going to the settings tab
   ![github_settings]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings.png)
   [(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings.png)
   and scrolling down to the GitHub Pages section
   ![github_settings_pages]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings_pages.png)
   [(click to zoom)]({{ BASE_PATH }}/assets/simple_website_tutorial/github_settings_pages.png)



#### Update the website files with your info:
* **ReadMe.md**: This is the file you'll see displayed on the home page of your GitHub repository

* **_config.yml**: Edit lines 11-18 (title - production URL) with your info. The "Title" will be what shows up in the top left-hand corner of every page. (Note: I don't fully understand what this file does, so I can't provide much insight on what might happen if you mess with it...)

* **index.md**: This is where you will edit the info that shows up on the home page.
  * In the top header (the stuff at the very top between the two sets of dashes) edit the title, a description of your website, and some keywords. Below the header, edit the text you want to show up on the main page.
  
  * The curriculum vitae link does not need to be changed (I'll show you where to store your CV below).
  
  * In the &lt;div class="container"&gt; section change the name and email. The email is hidden so that you don't get spam from bots that crawl pages looking for email addresses. Add your email address in pieces between the text "I don't want spam! So please leave me alone!"
  
  * Change the name below  &lt;`img src="../assets/headshot.jpg"`
  
  * In the &lt;`div class="navbar"`&gt; section you can add or remove things from the footer navigation bar. The link to the CV does not need to be changed, but you can add your github URL and username and twitter URL and username. Alternatively you can remove these if you don't want them, or add an additional field. Note that this footer navigation bar only shows up on the home page.
  
* **pages/research.md**: This is the page you will get to by clicking the "research" tab in the top navigation bar. You can add descriptions of your research and link to working papers and code (or whatever you want).

  * Edit the description in the header.
  
  * If you want to link to working papers, you can add them to the folder *pages/working_papers* and link to them from this page. 
* **_includes/themes/twitter/default.html**: This is the file you can update if you want to change the navigation bar at the top. For example, if you wanted to add a "tutorials" link you add the following in the &lt;ul class="nav"&gt; section:
  ```html
  <li><a href="{{ BASE_PATH }}/pages/tutorials.html">tutorials</a></li>
  ```
  
  Then you would create a page called `tutorials.md` and store it in the `pages` directory. The tutorials page would follow the same syntax as `research.md` or `index.md`. 
* Edit 404.md to include your email address
* Replace the CV and headshot with your own. These are stored in the `assets/` folder. Keep the names CV.pdf and headshot.jpg so that the pages that link to them continue to work.

#### Publish your website:
The last step is to push all of the changes you made to your GitHub repository. To do this do the following (assuming you are in your top directory - which is the directory that contains the **pages** and **assets** folders):
```bash
git add .
git commit -m "update my website"
git push -u origin master
```

Sometimes it takes a few minutes for the pages to refresh, but at this point you should have an active website at http://username.github.io. 


#### Adding a custom domain name (yourname.com)
To add your own custom domain, follow [the instructions on github](https://help.github.com/articles/using-a-custom-domain-with-github-pages/). Note that you'll first need to purchase the domain name. I purchased mine from [GoDaddy](https://www.godaddy.com), but there are other options. 
