# 📊 Data Scraping & Analysis with YouTube API in Python
![image](https://github.com/user-attachments/assets/6a13b2da-3727-4050-b48c-8843e6147a5b)

## Project Overview
This project demonstrates the end-to-end process of extracting data from YouTube using the YouTube API and analyzing it with Python in Jupyter Notebook. By gathering video metrics and related data, we can explore various insights, such as content trends, engagement metrics, and audience behavior. This project highlights my skills in API data extraction, data analysis, and data visualization to deliver meaningful insights.

## Table of Contents
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Technologies & Tools](#Technologies--Tools)
  - [Languages](#languages)
  - [Tools & Libraries](#tools--libraries)
  - [APIs](#apis)
4. [Project Workflow](#project-workflow)
  - [API Setup](#API-Setup)
  - [Data Extraction](#data-extraction)
  - [Data Wrangling](#data-wrangling)
  - [Data Analysis](#data-analysis)
  - [Data Visualization](#data-visualization)
5. [Set up your YouTube API Key](#Set-up-your-YouTube-API-Key)
  - [Step 1: Create a Project in Google Cloud Console](#Step-1-Create-a-Project-in-Google-Cloud-Console)
  - [Step 2: Enable the YouTube Data API v3](#Step-2-Enable-the-YouTube-Data-API-v3)
  - [Step 3: Create an API Key](#Step-3-Create-an-API-Key)
  - [Step 4: Store Your API Key in the Project](#Step-4-Store-Your-API-Key-in-the-Project)
6. [Data Extraction](#Data-Extraction)
- [Future Improvements](#Future-Improvements) 

## Introduction
With the rise of video content, YouTube has become a valuable data source to understand online engagement patterns. In this repository I dived into gathering and analyzing data from YouTube using Python with ease. Whether you're a data analyst, developer, or curious enthusiast, this project will walk you through scraping data from the YouTube API and performing insightful analysis on it. 🎉

📌 What to expect  
1. Accessing YouTube’s API to pull in data such as video details, comments, likes, views, and more.
2. Data Processing in Python to clean and organize the data for meaningful analysis.
3. Data Visualization & Insights using libraries like pandas, matplotlib, and seaborn.  

🚀 Prerequisites
- Basic knowledge of Python 🐍
- Some familiarity with API requests 🔑

## Project Objectives
- **Extract YouTube Data:** Use the YouTube Data API to collect relevant information such as view counts, likes, comments, and video details.
- **Data Wrangling and Data Cleaning:** Process and clean the data to ensure consistency and usability.
- **Perform Data Analysis:** Analyze metrics like viewer engagement, subscriber ccount, number of videos uploaded and trending topics.
- **Visualize Insights:** Present data findings through visualizations to convey key insights clearly.

## Technologies & Tools
### Languages
- Python 🐍
### Tools
- Jupyter Notebook 📃
- YouTube Data API v3 🔑
### Libraries
- pandas 🐼
- numpy 💻
- matplotlib 📉
- seaborn 📊
- requests 🔑
- google-auth
### API
- YouTube Data API v3

## Project Workflow
### API Setup
- Setting up the YouTube API access and authentication.
### Data Extraction 
- Using API calls to gather data, including video statistics, channel information, and comments.
### Data Wrangling  
- Cleaning and organizing the extracted data.
### Data Analysis
Conducting analyses such as:
- Top-performing videos and channels
- View and engagement patterns over time
- Audience demographics and regional insights
### Visualization
- Visualizing data using charts to highlight trends and findings.

## Set up your YouTube API Key
- Make sure you sign in to your <a href="https://console.cloud.google.com/welcome?_gl=1*12nz4xc*_up*MQ..&gclid=Cj0KCQjwj4K5BhDYARIsAD1Ly2pq9w3uf4Gw3D9lTtQehZxichCPnq-iuIQt92FCZiUnqhT_cZxN6tAaAnllEALw_wcB&gclsrc=aw.ds&hl=en&project=causal-scarab-438518-h6">Google Console</a>

### Step 1: Create a Project in Google Cloud Console
1. Go to google console
![image](https://github.com/user-attachments/assets/f64ef4d5-50b8-4691-8303-d608fa1a9c86)
2. If you don't already have a project, click on Select Project in the top navigation bar, then create New Project.
   - Note I already have created a project named YouTube API as shown click on the drop down list and create a new project
![image](https://github.com/user-attachments/assets/112670cc-a6af-45f7-b381-4478e1a71e05)
3. Give your project a name, then click Create.
![image](https://github.com/user-attachments/assets/453aadac-55ce-4ef7-a99e-7dbcadaf0c57)

### Step 2: Enable the YouTube Data API v3
1. In your Google Cloud Console, go to the APIs & Services dashboard.
![image](https://github.com/user-attachments/assets/ab00f0b0-c33d-4f38-b62c-29b8b0b65db8)
2. Click on + ENABLE APIS AND SERVICES.
![image](https://github.com/user-attachments/assets/e26432cd-3b9c-4cfa-932c-2ee5f31d2f48)
3. In the search bar, type "YouTube Data API v3" and select it from the results.
![image](https://github.com/user-attachments/assets/4c0d80f3-cf4e-4edc-8427-30fbd30a0bac)
4. Click Enable to activate the API for your project.
![image](https://github.com/user-attachments/assets/866ade0f-6b9a-45af-97eb-913ba0cad54e)

### Step 3: Create an API Key
1. After enabling the API, go back to the APIs & Services dashboard.
![image](https://github.com/user-attachments/assets/fc81c4f2-3bee-47ed-857b-e325dd0d89c8)
2. Click on Credentials in the left sidebar.
![image](https://github.com/user-attachments/assets/224a5128-6139-4cae-bc79-9a45f667d0f7)
3. Select + CREATE CREDENTIALS and choose API Key.
![image](https://github.com/user-attachments/assets/5053c8f3-db52-43f0-a7fa-703a218dca81)
4. Copy the generated API key.
   - **NOTE: I DELETED THIS API KEY AFTER CREATING IT**


### Step 4: Store Your API Key in the Project
1. In the root directory of the project, create a ```.env``` file.
2. Open the .env file and add your API key like so:
```bash
YOUTUBE_API_KEY= YOUR API KEY
```
**Note: The .env file is included in .gitignore to keep your API key private. Do not share or commit this file in a public repository.**

## Data Extraction
- Import python libraries we will need for this project
```python
import os
from googleapiclient.discovery import build
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
plt.style.use('ggplot')
```
- Write a python function to fetch data from youtube in JSON format
```python
def channel_data(api_key, channel_id):
    all_data = []
    youtube = build('youtube', 'v3', developerKey = api_key)

    request = youtube.channels().list(
        part = 'snippet, contentDetails, statistics',
        id = ','.join(channel_id)
    )

    response = request.execute()
    for i in range(len(response['items'])):
        data = dict(channel_title = response['items'][i]['snippet']['title'],
                    created_date = response['items'][i]['snippet']['publishedAt'],
                    subscribers = response['items'][i]['statistics']['subscriberCount'],
                    total_videos = response['items'][i]['statistics']['videoCount'],
                    total_views = response['items'][i]['statistics']['viewCount'],
                    playlist_id = response['items'][i]['contentDetails']['relatedPlaylists']['uploads']
                   )
        all_data.append(data)
    return all_data
```

- Define your Api keys and Channel ID
- Import necessary libraries to access the API Key saved in the .env
  
~~~python
from dotenv import load_dotenv

# Load the .env file
load_dotenv()

# Access the API key
api_key = os.getenv("API_KEY")
~~~

- To find the chanel ID you can use <a href="https://www.tunepocket.com/youtube-channel-id-finder/?srsltid=AfmBOoqI_8UYGYspZ1Cc846BLsIar_mxQSzz-Wq1498Gxvc2SU48xbHP">Tune Pocket</a> sinceit makes it generates channel ID by just typing in the name of the channel you need Channel ID.
~~~python
CHANNEL_ID = ['UChQXn6sL9ENIpA74qqPG1HA',
              'UCaWu4TkcsWcZbw0Pg26OltQ',
              'UC6fVFxrbf0HDRW3B2mdWFGA',
              'UCE3KVkSH1GwUtAAMcVcJ3QQ',
              'UCFBoqaPTCtGJi8kr7pV33Tg',
              'UCJ7F5LT-7h8Hfplf6BTTiXg',
              'UC7h4tUtdH0L06sDZVmBMc4Q',
              'UC5h4-WH0LAV4CWs380yM33A',
              'UCx1WDOZzmyIa1MlK1W3RdOg',
              'UCgSP5G3RmKJl72aA2lBV_Jw',
              'UCVfZr3RQTqRgYQkA-eXAxiA',
              'UCPUMDSDu_WC8LVzWjiyVgNQ']
~~~

## Future Improvements
- **Automate Data Collection**
 Schedule regular data updates using cron jobs or serverless functions.
- **Expand Dataset**
 Include additional social media APIs to gather broader context.
- **Integrate Machine Learning**
 Develop models to predict engagement or trend patterns based on historical data.


