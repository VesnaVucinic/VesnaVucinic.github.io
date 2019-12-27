---
layout: post
title:      "CLI project about Royal Parks in London"
date:       2019-12-27 12:08:00 +0000
permalink:  cli_project_about_royal_parks_in_london
---


While I was working on my CLI project I learned a lot, finally managed to understand object orientation and how to use it, had a great fun with scarping tool Nokogiri and used my favourite method for validation of user input if input is integer learnd from my teacher Beth Scofield.

My work is about fabulous Royal Parks in London. 
Inspiration for logic how to create my project I found in videos by my teacher Beth Scofield about her project Eden Events (can be found on https://instruction.learn.co/student/home#/).

To get list of 10 Royal Parks I found scrapable web site and used Scraper Checker tool created by Jenifer Hanson, a Nokogiri-ready playground to test out scraping. 

 https://repl.it/@VesnaVucinic/ScraperChecker-Royal-Parks

After getting necessary data – list of parks, I made list with index because it’s better to ask from user number then to type name of park, it's is easier for user and prevents user to make spelling mistakes. 
I choose #each.with_index (1) to get list that starts with 1 (#each_with_index will start with 0).
 

To validate user input I used my favourite method for that purpose. Valid input is limited to be integer, maximal value of integer is length of scraped data (in this case 10), and minimal value must be greater than 0. Pure beauty in one-line code.

```
def valid_input(input, data)

      input.to_i <= data.length && input.to_i > 0
			
end
```
 
This method can be used in variety of different projects and that’s why I like it so much. 
Thanks to the Flatiron school I started process of gaining knowledge that I will use a lot in my future works.


