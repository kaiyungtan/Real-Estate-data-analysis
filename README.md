# Challenge: Data Analysis
Use pandas, Data visualisation libraries(Matplotlib or Seaborn) to establish conclusions about a dataset.

### Team member: Kai Yung (Adam) / Mathieu / Joffrey 

## Plan:

### Data Cleaning
1. Understand the requirements.
2. Identify the needs:
  - Dataset with postal code and cities.
  - Research on data visualization library.
  - A new price/m3 column.
  - Average, median price, and per m3.
3. Carefully remove the outliers (error, incorrect or absurd).
4. Eventually: Add facilities data

https://data.gov.be/fr/dataset/328ba4f140ba0e870dfc9c70635fe7c1840980b1

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

Postal codes correspondence to Region/Province

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



### Data Analysis

#### Which variable is the target ?
The price.
Why ? Our mission is to to create a machine learning model to predict prices on Belgium's sales.

#### How many rows and columns ?
We have 40395 rows (observations)
And 18 columns

Why: City Name, Lattitude, Longitude, Province, Region

#### What is the correlation between variable/target ? (Why?)




### Data interpretation

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
