# Carbon-Emission-Analysis
This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

![image](https://github.com/ngamt0410/Carbon-Emission-Analysis/assets/169979658/f184806a-6588-402f-a19b-11e867ba45d4)





# Data Source: Where Our Data Comes From

Our dataset is compiled from publicly available data from **nature.com** and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).


![image](https://github.com/ngamt0410/Carbon-Emission-Analysis/assets/169979658/60cc05cf-f621-45fa-9c66-ec74402335a8)

## product_emissions
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51                         | 70.41                        | 

## industry_groups
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 

## companies

| id | company_name                  | 
| -: | ----------------------------: | 
| 1  | "Autodesk, Inc."              | 
| 2  | "Casio Computer Co., Ltd."    | 
| 3  | "Cisco Systems, Inc."         | 
| 4  | "CNX Coal Resources, LP"      | 
| 5  | "Coca-Cola Enterprises, Inc." | 

## countries
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        | 

# Explore Data Analysis
## Which products contribute the most to carbon emissions?
    select * from 
    (
      select product_name,
    	  industry_groups.industry_group,
    	  round(sum(carbon_footprint_pcf)/sum(weight_kg), 1) carbon_per_kg
      from product_emissions 
      left join industry_groups
    	  on product_emissions.industry_group_id=industry_groups.id
      group by product_name,
    	industry_groups.industry_group
    ) a
    order by carbon_per_kg desc
    limit 5

| product_name                                                                                                                                                                                                                                                                                                                                                                            | industry_group                                   | carbon_per_kg | 
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | -----------------------------------------------: | ------------: | 
| Electric Motor                                                                                                                                                                                                                                                                                                                                                                          | Capital Goods                                    | 781.4         | 
| Small Rack Mount Switch                                                                                                                                                                                                                                                                                                                                                                 | Technology Hardware & Equipment                  | 736.5         | 
| Alliance (HPLC)                                                                                                                                                                                                                                                                                                                                                                         | "Pharmaceuticals, Biotechnology & Life Sciences" | 681.6         | 
| "ACQUITY® UPLC, ACQUITY® I-Class, ACQUITY® H-Class"                                                                                                                                                                                                                                                                                                                                     | "Pharmaceuticals, Biotechnology & Life Sciences" | 659.2         | 
| "Bloomberg's standard-issue flat panel configuration (prior to 2010) was two 19\" panels mounted on a metal stand. In early 2010 Bloomberg engaged in the WRI Product Life Cycle Roadtest for this functional unit (cradle-to-grave). The functional unit has a lifespan of 5 years, so the emissions indicated [in this report] are the full emissions associated with that lifespan." | Media                                            | 646.4         | 

* Top 5 Products most to carbon emissions per kg are Electric Motor, Small Rack Mount Switch, Alliance (HPLC), "ACQUITY® UPLC, ACQUITY® I-Class, ACQUITY® H-Class"
* Top Industry produce highest carbon emissions per kg are Capital Goods, Technology Hardware & Equipment, **Pharmaceuticals, Biotechnology & Life**

