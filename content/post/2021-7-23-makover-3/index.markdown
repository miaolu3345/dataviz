---
title: DataViz Makeover - 3
categories:
  - Post
tags:
  - blogdown
  - Post
subtitle: ''
summary: ''
authors: [Miao Lu]
date: '2021-07-23'
featured: no
disable_jquery: no
image:
  caption: ''
  focal_point: ''
  preview_only: yes
projects: []
---

The DataViz Makeover-3 report aims to optimize the original graph by using the data from [Open Data Covid-19 Provinsi DKI Jakarta](https://riwayat-file-covid-19-dki-jakarta-jakartagis.hub.arcgis.com/).

# 1. The original data
 ![](feature.jpeg)
 
  ![](feature-bar.jpeg)
 
# 2. Clarity

 In this section, the original data will implemented makeover based on clarity dimension.
 
  
  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1   | The scatter plot displays all figures of districts, but the title just says it shows top-5 districts which is inappropriate. | Just add a sub-title to explain that the graph also mark top-5 districts.
2   | Kota means city in English, so it should not be a sub-strict in the title | Modify the sub-district to city.
3   | The label of y-axis in the scatter graph is too tighten to tell which point corresponding to which label | Add the reference line in the pane to help people refer to.
4   | The title of scatter graph describe it as accumulative number, whereas the x-axis just shows the number of death which is in consistent. | Change the x-axis label as 'accumulative number of deaths'.


# 3. Aesthentics

In this section, the original data will implement makeover based on Aesthetics dimension.

  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1  | The marks in the pane overlapped the points in the graph. | Size down the marks in the pane. 
2  | The label of Y-axis in each graph seems a bit redundant. | Remove the label of Y-axis.
3  | There is no any reference to see whether the condistion of each district is bad or relative fine. | Add some reference lines in the pane to differentiate the condition.


# 4. Porposed Design

 ![](original_graph.jpeg)
 
## 4.1 The advantages of sketch
 + Add the relationship between the mortality rate and positive case, which would be clear to evaluate the condition.
 + Include the uncertainty in the second graph, which is clearer than before to compare the variance.
 + Add the filter to select the districts, it would be helpful when people want to compare the similar districts.
 
# 5. Detail steps of visualization

## 5.1 Data preprocessing in excel
There is a row which might be the sub-title of excel, I excluded it in the excel since there is no need to keep it.
 ![](sub-title_excel.png)
 
 Plus, there are several columns without value and we only focus on the positive case and mortality case, in this case I just removed them.
 ![](null_columns.png) 

 
## 5.2 Data preparation in Tableau

 + Import the processed data into Tableau, rename the data as '30 Juni 2021'. The data would be shown like the picture below:
 
![](data_in_tab.png) 
## 5.3 Graph visualization

> scatter plot makeover

 + Create a new fields
 
Created a new field, name it as 'mortality rate' and the formula is shown as below:
 
![](mortality_rate.png)

 + plot the basic graph
 
Drag and drop 'positif' into column, drag and drop 'mortality rate' into row.

![](column_row_scatter.png)

Put 'name kecamatan' into detail in the pane and also put it into the filter.

 ![](name_kecamanta.png)
 
  + Differentiate the district using color
  
Created a new field, name it as 'category-mortality', in this case, I would like to use this field to differentiate the districts where mortality rate is greater than average number and less than average number. The formula of it is shown as below.

![](category_mor.png)

Drag and drop 'category_mor' into the color in the pane, as the picture below.

![](mor_color.png)

 + Add reference lines
 
Insert 2 reference lines in the pane, the first one is the average mortality rate. Set it as dot line and the color is in blue.

 ![](mortality_rate_reference.png)
The second one is the average number of positive case. Set it as dot line as well, but the color of line is in red.

 ![](positive_reference.png)
  + Show filter

Right click on the filter and click on show filter, the filter display mode is set to be 'multiple value drop down'.

 ![](filter_set.png)
 
 + Optimize the visualization
 
 Rename the x-axis as 'The number of positive cases', name the y-axis as 'mortality rate'.
 Rename the Title of graph as 'The relationship between mortality rate and positive cases in all districts, 30 June'
 
 > Bar chart make over
 
 + Create several new fields
 
 Create a new field, name it as avg, the formula is shown as below:
 
 ![](avg_formula.png)
  
Create a new field, name it as sd(standard deviation), the formula is shown as below:

![](sd_formula.png)


Create a new field, name it as SE and the formula is shown as below:

 ![](SE_formula.png)
 
Finally, created the last 2 new fields to represent the upper limit and lower limit of the average number. The formula is shown as below:

![](upper_lower.png)

+ Plot the graph 

Put 'Nama Kota' into the column, put 'avg' into the row.
Drag and drop 'lower_limit' to the top x-axis.
![](lower_limit_drag.gif)
Repeat previous step, put the upper_limit into the same place.
Turn the graph into line, and put the measure value into the path area in the pane.

![](line.png)
Finally, make the color of the line to be same as the point of average number, optimize the size of the line and size of the circle in the middle of the line.

![](line_color.png)

 + Optimize the visualization
 
Since there are 2 x-axis in the pane, put the mouse in the top x-axis area, right click and select 'Edit Axis', move to 'Tick Mark' page and check the None in 'Tick mark' area, as the picture below.

![](remove_x.png)

Plus, the name of Y-axis looks a bit redundant, so put the mouse around the name of y-axis, right click and select 'Hidefield labelforRows' in the dropdown list.

![](remove_y_title.png)
Rename the title of the graph as 'Average accumulative number with variance in each district'.

## 5.4 Dashboard visualization

Put the 2 graph into the dashboard, the scatter plot is on the top the uncertainty plot is on the bottom. add one text on the bottom, add the source into the text.

The final dashboard would be shown as the picture below.

![](final.png)


 
 
# 6. Insights from new graph
 
 + relationship between mortality rate and number of positive case
  
The new scatter graph shows the deeper insight than last graph, it is useful to not only look at the number of deaths but also look at the mortality rate. The district on the top-left graph should be considered as 'high-risk' districts, since they have a relative low positive cases but higher mortality rate than average.

![](high_risk.png)
Plus, comparing to other districts,'LURA DKI JAKARTA' looks in a less bad condition, since it has a lot of positive cases for now but the mortality rate is less than average number.

![](good_condition.png)

 + variance of average number analysis
 
In the second graph, it mainly focuses on the uncertainty of average number since each city includes many districts. From the graph, we can see that 'KAB.ADM.KEP.SERIBU.' city has the least number of average number and it also has the least fluctuation comparing to other cities. It means that the condition of positive cases is a bit stable and predictable.

![](KAB.png)

'JAKARTA UTARA' has the highest average number and its variance is larger than any other city, meaning that it is in a unstable condition and need to pay more attention.

![](UTAR.png)

All other cities have a similar average number ranging from 1000 to 2000 and the variance is around 500.
