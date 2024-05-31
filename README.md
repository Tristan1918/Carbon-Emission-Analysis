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


