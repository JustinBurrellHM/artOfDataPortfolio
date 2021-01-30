---
layout: post
title: The Hospital Lab
subtitle: Due January 31, 2021
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [lab]
---
# The Distribution Lab!
#### Introduction
While looking at the different csv options to pick from for this lab, country_vaccinations.csv was the most interesting since it is reflexive on the world today. As it has almost been a year since the surge of COVID-19, the world is now scrambbling to distribute the vaccine. With ambitious goals to end the pandemic by the end of the year, I hypothesize that "developed countries" have more total vacciantions, since they have more money to buy and distribute vaccines to their citizens. In this lab, I will be looking at two categorical variables: country and vaccine type, and one quantitative variable: total vaccinations. Is there a correlation between country and total vaccinations? Is there a correlation between vaccine type and total vaccinations? Is there a correlation between country and vaccine type? We will answer these questions during this lab. Let's begin!

#### The Code
1. Importing python libraries (lines 1-5):
    - `import pandas as pd` allows me to use pandas libraries.
    - `import matplotlib.pyplot as plt` allows me to use plots libraries.
    - `import seaborn as sns` allows me to use seaborn libraries
    - `import csv` allows me to use csv libraries

![Step One](https://imgur.com/xPr6eFT.jpg)

2. Creating the countries dictionary (lines 10-28):
    - `with open("country_vaccinations.csv", "r") as f:` allows country_vaccinations.csv to be analyzed.
    - `data = csv.DictReader(f)` sets data as sv.DictReader(f), making it easier to use as I code.
    - `for row in data:` for each row in the csv file:
        - `country = row["country"]` creates the variable country, which represents the country key in the csv file. 
        - `if row["daily_vaccinations"] == '':` standardizes, if there is an empty string in the daily vaccinations key of the csv file:
            - `row["daily_vaccinations"] = '0'` change the empty string to 0, which allows me to convert the daily vaccinations' strings to floats without errors.
        - `if country not in countries:` if a country is not in the countries dictionary:
            - `x = 0` sets the variable x as 0.
            - `x += float(row["daily_vaccinations"])` adds the float verison of (row["daily_vaccinations"]) to the variable x. This is the first daily vaccination for the first occurance of each country.
            - `countries[country] = {'Vaccine': row["vaccines"], 'Total Vaccinations': x}` in the key dictionary country in my dicionary countries, creates two dictionary key values: Vaccine, which include row["vaccines"], or the name of the vaccine used, and Total Vaccinations, which is x.
        - `else:` if the country is already a key in the dictionary countries:
            - `countries[country]["Total Vaccinations"] += float(row['daily_vaccinations'])` continue to add the float verisons of (row["daily_vaccinations"]) to `countries[country]["Total Vaccinations"] until we move on to the next country. 

After this, we should have the dictionary countries. In countries, there will be a dictionary key for each country in the csv. In each of those dictionary keys, there will be two dicionary keys: Vaccine, which includes the vaccine type, and Total Vaccinations, which after this for loop should include the total daily vaccinations from each day for each country. This dicionary will be used to not only find the max and min values of the dictionary to answer the original questions of my research.

![Step Two](https://imgur.com/y4TzZxy.jpg)

3. Finding the max and min values (lines 30-45):
    - `maxCountry = max(countries, key=lambda country: countries[country]["Total Vaccinations"])` creates the variable maxCountry, which is the key of the max value from  the Total Vaccination of each country. This returns the name of the country.
    - `maxCountryVaccine = countries[maxCountry]["Vaccine"]` creates the variable maxCountryVaccine, which is countries[maxCountry]["Vaccine"], or the vaccine type of the max value's country.
    - `maxCountryTotal = countries[maxCountry]["Total Vaccinations"]` creates the variable maxCountryTotal, which is countries[maxCountry]["Total Vaccinations"], or the number of total vaccinations of the max value's country.

    - `minCountry = min(countries, key=lambda country: countries[country]["Total Vaccinations"])` creates the variable minCountry, which is the key of the min value from  the Total Vaccination of each country. This returns the name of the country.
    - `minCountryVaccine = countries[minCountry]["Vaccine"]` creates the variable minCountryVaccine, which is countries[minCountry]["Vaccine"], or the vaccine type of the min value's country.
    - `minCountryTotal = countries[minCountry]["Total Vaccinations"]` creates the variable minCountryTotal, which is countries[minCountry]["Total Vaccinations"], or the number of total vaccinations of the min value's country.

    - `print("The country with the highest total number of vaccinations is {}, which their vaccines distributed by {}, and a vaccination total of {}. The country with the lowest total number of vaccinations is {}, which their vaccines distributed by {}, and a vaccination total of {}".format(maxCountry, maxCountryVaccine, maxCountryTotal, minCountry, minCountryVaccine, minCountryTotal))` prints out the string in a clear way, which allows me to easily find the answers to some of my questions.

After running the file, we get the following text: The country with the highest total number of vaccinations is United States, which their vaccines distributed by Moderna, Pfizer/BioNTech, and a vaccination total of 16742505.0. The country with the lowest total number of vaccinations is Kuwait, which their vaccines distributed by Pfizer/BioNTech, and a vaccination total of 0.0. From this, we have the answers to some of our questions.
![Step Three](https://imgur.com/S5d5uLM.jpg)

4. Creating the country chart (lines 47-55):
    - `countrydf = pd.DataFrame.from_dict(countries, orient = 'index')` sets countrydf as the dataframe from the countries dictionary, and organizing my dataframe an index.
    - `countrydf["Country"] = countrydf.index` this sets countrydf["Country"], or each country name, as the index of my dataframe.
    - `_data = countrydf` sets _data as countrydf, so it could be easier to use later to generate a chart of the dataframe.
    - `graph = sns.barplot(data=_data, x='Country', y='Total Vaccinations', hue="Vaccine")` sets graph as a barplot, where the data is from _data, the x axis contains the country names, the y-axis contains the total vaccinations, and each country is differentiated by vaccine type.
    - `plt.xticks(rotation = 60)` this turns the country names on the x axis by 60 degrees, so it can be easier to see the names on the x-axis (there are dozens of them).
    - `plt.xlabel("Country")` this labels the x-axis as Country.
    - `plt.ylabel("Total Vaccinations")` this labels the y-axis as Total Vaccinations.
    - `plt.show()` this shows the generated graph.

![Step Four](https://imgur.com/zomSHHe.jpg)

By doing this, this allows me to visulaize the difference betweeen the total vaccinations for each country, and differentiate them based by vaccine type. This is the generated chart from this code snippet:
![Chart One](https://imgur.com/jED27xm.jpg)

5. Creating the vaccine chart (lines 57-65):
    - `vaccinedf = countrydf.groupby(['Vaccine']).sum()` sets vaccinedf as the dataframe countrydf, however, the dataframe is grouped by vaccine type, and the sum of total vaccinations for each vaccine type is used to create the dataframe.
    - `vaccinedf['Vaccine'] = vaccinedf.index` this sets vaccinedf['Vaccine'], or the name of each vaccine, as the index of my dataframe.
    - `_data2 = vaccinedf` sets _data2 as vaccinedf, so it could be easier to use later to generate a chart of the dataframe.
    - `graph2 = sns.barplot(data=_data2, x='Vaccine', y='Total Vaccinations', hue="Vaccine")` sets graph2 as a barplot, where the data is from _data2, the x axis contains the vaccine names, the y-axis contains the total vaccinations, and each x-axis tick is differentiated by vaccine type.
    - `plt.xticks(rotation = 30)` this turns the vaccine names on the x axis by 30 degrees, so it can be easier to see the names on the x-axis
    - `plt.xlabel("Vaccine Type")` this labels the x-axis as Vaccine Type.
    - `plt.ylabel("Total Vaccinations")` this labels the y-axis as Total Vaccinations.
    - `plt.show()` this shows the generated graph.

![Step Five](https://imgur.com/NPgsyGk.jpg)

By doing this, this allows me to visulaize the difference betweeen the total vaccinations for each vaccine type. Because I did not need the exact numbers in order to determine the most popular vaccine type, I only created this chart rather than use the countries dictionary to find the min and max values for each vaccine type. This is the generated chart from this code snippet:
![Chart Two](https://imgur.com/15skAgx.jpg)

#### 1. Which country has the most total vaccinations? What company is distributing vaccines for them?
The country with the highest total number of vaccinations is the United States, which their vaccines distributed by Moderna, Pfizer/BioNTech, and a vaccination total of 16742505.0.

#### 2. Which country has the least total vaccinations? What company is distributing vaccines for them?
The country with the lowest total number of vaccinations is Kuwait, which their vaccines distributed by Pfizer/BioNTech, and a vaccination total of 0.0.


#### 3. Which company is distributing the most vaccines? Which company is distirbuting the least vaccines?
Modern, Pfizer/BioNTech is distributing the most vaccines, while Sinopharm is distributing the least amount of vaccines.

#### 4. Is there a correlation between a country, its vaccine type and its total vaccinations, or are there other factors that impact a country's total vaccinations?
After analyzing the data, I think there is not a correlation between vaccine type and total vaccinations, and even a country and vaccine type. Rather, my original hypothesis that there is a correlation between a country's wealth and its total vaccinations is correct. When looking at the first graph, you'll notice that the United States leads the charge in total vaccinations, followed by China and the UK. According to stats from [investopedia.com](https://www.investopedia.com/insights/worlds-top-economies/),the United States currently has the highest nominal GDP at $21.43 trillion followed by China at $14.34 trillion. Also, as of January 27, 2021, according to [statista.com](https://www.statista.com/chart/21467/coutries-most-covid-19-cases/), the United States has the most COVID-19 cases at 25,445,091, followed by India at 10,689,527, and then Brazil at 8,933,356. Yes, the United States leads in GDP and COVID-19 cases, but that has to do with former President Trump's incompetence in originally dealing with the virus than the correlations we are evaluating, and also American citizen's total disregard of social distancing regulations. Even though India is number two in most COVID-19 cases, it is on of the lower countries in terms of total vaccinations. There is no coincidence that the United States and China lead in both GDP and total vaccinations. The simple answer to that is money. 

#### Struggles
During this lab, I am proud to say I did not struggle with anything persay, even though that is normally a common thing for me in these labs. I knew what I wanted to do, and executed. The biggest concern for me during this lab was finding out which type of graph I should use to visualize my dataframes. Originally, I thought scatter plots were ideal, since they could be easily hued. However, I realized I should use barplots, since they are ideal for two categorical variables (country and vaccine type) and one quantitative variable (total vaccinations). For my bar graph, I put the quantitative variable on the y-axis, one categorical variable on the x-axis, and use hues to differentiate my x-axis by another categorical variable. Other than a few questions for Mr. Lee during class time or during office hours, this lab was no problem!

#### Conclusion
In conclusion, I learned how to use dictionaries to create dataframes that can then be plotted to create charts. I went with the dictionaries route since it was something I had mastered in previous labs. Ultimately, there was a correlation between a country's wealth and its total vaccinations. If we as a society want to move past the pandemic, all countries have to have access to the vaccines, not just wealthy countries. I really enjoyed this lab, I loved having autonomy over my own lab. It's really cool to see all the things we've covered in the first semester come together, and I look forward to more creative labs throughout the second semester!




