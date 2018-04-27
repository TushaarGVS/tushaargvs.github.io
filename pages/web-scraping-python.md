---
layout: page
title: Web Scraping Part II: Python
description: Tutorial on using Python to scrape data from the web
---

This tutorial is written for Python 2.7. Instructions for viewing the page source are based on Google Chrome. Command-line things are for Mac. Note that the command-line
commands are not a huge part of the tutorial, so this can be easily adapted for use on a Windows machine. 


<div class="alert">
  <p><strong>Note:</strong> If you have never run a Python script from your computer, you might need to install Python. Additionally, if you don't have them you'll want to install Xcode, command line tools, Homebrew,
and PIP. <a href="https://www.macworld.co.uk/how-to/mac/coding-with-python-on-mac-3635912/">Click here for a tutorial that will walk you through this on a Mac.</a></p>
</div>

In this tutorial we will collect information on Medicare Part D prescription drug plans. The end result will be a CSV file containing information on every part D plan available in every state, with information on monthly premium, deductible, whether there is a "donut hole"
coverage gap, tier information, as well as information on the formulary position of every drug (tier number, cost-sharing, and drug usage management)

#### Here's what we want to do:
1. Navigate to the website [q1medicare.com](https://q1medicare.com)
2. On this webpage you'll see a box where you can **"Review 2018 Medicare Part D Plans"**. Click on any state you wish (I'm clicking on **AK**)
3. Scroll down to the chart that says **"There are 19 Alaska 2018 stand-alone [...]**. In this chart, you'll see all of the different plans and
information about them. This is the first set of information we want to collect. In our spreadsheet we're going to collect:
   1. Monthly prem.
   2. Deductible
   3. (Donut Hole) Gap Coverage
   4. Preferred Pharmacy Copay/Coinsurance 30-Day Supply
   5. Total Formulary Drugs (number)
   6. URL containined in the link "Browse Formulary" (we will use this in the second part to collect information on all the drugs in the formulary)
   
   
   
Now that we have an idea of what we want to do, we'll start coding it up.

If you need a refresher on how to run a Python script, check out my very short tutorial INSERT HERE.

The modules we are going to need to import are the following:

You might need to install these if you haven't already. To do this, go to the command line and type:
```bash

```

Let's start by importing the modules we will need. At the top of your python file, add:
```python
from bs4 import BeautifulSoup
```



If you look at the URL for each state, you'll notice that the formula of the URL is the same - only the state code changes:
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AK#results
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state=AR#results

Because the URLs have this structure, we will loop through all the URLs to get each state landing page. Note that if the URLs were not the same, we would
instead have python "click" on the link for each state. But this is easier.











If you need a quick primer on how to run python files, see my very short tutorial on "how to actually run a python script" 


