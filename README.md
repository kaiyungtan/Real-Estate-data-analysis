# Challenge: Data Analysis
Use pandas, Data visualisation libraries(Matplotlib or Seaborn) to establish conclusions about a dataset.

### Team member:  

Kai Yung (Adam) https://github.com/kaiyungtan

Joffrey https://github.com/Joffreybvn

Mathieu https://github.com/leersmathieu


![alt text](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/Visualisation/Immoweb%20house%20logo.png?raw=true)

## Introduction

The real estate company "ImmoEliza" wants you to create a machine learning model to predict prices on Belgium's sales.

You need to do a complete analysis and interpretation of the dataset.

Dataset were scrapped from https://www.immoweb.be

Raw dataset : dataset_house_apartment.csv were obtained https://github.com/MDropsy/challenge-collecting-data

In this dataset we have 52077 rows and 20 columns.

### Details of the columns

- locality (postal code of city)
- type_of_property (House/apartment)
- subtype_of_property (Bungalow, Villa, ...)
- price (€)
- type_of_sale (Exclusion of life sales)
- number_of_rooms (number)
- house_area (m2)
- fully_equipped_kitchen (Yes/No)
- furnished (Yes/No)
- open_fire (Yes/No)
- terrace (Yes/No) 
- terrace_area (m2)
- garden (Yes/No)
- garden_area (m2)
- surface_of_the_land (m2)
- surface_of_the_plot_of_land (m2)
- number_of_facadess (number)
- swimming_pool (Yes/No)
- state_of_the_building (Good, As new,to be renovated, ...)
- construction_year (year of the property built)

## Plan:

1. Create the repository (Adam)
2. Study the request (Adam,Joffery,Mathieu)
3. Identify technical challenges (Adam,Joffery,Mathieu)
4. Data Cleaning (Adam,Joffery,Mathieu)
5. Data Visualisation (Adam,Joffery,Mathieu)
6. Data Analysis (Adam,Joffery,Mathieu)
7. Data Interpretation (Adam,Joffery,Mathieu)
8. Update repository (Adam,Joffery,Mathieu)

## 1. Repository 

https://github.com/kaiyungtan/challenge-data-analysis/

## 2. Request

Based on the request, the team decided to search for additional information related to postal code i.e name of the city,province ...

From code-postaux-belge.csv which can be obtained from https://data.gov.be/fr/dataset/328ba4f140ba0e870dfc9c70635fe7c1840980b1

We have information as follow:

'column_1': postal code

'column_2': city name 

'column_3': longitude

'column_4': lattitude	

'coordonnees': coordinate of the city (longtitude,lattitude) 

'geom' : empty column

- code-postaux-belge.csv will be merge with dataset_house_apartment.csv to have the final raw dataset.
- only column 1-4 from code-postaux-belge.csv will be merge.

In addition, the team has to find out postal codes with their associated provinces and regions.

## 3. Technical challenges

To find all postal codes with their associated provinces and regions:

 - A function convert_by_postal_code() created to map related postal code to their associated provinces and regions. (credit to Joffrey)

To create maps with interesting information:

 - Visualize data on a Leaflet map via folium.
 - Folium builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the leaflet.js library. 

#### Postal codes correspondence to Region/Province

1000–1299 : Région de Bruxelles-Capitale

1300–1499 :  Province du Brabant wallon

1500–1999 :  Province du Brabant flamand (arrondissement de Hal-Vilvorde, sauf Overijse)

2000–2999 :  Province d'Anvers

3000–3499 :  Province du Brabant flamand (arrondissement de Louvain, plus Overijse)

3500–3999 :  Province de Limbourg

4000–4999 :  Province de Liège

5000–5999 : Province de Namur

6000–6599 :  Province de Hainaut (1)

6600–6999 :  Province de Luxembourg

7000–7999 :  Province de Hainaut (2)

8000–8999 :  Province de Flandre-Occidentale

9000–9999 :  Province de Flandre-Orientale

## 4. Data Cleaning

1. Understand the requirements.

2. Identify the needs:

  - Dataset with postal code and cities.
  - Research on data visualization library.
  - A new price/m3 column.
  - Average, median price, and per m3.
  
3. Carefully remove the outliers (error, incorrect or absurd).
 

Cleaning:
- Drop the duplicated rows
- Move columns (city_name)
- Drop columns with unique value
- Check each columns's properties
- Include provinces
- Include regions
- Reset index

- subtype: supprimer appartement block, puis supprimer subtype
- room number: delete +20
- price: float ? -> to int
- house surface : delete 1, 31700
- terrace_area: delete
- garden_area: delete
- surface: garder et supprimer au moment du calcul
- facade: remove 1
- state of building: None to unknown



## 5. Data Visualisation


## 6. Data Analysis

#### Which variable is the target ?
The price.
Why ? Our mission is to to create a machine learning model to predict prices on Belgium's sales.

#### How many rows and columns ?
We have 40395 rows (observations)
And 18 columns

Why: City Name, Lattitude, Longitude, Province, Region

#### What is the correlation between variable/target ? (Why?)




## 7. Data Interpretation 

- to create new column price/house area to answer price per square meter for the following questions.

#### What are the most expensive municipalities in Belgium? (Average price, median price, price per square meter)

#### What are the most expensive municipalities in Wallonia? (Average price, median price, price per square meter)

#### What are the most expensive municipalities in Flanders? (Average price, median price, price per square meter)

#### What are the less expensive municipalities in Belgium? (Average price, median price, price per square meter)

#### What are the less expensive municipalities in Wallonia? (Average price, median price, price per square meter)

#### What are the less expensive municipalities in Flanders? (Average price, median price, price per square meter)


## Pandas profiling report:

https://kaiyungtan.github.io/challenge-data-analysis/data/clean/report.html

## Average Price per Square Meter map:

For both houses & apartments in Belgium:

https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_house&apartment.html

For apartments in Belgium:

https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_apartment.html

For houses in Belgium:

https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_house.html
