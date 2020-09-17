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
3. Carefully remove the outliers (Weird, incorrect or absurd).
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

1	1000–1299 : Région de Bruxelles-Capitale
2	1300–1499 :  Province du Brabant wallon
3	1500–1999 :  Province du Brabant flamand (arrondissement de Hal-Vilvorde, sauf Overijse)
4	2000–2999 :  Province d'Anvers
5	3000–3499 :  Province du Brabant flamand (arrondissement de Louvain, plus Overijse)
6	3500–3999 :  Province de Limbourg
7	4000–4999 :  Province de Liège
8	5000–5999 : Province de Namur
9	6000–6599 :  Province de Hainaut (1)
10	6600–6999 :  Province de Luxembourg
11	7000–7999 :  Province de Hainaut (2)
12	8000–8999 :  Province de Flandre-Occidentale
13	9000–9999 :  Province de Flandre-Orientale


- create new column Price/m3
### Data Analysis


### Data interpretation
