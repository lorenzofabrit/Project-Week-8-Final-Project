<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>


# Smart Cities for Public Transport
*[Lorenzo Fabritius]*

*[Data Analytics, Barcelona, March 2020]*

## Content
- [Project Description](#project-description)
- [Hypotheses / Questions](#hypotheses-questions)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Analysis](#analysis)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Workflow](#workflow)
- [Organization](#organization)
- [Links](#links)

## Project Description
With the advent of big data, we have witnessed the emergence of so-called "smart cities" where administrative bodies make use of large sets of available data in order to more effectively govern the public space and improve the quality of life of its citizens. 

One major element of this development is represented by the improvement of public transport services. Public transport is crucial to functioning of a city in various facets. If done correctly, it has the potential to reduce traffic, encourage mobility and reduce air pollution. 

Hence, the idea of my project was to utilize the data of a city's public transport system in order to understand the functioning of such a complex network and then go from there to make suggestions for improvements.

## Hypotheses / Questions
The main questions that I want to answer with this project are:
* What are the weak points of the public transport system that I am analysing?
* Are the trains overloaded and unpunctual?
* Is there a way to solve or at least mitigate these weak points?


## Dataset
In order to answer the questions presented above, I researched the datasets of as many cities as I could find, in order to find the one with the most extensive detail and number of dimensions. I finally opted for the public transport dataset of Zurich's Open Data website for the year 2019. The dataset is divided into 4 distinct tables. The main table details the average amount of people on each transportline during all of its runningtimes for the year - this table consists of roughly 1.2 Million lines of data. The 3 other tables are supporting tables that contain information of the transportlines, the bus- and tramstops as well as the daytype. All of the tables are in CSV format. [Link to the dataset](https://data.stadt-zuerich.ch/dataset/vbz_fahrgastzahlen_ogd)   

## Cleaning
The cleaning process of the dataset has been entirely conducted in a Jupyter Notebook named Train Users Datacleaning, as is explained in the organisation section. I structured it in the following manner:
  
  1. Dataset Translation
  
  As a first step, I had to translate all column headers from German to English so as to facilitate the comprehension of my workflow for 3rd parties. 
  
  2. Drop irrelevant columns
  
  I then went on to remove the columns from my dataset which I didn't believe to be helpful in my analysis. 
     
  3. Aggregate Daytypes
  
  In order to get a better overview of my data, I decided to aggregate my encoded daytypes so that I would end up with two daytype groups: Weekday and Weekend.
     
  4. DateTime column transformation
  
  In order to deal with the temporal information of the dataset, I converted the time       columns from object to DateTime.
  
  5. Create column identifying vehicle type
  
  In order to understand the load capacities of the vehicles in the Zurich public    transport system I created a column to classify the lines by their vehicle types. This is done in accordance with the Vehicle Table as well as internet research. I ended up with 4 vehicle types: tram, bus, large_bus and trolleybus. I then also created another column called maximum_capacity, which contains that maximum amount of people for the vehicle type; this was researched on the internet. 
     
  6. Create column designating occupancy rate
  
  At this point I was able to create an occupancy rate column. This column describes how          full the vehicle was at each datapoint and was achieved by dividing the occupancy by the        maximum capacity. 

  7. Remove rows with null measurement days
  
  I went on to remove all rows were the measurement_days column was null, as this  meant that these rows cannot be regared as representative. 

## Analysis
When starting this project, my main hypotheses were that there would be certain timeframes and areas in which the occupancy rates would regularly reach their peak and thus diminish the quality of the transport service provided. In this respect, my main goal was to ensure that the occupancy rate of all vehicles of the Zurich public transport system would never exceed 85%. 

A first query shows that the two main timeframes with an occupancy rate higher than 85% are 07:00 - 09:00 and 17:00 - 18:00. 

I then conducted queries for these timeframes in order to isolate the affected tram- and buslines, as well as the stations at which the high occupancy was measured. This gave me an idea of the specific areas that needed to be adressed in order to improve the public transport system as a whole.

Having isolated the problematic timeframes, lines and stations I wanted to come up with a way of reducing their occupancy. I therefore made search queries for the maximum occupancy rate of all lines according to vehicle type in order to find the lowest values. My idea was that these lines could reduce their frequencies and redirect vehicles towards the more occupied lines in the timeframes that I was analysing. I decided that I would increase the frequency of the overused lines by 20% during the two timeframes while decreasing the frequency of the underused lines by 30%. I found that this aim was totally within the means of the Zurich public transport system, as there were numerous underused lines that could be redirected towards the overused ones exactly in the timeframes in which they were needed.  


## Conclusion
My analysis has enabled me to gain an insight on how to spot inefficiencies within a public transport system, as well as what levers can be used in order to improve it without having to commit further resources to it.

It is evident that my analysis is predicated upon the availability of large amounts of data on a transport system. In my research, Zurich was the only city that I could find with openly available data in such detail. I believe that furthering data measurement and analysis in cities around the world is going to be the main driver of improving public transport systems, especially in large cities which, unlike Zurich, are subject to chronically deficient transport systems. 

## Future Work
In my future work I would look to enhace my analysis in two ways:

1. Every week, Open Data Zurich releases a dataset on the punctuality of all the vehicles in the public transport system. By including this data into my analysis, I could identify bottleneck hotspots and make further recommendations on how to prevent these.

2. My current proposal of diverting vehicles from underused lines could go a level deeper my identifying the exact vehicles to be sent to specific overused lines. The decisive criteria here would be the shortest driving distance for the vehicles in order to reduce fuel costs. 

## Organization
Github was the main tool that I used to organize my project. It helped me to maintain control of all project versions and to be able to upload them to the cload in a structured manner. My repository is structured as follows:

Data:

raw_data → Folder containing the raw data csv files coming from Zurich Open Data.

clean_data → Folder containing the cleaned csv file obtained from datacleaning_1.ipynb notebook and which will be used in the data_analysis_1.ipynb notebook.


Jupyter Notebooks:

datacleaning_1.ipynb → Data wrangling, cleaning and exporting to GoogleCloud SQL

data_analysis_1.ipynb → Data analysis for public transport optimization.

datacleaning_notes.ypnb → Used for minor calculation during datacleaning and analysis; not uploaded to repository.


Visualization Data:

CSV files containing the coordinates of all overloaded public transport stops, in the morning as well as the evening. These were used for a visualization map created on Tableau.

Visualizations:

Contains the Tableau visualizations as well as a barchart.

README markdown file:

File that you are currently reading, with all the basic information about the project that has been carried out.


## Links
[Repository](https://github.com/lorenzofabrit/Project-Week-8-Final-Project)  
[Slides](https://docs.google.com/presentation/d/1O5_VwYxWyWCZ3arJHH2sELQaa5WRRrW9XCTC81_Te8M/edit#slide=id.g7f0fd2af9f_0_132)  
 
