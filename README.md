# Challenge: Data Analysis
Using pandas and data visualisation libraries (Matplotlib, Seaborn), let's establish conclusions about a dataset.

### Team member:  

<table style="width: 100%;" >
<tbody>
<tr>
<td style="border: 1px solid #ffffff00" width="90%">
Kai Yung (Adam) <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> https://github.com/kaiyungtan<br>
Joffrey Bienvenu <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> https://github.com/Joffreybvn<br>
Mathieu Leers <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> https://github.com/leersmathieu
</td>
<td>
<img src="https://github.com/kaiyungtan/challenge-data-analysis/blob/master/Visualisation/Immoweb%20house%20logo.png?raw=true">
</td>
</tr>
</tbody>
</table>

### Price/m2 Map:
Here is a quick introduction to our work: A map of all belgian's municipalities with their median price/m2. **Click to enlarge**
[![https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/map_pricem2.png](https://github.com/kaiyungtan/challenge-data-analysis/raw/master/Visualisation/map_pricem2.png)](https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/map_pricem2.html)

## Challenge's summary
**The mission is**: Cleaning and doing a complete analysis and interpretation of the dataset created during the previous challenge. In order to create a machine learning model to predict prices on Belgium's real estate's sales.

### Objectives:
 - [x] Using Pandas for data manipulation.
 - [x] Using MatplotLib and/or Seaborn for plotting.
 - [x] Finding and understanding correlations between dataset's variables.

## The dataset: a 50.000 entries' one !

To complete this challenge, we used **a Dataset of 50.000 real estate's observations**, previously scrapped by [Kai Yung]( https://github.com/kaiyungtan) and its team during a previous challenge.

To get geographical informations about our data, we merged this dataset with the [Postal Codes dataset from belgium.be](https://data.gov.be/fr/dataset/328ba4f140ba0e870dfc9c70635fe7c1840980b1) and later, witht the [Belgium Municipalities GeoJSON](https://hub.arcgis.com/datasets/esribeluxdata::belgium-municipalities-1) provided by ArcGis.

### Why this dataset ?
We choose to use this dataset because:

*   **It has a lot of entries**: And they are not totally clean ! One of the key exercice of this challenge, was to be able to work with uncomplete/corrupted data. And at the same time, having the maximum amount of data to discover interesting correlations, and have a meaningfull analyse.

*   **It was scrapped from ImmoWeb**: [Immoweb](https://www.immoweb.be/fr) is probably the biggest real estate website of Belgium. It has more detailed data than [Zimmo](https://www.zimmo.be/fr/), for example.

*   **It was scrapped by colleagues**: The dataset "*dataset_house_apartment.csv*" was scrapped by a Becode colleague and can be found on [this repository](https://github.com/MDropsy/challenge-collecting-data).

In this dataset we have **52.077 rows** and **20 columns**.

### CSV architecture

You can download the raw CSV directly [from this link](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/data/raw/dataset_house_apartment.csv).

<details>
  <summary>Show the CSV architecture</summary>
 
- **locality** *str*: Postal code of city.
- **type_of_property** *str*: House or Apartment.
- **subtype_of_property** *str*: Bungalow, Villa, ...
- **price** *float*: Price (€) of the property.
- **type_of_sale** *str* The type of sale.
- **number_of_rooms** *int*: The number of rooms of the property.
- **house_area** *int*: The area (m2) of the house (floors).
- **fully_equipped_kitchen** *bool*: If the house has a fully equipped kitchen or not.
- **furnished** *bool*: If the house is furnished or not.
- **open_fire***bool*: If there's an open fire or not.
- **terrace** *bool*: If there's a terrace or not.
- **terrace_area** *float*: The area (m2) of the terrace.
- **garden** *bool*: If there's a garden or not.
- **garden_area** *float*: The area (m2) of the garden.
- **surface_of_the_land** *float*: The area (m2) of the land.
- **surface_of_the_plot_of_land** *float*: The area (m2) of the land's plot.
- **number_of_facadess** *int*: The number of facades (0 to 4).
- **swimming_pool** *bool*: If there's a swimming pool or not.
- **state_of_the_building** *str*: Good, As new, To be renovated, ...
- **construction_year** *int*: The property built's year.
  
</details>

---

# The Challenge

## 1. Request study & technical challenge
Our goal is to clean and do a complete analysis and interpretation of the dataset. As we are manipulating real estate data, we decided to add geographical data to our dataset.

### Adding geographical data
Based on the request, we decided to search for additional informations about the location of the dataframe's observations.

#### Why ?
1. These information could help us to create maps, and visualize the data geographically with [Folium](https://pypi.org/project/folium/)<br><img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> A much better way to understand the real estate situation in Belgium !

2. We used [Folium](https://pypi.org/project/folium/) because it allow to visualize data on a Leaflet map easily.<br><img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> Folium is build on the data wrangling strengths of the Python ecosystem and the mapping strengths of the leaflet.js library. A very powerfull tool !

### Merging with a [Postal Codes dataset](https://data.gov.be/fr/dataset/328ba4f140ba0e870dfc9c70635fe7c1840980b1):
From the file *code-postaux-belge.csv*, which can be obtained from [this link](https://data.gov.be/fr/dataset/328ba4f140ba0e870dfc9c70635fe7c1840980b1), we retrieved the following informations:

* **column_1** <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> postal_code *int*
* **column_2** <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> city_name *str*
* **column_3** <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> longitude *float*
* **column_4** <img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> lattitude *float*

We dropped the other columns of this dataset (to keep only 4), as they were useless.

### Adding the Provinces and Regions
We also needed to associate the postal code with their provinces and regions. They were no dataset with these informations. So we created it from [this wikipedia page](https://fr.wikipedia.org/wiki/Provinces_de_Belgique).

<details>
  <summary>Postal codes correspondence to Region/Province</summary>


* **1000–1299** :  Région de Bruxelles-Capitale
* **1300–1499** :  Province du Brabant wallon
* **1500–1999** :  Province du Brabant flamand (arrondissement de Hal-Vilvorde, sauf Overijse)
* **2000–2999** :  Province d'Anvers
* **3000–3499** :  Province du Brabant flamand (arrondissement de Louvain, plus Overijse)
* **3500–3999** :  Province de Limbourg
* **4000–4999** :  Province de Liège
* **5000–5999** :  Province de Namur
* **6000–6599** :  Province de Hainaut (1)
* **6600–6999** :  Province de Luxembourg
* **7000–7999** :  Province de Hainaut (2)
* **8000–8999** :  Province de Flandre-Occidentale
* **9000–9999** :  Province de Flandre-Orientale
</details>

A function "*convert_by_postal_code()*" was created to map related postal code to their associated provinces and regions. You can see it in the [Step 1-Cleaning notebook](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/step1_cleaning.ipynb) or below:

<details>
  <summary>Expand this function</summary>
 
```Python

provinces = {
    'Bruxelles-Capitale': {
        'range': [(1000, 1299)],
        'region': 'Bruxelles'
    },
    'Brabant wallon': {
        'range': [(1300, 1499)],
        'region': 'Wallonie'
    },
    'Brabant flamand': {
        'range': [(1500, 1999), (3000, 3499)],
        'region': 'Flandre'
    },
    'Anvers': {
        'range': [(2000, 2999)],
        'region': 'Flandre'
    },
    'Limbourg': {
        'range': [(3500, 3999)],
        'region': 'Flandre'
    },
    'Liège': {
        'range': [(4000, 4999)],
        'region': 'Wallonie'
    },
    'Namur': {
        'range': [(5000, 5999)],
        'region': 'Wallonie'
    },
    'Hainaut': {
        'range': [(6000, 6599), (7000, 7999)],
        'region': 'Wallonie'
    },
    'Luxembourg': {
        'range': [(6600, 6999)],
        'region': 'Wallonie'
    },
    'Flandre-Occidentale': {
        'range': [(8000, 8999)],
        'region': 'Flandre'
    },
    'Flandre-Orientale': {
        'range': [(9000, 9999)],
        'region': 'Flandre'
    }
}

def convert_by_postal_code():
  """
  Convert the 'provinces' dictionnary to a dictionnary of postal codes as key,
  and its region and province as values.
  """
  postal_dict = {}

  # Loop through each entry in the "provinces" dictionnary
  for province, content in provinces.items():

    # Loop though each postal code
    for postal_code_tuple in content['range']:
      for code in range(postal_code_tuple[0], postal_code_tuple[1] + 1):

        # Append the province and region for each postal code.
        postal_dict[code] = {'province': province, 'region': content['region']}

  return postal_dict

postal_dict = convert_by_postal_code()

# Then, the result is merged with our dataframe.
# Get the details on: https://github.com/kaiyungtan/challenge-data-analysis/blob/master/step1_cleaning.ipynb
```
</details>


## 2. Data Cleaning
The cleaning phase is very important: without a good cleaning, our analysis could be badly influenced by outliers. So, we decided to identify our neer during the analysis phase, to drop the useless column and clean the usefull ones.

### Identifing the needs:
To proceed to the analysis, we needed a clean dataset containing at least:

  - Prices, postal code and city names.
  - A price/m2 column
  
### Removing the outliers (error, incorrect or absurd).
It's good to have a lot of columns, as it can create more correlations between them. However, it's bad to have columns with errors, incorrect, missing or absurd values. That's why **we divided our cleaning in two phases**:

#### Cleaning the raw:
A very first clean to the raw data. We were focused on "**dropping the big lies**":

- **Dropping** the duplicated rows
- **Dropping** columns with only one unique value
- **Checking** each columns's properties

#### Refining the values
Some tweaks were made on the dataset to **remove outliers and useless columns**, due to their high rate of *None* value. This steap required deeper investigation intop the data:

<details>
  <summary>Show the details</summary>

- **Dropping** "*terrace_area*" column<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> It has more than 30% of None.
- **Dropping** "*garden_area*" column<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> It has more than 50% of None.
- **Dropping** "*subtype*" column<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> Lots of property subtype. Some with less than 100 entries, in a dataset of 50.000. This column was not relevant.
- **Removing** the "Apartment blocks" entries<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> Apartment blocks are a whole building. It's not the kind of real estate sales we want here.
- **Changing** *None* to "unknow"

</details>

We also refactored all *float* to *int*. At the end of the cleaning, **we merged our dataframe with the two other ones created during the request study**.

### How many rows and columns ?
At the end of the cleaning phase, we had **40.395 rows** (observations) and **18 columns**. We also made a [Pandas Profiling Report](https://kaiyungtan.github.io/challenge-data-analysis/data/clean/report.html) to prove the clea


## 3. Data Analysis & Interpretation
This is where the fun start ! :partying_face: 

> Three people know more than one.

To get the most out of our data, and to allow each of us to get experience manipulating Pandas and Seaborn, we decided to work separately. Later we reviewed our work and merged the results.

### Our target: The Price.
The price is obviously the target of this challenge, as ou goal is to to create a machine learning model to predict prices on Belgium's sales.

### Correlation between variables ?
To identify the correlation, we used this heatmap:

![https://github.com/kaiyungtan/challenge-data-analysis/blob/master/Visualisation/Heatmap.png](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/Visualisation/Heatmap.png)

#### Observations:
1. The **Price** is mainly correlated with the *Number of rooms* and the *House area*.
2. The **Number of rooms** and *House area* seems mainly correlated with each other.
3. The **Type of property** is the variables which has the most correlation with other variables.

They are many other observations we did and we investigated. These are detailed in the [step 2 notebooks](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/step2_analysis_adam.ipynb) [of each](https://github.com/kaiyungtan/challenge-data-analysis/blob/master/step2_analysis_joffrey.ipynb) [of us]().

### Conclusions:
Based on theses observations, we came to the following conclusion:

<p align="center">
  <img src="https://raw.githubusercontent.com/kaiyungtan/challenge-data-analysis/master/Visualisation/correlations.svg">
</p>

The **Open fire**, the **Garden**, the **Location** of the house (municipality) and its **Number of facades** determine the **Type of property**.
Which influence greatly on the **Number of rooms** and the **House area**: An apartement will have less space and less rooms than a house.

**Number of rooms** and **house area** are two variables based on the size of the property. And they are the main influence on the **Price**: A larger house/apartment is more expensive than a smaller house/apartment.

## Challenge's answers:
For this challenge, we had to reply to the following questions:

- to create new column price/house area to answer price per square meter for the following questions.

### What are the most expensive municipalities in Belgium? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Belgium (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Knokke** | 472 000 | 5500 | 5500 |
**Leuven** | 365 000 | 4100 | 4700 |
**Ramskapelle** | 356 000 | 4200 | 4400 |

### What are the most expensive municipalities in Wallonia? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Wallonia (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Louvain-La-Neuve** | 465 000 | 3800 | 3750 |
**Thines** | 550 000 | 3400 | 3440 |
**Ottignies** | 380 000 | 3400 | 3160 |

### What are the most expensive municipalities in Flanders? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Flanders (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Knokke** | 472 000 | 5500 | 5500 |
**Leuven** | 365 000 | 4100 | 4700 |
**Ramskapelle** | 356 000 | 4200 | 4400 |

### What are the less expensive municipalities in Belgium? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Belgium (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Beauwelz** | 70 000 | 350 | 350 |
**Focant** | 80 000 | 390 | 390 |
**Nollevaux** | 139 000 | 420 | 420 |

### What are the less expensive municipalities in Wallonia? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Belgium (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Beauwelz** | 70 000 | 350 | 350 |
**Focant** | 80 000 | 390 | 390 |
**Nollevaux** | 139 000 | 420 | 420 |

### What are the less expensive municipalities in Flanders? 
(Average price, median price, price per square meter)

The following was calculated based on the average price/m2:

Flanders (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|:--------:|:-------:|:-------:|
**Bossuit** | 220 000 | 700 | 700 |
**Elverdinge** | 290 000 | 730 | 730 |
**Wijtschate** | 100 000 | 830 | 830 |

## Apartments & houses in the dataset seperated to get insight for the following:

### The most & less expensive municipalities for apartments:

Brussels (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| Auderghem | 429326 | 392500 | 4191 |
| Molenbeek-Saint-Jean| 234724| 219000  | 2288 |
 
Wallonia (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| La Hulpe | 346000 | 332500 | 3898|
| Villers-Sur-Semois | 14500| 14500  | 517 |
 
Flanders (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| Knokke | 550494 | 515000 |  6363 |
| Kermt | 229500 | 229500 | 1213 |

### The most & less expensive municipalities for houses:

Brussels (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| Watermael-Boitsfort | 637965 | 595000 | 3426 |
| Koekelberg | 377500 | 330000 | 1725 |
 
Wallonia (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| Louvain-La-Neuve | 595200 | 580000 |  3159|
| Beauwelz | 70000 | 70000  | 350 |
 
Flanders (€)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Average price&nbsp;&nbsp; | Median/sqm&nbsp;&nbsp; | Average/sqm&nbsp;&nbsp; |
|--------|--------|-------|-------|
| Boutersem | 443245 | 360000 |  3750 |
| Bossuit | 220000 | 220000 | 698 |

## Some map to better understand the situation:

### Average price/sqm for houses & apartments in Belgium:
https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_house&apartment.html

### Average price/sqm for apartments in Belgium:
https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_apartment.html

### Average price/sqm for houses in Belgium:
https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/average_price_per_sqm_belgium_house.html

---

# Debriefing: Difficulties encountered
  
## Teamwork 
  
1. The first difficulty was to **find a method of collaborative work** adapted to our desires.<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> We chose to work via google colab pages and to gather valid cells on this github repo.

2. The second "big" difficulty was to **quickly learn how to use tools** such as matplotlib or seaborn (for data visualisation).
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> This was solved by working on our own, and sharing our work with each other.

3. Another challenge has been the **fair distribution of work**.<br>
<img src="https://raw.githubusercontent.com/Joffreybvn/challenge-collecting-data/master/docs/arrow.svg" width="12"> We do not all have the same ease of understanding in statistics and programming... So everyone was doing their best, and then we merged our result.

4. We encountered a small problem about the file name due to the fact that we don't work on the same environment (Win/Ubuntu...).

## Data Analysis & Interpretation
One of the difficulties encountered with graphs, was that **if we takeall the values without filtering them a minimum, then the visualization is not very relevant**.

<details>
  <summary>Show exemple</summary>
 
  ![Exemple](https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/hareaforprice.png)
  ![Exemple](https://kaiyungtan.github.io/challenge-data-analysis/Visualisation/lareaforprice.png)

  On the first graph all the values are taken into account while on the second, just the areas below 500m² (or 1000m² for the surface of the land) are counted.
  The second graph is **way more clear and understandable** !
  
</details>





