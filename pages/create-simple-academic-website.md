
FOR THOSE UNFAMILIAR WITH GITHUB/GIT:
* Download the approriate git software https://git-scm.com/downloads and install it.
* Create a github account. The Hello World tutorial is a good thing to start with: https://guides.github.com/activities/hello-world/
* If you need to know how to clone a repository see: https://help.github.com/articles/cloning-a-repository/
* If you need to know how to create a new repository see:  https://help.github.com/articles/creating-a-new-repository/
* This github cheat sheet is useful: https://education.github.com/git-cheat-sheet-education.pdf
* custom domain on github pages: https://help.github.com/articles/using-a-custom-domain-with-github-pages/

1) Clone my repository ENTER URL HERE (see this page if you don't know how to clone a repository https://help.github.com/articles/cloning-a-repository/)
2) remove the .git directory
3) Edit a bunch of pages
4) Use git init, git add, git commit
5) create a new repository of the form: username.github.io
    So if my username is mbcarlos, then I would create a repository called mbcarlos.github.io
    when you create this repository do not initialize with a readme or add a license - just leave it blank adn we will push all the files to it
    If you've never created a repository see: https://help.github.com/articles/creating-a-new-repository/
6) Push your changes to github using git push -u origin master




#### Creating a Simple Academic Website

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





ADD PART ABOUT EDITING:
0) edit _config.yml with all of your info (line 11-19)
1) 
1) Replace my CV and headshot with your CV and headshot. Save them in the assets folder as CV.pdf and headshot.jpg. If you want to name them something else you'll have to edit the links on the home page (index) and navigation bar (_includes/themes/twitter/default.html)
2) Edit the research page in pages/research.md to include summaries of your research. ADD INFO ABOUT LINKING TO DRAFT OF WORKING PAPER
3) Edit 404.md to include your email address
4) 
3) If you want to add any addtional pages to the top navigation bar


I NEED TO GO IN AND EDIT THE TOP NAVIGATION BAR TO REMOVE RESOURCE AND TUTORIALS 