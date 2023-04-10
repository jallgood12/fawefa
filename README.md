# fawefa

# MechaCar Statistical Analysis 👨‍🔧
 Use of Statistics and R
---
## Background

The MechaCar, AutosRUs' newest prototype, is experiencing production issues that are impeding the manufacturing team's progress. Upper management at AutosRUs has asked Jeremy and the data analytics team to review production data for insights that can help the manufacturing team.

In this challenge we will:

* Conduct multiple linear regression analysis to determine which variables in the dataset predict MechaCar prototype mpg.
* Compile summary data on the pounds per square inch (PSI) of suspension coils from manufacturing lots.
* Use t-tests to see if the manufacturing lots differ statistically from the average population.
* Create a statistical study to compare the performance of MechaCar vehicles to other manufacturers' vehicles.

## :one: Deliverable 1

### 1.1 Use the `library()` function to load the `dplyr` and `tidyverse` packages.

#### Code
```
# 1.1 Load packages
library(dplyr)
library(tidyverse)
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170587149-cc8b18e5-974f-460d-a2c3-477ca617aec0.png)

### 1.2 Import and read in the `MechaCar_mpg.csv` file as a dataframe

#### Code
```
# 1.2 Import and read the csv file MechaCar_mpg.csv
mecha_car <- read.csv(file = 'Data/MechaCar_mpg.csv', check.names = F, stringsAsFactors = F)
head(mecha_car)
```
#### Output

![image](https://user-images.githubusercontent.com/98360572/170586909-4a14a17d-d180-4fb9-9d82-46af3e944483.png)

### 1.3 Perform linear regression using the `lm()` function. In the `lm()` function, pass in all six variables, and add the dataframe created above as the data parameter.

#### Code
```
# 1.3 Linear regression for the six variables using the lm() function
lm(mpg ~ vehicle_length + vehicle_weight + spoiler_angle + ground_clearance + AWD , data = mecha_car)
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170591748-63d56991-2411-4425-9af4-5944d544ea31.png)

### 1.4 Using the `summary()` function, determine the `p-value` and the `r-squared` value for the linear regression model.

#### Code
```
# 1.4 Use summary to find p-value and r-squared for all variables
summary(lm(mpg ~ vehicle_length + vehicle_weight + spoiler_angle + ground_clearance + AWD , data = mecha_car))
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170592016-33ee6c36-0557-48bf-8897-1f39f12388a1.png)

## Linear Regression to Predict MPG

With multiple linear regression, we find which variables (vehicle weight, spoiler angle, ground clearance, AWD, and vehicle length) predict MechaCar prototype mpg. We're asking if MechaCar prototype factors affect mpg.

Hypothesis established using multiple linear regression model:

`H0`: The linear model's slope is zero, or `m = 0`. Our linear model is a flat line with 0 slope.

`Ha`: The slope of the linear model is not zero, or `m ≠ 0`. Our linear model is not really a flat line with a slope larger than 0.

* Which variables/coefficients provided a non-random amount of variance to the mpg values in the dataset?

To discover whether variables affect `mpg` non-randomly, we must examine their `p-values`. If the `p-value is < 0.05`, random variance to the linear model is unlikely, implying those variables affect `mpg`. According to our results shown in the figure below, ground clearance `p-value = 5.21 x 10-8`, vehicle length `p-value = 2.60 x 10-12`, and intercept `p-value = 5.08 x 10-8` provided non-random mpg variance. When an intercept is statistically significant, other variables and factors that affect mpg are missing from the model. These variables may be in our dataset or need to be collected or observed.

![image](https://user-images.githubusercontent.com/98360572/170800519-13d30677-2919-4f69-8b23-c95f1917b146.png)

* Does this linear model predict mpg of MechaCar prototypes effectively? Why or why not?

To assess if this linear model accurately predicts MechaCar `mpg`, we must examine its `r-squared` and `p-value`. According to our data in the figure above, `r-squared` is `0.7149`, indicating a strong positive linear association. This linear model accurately predicts MechaCar prototype `mpg`.

## :two: Deliverable 2

### 2.1 Import and read in the `Suspension_Coil.csv` file as a table

#### Code
```
# 2.1 Import and read the csv file
suspension_coil <- read.csv(file = 'Data/Suspension_Coil.csv', check.names = F, stringsAsFactors = F)
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170603494-c2052c7a-7c71-4a86-b560-f03fd792cce4.png)


### 2.2 Create a `total_summary` dataframe using the `summarize()` function to get the mean, median, variance, and standard deviation of the suspension coil’s PSI column

#### Code

```
# 2.2 Create total summary df, using summarize()
total_summary <-  suspension_coil %>% summarize(Mean=mean(PSI),Median=median(PSI),Variance=var(PSI),SD=sd(PSI), .groups = 'keep')
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170603615-f4863252-b09c-4c44-9745-749792e96139.png)

### 2.3 Write an RScript that creates a `lot_summary` dataframe using the `group_by()` and the `summarize()` functions to group each manufacturing lot by the mean, median, variance, and standard deviation of the suspension coil’s PSI column

#### Code

```
# 2.3 Create lot summary df, using group_by() & summarize()
lot_summary <- suspension_coil %>% group_by(Manufacturing_Lot) %>% summarize(Mean=mean(PSI),Median=median(PSI),Variance=var(PSI),SD=sd(PSI), .groups = 'keep')
```

#### Output
![image](https://user-images.githubusercontent.com/98360572/170603948-4b712b62-8b83-43a7-939d-27054d176d95.png)

## Summary Statistics on Suspension Coils

* The design specifications for the MechaCar suspension coils dictate that the variance of the suspension coils must not exceed 100 pounds per square inch. Does the current manufacturing data meet this design specification for all manufacturing lots in total and each lot individually? Why or why not?

![image](https://user-images.githubusercontent.com/98360572/170603711-56b623b9-fca7-4503-bdca-75f54d3daa2e.png)

![image](https://user-images.githubusercontent.com/98360572/170603987-03230624-cab3-4f06-bddb-538def5977ca.png)

There are no significant differences between the mean and median of Lot 1 and Lot 2 based on the design parameters. There is a lot of variation in Lot 3 compared to the manufacturer's specifications.

## :three: Deliverable 3

### 3.1 write an RScript using the `t.test()` function to determine if the PSI across all manufacturing lots is statistically different from the population mean of 1,500 pounds per square inch.

#### Code
```
# 3.1 t-test across all manufacturing lots against the population mean = 1500 PSI
t.test(suspension_coil$PSI, mu=1500)
```
#### Output
![image](https://user-images.githubusercontent.com/98360572/170604850-edbbcb04-34fa-41d4-b327-34d29fe43336.png)

### 3.2 Write three more RScripts using the `t.test()` function and its `subset()` argument to determine if the PSI for each manufacturing lot is statistically different from the population mean of 1,500 pounds per square inch.

#### Code
```
# 3.1.1 t-test lot1 against population mean = 1500 PSI
lot1 <- suspension_coil %>% subset(Manufacturing_Lot=="Lot1")
t.test(lot1$PSI, mu=1500)

# 3.1.2 t-test lot2 against population mean = 1500 PSI
lot2 <- suspension_coil %>% subset(Manufacturing_Lot=="Lot2")
t.test(lot2$PSI, mu=1500)

# 3.1.3 t-test lot3 against population mean = 1500 PSI
lot3 <- suspension_coil %>% subset(Manufacturing_Lot=="Lot3")
t.test(lot3$PSI, mu=1500)
```


#### Output 3.1.1
![image](https://user-images.githubusercontent.com/98360572/170605237-94f442b3-ca78-471e-b5f0-bf65bef9d968.png)

#### Output 3.1.2
![image](https://user-images.githubusercontent.com/98360572/170605319-2b8d9133-1246-4145-90ec-5be27ad4fc0c.png)

#### Output 3.1.3
![image](https://user-images.githubusercontent.com/98360572/170605396-9a794fb7-e5c1-43ee-aefa-e6cc18df85e1.png)

It has been determined through data analysis that the two suspension coil lots with variation and standard deviation less than 100 pounds per square inch will meet the design specifications. Lot 3's variance and standard deviation, on the other hand, are larger than 100 pounds per square inch, so it fails to meet the design criteria.

## T-Tests on Suspension Coils

It is necessary to conduct a `one-sample t-test` to evaluate whether there is a statistically significant difference between the means of a sample dataset and a population dataset with a given mean of `1,500 PSI`. We establish a `hypothesis with the t-test`.

`H0`: There's no statistical difference between the suspension coil data set mean and `1,500 PSI`.

`Ha`: The suspension coil data set mean is different from its `1,500 PSI` population mean.

To reject or fail to reject our null hypothesis, we examine at the `p-value`, which establishes if there is a statistical difference between the observed sample mean and its presumed population mean. The `p-values` for all manufacturing lots are: 
| Test Number | p-value |
| ----------- | ----------- |
| 3.1      | 0.06028 |
| 3.1.1      | 1 |
| 3.1.2   | 0.6072 |
| 3.1.3   | 0.04168 |

In `3.1`, `3.1.1` and `3.1.2` the `p-value` is over `0.05`, which means that **there is insufficient evidence that the three means are not statistically different**.

In `3.1.3` the `p-value` is lower than `0.05` and so **this lot's mean is different from its `1,500 PSI` population mean**. 

## :four: Deliverable 4

### 4.1 Study Design: MechaCar vs Competition

#### What metric or metrics are you going to test?

Customers are becoming increasingly concerned about pollution and automobile emissions as electric vehicles and environmental consciousness grow in popularity. MechaCar can be a viable alternative for customers who cannot or will not invest in an electric vehicle. MechaCar should be compared to the competitors using a single dependent variable, for example `exhaust system emissions`, compared to a single independent variable, `transmission efficiency`.

#### What is the null hypothesis or alternative hypothesis?

My hypotheses for comparing MechaCar to the competition are as follows:

`H0`: The means of exhaust system emissiomns of all groups are the same.

`Ha`: There is at least one method of exhaust system emissions that is distinct from the rest of the groups.

#### What statistical test would you use to test the hypothesis? And why?

To compare the means of one dependent variable across many independent variables, we will want to do an analysis of variance (ANOVA). Emissions from various cars' exhaust systems, based on transmission efficiency in our example. At least one method for exhaust system emissions must be different from the others for the null hypothesis to be rejected.

#### What data is needed to run the statistical test?

* Exhaust system emissions data
* Transmission efficiency data


---
## :five: References

**Module 15: Using Statistics and R to Boost Your Data Science Repertoire**, https://courses.bootcampspot.com/courses/1145/pages/15-dot-0-1-using-statistics-and-r-to-boost-your-data-science-repertoire, :copyright: 2020-2021 Trilogy Education Services, Web 27 May 2022.

**R Studio Cloud**, https://rstudio.cloud/

**Complete Code Used in this Challenge**, https://github.com/Peteresis/MechaCar_Statistical_Analysis/blob/main/MechaCarChallenge.R
