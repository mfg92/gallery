---
title: Food
author: Aman Bhargava
date: '2020-12-20'
slug: []
categories: []
tags:
  - plot
hero: /images/hero-3.jpg
excerpt: Looking at the food habits and nutriotion status of school going children in R.
---
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/htmlwidgets-1.5.3/htmlwidgets.js"></script>

<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/datatables-css-0.0.0/datatables-crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/datatables-binding-0.16/datatables.js"></script>
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/js/jquery.dataTables.min.js"></script>
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/crosstalk-1.1.0.1/css/crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/crosstalk-1.1.0.1/js/crosstalk.min.js"></script>
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/htmlwidgets-1.5.3/htmlwidgets.js"></script>
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/datatables-css-0.0.0/datatables-crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/datatables-binding-0.16/datatables.js"></script>
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/dt-core-1.10.20/js/jquery.dataTables.min.js"></script>
<link href="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/crosstalk-1.1.0.1/css/crosstalk.css" rel="stylesheet" />
<script src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/crosstalk-1.1.0.1/js/crosstalk.min.js"></script>

# The Dataset

{{< gallery match="images/*" sortOrder="desc" rowHeight="150" margins="5" resizeOptions="600x300 q90 Lanczos" showExif="true" previewType="blur" embedPreview="true" loadJQuery="True">}}

This dataset[^1] contains data on nutrition status and food habits collected from 1265 students in rural and urban, private and government schools in Dehradun, Uttarakhand. The questionnaire used to collect the data covered an extensive range of questions, including the participant's family type (nuclear, joint), their daily caloric intake (classified by breakfast, lunch and dinner), their physical activity, food habits, occupation of their parents, height, and weight. 


```r
knitr::opts_chunk$set(out.width='900px', dpi=200)
library(tidyverse)
library(knitr)
library(kableExtra)
library(DT)
library(dplyr)
library(viridis)
library(hrbrthemes)
library(ggThemeAssist)
library(ggridges)
library(forcats)

data = read.csv("https://raw.githubusercontent.com/thedivtagguy/blog/main/dataset.csv")
data$group_code <- gsub("UG", "Urban Government", data$group_code)
data$group_code <- gsub("RG", "Rural Government", data$group_code)
data$group_code <- gsub("RP", "Rural Private", data$group_code)
data$group_code <- gsub("UP", "Urban Private", data$group_code)
```

{{< gallery match="images/*" sortOrder="desc" rowHeight="150" margins="5" resizeOptions="600x300 q90 Lanczos" showExif="true" previewType="blur" embedPreview="true" >}}

Let's expand the table to see what is inside.


```r
Variable_Explain <- c("Type of School (UG/UP/RP/RG)", "Class", "Gender", "Age", "Age Group (15-18, etc)", "Father's Education", "Father's Occupution", "Mother's Education", "Mother's Occupuation", "Vegetarian/Non-Vegetarian", "Do they have breakfast daily?", "Do they carry a school lunch?", "Do they have mid-day meal?", "Do they skip meals?", "How often do they eat out", "Do they eat in front of the TV?", "Calories for Breakfast", "Calories for Tiffin", "Calories for Lunch", "Calories for Evening", "Calories for Dinner", "Other Calories", "Calories for Snacks", "Total Calories", "Recommended Daily Allowance for calories", "Excess or Deficit of RDA", "Percentage of Excess or Deficit", "Frequency of having soft drinks", "Frequency of Having Junk Food", "Frequency of having sweets", "Frequency of having snacks", "Frequency of having noodles", "Frequency of having candies", "Fruit intake", "Distance to school", "How do they go to school?", "Does their school have a playground?", "Does their school give them sports materials?", "Does their school have rides?", "Do they play during recess?", "What do they do during recess?", "Do they play during the evening", "Do they watch TV?", "How long do they watch TV?", "Do they have a computer at home?", "Do they have a playground near their house?", "How do they see themselves?", "Height", "Weight", "BMI", "Z-score", "Nutrition category based on BMI")
```




```r
library(DT)

cols <- colnames(data) %>% as.data.frame()
dataframe.variables <- data.frame(cols, Variable_Explain) 
names(dataframe.variables)[names(dataframe.variables) == "."] <- "Variable Name"
names(dataframe.variables)[names(dataframe.variables) == "Variable_Explain"] <- "Variable Information"
DT::datatable(dataframe.variables)
```

<div id="htmlwidget-1" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52"],["group_code","class","sex","age_years","age_group","father_edu","father_occ","mother_edu","mother_occ","food","BF_daily","school_lunch","MDM","skip_meals","eat_out","eat_TV","BF_calories","tiffin_calories","lunch_calories","eve_calories","dinner_calories","other_calories","snack_cal","total_calories","RDA","excess_deficit","percent_exc_def","softdrinks","junkfood","sweets","snacks","noodles","candies","fruit_intake","distance","tranport_school","playground","sports_material","rides","recess_play","recess_activity","play_eve","watch_TV","hours_TV","computer_home","playground_house","self_image","height","weight","BMI","Z_score","Nutrition_cat"],["Type of School (UG/UP/RP/RG)","Class","Gender","Age","Age Group (15-18, etc)","Father's Education","Father's Occupution","Mother's Education","Mother's Occupuation","Vegetarian/Non-Vegetarian","Do they have breakfast daily?","Do they carry a school lunch?","Do they have mid-day meal?","Do they skip meals?","How often do they eat out","Do they eat in front of the TV?","Calories for Breakfast","Calories for Tiffin","Calories for Lunch","Calories for Evening","Calories for Dinner","Other Calories","Calories for Snacks","Total Calories","Recommended Daily Allowance for calories","Excess or Deficit of RDA","Percentage of Excess or Deficit","Frequency of having soft drinks","Frequency of Having Junk Food","Frequency of having sweets","Frequency of having snacks","Frequency of having noodles","Frequency of having candies","Fruit intake","Distance to school","How do they go to school?","Does their school have a playground?","Does their school give them sports materials?","Does their school have rides?","Do they play during recess?","What do they do during recess?","Do they play during the evening","Do they watch TV?","How long do they watch TV?","Do they have a computer at home?","Do they have a playground near their house?","How do they see themselves?","Height","Weight","BMI","Z-score","Nutrition category based on BMI"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Variable Name<\/th>\n      <th>Variable Information<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"order":[],"autoWidth":false,"orderClasses":false,"columnDefs":[{"orderable":false,"targets":0}]}},"evals":[],"jsHooks":[]}</script>

# What will we try to look at?

The large amount of variables for each observation give us a chance to look into a lot of things, but for the purpose of this piece we will try to look at the following questions: 

1. How many calories do students eat during the day and how does this vary with their
age?

2. As students get older, how does their intake compare against the Recommended Daily Allowance? 

3. Does the midday meal plan have anything to do with caloric intake through the ages?

4. What are their nutritional categories, and how do they vary with school? <br><br>


---

<br>

## Q.1 How many calories do students eat during the day?
### And how does this vary with school-type?


```r
data %>%
  ggplot( aes(x=fct_reorder(group_code, total_calories, .desc = TRUE), y=total_calories, fill=group_code)) +
    geom_boxplot() +
    scale_fill_viridis(discrete = TRUE, alpha=0.6) +
    theme_ipsum() +
    theme(legend.position="none",plot.title = element_text(size=11)) +
    xlab("Type of School") +
    ylab("Calories")+  theme(axis.line = element_line(),
        panel.border = element_blank(),
        panel.background = element_blank(),
        plot.background = element_rect(color = "#E5E5E5"),
        axis.text.x = element_text(angle = 45, hjust = 1))
```

<img src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/figure-html/mean caloric intake by school-type-1.png" width="900px" />

<br>
As the boxplot above shows, students from urban and rural private schools have a better daily caloric intake than those in government schools (irrespective of area). 

<br>
<br>

---

<br>
<br>


## Q.2 How does this caloric intake vary with age?
### And to what can we attribute this pattern?

How does this vary with the various ages, for each school type? For this, it makes sense to have some standard to compare it against. For this, we will use the RDA observations: 

> Recommended Dietary Allowances (RDAs) are the levels of intake of essential nutrients that, on the basis of scientific knowledge, are judged by the Food and Nutrition Board to be adequate to meet the known nutrient needs of practically all healthy persons.[^2]

Alright! The `percent_exc_def` observations for each participant tells us how much lesser or how much more are they consuming, compared against what is recommended for them at that age.


```r
#Editing the dataset to something more meaningful. Mainly rounding off numbers.
data$age_years <- round(data$age_years)
data$age_years <- as.factor(data$age_years)
data$percent_exc_def <- round(data$percent_exc_def)

#New Dataframe with only these values
calories <- data %>% select(percent_exc_def, RDA, age_years, MDM, group_code)



calories %>%
  #Reorder based on age
  mutate(age_years = fct_reorder(age_years, percent_exc_def, .desc = TRUE)) %>%
  ggplot( aes(y=age_years, x=percent_exc_def,  fill=age_years)) +
    geom_density_ridges(alpha=0.6) +
    scale_fill_viridis(discrete=TRUE) +
    scale_color_viridis(discrete=TRUE) +
    theme_ipsum() +
    theme(
      legend.position="none",
      panel.spacing = unit(0.1, "lines"),
      strip.text.x = element_text(size = 8)
    ) +
    labs(title= "Percentage of Excess or Deficit Caloric Intake", subtitle = "(by age) against the Recommended Daily Allowance")+
    xlab("Percentage of Excess/Deficit") +
    ylab("Age")
```

<img src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/figure-html/perc ex, -1.png" width="900px" />
<br>

As students get older, they seem to be drifting further away from their recommended daily allowances and their caloric intakes are decreasing! What could be the possible reason for this pattern? 

<br>
<br>

---

<br>
<br>

## Q.3 What affect, if any, does midday meal have on the excess or deficit of calories against normal amount?
### Does school-type also factor in?



```r
calories %>%
  #Reorder based on age
  mutate(age_years = fct_reorder(age_years, percent_exc_def, .desc = TRUE)) %>%
  ggplot( aes(y=age_years, x=percent_exc_def,  fill=MDM)) +
    geom_density_ridges(alpha=0.6) +
   #Facet Wrap by School Type
    facet_wrap(~group_code) +
    scale_fill_viridis(discrete=TRUE) +
    scale_color_viridis(discrete=TRUE) +
    theme_ipsum() +
    theme(
      panel.spacing = unit(2, "lines"),
      strip.text.x = element_text(size = 8)) +
    labs(title= "Percentage of Excess or Deficit Caloric Intake", subtitle = "(by age) against the Recommended Daily Allowance")+
    xlab("Percentage of Excess/Deficit") +
    ylab("Age")
```

<img src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/figure-html/midday-1.png" width="900px" />

<br>

Interesting! We can almost see the ages at which students stop receiving midday meals in government schools. This only exacerbates the shift away from their RDAs, which you can also compare with their private school counterparts. The difference is clear, there are more students in private schools, both rural and urban, whose intake is far lesser than what it should be at their age.


<br>
<br>

---

 <br>
 <br>

## Q.4 What are their nutritional categories?
### Does their school-type play a role in this?

To see this, first, we need to count the number of students in each category:


```r
#Count Number of Students in Each category
category <- data %>%
  arrange(Nutrition_cat) %>% 
  group_by(Nutrition_cat, group_code) %>% 
  summarise(count = n())
```

Let's see what this looks like: 


```r
DT::datatable(category)
```

<div id="htmlwidget-2" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22"],["normal","normal","normal","normal","obese","obese","obese","obese","overweight","overweight","overweight","overweight","severe underweight","severe underweight","severe underweight","severe underweight","severely obese","severely obese","underweight","underweight","underweight","underweight"],["Rural Government","Rural Private","Urban Government","Urban Private","Rural Government","Rural Private","Urban Government","Urban Private","Rural Government","Rural Private","Urban Government","Urban Private","Rural Government","Rural Private","Urban Government","Urban Private","Rural Private","Urban Private","Rural Government","Rural Private","Urban Government","Urban Private"],[218,223,259,198,2,24,2,30,7,44,12,66,19,6,7,4,3,7,71,17,40,7]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Nutrition_cat<\/th>\n      <th>group_code<\/th>\n      <th>count<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":3},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

And now let's plot it: 


```r
ggplot(category, aes(fill=Nutrition_cat, y=count, x=group_code)) + 
    geom_bar(position="stack", stat="identity")+
    scale_fill_viridis(discrete=TRUE) +
    scale_color_viridis(discrete=TRUE) +
    theme_ipsum() +
    theme(
      panel.spacing = unit(2, "lines"),
      strip.text.x = element_text(size = 8)) +
    labs(title= "Nutritional Category by School Type")+
    xlab("School Type") +
    ylab("Number of Students")
```

<img src="{{< relref "post/2020-12-20-food/index.markdown" >}}index_files/figure-html/plot cat-1.png" width="900px" />


<br>
Students in Urban Private schools are more overweight, whereas those in Rural Government schools are more underweight. This makes sense, given that the kind of school is a good indicator of the student's socio-economic status.

<br>
---


[^1]: Madhavi Bhargava,Overweight and Obesity in School Children of a Hill State in North India, 2016
[^2]: https://www.ncbi.nlm.nih.gov/books/NBK234926/


<p style="text-align: center;">By <a href="https://github.com/thedivtagguy/">Aman Bhargava</a></p>
<p style="text-align: center;"><span style="color: #808080;"><em>amanbhargava2001@gmail.com</em></span></p>
&nbsp;
