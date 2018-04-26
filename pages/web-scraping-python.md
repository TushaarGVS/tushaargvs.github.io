---
layout: page
title: Web Scraping Part II: Python
description: Tutorial on using Python to scrape data from the web
---

This tutorial is written for Python 2.7. Instructions for viewing the page source as based on Google Chrome. Command-line things are for Mac. Note that the command-line
commands are not a huge part of the tutorial, so this can be easily adapted for use on a Windows machine. 

In this tutorial we will collect information on Medicare Part D prescription drug plans. The end result will be a CSV file containing information on every part D plan available in every state, with information on monthly premium, deductible, whether there is a "donut hole"
coverage gap, tier information, as well as information on the formulary position of every drug (tier number, cost-sharing, and drug usage management)

Here's what we want to do:
1. Navigate to the website [q1medicare.com](https://q1medicare.com)
2. On this webpage you'll see a box where you can **Review 2018 Medicare Part D Plans**. Click on any state you wish (I'm clicking on **AK**)
3. Scroll down to the chart that says **There are 19 Alaska 2018 stand-alone Medicare Part D plans meeting your criteria**. In this chart, you'll see all of the different plans and
information about them. This is the first set of information we want to collect. In our spreadsheet we're going to collect:
   1. Monthly prem.
   2. Deductible
   3. (Donut Hole) Gap Coverage
   4. Preferred Pharmacy Copay/Coinsurance 30-Day Supply
   5. Total Formulary Drugs (number)
   6. URL containined in the link "Browse Formulary" (we will use this in the second part to collect information on all the drugs in the formulary)
   
   
If you look at the URL for each state, you'll notice that the formula of the URL is the same:
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state= **AK** #results
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state= **AR** #results
- https://q1medicare.com/PartD-SearchPDPMedicare-2018PlanFinder.php?state= **AK** #results







If you need a quick primer on how to run python files, see my very short tutorial on "how to actually run a python script" 


