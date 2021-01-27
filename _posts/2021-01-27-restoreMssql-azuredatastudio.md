---
title: "How to restore Microsoft SQL Server Database 2017 running in a linux docker container with Azure Data Studio"
excerpt_separator: "<!--more-->"
categories:
  - today-i-learned
tags:
  - til 
---

> Dealing with the "Exclusive access could not be obtained because the database is in use”

<!--more-->

## Expected Solution:

Just select the database, click restore and choose the file to restore from and target database from the UI.  

![expected-image](assets/images/expected.png)


## Problem:

We get this error: `Exclusive access could not be obtained because the database is in use` and the close database 
connections checkbox in the options is greyed out. 

![error-image](assets/images/error.png)

## Solution:

![error-image](assets/images/options.png)


1. Click restore and then immediately go to options and select the close database connections option. 
2. Then change the database restore method to file and select your file, Even if the checkbox
is greyed out this time, it will still be selected and the restore will work.

