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
2. On this webpage you'll see a box where you can **"Review 2018 Medicare Part D Plans"**. Click  on **AK** (Alaska).
3. Scroll down to the chart that says **"There are 19 Alaska 2018 stand-alone [...]**. In this chart, you'll see all of the different plans and information about them. This is the first set of information we want to collect. In our spreadsheet we're going to collect:
   1. Monthly prem.
   2. Deductible
   3. (Donut Hole) Gap Coverage
   4. Preferred Pharmacy Copay/Coinsurance 30-Day Supply
   5. Total Formulary Drugs (number)
   6. URL containined in the link "Browse Formulary" (we will use this in a later tutorial to collect information on all the drugs in the formulary)
   
**Here's what the first row of our output should look like:**
![scraping output spreadsheet example]({{ BASE_PATH }}/assets/scraping_output_spreadsheet_example.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/scraping_output_spreadsheet_example.png)

Our end result will be a spreadsheet containing the above information for every plan in every state.

Now that we have an idea of what we want to do, we'll start coding it up.

<div class="info">
  <p><strong>Note:</strong> If you need a refresher on how to run a Python script, check out my very short tutorial on  <a href="{{ BASE_PATH }}/pages/how-to-run-python-file">how to run a python script.</a></p>
</div>


The python modules we will need to run our code are the following:
* [Selenium](http://selenium-python.readthedocs.io)
* [bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
* [xlsxwriter](http://xlsxwriter.readthedocs.io)

You will need to install these if they aren't already on your machine. To do this, go to the **command line** and type:
```bash
pip install selenium
pip install bs4
pip install xlsxwriter
```

Now let's start writing out Python code. In a new python file (I'm calling mine "medicare_PDP_scrape.py) add the modules that we will need to the top of the script:
```python
from bs4 import BeautifulSoup
from selenium import webdriver
import xlsxwriter
```

We will also want to create a variable containing the path of the directory we want to save our spreadsheet in:

```python
save_output_path = '/Users/marisacarlos/Dropbox/mbcarlos.github.io/tutorial_files'
```

At the top of all of my python files I define a function that prints a new (blank) line, dashed line, and another new line. I use it to make printing to the console easier to read. After we define the function, we can call it by typing `print_line()`:
```
def print_line():
    print " "
    print "----------------------------------------------------------------------------------------------------------------------"
    print " "
```


If you look at the URL for each state, you'll notice that the only thing that changes between two states is the state code (**AK** versus **AL**):
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AK#results
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AL#results

This will make it easy to loop through the URLs for all states. We can create a list of state codes, and then loop through that list. 

Add a line containing a list of state codes:
```python
# state_codes = ["AK", "AL", "AZ", "AR", "CA", "CO", "CT", "DC", "DE", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC","SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"]
state_codes = ["AK","AL"]
```

I added two lines, one commented out (has the # in front) and one uncommented. It's much more efficient to write and test our code using the shorter list. If we loop through all the states every time we test the code, it will take much longer and won't buy us anything. When we've finished our code and want to actually collect the data, remove the short list and uncomment the long list.



ADD COMMANDS HERE FOR PYTNON BEGINNING AT "FIRST WE WANT TO LOOP THROUGH THE STATES"
### PUT THESE COMMANDS AT THE VRY BOTOTM OF YOUR PYTHON FILE SO THAT EVERYTHING PROPERLY CLOSES WHEN YOU RUN IT WHILE WE ARE TESTING/BUILDING
```python
workbook.close()
driver.quit()
```


The next part is the trickest part of web scraping. We need to figure out where the information we want to collect is and figure out a well to tell the machine what information we want. We'll start by looking at the page source. In Google Chrome  paste the following into your address bar:
```
view-source:https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AK#results
```

Notice this is just the website prefixed with **view-source:**. You can also get to this by going to the website, right clicking anywhere, and selecting "view page source."

Scrolling through the page source, it's clear that there is a whole lot of information we don't need. We want to find a way to identify each row of the table in the page source. When I looked at the webpage I noticed that every row of the table has the text "Preferred Generic". If I search the page I can see that this text only occurs in the table, and it occurs in every single row.

I can search for this text in the page source to glean some insight into what tags contain the information I want:
![preferred_generic_page_source_search]({{ BASE_PATH }}/assets/preferred_generic_page_source_search.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/preferred_generic_page_source_search.png)

The screenshot above shows the entire tag, which contains all of the information that we need. It is a `<tr>` tag - which we know because it starts with `<tr>` and ends with `</tr>`:
![tr_tag_illustration]({{ BASE_PATH }}/assets/tr_tag_illustration.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/tr_tag_illustration.png)

All of the information we are looking for is contained within the tag:
![tr_tag_column_info_highlighted]({{ BASE_PATH }}/assets/tr_tag_column_info_highlighted.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/tr_tag_column_info_highlighted.png)

We can see that the TR tag has the characteristics:
```html
valign="middle" class="tbldark"
```
If we scroll down to the tag containing the second row of data we want to scrape, we see the TR tag has the characteristics:
```html
valign="middle" class="tbllight"
```
![second_tr_tag_illustration]({{ BASE_PATH }}/assets/second_tr_tag_illustration.png)
[(click here to zoom)]({{ BASE_PATH }}/assets/second_tr_tag_illustration.png)

Luckily for us, it looks like TR tags with asset valign="middle" are **only** used for the rows in the table with the data we want. Becuase of this we can pull out all the TR tags with this attribute:
```python
soup.find_all('tr',{"valign":"middle"})
```
The `find_all` command searches through the "soup" and pulls out all of the tags with the attributes you specify. In this case, we've told it to pull out all the 'tr' tags where valign="middle". We can see how many `<tr>` tags by printing the length of the list:
```python
print len(soup.find_all('tr',{"valign":"middle"}))
```

If this number is 19 (the number of rows in the table for Alaska) then it's likely that we are pulling out the information we need and nothing more.

We can loop through all of these tags and print each one using the following code:
```python
for tr_tag in soup.find_all('tr',{"valign":"middle"}):
    print_line()
    print tr_tag
```

We see that within each `<tr>` tag there are a bunch of other tags. The information we want to pull for each row is containing in a separate tag. From inspecting the page source it looks like this information is contained in the `<td>` tags:



Within each tr tag, I can pull out each td tag. Underneath the `for tr_tag in [...]` loop add a loop that pulls out each td tag:
```python
for tr_tag in soup.find_all('tr',{"valign":"middle"}):
    print_line()
    #print tr_tag #I'm commenting this out for now to make the console less messy
    
    td_tag_num = 0 #We will use this variable to count the number of td tags that are within each tr tag.
    for td_tag in tr_tag.find_all('td'): #Loop through the td tags
        td_tag_num+=1 #Adds 1 to the td_tag_num variable every time we go through the loop
        print_line()
        print "td tag num:", td_tag_num
        print td_tag
```

If we look at the output in the console, we see that with the exception of the first td tag, we've succesfully found the tags that contain just the information we are looking for. So for tags 2-7 we can extract the text (tag 7 we'll need to extract the url too) and then in tag 1 we can pull out the text and URL from the first `<a>` tag which has the information we want. 

For a complete list of tag types see [w3schools](https://www.w3schools.com/tags/default.asp)






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
