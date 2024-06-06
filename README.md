# Carbon-Emission-Analysis

What is the project about?

![image](https://cdn.prod.website-files.com/63d2626cedcc41357cddabdf/664b69922ce036842dd8a5d0_chris-leboutillier-TUJud0AWAPI-unsplash-p-800.webp)

Photo by Chris LeBoutillier (unsplash.com)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.

Data Source: Where Our Data Comes From

Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

Data Structure

![image](https://github.com/Tristan1918/Carbon-Emission-Analysis/assets/170103101/930e2bf0-99fc-4233-9241-056bcf6af8a4)


The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.

Which products contribute the most to carbon emissions?

```sql
select * 
from product_emissions
order by carbon_footprint_pcf desc
limit 5
```

id           | company_id | country_id | industry_group_id | year | product_name                                                       | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf                       | operations_percent_total_pcf                     | downstream_percent_total_pcf                     | 
| -----------: | ---------: | ---------: | ----------------: | ---: | -----------------------------------------------------------------: | --------: | -------------------: | -----------------------------------------------: | -----------------------------------------------: | -----------------------------------------------: | 
| 22917-4-2015 | 10         | 23         | 13                | 2015 | Wind Turbine G128 5 Megawats                                       | 600000    | 3718044              | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 22917-5-2015 | 10         | 23         | 13                | 2015 | Wind Turbine G132 5 Megawats                                       | 600000    | 3276187              | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 22917-3-2015 | 10         | 23         | 13                | 2015 | Wind Turbine G114 2 Megawats                                       | 400000    | 1532608              | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 22917-2-2015 | 10         | 23         | 13                | 2015 | Wind Turbine G90 2 Megawats                                        | 361000    | 1251625              | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 8362-1-2016  | 11         | 16         | 7                 | 2016 | Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit. | 2272.33   | 191687               | 2.90                                             | 0.25                                             | 96.85                                            | 


What are the industry groups of these products?

```sql
select * 
from industry_groups
where id = 7 or id = 13
```

| id | industry_group                     | 
| -: | ---------------------------------: | 
| 7  | Automobiles & Components           | 
| 13 | Electrical Equipment and Machinery | 

What are the industries with the highest contribution to carbon emissions?

```sql
select industry_groups.industry_group, SUM(carbon_footprint_pcf) 
from industry_groups
join product_emissions
on industry_groups.id = product_emissions.industry_group_id
group by industry_groups.industry_group
order by SUM(carbon_footprint_pcf) desc
limit 5
```

| industry_group                     | SUM(carbon_footprint_pcf) | 
| ---------------------------------: | ------------------------: | 
| Electrical Equipment and Machinery | 9801558                   | 
| Automobiles & Components           | 2582264                   | 
| Materials                          | 577595                    | 
| Technology Hardware & Equipment    | 363776                    | 
| Capital Goods                      | 258712                    | 

What are the companies with the highest contribution to carbon emissions?

```sql
select companies.company_name, SUM(carbon_footprint_pcf) 
from companies
join product_emissions
on companies.id = product_emissions.company_id
group by companies.company_name
order by SUM(carbon_footprint_pcf) desc
limit 5
```

| company_name                            | SUM(carbon_footprint_pcf) | 
| --------------------------------------: | ------------------------: | 
| Gamesa Corporación Tecnológica, S.A.  | 9778464                   | 
| Daimler AG                              | 1594300                   | 
| Volkswagen AG                           | 655960                    | 
| Mitsubishi Gas Chemical Company, Inc. | 212016                    | 
| Hino Motors, Ltd.                     | 191687                    | 

What are the countries with the highest contribution to carbon emissions?

```sql
select countries.country_name, SUM(carbon_footprint_pcf)
from countries
join product_emissions
on countries.id = product_emissions.country_id
group by countries.country_name
order by SUM(carbon_footprint_pcf) desc
limit 5
```

| country_name | SUM(carbon_footprint_pcf) | 
| -----------: | ------------------------: | 
| Spain        | 9786130                   | 
| Germany      | 2251225                   | 
| Japan        | 653237                    | 
| USA          | 518381                    | 
| South Korea  | 186965                    | 

What is the trend of carbon footprints (PCFs) over the years?
 ```sql
select year, sum(carbon_footprint_pcf)
from product_emissions
group by year
```

| year | sum(carbon_footprint_pcf) | 
| ---: | ------------------------: | 
| 2013 | 503857                    | 
| 2014 | 624226                    | 
| 2015 | 10840415                  | 
| 2016 | 1640182                   | 
| 2017 | 340271                    | 

Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

```sql
select product_emissions.year, industry_groups.industry_group, sum(carbon_footprint_pcf)
from product_emissions
join industry_groups
on product_emissions.industry_group_id = industry_groups.id
group by industry_groups.industry_group
order by product_emissions.year
```


