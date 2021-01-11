---
layout: post
title: The Hospital Lab
subtitle: Due December 6, 2020
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [lab]
---

# The Hospital Lab!

#### Which county has the most hospital beds per person (regardless of bed type)?
New York

#### How to Create Hospital.csv (getCSV.py)
##### Step One: The Setup
1. I imported requests and csv in order to use csv and requests commands.
2. I established the url and key to the hospital API.
![Step One](https://imgur.com/ZfAbLh2.jpg)

##### Step Two: The Query Function
1. In the query function, an id is given, and a query is generated.
2. What lines 10-18 mean:
    - `payload = {}` this establishes the payload, including a key, which is the key variable, and an id, which is the id parameter.
    - `response = requests.get(url, params=payload)` creates the variable response, which is the requests of the API.
    - `return response` the variable response, or requests.get is returned by the end of the method.
![Step Two](https://imgur.com/rqa7K6K.jpg)

##### Step Three: The While Loop
1. A while loop is needed in order to iterate through the query method in order to figure out how many ids there are.
2. What lines 23-30 mean:
    - `x = 0` creates the variable x, which starts at 0, and then will be used in the while loop.
    - `results = query(x)` sets the variable results, which is just the query method with the parameter x, which starts off at 0.
    - The while loop
        - `while results.status_code == requests.codes.ok:` while there is not an error with the API requests.
        - `results = query(x)` sets the variable results, which is just the query method with the parameter x, which starts off at 0.
        - `data = results.text` data is set to represent the text of that specific id
        - `print(data)` prints out data, the text for a specific id.
        - `x +=1` adds 1 to x, starting at 0, and continues to iterate until there is an error, which lets us known when we should stop.

    - This is the first file needed for the lab. In my terminal, I piped the final returned result, a bunch of text for each id, into a csv file, hospital.csv.
![Step Three](https://imgur.com/KCzfYZZ.jpg)
 
#### Evaluating Hospital.csv (hospital.py)
##### Step One: The Setup 
1, I imported csv in order to use csv commands.
2. I created a blank dictionary named counties.
![Step One](https://imgur.com/aeBvUff.jpg)

##### Step Two: Reading Hospital.csv
1. Used to add to the counties dictionary
2. What lines 8-37 mean:
    - `with open("hospital.csv", "r") as f:` allows us to read hosptial.csv.
    - `data = csv.DictReader(f)` sets the variable data, which will use DictReader to analyze the csv file.
    - `for row in data:` iterates through each row in data
    - `county = row["county"]` sets the variable county to represent row['county'], or each county in the csv file
    - `if county not in counties:` if the variable county is not already in the dictionary counties,
        - `counties[county] = []` add that county as a key to counties, giving it a blank list as its value

    - Standarizing so the measures are all equal to 1000HAB, changing the beds so the beds are proportional to 1000HAB:
        - `if row["measure"] == '500HAB':` if the measure from the csv file is 500HAB,
            - `row["measure"] = '1000HAB'` change the measure to 1000HAB,
            - `beds = float(row["beds"])*2` create the variable beds which is row['beds'] * 2 in order to make the beds proportional to the measure,
            - `bed_count = (float(row["population"])/1000)*beds` create the variable bed_Count, which is just the population divided by 1000 mutipled by the variable beds,
            - `counties[county].append(int(bed_count))` append the variable bed_count into the blank list value into the key county in the dictionary counties.
        - `if row["measure"] == '2000HAB':` if the measure from the csv file is 2000HAB,
            - `row["measure"] = '1000HAB'` change the measure to 1000HAB,
            - `beds = float(row["beds"])/2` create the variable beds which is row['beds'] / 2 in order to make the beds proportional to the measure,
            - `bed_count = (float(row["population"])/1000)*beds` create the variable bed_Count, which is just the population divided by 1000 mutipled by the variable beds,
            - `counties[county].append(int(bed_count))` append the variable bed_count into the blank list value into the key county in the dictionary counties.
        - `if row["measure"] == '1000HAB':` if the measure from the csv file is 1000HAB,
            - `row["measure"] = '1000HAB'` the measure stays the same,
            - `beds = float(row["beds"])` create the variable beds which is row['beds'] in order to keep the beds proportional to the measure,
            - `bed_count = (float(row["population"])/1000)*beds` create the variable bed_Count, which is just the population divided by 1000 mutipled by the variable beds,
            - `counties[county].append(int(bed_count))` append the variable bed_count into the blank list value into the key county in the dictionary counties.


![Step Two](https://imgur.com/3ZwgsPX.jpg)

##### Step Three: Returning the key of the max value in a dictionary
1. What lines 40-43 mean:
    - `maxKey = max(counties, key=counties.get)` creates the variable maxKey, which is the return value of the max function, which the parameters of the dictionary counties.
    - `print("The county that has the most hospital beds per person, regardless of bed type, is {}".format(maxKey))` prints out a sentecne that uses maxKey to let the user know the county with the most hospital beds per person.
![Step Three](https://imgur.com/3dDdSqM.jpg)

##### My Struggles 
It was a challenge to create getCSV.py. I had an idea in my mind how it should work, but I was confused on what the psuedo or real code would look like. I had first established my payload and response, but after meeting with Mr. Lee, I realized I should have a while loop that iterates through a query method. After this revelation, it was easy for me to finish the first file. Then, I was confused on how to pipe the returns from my while loop into a csv file. Mr. Lee had told me that it was easy, all we had to do was use the following format: python3 fileName > newFileName in order to pipe the returns from one file into a new one. I used this in order to pipe the returns of getCSV.py into hospital.csv. After making the csv, I had a good idea how I would analyze the csv file in hospital.py. Similar to my approach in the Iris Lab, I would use DictReader to add data to a blank dictionary. It was easy for me to add each county as a key to my dictionary, while appending the bed count to a blank list value in each key. A struggle I encountered on the second file was how to find the max value of the dictionary, and the grab the key attached to that value. I was able to find a great source online from [GeeksforGeek](https://www.geeksforgeeks.org/python-get-key-with-maximum-value-in-dictionary/) that showed me how to do it. After completeing hospital.py I found out that New York had the most beds per person!

##### What I Learned 
1. How to Pipe Files
2. How to Standardize
3. How to return the key of the max value in a dictionary
