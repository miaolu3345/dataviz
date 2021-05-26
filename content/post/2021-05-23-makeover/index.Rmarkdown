---
title: DataViz Makeover - 1
categories:
  - Makeover
tags:
  - blogdown
  - Makeover
subtitle: ''
summary: ''
authors: [Miao Lu]
date: '2021-05-26'
featured: no
disable_jquery: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


The DataViz Makeover-1 report aims to optimize the original graph by using the data from [Department of Statistics in Singapore](https://www.singstat.gov.sg/find-data/search-by-theme/trade-and-investment/merchandise-trade/latest-data).

# 1. The original data
 ![](original_graph.png)
 
# 2. Clarity

 In this section, the origincal data will be implement makeover based on clarity dimension.
 
  
  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1   | The title does not clarify that the Top-6 countries are extracted based on which benchmark, the number of import trading or export trading? Which period of time? | Create a subtitle to give a brief explanation.|
2   | The title shows the period of time is from 2019 to 2020 whereas the X-axis in graph is from 2019 to 2021. | Modify the period in title (2019-2021)
3   | The graphs plot the line year to year, but the legend is written as ‘month of period’, which is absolutely wrong. | Change the legend of x-axis as ‘year of period’.
4   | The x-axis in Japan graph only gives one mark of year (2020), 2019 and 2021 are removed from x-axis. | Include 2019 and 2021 in X-axis.
5   | Name of category on the right is ‘Measure name’, which is not very clear | Rename the title of category as ‘Trading type’

# 3. Aesthentics

In this section, the origincal data will be implement makeover based on Aesthentics dimension.

  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1  | The shading would make people unable to differentiate which line is export and which line is import.  | Make the area under the line blank rather than filled them up with color.
2  | The unit length of Y-axis is different from one to another, which is not clear for comparison. | Standardize the unit length of Y-axis (for example 1 million)
3  | Each graph has different width, which looks inconsistent. It is also difficult to compare. | Set the graphs to keep the same width.
4  | The 6 graph is sorted in a random order instead of a logical way, which is not very suitable for people to compare. | Use one of dimension to sort them.
5  | The x-axis marks are removed which is difficult to detect a clear boundary between each year. | Mark each year in x-axis.

# 4. Porposed Design

 ![](sketch.png)
 
## 4.1 The advantages of sketch
 + Split the export value and import value up for separate comparison.
 + Include quarter marks in x-axis to have a long x-axis so that people can see the detailed changes of value over time.
 + Include the average value for comparison.
 
# 5. Detail steps of visualization

## 5.1 Data preprocessing in excel
There are several rows on top of table which is unnecessary in data, so I removed them from excel.
 ![](unneccessary_title_in_data.png)
Since we need to compare the trading value based on countries instead of region. The first 6 rows show total value based on continents, so I removed them also.
 ![](remove_continent.png)
 
## 5.2 Data preprocessing in Tableau

 + Import two tables of data one by one into Tableau, remove the columns not in 2019-2021.
![](remove_precious_years_data.png)
 + Select all remaining years in the data, right click and select ‘Pivot’.
![](pivot_data.png)
 + Rename the field name 
![](modify_name_and_variable_type.png)

## 5.3 Visualization

Once two tables are done with the 2 steps above, import them into tableau.

 +	Data blending
 
Blend 2 data by linking Data relationship and country relationship between two tables.
![](data_blending.png)
![](data_blending_setup.png)
A sign will appear next to the linked column in primary data.
![](relationship_link_label.png)

 + Drag ‘Date’ into column and sum (import value) , then drag the sum (export value) into  the same position.
 
![](column_and_rows.png)

 + Apply filter
 
Drag either one of country in two table into the filter position (since two country columns are linked). Select particular 6 country in the list.
![](filter_and_add.png)

 + Apply color
 
Drag country into ‘color’ in the pane, since there are lots of countries in the column, so we need to filter first then add. Check the particular 6 countries, then select ok.
The initial colors in the filter are shown like the picture below.
![](initial_filter_color.png)
I add a reference line in each graph to determine the hue of line:

1) The countries whose export number is more than 100M will be set as red hue.
2) The countries whose export number is less than 10M will set as blue hue.
Then the colors are set like the picture below.
![](optimal_color.png)

 + Rename titles and axis.
 
 Title was changed as ‘Merchandise Trade of Six Countries, 2019-2021),
Y-axis title was changed as ‘Import Value (1000 \$)’ and ‘Export Value (1000$),
X-axis title was removed.

## 5.4 Create proportion table

 + Create a new sheet in the Tableau workbook.
 + Drag countries into rows and drag import value into rows, change calculation as sum().
 + Change the way of showcase to ‘highlight table’.
![](show_way.png)
 + Change the value shown as percentage
 
 Right click on the sum (import value) > quick table calculation > percent of total.
 ![](percent_of_total.png)
 
 + Rename header and repeat the same step to create import value table.
  
 ![](final_table_import.png)

## 5.5 Dashboard visualization

 + Add sheets
 
 Drag line graph into the left and drag two tables int the right.
 
  + Add source

Using Object > Text > drag text to the bottom, then add the source and the raw data link.

The final dashboard would be shown like the picture below.
 ![](merchandise.png)
 
# 6. Insights from new graph
 
 + Japan and Taiwan have the similar flat trend in terms of Export value changes over time.
 + Mainland China has the most value in both export and import most of time.
 + Hong Kong has a very large number of export value during 2 years whereas, in comparison to import value, it has the least import value.
 + For United States, we can see a downward trend both in import and export.
