# Spotify API Data Pipeline
In this project, data is captured from the Spotify Web API using the python request module. The data collected from the Spotify Web API is stored in CSV file, JSON file, and SQL Serve database. ETL jobs are written in python and scheduled in airflow to run every 12 midnight (UTC).

## ETL Pipeline Architecture
<a href="https://drive.google.com/uc?export=view&id="><img src="https://drive.google.com/uc?export=view&id=1ZxmiU4iIX67lbp7JzA8Z-3kL_Yo49o8N" style="width: 1000px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

#### Amazing Tools used in the pipeline:
- Spotify Web API
- Python libraries: pandas, json, and pyodbc
- SQL Server
- Power BI
- Airflow and Docker for orchestration

## Data Pipeline Steps Overview
1. Send a Post request to spotify token API to get new access token
2. Using the access token, send a GET request to spotify webplayer API and transfer the response into json object in Python
3. From the json object created, select the relevant fields needed and transfer into dataframe
4. Validate the dataframe, if:
    - Empty or has blank data received
    - The song is played yesterday. If not, remove the records with playtime not matching yesterday
    - There are duplicates in the data received. Duplicate data are removed
    - Check if there are null data. Remove records containing null values
5. Save the dataframe into CSV and JSON files
6. Read the saved json file into dataframe
7. Establish connection and cursor into the sql server database
8. Per row in the dataframe, insert value into the database
9. Since the 'played_at' sent by the API is in iso8601 datetime format. We created a stored procedure that will run every 8AM and 8PM which will convert the field into datetime format
10. Connect Power Bi with the sql server database then Visualize

## Power BI Dashboard
With all the ETL steps done in this project, I am very happy with the output dashboard. Just like the yearly "Music Reflections Spotify is wonderfully providing us, we can use this dashboard to check our music streaming behavior and tastes.

<a href="https://drive.google.com/uc?export=view&id="><img src="https://drive.google.com/uc?export=view&id=1BMMV9pzywZe6uPqHdozjm4Nxfib-vrXO" style="width: 1000px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

In this dashboard, we have 4 visualizations:
1. Most Listened Decade : a doughnut chart which shows us in what decade our ears belong
2. Top Artists : a horizontal bar chart showing the top artists we religiously listening to
3. Top Songs : same with Top Artists, a horizontal bar chart showing our most favorite song
4. Streaming Behavior Tracker : well in this, if you are interested to your listening behavior, we can see in what hour and day you typically need your daily dose of amazing music

## Realizations and Cool Things Discovered
As a newbie trying to create this more complicated end-to-end data pipeline project, I had many realizations and cool things discovered:
1. The most complicated and energy-draining step is setting up AIRFLOW!!!  <br />
At first, I'm trying to setup airflow just using wsl but been frustrated with the barrage of errors I'm encountering. Luckily, I found an easier and less complicated way, which is to use DOCKER.  <br />
2. Your understanding about the problem is more important than the tools!!.  <br />
In this end-to-end project, there are so many ways and tools available out there in order to get the data from Spotify until we can visualize it.
But the main thing helped me is that I know the general requirements needed in order to do that. API Request, Data Transformations and Validations,
Data Storage and Data Viz Tool. <br />
3. BE CONSISTENT AND NEVER GIVE UP 😉 <br />
One of the greatest obstacles we can encounter while doing a project and self-learning is our drive to finish it until the end.  <br />
During the initial phase in doing this project, I'm very excited since I'm gonna be able to use the 'cool' stuff data engineers use. But there are:
    - a lot of bugs. Bugs, which some of them, frustrates me for a day or even a week finding solutions and fixes.
    - times when I'm being lazy. Yes, and that's a lot of times 😂 Doom-scrolling socmeds, binge-watch an anime, read ONE PIECE manga! and much more
    - and much more I cannot enumerate as this will be TLDR  <br />
4. IT IS NOT OKAY TO BE LONELY  <br />
Communities really helped me to finish this project. Stack Overflow, Discord Channels, and my one true friend GOOGLE!!! I'm really grateful for all the people who patiently and generously answer the frustrations we have, the errors, bugs, setup problems, etc.

## Features I wish to add and study
1. Deploy this in a cloud environment so I don't need to open my laptop every day
2. As you can see in the Power BI dashboard, I want to have some additional features:
    - Pictures in the upper left which will show the Top Artist and Top Song I listened to
3. Web Scraping and ML features. There are fields in the data stream that I haven't use such as 'is_local' and 'is_explicit'. The data that Spotify Web API is providing is inaccurate and cannot really create some insights about those 'not so good' data. By incorporating these two features, we can have additional insights with our 'MUSIC EXPERIENCE'