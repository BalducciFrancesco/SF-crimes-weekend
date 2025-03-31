---
layout: post
title: "Assignment 2"
date:   2025-03-27 15:00:00 +0100
tags: assignment
---

# Table of Contents

* Table of Contents  
{:toc}

# Context

This assignment is part of the [Social Data Analysis and Visualization course](https://kurser.dtu.dk/course/02806). The goal of the course is to teach us new techniques for exploring and visualizing raw datasets, as well as introducing some analytical tools. Full guidelines for the course can be found on [GitHub](https://github.com/suneman/socialdata2025).

# About the Dataset

The datasets used in this assignment can be easily accessed [here](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-Historical-2003/tmnf-yvry/about_data) and [here](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783/about_data). They are .csv files where each row represents a crime reported by the San Francisco Police Department, with columns detailing information like the type of crime, its location, and more.

We merged the datasets using code since the first contains "historical" data (up to 2018) and the second includes "recent" data (from 2018 to the present). We also cleaned the data to standardize column names. The final dataset includes the following columns:

- Incident Category (e.g., homicide, fraud, etc.)
- Police District
- Resolution
- Latitude
- Longitude
- Incident Datetime

In total, there are **3,004,644** crimes recorded **from 2003 to 2024**, which we analyzed (and yes, it’s a depressing number).

# Goal of the Assignment

The purpose of this assignment is to bring together everything we've learned about data visualization. This includes using techniques for data exploration and effectively communicating findings, all while making the information accessible to a broad audience.

# Step-by-stepsdas

Here we go with the actual analysis. Brace yourselves!

One phenomenon that caught everyone’s attention is the **different behavior people seem to exhibit on weekends and at night**. Of course, we’re still talking about crimes, and alcohol and hanging out might play a significant role in this. Everything that follows aims to find evidence-backed explanations for this intuition.

To kick off our investigation, we used our *Python programming skills* to create a huge (and somewhat ugly) plot where, for *each crime category*, we displayed the number of crimes *per weekday* and *per hour range*. We're skipping this plot for the sake of brevity. As suggested in [Data Analysis with Open Source Tools (DAOST)](https://www.oreilly.com/library/view/data-analysis-with/9781449389802/), when presenting graphical analysis, we intentionally kept it quick to avoid any bias from spending too much time making it visually appealing.

> From now on, *"hour range"* will refer to the following daily time slots: 6-14, 14-22, and 22-6. We also decided to define "weekdays" as Monday through Thursday and "weekend" as Friday through Sunday.

At first glance, it was clear that most crimes occur more often at night than during the day, with not many showing a distinct peak over the weekend.

However, there were some surprises. For example, it might be surprising to learn that most drug offenses and prostitution were reported on Wednesdays, rather than on the weekend.

Returning to our goal, we observed that **assaults** and **malicious mischief** indeed occurred more frequently on weekends and at night. So, we created a specific plot to highlight these findings:

![Crime categories occurring more often in the weekend and at night]({{ site.baseurl }}/assets/images/assignment2_plot1.png)

As seen in the plot, considering the entire data span, assaults rarely exceeded 30,000 during the weekdays, while on the weekend, they grew and almost reached 40,000 on Saturdays. The same pattern applies (with about 10,000 fewer daily occurrences overall) for malicious mischief, with the only difference being that Fridays had more occurrences than Sundays. A **clear preference for Saturdays and nighttime hours** seems to apply in both cases, suggesting that external factors like drinking or hanging out may play a role.

## Navigating San Francisco: Where to Go and What to Avoid  

It’s the weekend, and like most people, you’re ready to unwind and explore the city. Maybe you’re a family looking to relax in one of San Francisco’s beautiful parks, or a group of college friends excited for a night out at your favorite pub. The last thing on your mind? Crime.  

But what if you could know exactly where and when crime is most likely to happen? That’s exactly what we set out to uncover. By analyzing crime data of assaults and malicious mischief, which came out that have their peak during weekends, and visualizing it in a **Time Heat Map**, we reveal the city’s weekend crime, so you choose the safest places to enjoy your time. 

<iframe src="{{ site.baseurl }}/assets/templates/sf_heatmap.html" frameborder="0" style="width: 100%; height: 500px"></iframe>

This interactive map allows you to explore crime trends across the city and different time periods. We grouped the data into three-hour intervals, covering the period **from Friday at 6 PM to Sunday at midnight**. Now let's have a look to some possible scenarios.

Good news! Most parks are safe havens. Whether you’re planning a picnic or letting the kids play, you generally have little to worry about. That said, **Golden Gate Park** does show a slight uptick in assaults during the afternoon (3–6 PM). This could be due to its big size and popularity, but compared to other areas, it remains relatively safe.  

## If You’re Exploring San Francisco’s Nightlife
If you’re searching for a pub or club, things get trickier. On Saturday night (9 PM–midnight), much of the city center turns red, indicating a high concentration of crime. But don’t worry, there are still safer areas to enjoy.  

- **Tenderloin: A No-Go Zone**  
  Despite its many clubs, theaters, and bars near Union Square, it remains one of the city’s **most dangerous areas**. It’s no secret that the Tenderloin has a bad reputation, and the heat map confirms it. Nearly every street in this neighborhood turns red on Saturday night (9 PM–midnight), indicating high crime levels. As [Wikipedia](https://en.wikipedia.org/wiki/Tenderloin,_San_Francisco#Crime) puts it, this neighborhood has *particularly violent street crime such as robbery and aggravated assault*.  

- **11th Street: Fun but Risky**  
  Located between the **SOMA and Mission** neighborhoods, **11th Street** is home to some of the city’s [most popular clubs](https://www.yelp.com/search?cflt=danceclubs&find_loc=11th+St%2C+San+Francisco%2C+CA+94103). The heat map suggests that while not as dangerous as the Tenderloin, it still has a noticeable crime presence, so stay aware of your surroundings. 

- **Richmond & Presidio: A Safer Alternative**  
  How about enjoying a **laid-back night with craft beers** in a safer setting? Head to **Richmond or Presidio**. These neighborhoods are home to some of San Francisco’s best [microbreweries](https://www.sftravel.com/article/san-francisco-nightlife-neighborhood) and show **significantly lower crime rates** compared to downtown nightlife districts.  

# Bokeh plot
This visualization displays the average number of incidents throughout the year for the two crime categories mentioned, highlighting the individual weeks. The main plot shows daily averages, with weekends highlighted in a light red shade to indicate potential shifts in crime patterns between weekdays and weekends. An interactive time slider below presents the total number of incidents per week, allowing users to adjust the view in the main plot. The legend on the right distinguishes between the two crime categories, providing a clear comparison of their trends over time.

<iframe src="{{ site.baseurl }}/assets/templates/combined_crime_patterns_with_legend.html" frameborder="0" style="height: 550px; width: 100%; min-width: 800px"></iframe>

The plot underscores a clear weekend dependency for both assault and malicious mischief, with crime levels for both categories consistently spiking on weekends compared to weekdays. This pattern suggests that external factors, such as increased social activity or alcohol consumption, may play a significant role in driving these trends. While the two crime types often rise and fall together, this correlation appears to be a consequence of their shared weekend dependency rather than a direct relationship. Notably, exceptions such as weeks 1, 30, 34, 35, 36, 41, and 50 reveal midweek spikes in assault that are not mirrored by malicious mischief, further emphasizing the independent yet parallel weekend-driven behavior of these crimes. Despite these weekend surges, overall crime levels remain relatively stable, ranging between 17 and 35 incidents per week.

### Notable Time Periods
- **New Year’s Celebrations (Weeks 52 & 1)**
  The transition between these two weeks includes New Year's Eve and New Year's Day, both of which are associated with celebrations that can lead to heightened incidents of assault and vandalism. Here we do see a spike, especally in the end of week 52.

- **Spring Break (Weeks 12–16)**
  Different school districts and colleges schedule their spring breaks at varying times during March and April. This period often sees increased nightlife activity, which could influence crime patterns.

- **Summer & 4th of July (Weeks 26–32)**
  Independence Day (Week 27) is one of the most widely celebrated holidays in the U.S., with large gatherings, fireworks, and alcohol consumption contributing to spikes in crime. More broadly, the summer vacation period (Weeks 26–32) attracts many tourists to San Francisco, leading to increased public activity. Assault incidents rise notably on weekends and Fridays, suggesting a link to social events.

- **Late Summer & Tourism Peaks (Weeks 30, 34–36)**
  These weeks fall within the core of the American summer vacation season. With schools closed and high tourist activity, increased public interactions may contribute to fluctuations in crime rates.

- **Autumn Break (Week 41)**
  Many schools schedule a short break in mid-October, potentially creating crime patterns due to increased leisure time.

- **Halloween (Week 44)**
  Halloween celebrations can contribute to public disturbances and vandalism. Interestingly, while both crime types show a midweek spike, malicious mischief does not increase as much as expected. A dip in crime in the following week suggests that incidents may cluster around Halloween before returning to normal levels.

- **Pre-Holiday Season (Week 50)**
  Crime rates begin to rise again in mid-December, possibly influenced by holiday shopping, social events, and end-of-year festivities.

While crime levels remain relatively stable, they are influenced by social patterns, seasonal events, and major holidays. Assault and malicious mischief generally follow the same trends, with weekend spikes and holiday-related fluctuations standing out as key factors.

# Contributions

We worked together on the exercises during class and then collaborated closely, contributing equally to the assignment. All student have worked on all parts of the assignment, but each student had parts that they were responsible for, this can be seen below. 

| Student              | Main Responsibility           |
| ---------------------|-------------------------------|
| Ludovico Cappellato  | Third step                    |
| Maja Klerk           | Second step                   |
| Francesco Balducci   | Website, Introduction, First step |