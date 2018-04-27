---
layout: page
title: How to run a Python script
description: Tutorial on how to run a Python script
---

#### IDE versus Text Editor

There are two main options for writing/running python scripts. The first is to use an IDE (integrated development environment) that allows you to write your code in the same program that you compile/run the code. This is similar to what you would do if you use Stata - open Stata, write a do-file, then click "do" and your program runs. There are a number of software packages that you can use to do this, one is Anaconda. To get to the editor, open anaconda launcher and launch "Spyder". See the attached screenshot for where you write the code and how to get it to run.

**Here's a screenshot of where to write your code and how to get it to run using Anaconda:**
![Anaconda IDE Screenshot]({{ BASE_PATH }}/assets/anaconda_python_IDE.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/anaconda_python_IDE.png)

I personally don't like Anaconda because it takes too long to open and it feels too crowded with all of the boxes in one window. I prefer to write my codes using a text editor and run them from the command line. I use Komodo Edit as my text editor, which is free and easy to use.

#### How to create and run your code

1. Open your text editor (in my case Komodo Edit) and create a new file. In Komodo Edit, click on "text" near the bottom right corner and select "python" from the drop down menu. 
2. Write your code and then save it - be sure to add .py to the end of the file so your computer knows its a python script.
3. Open your terminal and navigate to the folder (directory) where you saved your python code. For example, if my code was saved in /Users/marisacarlos/Dropbox I would type:
   ```bash
   cd /Users/marisacarlos/Dropbox
   ```

   Note that if you have spaces in your path name you'll need to use double quotes around it.

4. Run your code. If your code is called pythoncode.py you would type:
   ```bash
    python pythoncode.py
    ```
    If you have any print statements in your code, they will show up in your terminal window. Same goes for any error messages. If you don't have any print statements and your code runs without error, then after you hit enter and it runs you'll be returned to the command line (e.g. marisacarlos$ next to a blinking cursor)
If you get an error when you try to run your code in the terminal that says something like "command not found" or that you "need to add python to your path", let me know and I will send instructions on how to do that.

I encourage you to explore both of these options (IDE versus text editor/terminal) and see which one you like. There are many more options than just the two I sent you, so feel free to search for something else if you don't like either of those! 