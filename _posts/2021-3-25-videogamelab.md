---
layout: post
title: The Video Game Lab
subtitle: Due March 14, 2021
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [lab]
---
#### Introduction
While searching for databases, I wanted to find one that involves some of my interests. I attempted to find a basketball or real estate csv, however, I eventually found a [database](https://www.kaggle.com/gregorut/videogamesales
) from kaggle.com about Video Game Sales. From spending hours trying to get Pokemon with perfect IVs, to spending hours in Terrorist Hunt on Rainbow Six Siege to improve my aim, I have always had a passion for gaming. I have played the DS, DSI, Wii, Wii U, 3DS, Xbox, Xbox 360, and the Xbox One. After quickly reading the documentation for the database, it is really interesting to see how the data about popular games and their success in sales. This database was made my Gregory Smith. This csv includes the following:
- Rank - Ranking of overall sales

- Name - The games name

- Platform - Platform of the games release (i.e. PC,PS4, etc.)

- Year - Year of the game's release

- Genre - Genre of the game

- Publisher - Publisher of the game

- NA_Sales - Sales in North America (in millions)

- EU_Sales - Sales in Europe (in millions)

- JP_Sales - Sales in Japan (in millions)

- Other_Sales - Sales in the rest of the world (in millions)

- Global_Sales - Total worldwide sales (in millions)

Even though this database is great, inclduing over 16,000 unique entries, it is missing what some may say are critical information. For example, they should specify the sales from Africa, Asia, Austrila, and South America. Why are these continents categorized as "Other_Sales?" If they were specified, we could analyze the sales of each continent. Since it does not include the PS4 and Xbox One, PS5, and Xbox X, the data is skewed in favor of Nintendo games. Becasue Ninetendo dominated video games from 1985-2010, their platforms seem more success than they are in hindsight. By the end of the lab, I plan to continue to understand the fundamentals of Altair. Also, I want to learn how to evaluate categorical and quantitative variables. Let's get started!



#### The Setup
In order to begin our analysis, I must first gain access to the libraries we will use. After importing panadas, altair, and squarify libraries, established data as a database for vgsales.csv.


```
import pandas as pd
import altair as alt
```


```
csv = "vgsales.csv" #csv is the string of the csv file
og_database = pd.read_csv(csv) #declares og_database as the dataframe that is generated from the csv variable
```

#### Genre
I want to see how genre effects sales. Do certain genres have more success in specific regions? To begin I must create visualizations in order to prove my results.


```
pd.set_option('display.max_columns', None) #this ensures that when a database is printed every column is printed
database = og_database.drop(columns=["Rank", "Year", "Global_Sales"]) #creates database as the dataframe without the Rank, Year, and Global_Sales colmuns
sum1 = (database.groupby("Genre").sum()).reset_index() #creates sum1 as a dataframe of database grouped by genre with their sum values, followed by reset_index() in order to allow the dataframe to be read properly

genre_lf = sum1.melt("Genre", var_name="Region", value_name="Sales")# Convert csv from wide-form to long-form
```


```
#Generate Visualization
alt.Chart(genre_lf).mark_bar().encode( #marks that are bars
    #channels
    x="Region:N", 
    y="Sales:Q",
    tooltip=["Region", "Genre", "Sales:Q"],
    column = "Genre:N"
)
```





<div id="altair-viz-79e753c75afb44bfa1eea821ebfaaf9e"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-79e753c75afb44bfa1eea821ebfaaf9e") {
      outputDiv = document.getElementById("altair-viz-79e753c75afb44bfa1eea821ebfaaf9e");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "data": {"name": "data-96a40b2e834db1055f93d304d481b8ab"}, "mark": "bar", "encoding": {"column": {"type": "nominal", "field": "Genre"}, "tooltip": [{"type": "nominal", "field": "Region"}, {"type": "nominal", "field": "Genre"}, {"type": "quantitative", "field": "Sales"}], "x": {"type": "nominal", "field": "Region"}, "y": {"type": "quantitative", "field": "Sales"}}, "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-96a40b2e834db1055f93d304d481b8ab": [{"Genre": "Action", "Region": "NA_Sales", "Sales": 877.8299999999916}, {"Genre": "Adventure", "Region": "NA_Sales", "Sales": 105.79999999999998}, {"Genre": "Fighting", "Region": "NA_Sales", "Sales": 223.59000000000017}, {"Genre": "Misc", "Region": "NA_Sales", "Sales": 410.23999999999904}, {"Genre": "Platform", "Region": "NA_Sales", "Sales": 447.0499999999991}, {"Genre": "Puzzle", "Region": "NA_Sales", "Sales": 123.78000000000009}, {"Genre": "Racing", "Region": "NA_Sales", "Sales": 359.41999999999774}, {"Genre": "Role-Playing", "Region": "NA_Sales", "Sales": 327.279999999999}, {"Genre": "Shooter", "Region": "NA_Sales", "Sales": 582.599999999995}, {"Genre": "Simulation", "Region": "NA_Sales", "Sales": 183.31000000000068}, {"Genre": "Sports", "Region": "NA_Sales", "Sales": 683.3499999999967}, {"Genre": "Strategy", "Region": "NA_Sales", "Sales": 68.70000000000019}, {"Genre": "Action", "Region": "EU_Sales", "Sales": 524.9999999999854}, {"Genre": "Adventure", "Region": "EU_Sales", "Sales": 64.13000000000008}, {"Genre": "Fighting", "Region": "EU_Sales", "Sales": 101.32000000000025}, {"Genre": "Misc", "Region": "EU_Sales", "Sales": 215.98000000000036}, {"Genre": "Platform", "Region": "EU_Sales", "Sales": 201.63000000000017}, {"Genre": "Puzzle", "Region": "EU_Sales", "Sales": 50.77999999999998}, {"Genre": "Racing", "Region": "EU_Sales", "Sales": 238.39000000000024}, {"Genre": "Role-Playing", "Region": "EU_Sales", "Sales": 188.06000000000031}, {"Genre": "Shooter", "Region": "EU_Sales", "Sales": 313.2699999999967}, {"Genre": "Simulation", "Region": "EU_Sales", "Sales": 113.3800000000002}, {"Genre": "Sports", "Region": "EU_Sales", "Sales": 376.84999999999457}, {"Genre": "Strategy", "Region": "EU_Sales", "Sales": 45.34000000000005}, {"Genre": "Action", "Region": "JP_Sales", "Sales": 159.95000000000087}, {"Genre": "Adventure", "Region": "JP_Sales", "Sales": 52.0700000000003}, {"Genre": "Fighting", "Region": "JP_Sales", "Sales": 87.35000000000014}, {"Genre": "Misc", "Region": "JP_Sales", "Sales": 107.75999999999995}, {"Genre": "Platform", "Region": "JP_Sales", "Sales": 130.77000000000012}, {"Genre": "Puzzle", "Region": "JP_Sales", "Sales": 57.30999999999997}, {"Genre": "Racing", "Region": "JP_Sales", "Sales": 56.69000000000002}, {"Genre": "Role-Playing", "Region": "JP_Sales", "Sales": 352.3099999999979}, {"Genre": "Shooter", "Region": "JP_Sales", "Sales": 38.28000000000007}, {"Genre": "Simulation", "Region": "JP_Sales", "Sales": 63.70000000000007}, {"Genre": "Sports", "Region": "JP_Sales", "Sales": 135.3700000000004}, {"Genre": "Strategy", "Region": "JP_Sales", "Sales": 49.46000000000003}, {"Genre": "Action", "Region": "Other_Sales", "Sales": 187.3799999999972}, {"Genre": "Adventure", "Region": "Other_Sales", "Sales": 16.810000000000024}, {"Genre": "Fighting", "Region": "Other_Sales", "Sales": 36.67999999999998}, {"Genre": "Misc", "Region": "Other_Sales", "Sales": 75.32000000000136}, {"Genre": "Platform", "Region": "Other_Sales", "Sales": 51.589999999999776}, {"Genre": "Puzzle", "Region": "Other_Sales", "Sales": 12.549999999999935}, {"Genre": "Racing", "Region": "Other_Sales", "Sales": 77.27000000000116}, {"Genre": "Role-Playing", "Region": "Other_Sales", "Sales": 59.60999999999999}, {"Genre": "Shooter", "Region": "Other_Sales", "Sales": 102.69000000000112}, {"Genre": "Simulation", "Region": "Other_Sales", "Sales": 31.520000000000294}, {"Genre": "Sports", "Region": "Other_Sales", "Sales": 134.96999999999758}, {"Genre": "Strategy", "Region": "Other_Sales", "Sales": 11.359999999999932}]}}, {"mode": "vega-lite"});
</script>



The most notable part of this visualization is North America's sales. In every genre except for RPGs, North Americans have consumed the most video games. I think this is because of the spike in video game consumption by American children. The most popular European genre is Action, the most famous Japanese genre is RPGs, the most popular North American genre is Action, while the most popular genre from other countries is Action. In total, the most popular genre is Action, while the least popular genre is Strategy. I decided to use a group side-by-side bar chart because it best compares the different genres. The two variables compared in the visualization is the categorical variable Genre and the quantative variable Sales. The marks are bars, while the channels are Sales, Region, EU, JP, NA, and Other Sales. I created 12 groups of side-side bar charts, each having data for EU, JP, NA, and Other Sales. With the use of tooltips, users can easily compare the Sales of each section. With this layout, all the needed information is displayed without it being a burden to interpret the data!

#### Platform
Next, text I want to see how platform effects sales. Do certain platforms have more success in specific regions? To begin I must create visualizations in order to prove my results.


```
sum2 = (database.groupby("Platform").sum()).reset_index() #creates sum2 as a dataframe of database grouped by platform with their sum values, followed by reset_index() in order to allow the dataframe to be read properly
# print(sum2) 

platform_lf = sum2.melt("Platform", var_name="Region", value_name="Sales")# Convert csc from wide-form to long-form
```


```
#Generate Visualization
alt.Chart(platform_lf).mark_bar().encode( #marks that are bars
    #channels
    x="Region:N",
    y="Sales:Q",
    tooltip=["Region", "Platform", "Sales:Q"],
    column = "Platform:N"
)
```





<div id="altair-viz-a0d2da7f435048608d6d25142c6123e4"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-a0d2da7f435048608d6d25142c6123e4") {
      outputDiv = document.getElementById("altair-viz-a0d2da7f435048608d6d25142c6123e4");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "data": {"name": "data-c6afae2770b6abe57717b4886395a714"}, "mark": "bar", "encoding": {"column": {"type": "nominal", "field": "Platform"}, "tooltip": [{"type": "nominal", "field": "Region"}, {"type": "nominal", "field": "Platform"}, {"type": "quantitative", "field": "Sales"}], "x": {"type": "nominal", "field": "Region"}, "y": {"type": "quantitative", "field": "Sales"}}, "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-c6afae2770b6abe57717b4886395a714": [{"Platform": "2600", "Region": "NA_Sales", "Sales": 90.59999999999992}, {"Platform": "3DO", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "3DS", "Region": "NA_Sales", "Sales": 78.86999999999996}, {"Platform": "DC", "Region": "NA_Sales", "Sales": 5.43}, {"Platform": "DS", "Region": "NA_Sales", "Sales": 390.7099999999977}, {"Platform": "GB", "Region": "NA_Sales", "Sales": 114.32000000000001}, {"Platform": "GBA", "Region": "NA_Sales", "Sales": 187.54000000000033}, {"Platform": "GC", "Region": "NA_Sales", "Sales": 133.46000000000004}, {"Platform": "GEN", "Region": "NA_Sales", "Sales": 19.27}, {"Platform": "GG", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "N64", "Region": "NA_Sales", "Sales": 139.02000000000015}, {"Platform": "NES", "Region": "NA_Sales", "Sales": 125.94000000000005}, {"Platform": "NG", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "PC", "Region": "NA_Sales", "Sales": 93.2800000000005}, {"Platform": "PCFX", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "PS", "Region": "NA_Sales", "Sales": 336.509999999998}, {"Platform": "PS2", "Region": "NA_Sales", "Sales": 583.8399999999925}, {"Platform": "PS3", "Region": "NA_Sales", "Sales": 392.2599999999998}, {"Platform": "PS4", "Region": "NA_Sales", "Sales": 96.79999999999998}, {"Platform": "PSP", "Region": "NA_Sales", "Sales": 108.98999999999975}, {"Platform": "PSV", "Region": "NA_Sales", "Sales": 16.200000000000006}, {"Platform": "SAT", "Region": "NA_Sales", "Sales": 0.7200000000000001}, {"Platform": "SCD", "Region": "NA_Sales", "Sales": 1.0}, {"Platform": "SNES", "Region": "NA_Sales", "Sales": 61.22999999999998}, {"Platform": "TG16", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "WS", "Region": "NA_Sales", "Sales": 0.0}, {"Platform": "Wii", "Region": "NA_Sales", "Sales": 507.7099999999991}, {"Platform": "WiiU", "Region": "NA_Sales", "Sales": 38.31999999999999}, {"Platform": "X360", "Region": "NA_Sales", "Sales": 601.0499999999992}, {"Platform": "XB", "Region": "NA_Sales", "Sales": 186.6900000000008}, {"Platform": "XOne", "Region": "NA_Sales", "Sales": 83.19000000000003}, {"Platform": "2600", "Region": "EU_Sales", "Sales": 5.46999999999998}, {"Platform": "3DO", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "3DS", "Region": "EU_Sales", "Sales": 58.52000000000003}, {"Platform": "DC", "Region": "EU_Sales", "Sales": 1.6900000000000002}, {"Platform": "DS", "Region": "EU_Sales", "Sales": 194.64999999999938}, {"Platform": "GB", "Region": "EU_Sales", "Sales": 47.82}, {"Platform": "GBA", "Region": "EU_Sales", "Sales": 75.25000000000061}, {"Platform": "GC", "Region": "EU_Sales", "Sales": 38.71000000000004}, {"Platform": "GEN", "Region": "EU_Sales", "Sales": 5.5200000000000005}, {"Platform": "GG", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "N64", "Region": "EU_Sales", "Sales": 41.060000000000045}, {"Platform": "NES", "Region": "EU_Sales", "Sales": 21.150000000000006}, {"Platform": "NG", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "PC", "Region": "EU_Sales", "Sales": 139.68000000000015}, {"Platform": "PCFX", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "PS", "Region": "EU_Sales", "Sales": 213.60000000000065}, {"Platform": "PS2", "Region": "EU_Sales", "Sales": 339.2899999999957}, {"Platform": "PS3", "Region": "EU_Sales", "Sales": 343.70999999999805}, {"Platform": "PS4", "Region": "EU_Sales", "Sales": 123.69999999999995}, {"Platform": "PSP", "Region": "EU_Sales", "Sales": 68.25000000000016}, {"Platform": "PSV", "Region": "EU_Sales", "Sales": 16.330000000000005}, {"Platform": "SAT", "Region": "EU_Sales", "Sales": 0.54}, {"Platform": "SCD", "Region": "EU_Sales", "Sales": 0.36}, {"Platform": "SNES", "Region": "EU_Sales", "Sales": 19.040000000000013}, {"Platform": "TG16", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "WS", "Region": "EU_Sales", "Sales": 0.0}, {"Platform": "Wii", "Region": "EU_Sales", "Sales": 268.3799999999979}, {"Platform": "WiiU", "Region": "EU_Sales", "Sales": 24.230000000000015}, {"Platform": "X360", "Region": "EU_Sales", "Sales": 280.5799999999964}, {"Platform": "XB", "Region": "EU_Sales", "Sales": 60.95000000000009}, {"Platform": "XOne", "Region": "EU_Sales", "Sales": 45.650000000000055}, {"Platform": "2600", "Region": "JP_Sales", "Sales": 0.0}, {"Platform": "3DO", "Region": "JP_Sales", "Sales": 0.1}, {"Platform": "3DS", "Region": "JP_Sales", "Sales": 97.35000000000002}, {"Platform": "DC", "Region": "JP_Sales", "Sales": 8.56}, {"Platform": "DS", "Region": "JP_Sales", "Sales": 175.57000000000048}, {"Platform": "GB", "Region": "JP_Sales", "Sales": 85.12000000000002}, {"Platform": "GBA", "Region": "JP_Sales", "Sales": 47.330000000000005}, {"Platform": "GC", "Region": "JP_Sales", "Sales": 21.580000000000002}, {"Platform": "GEN", "Region": "JP_Sales", "Sales": 2.669999999999999}, {"Platform": "GG", "Region": "JP_Sales", "Sales": 0.04}, {"Platform": "N64", "Region": "JP_Sales", "Sales": 34.21999999999999}, {"Platform": "NES", "Region": "JP_Sales", "Sales": 98.64999999999996}, {"Platform": "NG", "Region": "JP_Sales", "Sales": 1.4400000000000004}, {"Platform": "PC", "Region": "JP_Sales", "Sales": 0.16999999999999998}, {"Platform": "PCFX", "Region": "JP_Sales", "Sales": 0.03}, {"Platform": "PS", "Region": "JP_Sales", "Sales": 139.82000000000002}, {"Platform": "PS2", "Region": "JP_Sales", "Sales": 139.20000000000064}, {"Platform": "PS3", "Region": "JP_Sales", "Sales": 79.99000000000005}, {"Platform": "PS4", "Region": "JP_Sales", "Sales": 14.299999999999976}, {"Platform": "PSP", "Region": "JP_Sales", "Sales": 76.7900000000002}, {"Platform": "PSV", "Region": "JP_Sales", "Sales": 20.960000000000083}, {"Platform": "SAT", "Region": "JP_Sales", "Sales": 32.260000000000005}, {"Platform": "SCD", "Region": "JP_Sales", "Sales": 0.45}, {"Platform": "SNES", "Region": "JP_Sales", "Sales": 116.54999999999997}, {"Platform": "TG16", "Region": "JP_Sales", "Sales": 0.16}, {"Platform": "WS", "Region": "JP_Sales", "Sales": 1.42}, {"Platform": "Wii", "Region": "JP_Sales", "Sales": 69.35000000000001}, {"Platform": "WiiU", "Region": "JP_Sales", "Sales": 12.789999999999994}, {"Platform": "X360", "Region": "JP_Sales", "Sales": 12.429999999999923}, {"Platform": "XB", "Region": "JP_Sales", "Sales": 1.3800000000000006}, {"Platform": "XOne", "Region": "JP_Sales", "Sales": 0.34000000000000014}, {"Platform": "2600", "Region": "Other_Sales", "Sales": 0.9100000000000006}, {"Platform": "3DO", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "3DS", "Region": "Other_Sales", "Sales": 12.629999999999946}, {"Platform": "DC", "Region": "Other_Sales", "Sales": 0.27}, {"Platform": "DS", "Region": "Other_Sales", "Sales": 60.52999999999964}, {"Platform": "GB", "Region": "Other_Sales", "Sales": 8.199999999999998}, {"Platform": "GBA", "Region": "Other_Sales", "Sales": 7.729999999999941}, {"Platform": "GC", "Region": "Other_Sales", "Sales": 5.179999999999967}, {"Platform": "GEN", "Region": "Other_Sales", "Sales": 0.8900000000000001}, {"Platform": "GG", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "N64", "Region": "Other_Sales", "Sales": 4.37999999999999}, {"Platform": "NES", "Region": "Other_Sales", "Sales": 5.309999999999989}, {"Platform": "NG", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "PC", "Region": "Other_Sales", "Sales": 24.86000000000044}, {"Platform": "PCFX", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "PS", "Region": "Other_Sales", "Sales": 40.909999999999926}, {"Platform": "PS2", "Region": "Other_Sales", "Sales": 193.44000000000062}, {"Platform": "PS3", "Region": "Other_Sales", "Sales": 141.92999999999992}, {"Platform": "PS4", "Region": "Other_Sales", "Sales": 43.359999999999935}, {"Platform": "PSP", "Region": "Other_Sales", "Sales": 42.18999999999995}, {"Platform": "PSV", "Region": "Other_Sales", "Sales": 8.449999999999983}, {"Platform": "SAT", "Region": "Other_Sales", "Sales": 0.07}, {"Platform": "SCD", "Region": "Other_Sales", "Sales": 0.05}, {"Platform": "SNES", "Region": "Other_Sales", "Sales": 3.2199999999999975}, {"Platform": "TG16", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "WS", "Region": "Other_Sales", "Sales": 0.0}, {"Platform": "Wii", "Region": "Other_Sales", "Sales": 80.6100000000016}, {"Platform": "WiiU", "Region": "Other_Sales", "Sales": 6.449999999999989}, {"Platform": "X360", "Region": "Other_Sales", "Sales": 85.54000000000137}, {"Platform": "XB", "Region": "Other_Sales", "Sales": 8.71999999999992}, {"Platform": "XOne", "Region": "Other_Sales", "Sales": 11.919999999999972}]}}, {"mode": "vega-lite"});
</script>



The most exciting part of this visualization is the popularity of the PS2, Wii, and Xbox 360. It is crucial to keep in mind that most of the platforms mentioned are Nintendo platforms. I'd want to do further research to see how long each Nintendo console was supported, which would explain why there have been so many Nintendo consoles in the past 25 years. If some Nintendo platforms were unsuccessful, that could be why Nintendo decided to make a new console to regain consumers' interests. When you look at Sony or Mircosoft's platforms, they only have 3-5 platforms mentioned. Why is that? Is it because their platforms consistently get sales? The highest sales are the PS3 sales in North America and the Xbox 360 sales in North America. Sony supported the PS3 for almost 12 years. The only two Nintendo platforms supported for a long time are the DS and Wii; it is not a coincidence that they have been the most commercially successful consoles? In terms of creating the visualizations, I decided to make a grouped side-by-side bar chart. The two variables compared in the visualization is the categorical variable Platform and the quantative variable Sales. The marks are bars, while the channels are Sales, Region, EU, JP, NA, and Other Sales. Each group contains that platform's sales from the four major regions. Even though there are 31 platforms, this layout is still the easiest to interpret. Since there are 31 different platforms, having the side-by-side bar charts next to each other makes it simple to compare each platform's regional sales.

#### Publisher
Then, I want to see how publisher effects sales. Do certain publishers have more success in specific regions? To begin I must create visualizations in order to prove my results.


```
#Create 
database2 = og_database.drop(columns=["Rank", "Year",  "NA_Sales", "EU_Sales", "JP_Sales", "Other_Sales"]) #creates database2 as the dataframe without the Rank, Year, NA_Sales, EU_Sales, JP_Sales, and Other_Sales colmuns
sum3 = (database2.groupby("Publisher").sum()).reset_index() #creates sum3 as a dataframe of database grouped by publisher with their sum values, followed by reset_index() in order to allow the dataframe to be read properly

publisher_lf = sum3.nlargest(30, 'Global_Sales') #Specify top 30
print(publisher_lf)#allows me to see the numbers for the top 30 publishers
```

                                      Publisher  Global_Sales
    359                                Nintendo       1786.56
    138                         Electronic Arts       1110.32
    21                               Activision        727.46
    456             Sony Computer Entertainment        607.50
    525                                 Ubisoft        474.72
    494                    Take-Two Interactive        399.54
    488                                     THQ        340.77
    275            Konami Digital Entertainment        283.64
    446                                    Sega        272.99
    347                      Namco Bandai Games        254.09
    323                  Microsoft Game Studios        245.79
    85                                   Capcom        200.89
    53                                    Atari        157.22
    549  Warner Bros. Interactive Entertainment        153.89
    465                             Square Enix        145.18
    126              Disney Interactive Studios        119.96
    137                       Eidos Interactive         98.98
    288                               LucasArts         87.34
    66                       Bethesda Softworks         82.14
    325                            Midway Games         69.85
    17                    Acclaim Entertainment         64.14
    545                           Vivendi Games         58.21
    466                              SquareSoft         57.65
    6                                 505 Games         55.91
    500                              Tecmo Koei         53.55
    91                              Codemasters         47.87
    542                      Virgin Interactive         43.87
    530                                 Unknown         34.66
    144                        Enix Corporation         33.74
    120                             Deep Silver         25.67



```
alt.Chart(publisher_lf, title= "Publisher").mark_bar().encode( #marks that are bars
    #channels
    x="Publisher:N",
    tooltip=["Publisher","Global_Sales:Q"],
    y="Global_Sales:Q",
)
```





<div id="altair-viz-b9c0cfe4da9c49a5ae5a2c3a6fc6db4c"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-b9c0cfe4da9c49a5ae5a2c3a6fc6db4c") {
      outputDiv = document.getElementById("altair-viz-b9c0cfe4da9c49a5ae5a2c3a6fc6db4c");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "data": {"name": "data-5dc9ec0b6e2d74f37ab6d43f60e33b3b"}, "mark": "bar", "encoding": {"tooltip": [{"type": "nominal", "field": "Publisher"}, {"type": "quantitative", "field": "Global_Sales"}], "x": {"type": "nominal", "field": "Publisher"}, "y": {"type": "quantitative", "field": "Global_Sales"}}, "title": "Publisher", "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-5dc9ec0b6e2d74f37ab6d43f60e33b3b": [{"Publisher": "Nintendo", "Global_Sales": 1786.5599999999981}, {"Publisher": "Electronic Arts", "Global_Sales": 1110.3199999999915}, {"Publisher": "Activision", "Global_Sales": 727.4599999999983}, {"Publisher": "Sony Computer Entertainment", "Global_Sales": 607.4999999999989}, {"Publisher": "Ubisoft", "Global_Sales": 474.71999999999935}, {"Publisher": "Take-Two Interactive", "Global_Sales": 399.5399999999996}, {"Publisher": "THQ", "Global_Sales": 340.7699999999994}, {"Publisher": "Konami Digital Entertainment", "Global_Sales": 283.639999999998}, {"Publisher": "Sega", "Global_Sales": 272.98999999999927}, {"Publisher": "Namco Bandai Games", "Global_Sales": 254.0900000000008}, {"Publisher": "Microsoft Game Studios", "Global_Sales": 245.79000000000005}, {"Publisher": "Capcom", "Global_Sales": 200.89000000000001}, {"Publisher": "Atari", "Global_Sales": 157.22000000000025}, {"Publisher": "Warner Bros. Interactive Entertainment", "Global_Sales": 153.89000000000013}, {"Publisher": "Square Enix", "Global_Sales": 145.18000000000026}, {"Publisher": "Disney Interactive Studios", "Global_Sales": 119.96000000000004}, {"Publisher": "Eidos Interactive", "Global_Sales": 98.97999999999998}, {"Publisher": "LucasArts", "Global_Sales": 87.34000000000003}, {"Publisher": "Bethesda Softworks", "Global_Sales": 82.14000000000003}, {"Publisher": "Midway Games", "Global_Sales": 69.84999999999994}, {"Publisher": "Acclaim Entertainment", "Global_Sales": 64.13999999999997}, {"Publisher": "Vivendi Games", "Global_Sales": 58.21000000000002}, {"Publisher": "SquareSoft", "Global_Sales": 57.65}, {"Publisher": "505 Games", "Global_Sales": 55.91000000000003}, {"Publisher": "Tecmo Koei", "Global_Sales": 53.55000000000003}, {"Publisher": "Codemasters", "Global_Sales": 47.870000000000026}, {"Publisher": "Virgin Interactive", "Global_Sales": 43.87000000000001}, {"Publisher": "Unknown", "Global_Sales": 34.66000000000005}, {"Publisher": "Enix Corporation", "Global_Sales": 33.739999999999974}, {"Publisher": "Deep Silver", "Global_Sales": 25.670000000000005}]}}, {"mode": "vega-lite"});
</script>



Before I created the visualization, I decided to look at the top 30 publishers from the dataset. There were over 500 publishers, and most of them don't have many sales. The top 30 publishers contribute to the majority of sales. With that in mind, by analyzing the top 30 publishers, I can see which publishers are the most relevant in the dataset. Nintendo and Electronic Arts (EA) dominate the dataset, followed by Activision. Nintendo has 1.7 billion sales, EA has 1.1 billion sales, and Activision has 727 million sales. It makes sense that Nintendo dominates the dataset since they have the most platforms. Since they publish the vast majority of their platforms' games, it is expected that they have the most sales. It makes sense that EA has the second-highest sales; they make sports games for most platforms. It is also reasonable that Activision has the third-highest sales; they produce Call of Duty games, arguably the most successful game series ever for multiple platforms.

Interestingly, these three publishers have most of the total sales in this visualization; it shows how consumers than to buy from only a few publishers since they make the best games. In terms of the structure of the visualization, I decided to make a bar chart. The two variables compared in the visualization are the categorical variable Publisher and the quantitative variable Sales. The marks are bars, while the channels are Sales and each publisher name. This visualization was the easiest to make since it is a basic bar chart. Users can easily interpret the data.

#### Is there a correlation between Genre, Platform, and Publisher?
Finally, I want to see if there is a correlation between Genre, Platform, and Publisher. 


```
final = database2.nlargest(100, 'Global_Sales') #Specify top 100 games in terms of Global Sales
```


```
selection = alt.selection_multi(fields=['Publisher']) # A different kind of selection!

species_color = alt.condition(selection,    # Set the color to change depending on a the selection
                              alt.Color("Publisher:N", legend=None),
                              alt.value("lightgray"))

# Create stacked bar chart of platform vs. publisher vs. sales
sales = alt.Chart(final, title="Correlation between Sales, Publisher, and Platform").mark_bar().encode(
    x=alt.X("Platform:N"),
    y=alt.Y("Global_Sales:Q"),
    tooltip=['Publisher', 'Platform', 'Global_Sales'],
    color=species_color
).interactive()

# Create corresponding legend for the visualization
legend = alt.Chart(final).mark_rect().encode(
    y=alt.Y("Publisher:N", axis=alt.Axis(orient="right")),
    color=species_color
).add_selection( # We have to tell the chart to use the selection we've defined
    selection
).interactive()

#combines the two visualizations
sales | legend
```





<div id="altair-viz-4341661cf6554a6e962abaed3edcf90d"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-4341661cf6554a6e962abaed3edcf90d") {
      outputDiv = document.getElementById("altair-viz-4341661cf6554a6e962abaed3edcf90d");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "hconcat": [{"mark": "bar", "encoding": {"color": {"condition": {"type": "nominal", "field": "Publisher", "legend": null, "selection": "selector013"}, "value": "lightgray"}, "tooltip": [{"type": "nominal", "field": "Publisher"}, {"type": "nominal", "field": "Platform"}, {"type": "quantitative", "field": "Global_Sales"}], "x": {"type": "nominal", "field": "Platform"}, "y": {"type": "quantitative", "field": "Global_Sales"}}, "selection": {"selector014": {"type": "interval", "bind": "scales", "encodings": ["x", "y"]}}, "title": "Correlation between Sales, Publisher, and Platform"}, {"mark": "rect", "encoding": {"color": {"condition": {"type": "nominal", "field": "Publisher", "legend": null, "selection": "selector013"}, "value": "lightgray"}, "y": {"type": "nominal", "axis": {"orient": "right"}, "field": "Publisher"}}, "selection": {"selector013": {"type": "multi", "fields": ["Publisher"]}, "selector015": {"type": "interval", "bind": "scales", "encodings": ["x", "y"]}}}], "data": {"name": "data-9946e36c977c188a13d506b5f8173d6a"}, "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-9946e36c977c188a13d506b5f8173d6a": [{"Name": "Wii Sports", "Platform": "Wii", "Genre": "Sports", "Publisher": "Nintendo", "Global_Sales": 82.74}, {"Name": "Super Mario Bros.", "Platform": "NES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 40.24}, {"Name": "Mario Kart Wii", "Platform": "Wii", "Genre": "Racing", "Publisher": "Nintendo", "Global_Sales": 35.82}, {"Name": "Wii Sports Resort", "Platform": "Wii", "Genre": "Sports", "Publisher": "Nintendo", "Global_Sales": 33.0}, {"Name": "Pokemon Red/Pokemon Blue", "Platform": "GB", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 31.37}, {"Name": "Tetris", "Platform": "GB", "Genre": "Puzzle", "Publisher": "Nintendo", "Global_Sales": 30.26}, {"Name": "New Super Mario Bros.", "Platform": "DS", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 30.01}, {"Name": "Wii Play", "Platform": "Wii", "Genre": "Misc", "Publisher": "Nintendo", "Global_Sales": 29.02}, {"Name": "New Super Mario Bros. Wii", "Platform": "Wii", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 28.62}, {"Name": "Duck Hunt", "Platform": "NES", "Genre": "Shooter", "Publisher": "Nintendo", "Global_Sales": 28.31}, {"Name": "Nintendogs", "Platform": "DS", "Genre": "Simulation", "Publisher": "Nintendo", "Global_Sales": 24.76}, {"Name": "Mario Kart DS", "Platform": "DS", "Genre": "Racing", "Publisher": "Nintendo", "Global_Sales": 23.42}, {"Name": "Pokemon Gold/Pokemon Silver", "Platform": "GB", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 23.1}, {"Name": "Wii Fit", "Platform": "Wii", "Genre": "Sports", "Publisher": "Nintendo", "Global_Sales": 22.72}, {"Name": "Wii Fit Plus", "Platform": "Wii", "Genre": "Sports", "Publisher": "Nintendo", "Global_Sales": 22.0}, {"Name": "Kinect Adventures!", "Platform": "X360", "Genre": "Misc", "Publisher": "Microsoft Game Studios", "Global_Sales": 21.82}, {"Name": "Grand Theft Auto V", "Platform": "PS3", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 21.4}, {"Name": "Grand Theft Auto: San Andreas", "Platform": "PS2", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 20.81}, {"Name": "Super Mario World", "Platform": "SNES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 20.61}, {"Name": "Brain Age: Train Your Brain in Minutes a Day", "Platform": "DS", "Genre": "Misc", "Publisher": "Nintendo", "Global_Sales": 20.22}, {"Name": "Pokemon Diamond/Pokemon Pearl", "Platform": "DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 18.36}, {"Name": "Super Mario Land", "Platform": "GB", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 18.14}, {"Name": "Super Mario Bros. 3", "Platform": "NES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 17.28}, {"Name": "Grand Theft Auto V", "Platform": "X360", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 16.38}, {"Name": "Grand Theft Auto: Vice City", "Platform": "PS2", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 16.15}, {"Name": "Pokemon Ruby/Pokemon Sapphire", "Platform": "GBA", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 15.85}, {"Name": "Pokemon Black/Pokemon White", "Platform": "DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 15.32}, {"Name": "Brain Age 2: More Training in Minutes a Day", "Platform": "DS", "Genre": "Puzzle", "Publisher": "Nintendo", "Global_Sales": 15.3}, {"Name": "Gran Turismo 3: A-Spec", "Platform": "PS2", "Genre": "Racing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 14.98}, {"Name": "Call of Duty: Modern Warfare 3", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 14.76}, {"Name": "Pok\u00e9mon Yellow: Special Pikachu Edition", "Platform": "GB", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 14.64}, {"Name": "Call of Duty: Black Ops", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 14.64}, {"Name": "Pokemon X/Pokemon Y", "Platform": "3DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 14.35}, {"Name": "Call of Duty: Black Ops 3", "Platform": "PS4", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 14.24}, {"Name": "Call of Duty: Black Ops II", "Platform": "PS3", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 14.03}, {"Name": "Call of Duty: Black Ops II", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 13.73}, {"Name": "Call of Duty: Modern Warfare 2", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 13.51}, {"Name": "Call of Duty: Modern Warfare 3", "Platform": "PS3", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 13.46}, {"Name": "Grand Theft Auto III", "Platform": "PS2", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 13.1}, {"Name": "Super Smash Bros. Brawl", "Platform": "Wii", "Genre": "Fighting", "Publisher": "Nintendo", "Global_Sales": 13.04}, {"Name": "Call of Duty: Black Ops", "Platform": "PS3", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 12.73}, {"Name": "Animal Crossing: Wild World", "Platform": "DS", "Genre": "Simulation", "Publisher": "Nintendo", "Global_Sales": 12.27}, {"Name": "Mario Kart 7", "Platform": "3DS", "Genre": "Racing", "Publisher": "Nintendo", "Global_Sales": 12.21}, {"Name": "Halo 3", "Platform": "X360", "Genre": "Shooter", "Publisher": "Microsoft Game Studios", "Global_Sales": 12.14}, {"Name": "Grand Theft Auto V", "Platform": "PS4", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 11.98}, {"Name": "Pokemon HeartGold/Pokemon SoulSilver", "Platform": "DS", "Genre": "Action", "Publisher": "Nintendo", "Global_Sales": 11.9}, {"Name": "Super Mario 64", "Platform": "N64", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 11.89}, {"Name": "Gran Turismo 4", "Platform": "PS2", "Genre": "Racing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 11.66}, {"Name": "Super Mario Galaxy", "Platform": "Wii", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 11.52}, {"Name": "Pokemon Omega Ruby/Pokemon Alpha Sapphire", "Platform": "3DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 11.33}, {"Name": "Super Mario Land 2: 6 Golden Coins", "Platform": "GB", "Genre": "Adventure", "Publisher": "Nintendo", "Global_Sales": 11.18}, {"Name": "Grand Theft Auto IV", "Platform": "X360", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 11.02}, {"Name": "Gran Turismo", "Platform": "PS", "Genre": "Racing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 10.95}, {"Name": "Super Mario 3D Land", "Platform": "3DS", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 10.79}, {"Name": "Gran Turismo 5", "Platform": "PS3", "Genre": "Racing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 10.77}, {"Name": "Call of Duty: Modern Warfare 2", "Platform": "PS3", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 10.69}, {"Name": "Grand Theft Auto IV", "Platform": "PS3", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 10.57}, {"Name": "Super Mario All-Stars", "Platform": "SNES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 10.55}, {"Name": "Pokemon FireRed/Pokemon LeafGreen", "Platform": "GBA", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 10.49}, {"Name": "Super Mario 64", "Platform": "DS", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 10.42}, {"Name": "Just Dance 3", "Platform": "Wii", "Genre": "Misc", "Publisher": "Ubisoft", "Global_Sales": 10.26}, {"Name": "Call of Duty: Ghosts", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 10.21}, {"Name": "Halo: Reach", "Platform": "X360", "Genre": "Shooter", "Publisher": "Microsoft Game Studios", "Global_Sales": 9.88}, {"Name": "Mario Kart 64", "Platform": "N64", "Genre": "Racing", "Publisher": "Nintendo", "Global_Sales": 9.87}, {"Name": "New Super Mario Bros. 2", "Platform": "3DS", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 9.82}, {"Name": "Halo 4", "Platform": "X360", "Genre": "Shooter", "Publisher": "Microsoft Game Studios", "Global_Sales": 9.76}, {"Name": "Final Fantasy VII", "Platform": "PS", "Genre": "Role-Playing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 9.72}, {"Name": "Call of Duty: Ghosts", "Platform": "PS3", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 9.59}, {"Name": "Just Dance 2", "Platform": "Wii", "Genre": "Misc", "Publisher": "Ubisoft", "Global_Sales": 9.52}, {"Name": "Gran Turismo 2", "Platform": "PS", "Genre": "Racing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 9.49}, {"Name": "Call of Duty 4: Modern Warfare", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 9.32}, {"Name": "Donkey Kong Country", "Platform": "SNES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 9.3}, {"Name": "Minecraft", "Platform": "X360", "Genre": "Misc", "Publisher": "Microsoft Game Studios", "Global_Sales": 9.2}, {"Name": "Animal Crossing: New Leaf", "Platform": "3DS", "Genre": "Simulation", "Publisher": "Nintendo", "Global_Sales": 9.09}, {"Name": "Mario Party DS", "Platform": "DS", "Genre": "Misc", "Publisher": "Nintendo", "Global_Sales": 9.02}, {"Name": "The Elder Scrolls V: Skyrim", "Platform": "X360", "Genre": "Role-Playing", "Publisher": "Bethesda Softworks", "Global_Sales": 8.84}, {"Name": "Super Mario Kart", "Platform": "SNES", "Genre": "Racing", "Publisher": "Nintendo", "Global_Sales": 8.76}, {"Name": "FIFA 16", "Platform": "PS4", "Genre": "Sports", "Publisher": "Electronic Arts", "Global_Sales": 8.49}, {"Name": "Wii Party", "Platform": "Wii", "Genre": "Misc", "Publisher": "Nintendo", "Global_Sales": 8.49}, {"Name": "Halo 2", "Platform": "XB", "Genre": "Shooter", "Publisher": "Microsoft Game Studios", "Global_Sales": 8.49}, {"Name": "Mario Party 8", "Platform": "Wii", "Genre": "Misc", "Publisher": "Nintendo", "Global_Sales": 8.42}, {"Name": "Pokemon Black 2/Pokemon White 2", "Platform": "DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 8.33}, {"Name": "FIFA Soccer 13", "Platform": "PS3", "Genre": "Action", "Publisher": "Electronic Arts", "Global_Sales": 8.24}, {"Name": "The Sims 3", "Platform": "PC", "Genre": "Simulation", "Publisher": "Electronic Arts", "Global_Sales": 8.11}, {"Name": "GoldenEye 007", "Platform": "N64", "Genre": "Shooter", "Publisher": "Nintendo", "Global_Sales": 8.09}, {"Name": "Mario & Sonic at the Olympic Games", "Platform": "Wii", "Genre": "Sports", "Publisher": "Sega", "Global_Sales": 8.06}, {"Name": "Final Fantasy X", "Platform": "PS2", "Genre": "Role-Playing", "Publisher": "Sony Computer Entertainment", "Global_Sales": 8.05}, {"Name": "Final Fantasy VIII", "Platform": "PS", "Genre": "Role-Playing", "Publisher": "SquareSoft", "Global_Sales": 7.86}, {"Name": "Pok\u00e9mon Platinum Version", "Platform": "DS", "Genre": "Role-Playing", "Publisher": "Nintendo", "Global_Sales": 7.84}, {"Name": "Pac-Man", "Platform": "2600", "Genre": "Puzzle", "Publisher": "Atari", "Global_Sales": 7.81}, {"Name": "Grand Theft Auto: Liberty City Stories", "Platform": "PSP", "Genre": "Action", "Publisher": "Take-Two Interactive", "Global_Sales": 7.72}, {"Name": "Super Mario Galaxy 2", "Platform": "Wii", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 7.69}, {"Name": "Star Wars Battlefront (2015)", "Platform": "PS4", "Genre": "Shooter", "Publisher": "Electronic Arts", "Global_Sales": 7.67}, {"Name": "Call of Duty: Advanced Warfare", "Platform": "PS4", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 7.6}, {"Name": "The Legend of Zelda: Ocarina of Time", "Platform": "N64", "Genre": "Action", "Publisher": "Nintendo", "Global_Sales": 7.6}, {"Name": "Crash Bandicoot 2: Cortex Strikes Back", "Platform": "PS", "Genre": "Platform", "Publisher": "Sony Computer Entertainment", "Global_Sales": 7.58}, {"Name": "Super Mario Bros. 2", "Platform": "NES", "Genre": "Platform", "Publisher": "Nintendo", "Global_Sales": 7.46}, {"Name": "Super Smash Bros. for Wii U and 3DS", "Platform": "3DS", "Genre": "Fighting", "Publisher": "Nintendo", "Global_Sales": 7.45}, {"Name": "Call of Duty: World at War", "Platform": "X360", "Genre": "Shooter", "Publisher": "Activision", "Global_Sales": 7.37}, {"Name": "Battlefield 3", "Platform": "X360", "Genre": "Shooter", "Publisher": "Electronic Arts", "Global_Sales": 7.34}]}}, {"mode": "vega-lite"});
</script>



In terms of creating the visualization, I decided to make a stacked bar chart. The three variables compared in the visualization are the categorical variables Platform and Publisher and the quantitative variable Global_Sales. The marks are bars, while the channels are Global_Sales, Platform, and Publisher. There is a legend on the side that is hued by Publisher, and this legend corresponds with the hue on the visualization. The y-axis is the Global_Sales, while the Platform is the x-axis. Each stack on the x-axis represents a Publisher. The chart has tooltips to see each stack's sales, while you can zoom and scroll in the visualization. When you click on the legend, the corresponding hue on the visualization pops out since everything else turns grey. With this, users can easily interpret the visualization and ultimately concluded that Nintendo games on the Wii are the most successful.

After creating the visualization, I wanted to determine why Nintendo games on the Wii are the most successful games in the dataset. After looking through the [dataset](https://www.kaggle.com/gregorut/videogamesales), I discovered that the data is from 1980- 2017, with less information for 2015-2017. That is the reason why Nintendo dominates the dataset.
 
<img src="https://imgur.com/vPVX3o5.jpg" 
alt="Updated visualization!" />

As you can see in this [recent visualization](https://www.statista.com/statistics/276768/global-unit-sales-of-video-game-consoles/), gaming as a whole has been on the decline. I think that is due to rise of social media. From 2004-2020, 2008 was the peak of gaming. Notice how this is before the peak of social media. Over the past ten years, gaming has declined at a constant rate; however, it rose in 2017. Of course, in 2020, gaming sales are at an all-time low since 2006 due to the COVID-19 pandemic. But, I noticed that the sales of games have become less diverse in the past five years. In 2012, the 3DS, Playstation Vita, PS3, Wii U, Xbox 360, PSP, Wii, and DS were the best-selling consoles. By 2020, only the PS4, Xbox One, and Nintendo Switch were the best-selling consoles. Nintendo is the most successful gaming company in terms of game and consoles sales in the dataset because the most popular gaming companies were obsolete before 2005. Since 2014, Nintendo games have been on the decline. I think this is because of the commercial failure of the Wii U. Because the Wii U was a flop, more consumers bought the Xbox 360 or PS3. Speaking from the I perspective, I loved Nintendo until 2012 when I got an Xbox 360. Those new Xbox or PlayStation consumers would purchase the PS4 or Xbox One when it came out in 2013. I got an Xbox One the summer of 2015 because I was sick of the Wii U. 

#### Conclusion
Overall, in the past 40 years, Nintendo has dominated the gaming industry. People still love Nintendo, but Nintendo is not the same compared to its popularity from 1990-2010. The recent commercial success of first-person shooters and action games on the Xbox One, PS4, and new consoles Xbox X and PS5, is the manifestation of Nintendo's fall from grace. It was amazing to create visualizations and conduct research on this dataset, and I am proud to say I can now create professional visualizations using Altair!
