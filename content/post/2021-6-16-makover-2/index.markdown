---
title: DataViz Makeover - 2
categories:
  - Post
tags:
  - blogdown
  - Post
subtitle: ''
summary: ''
authors: [Miao Lu]
date: '2021-06-16'
featured: no
disable_jquery: no
image:
  caption: ''
  focal_point: ''
  preview_only: yes
projects: []
---

The DataViz Makeover-2 report aims to optimize the original graph by using the data from [Department of Statistics in Singapore](https://www.singstat.gov.sg/modules/infographics/singapore-international-trade).

# 1. The original data
 ![](original.jpeg)
 
# 2. Clarity

 In this section, the original data will implemented makeover based on clarity dimension.
 
  
  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1   | Tooltip error β The figure in tooltip is not clarified, does it show the number of export or import? Or the difference between them. | Add some explanation of the figure in tooltip.|
2   | Axis error β the number of some countries in tooltip are inconsistent with the x-axis/y-axis.For example, the number of Mainland China has exceeded either one of axis number. | Modify the unit of x-axis/y-axis.
3   | Storytelling error β The results from storytelling is from past time instead of 2020. | Try to get some insights from the graph.
4   | Net importer/exporter is an inappropriate definition. | We can call it as trade deficit area or trade surplus area.


# 3. Aesthentics

In this section, the original data will implement makeover based on Aesthetics dimension.

  Index         |       Critiques      |  Improvement
------------- | ---------------------- | ----------------
1  | Circles are overlapping. Itβs hard to distinguish each area. | Reduce the size of each circle.
2  | The start point of x-axis and y-axis are less than 0. | Set the start point of x-axis and y-axis as 0.
3  | The tooltip of Mainland China and Hong Kong are out of the graph. | Reduce the size of tooltip.
4  | The units of x-axis and y-axis are unknown. | Add the unit of number along the x-axis and y-axis.

# 4. Porposed Design

 ![](framework.jpeg)
 
## 4.1 The advantages of sketch
 + Have an animation to control the time period.
 + The percentile of value can help to show the ranking.
 + Additional bar chart can compare the import value and export value over time.
 
# 5. Detail steps of visualization

## 5.1 Data preprocessing in excel
There are several rows on top of table which is unnecessary in data, so I removed them from excel.
 ![](excel.png)

 
## 5.2 Data preparation in Tableau

 + Import two tables of data one by one into Tableau, select all columns except for variable, right click and select βPivotβ.
![](pivot.png)
 + Split variable field
 
 Split the variable field into 2 columns, one is country name, the other one is currency.
 
![](split.png)
 + Rename the field names
 
Rename the current field to a propriate name.

Pivot field name β date

Pivot field value β import value

Variable-split 1 β country

Variable- split2 β unit

Variable β Hide it.

Repeat the steps above again to modify export table.

 + Change the data type in Date field and Value field
 ![](change_data_type.png)

## 5.3 Bubble plot visualization

Once two tables are done with the steps above, import them into tableau.

 +	Data blending
 
Blend 2 data source by linking Data relationship and country relationship between two tables.

![](data_blending.png)

A sign will appear next to the linked column in primary data.
![](relationship.png)

 + Calculate the real number of import/ export value
 
Since different value has different unit, so I created the real value by creating a new field, the formula is shown as below..
 
![](unit_num.png)

Then I created another new field to calculate the final value of import. Repeat the same step to get the final value of export.

![](final_value.png)

+ Drag βsum(export value-final)β into column, change the table calculation as percentile.Change the compute using as βcountryβ.Drag βsum(export value-final) to row, repeate the same step to modify it. 

![](computing_use_and_quick_cal.png)
+ Drag βcountryβ to detail, drag sum(export value- final) to size, drag sum(import value-final) to color.

![](pane_detail.png)

In this step, we can see that color represents the import value, meaning that the darker the circle is, the larger the import value is. And size represents export value, meaning that the larger the circle is, the larger the export value is.


 + Apply filter
 
Drag either one of country in two data sources into the filter (since two country columns are linked). Show the filter and select the area that I want to see, the default countries I check is top-10 Import value of the countries.

![](filter_top_10_country.png)

Right click show filter on the right so that I can filter the area in the future.
Drag the date field into the filter as well, since sometimes I just want to look at particular period of time instead of all time period.The default year I select is from 2011 to 2020.

 + Add diagonal reference line
 
Create a new calculation field named reference line, the content of field is equal to export value, shown as below.

![](diagnal_line_formula.png)

Drag the reference line to row, set the computing use as country and set quick table calculation as percentile, same as the export value field. Then minimize the size of line, the graph shown like the picture below.

![](before_dual.png)
Right click the reference line in the row, select dual axis in the menu. Two field will be put together.

![](click_dual.png)
Right click the reference line on the right y-axis, select synchronize Axis, then 2 y-axises will be consistent. Last step is to remove header on the right y-axis to keep on y-axis.

![](synchronize_and_remove_header.png)
Add the annotation on the right of diagonal line, the content of annotation is βTrade surplusβ and add another annotation on the left of line, the content of annotation is βTrade deficitβ.

+ Edit tooltip

Create a new calculation field named ranking by import, the formula is shown as below.

![](ranking_formula.png)

Create the similar calculation for export value data source, name it as ranking by export.
Open tooltip and edit the content of it, like the picture below.

![](tooltip_content.png)
Modify the format of import value and export value with billion unit and β$β.

![](value_format.png)

The content of tooltip in sheet will be shown as the picture below.
![](final_tooltip.png)

+ Add animation

Drag the month(date) to page area so that I can see the changes of graph over time.

![](create_animation.png)
Check the βshow historyβ box and set the speed as normal.

![](animation_setting.png)


 + Rename titles and axis.
 
Title was changed as βMerchandise Trade Performance- <page name>.

![](title.png)

Y-axis title was changed as βPercentile of Import Valueβ.

X-axis title was changed as βPercentile of Export Valueβ.



## 5.4 Bar chart visualisation

The bar chart aims to compare the import value and export value in particular country/area.

 + Drag sum(import value_final) and sum(export value_final) to column and drag country to row.
 
 + Right click the x-axis of import value, check reverse box.
![](reverse_chart.png)
 + Drag import value and export value to color respectively.
![](drag_to_color.png)
 + Add balance field

create a new calculation field named balance, the formula is shown as below.

![](balance_formula.png) 

created the other new field named balance-color, the formula is shown as below.

![](balance_color_formula.png) 
 
 Drag balance to column and drag balance-color to color area. 
 
 + Add filter
 
 Drag either one of country in two data sources into the filter (since two country columns are linked). Show the filter and select the area that I want to see, the default countries I check is top-10 Import value of the countries.
 
![](filter_bar_chart.png)
 + Add animation
 
 Drag the month(date) to page area so that I can see the changes of graph over time.
 

## 5.5 Time series of balance

 + Drag balance to rows and drag month(date) to column, change the format of balance like the picture below.
 
 ![](format_of_balance.png)
 
 + Add animation and filter
 
 Drag year(date) to filter, set the time period is from 2011 to 2020, consistent with other sheets. Drag month(date) to page so that the animation control in dashboard can be applied to the chart.
 
 ![](animation_time.png)



## 5.6 Dashboard visualization

 + Apply country filter to all sheets

Right click country filter, click on apply to worksheet, select all using this data source.

![](apply_to_all_sheets.png)

 + Drag bar chart and bubble plot into the dashboard, modify the layout of them.
 
 + Add source
 
 Using Object > Text > drag text to the bottom, then add the source and the raw data link.
 
 The final dashboard would be shown like the picture below.
 
 ![](dashboard1.png)
 
 
# 6. Insights from new graph
 
 + Europe:
  
  Europe has always been the top ranking importer over past 10 years. And the import value was always larger than export value.
 ![](ranking_by_import_value.png)
 
 In 2016 May, the export increased significantly even equal to import value,and 2 values are ranking 1 at the same time. The next few months of 2016, the gap between import value and export value remain small. After 2016, the gap returned to a relative large degree as normal.
 
![](ranking_equal_europe.png)
 
 + Mainland China: Mainland China was always ranking as 2 from 2013 onward, sometimes even became first ranking after 2020 as for the import value. 
 
 ![](ranking_1_china.png)
 
 The export value of Mainland China was always a bit larger than export value alla the time except for 2019 October, November and 2013 March. 
 
 ![](export_balance_china.png)
 
 
 + Indonesia: Indonesia used to be a powerful exporter, however, after 2014, the export value stared to go down to the lower lever and remain fluctuating, since 2020 March, the export value even went down sharply until 2021.
 
![](july_2013_indo.png)

![](may_2015_indo.png)
 
 + Malaysia: The import value of Malaysia used to be the top ranking until 2014, Mainland China caught up and exceed Malaysia. But the balance between import value and export value remain unchanged -- more or less than 1 billion.
