---
layout: page
title: Web Scraping Part II: Python
description: Tutorial on using Python to scrape data from the web
---

#### Web Scraping Part II: Python

This tutorial is written for Python 2.7. Instructions for viewing the page source are based on Google Chrome. Command-line things are for Mac. Note that using the command-line is not a huge part of the tutorial, so this can be easily adapted for use on a Windows machine.


<div class="warning">
  <p><strong>Note:</strong> If you have never run a Python script from your computer, you might need to install Python. Additionally, if you don't have them you'll want to install Xcode, command line tools, Homebrew, and PIP. <a href="https://www.macworld.co.uk/how-to/mac/coding-with-python-on-mac-3635912/">Click here for a tutorial that will walk you through this on a Mac.</a></p>
</div>

In this tutorial we will collect information on Medicare Part D prescription drug plans. The end result will be a CSV file containing information on every part D plan available in every state, with information on monthly premium, deductible, whether there is a "donut hole" coverage gap, tier information, as well as information on the formulary position of every drug (tier number, cost-sharing, and drug usage management)

#### Here's a roadmap of we want to do:
1. Navigate to the website [q1medicare.com](https://q1medicare.com)
2. On this webpage you'll see a box where you can **"Review 2018 Medicare Part D Plans"**. Click on any state you wish (I'm clicking on **AK**)
3. Scroll down to the chart that says **"There are 19 Alaska 2018 stand-alone [...]**. In this chart, you'll see all of the different plans and information about them. This is the first set of information we want to collect. In our spreadsheet we're going to collect:
   1. Monthly prem.
   2. Deductible
   3. (Donut Hole) Gap Coverage
   4. Preferred Pharmacy Copay/Coinsurance 30-Day Supply
   5. Total Formulary Drugs (number)
   6. URL containined in the link "Browse Formulary" (we will use this in the second part to collect information on all the drugs in the formulary)
   
**Here's what the first row of our output should look like:**
![scraping output spreadsheet example]({{ BASE_PATH }}/assets/scraping_output_spreadsheet_example.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/scraping_output_spreadsheet_example.png)

Our end result will be a spreadsheet containing the above information for every plan in every state.

Now that we have an idea of what we want to do, we'll start coding it up.

<div class="info">
  <p><strong>Note:</strong> If you need a refresher on how to run a Python script, check out my very short tutorial on  <a href="{{ BASE_PATH }}/pages/how-to-run-python-file)">how to run a python script.</a></p>
</div>


The modules we are going to need to import are the following:

You will need to install these if they aren't already on your machine. To do this, go to the command line and type:
```bash
pip install selenium
pip install bs4
pip install xlsxwriter
```

Let's start by importing the modules we will need. At the top of your python file, add:
```python
from bs4 import BeautifulSoup
from selenium import webdriver
import xlsxwriter
```

Add a line indicating the path that you want to save your output in. If you want to save in the same directory that you have your python file in, you can just leave it blank.
```python
save_output_path = '/Users/marisacarlos/Dropbox/mbcarlos.github.io/tutorial_files'
```
or
```python
save_output_path = ''
```

Add a line containing a list of state codes:
```python
# state_codes = ["AK", "AL", "AZ", "AR", "CA", "CO", "CT", "DC", "DE", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC","SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"]
state_codes = ["AK"]
```

I added two lines, one commented out (has the # in front) and one uncommented. It's much more efficient to write and test our code using the shorter list. If we loop through all the states every time we test the code, it'll take way too long. When we've finished our code and want to actually collect the data, remove the short list and uncomment the long list.



ADD COMMANDS HERE FOR PYTNON

Everything is arranged as a tree.


This next part is the trickiest part about web scraping. We need to figure out which tags have the information we want. Ideally, we'd like to find a set of tags that contains all the information we want for each drug plan, and be able to pull out **only** those tags. The **only** part is where it gets tricky. For this website, I looked through the page source and figured out the tag we were looking for had these unique characteristics:
```html
<tr class="tbllight" valign="middle"><td colspan="3" valign="middle">
<tr class="tbldark" valign="middle"><td colspan="3" valign="middle">
```
You'll notice that the class alernates between "tbllight" and "tbldark" but the **valign** and **


For a complete list of tag types see the list over at [w3schools](https://www.w3schools.com/tags/default.asp)
Types of tags:
- `<td>` tag defines a cell in an HTML table. 
- `<tr>`
- `<a> : contains hrefs (URL links)




If you look at the URL for each state, you'll notice that the formula of the URL is the same - only the state code changes:
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AK#results
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AR#results

Because the URLs have this structure, we will loop through all the URLs to get each state landing page. Note that if the URLs were not the same, we would instead have python "click" on the link for each state. But this is easier.



#### TROUBLESHOOTING:

Get stuck in a loop or run something that you didn't mean to? You can terminate the python command by doing the following. First open a new tab or window in your terminal. Then type:
```bash
ps aux | grep python
```
This will display a list of processes containing the term "python". Look for the process containing the command you issued (in my case it says:)
![ps aux output]({{ BASE_PATH }}/assets/ps_aux_grep_python.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/ps_aux_grep_python.png)

Figure out what the process ID is. In the example above the PID is 6380, so to stop this process I issue the command:
```
kill 6380
```
When you go back to the window where you issued the python command you'll see:
```bash
Terminated: 15
```
