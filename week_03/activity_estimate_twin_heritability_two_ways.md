---

title: Activity, Estimate Heritability from Twin Data using Two Methods in R

---

In this activity, you will estimate the heritability for scores on reading, grammar, or writing tests among twins, using both Falconer's equations and structural equation modeling (using a shortcut function that does it for you).

You will be modifying my example code analyzing the math phenotype as an example to analyze a different phenotype of your choosing. You may want to start by running my code as-is, to confirm that you are getting the same answers I describe below, before modifying the code to analyze either the reading, grammar, or writing phenotypes for your activity answers.

You will need:

two free software packages:
- R, https://www.r-project.org/Links to an external site.; and 
- RStudio, https://rstudio.com/products/rstudio/Links to an external site. (the free "desktop" version).
***OR*** A no-downloads-required option, you can use Rstudio in your web browser via the UIUC AnyWare system: https://uiucanyware.cloud.com/; instructions here: https://answers.uillinois.edu/105846

## Step 1

Open RStudio (it is a user-friendly wrapper/organizer for R, which is the base statistical software we're using).

## Step 2

In the left-side console area, paste the following code and hit enter to import the dataset from the web and save it to a dataset named 'twin_data':

~~~
twin_data = read.csv("https://ibg.colorado.edu/cdrom2020/colodro/bivariate/multiTwin.csv")
~~~

In R, when you see something that is text followed by parentheses (eg. read.csv()), that is a function that will operate on the inputs and options specified within the parentheses. You can look up functions in the Help tab in the bottom right panel in RStudio, which will show you the available options, some examples of how to use the function, and often suggest related functions to consider.

Notice after running this line of code that a descriptor has appeared in the upper right corner of the screen listing twin_data under the Data header on the Environment tab, identifying 1200 obs. (observations, or rows) of 22 variables (or columns)

## Step 3

Take a look at the first few rows of the dataset to get a sense of what's in there:

~~~
head(twin_data)
~~~

This will print to the console area the first six lines of data plus the variable names at the top. These data are arranged so that both twins from within a family are on a single row. The 'FAMID' variable is a unique identifier for each family. The last variable, 'zyg', is the twin zygosity (here it's coded as: 1 = MZ male, 2 = MZ female, 3 = DZ male, 4 = DZ female, 5 = DZ opposite-sex where Twin 1 is male, 6 = DZ opposite sex where Twin 1 is female). Every other variable ends in either \_1 or \_2; this identifies which twin within the pair that variable is referring to (that is, is it a variable containing the data from Twin 1 or from Twin 2?). Here we've got information on sex (0 = female, 1 = male), age, and scores on reading, grammar, writing, and math (the variables that start with Z indicate that they have been z-scored, or scaled, so that they have a mean of 0 and a variance of 1).

## Step 4

To make estimating our correlations easier, we're going to split the data into two datasets, containing (1) MZ twin pairs and (2) only same-sex DZ twin pairs.

~~~
mz_data = subset(twin_data, zyg==1|zyg==2)
dz_data = subset(twin_data, zyg==3|zyg==4)
~~~

The pipe (|) here means "or", so it's taking all twins with zygosity = 1 or 2 and assigning them to the mz_data dataset, and all twins with zygosity = 3 or 4 and assigning them to the dz_data dataset. Those two new datasets should now appear in your upper right side Environment list, both of which still have 22 variables, but with only 500 observations in the dz_data group and 400 observations in the mz_data group.

## Step 5

Decide which phenotype you'd like to analyze: Reading, Grammar, or Writing. DO NOT use the Math phenotype -- I use Math from here onward for the demonstration. For credit for the participation activity, you will need to MODIFY the code examples I'm providing below to reference either the Zread, or the Zgram, or the Zwrit variables (whichever you choose) instead of the Zmath variables used in the examples.

## Step 6

For the z-scored version of the phenotype you're interested in, estimate the twin correlations for the monozygotic and dizygotic pairs separately.

~~~
cor(mz_data$Zmath_1,mz_data$Zmath_2)
cor(dz_data$Zmath_1,dz_data$Zmath_2)
~~~

Note that the text before the $s in the above statements identifies the dataset where the data are located, and the text after the $s identified the variable name within that dataset. Take note of the numbers; you'll need them in Step 8. For the z-scored math phenotype, we get an MZ twin correlation of 0.75 (rounded to two decimal places) and a DZ twin correlation of 0.48.

## Step 7

Make a couple of graphs!

~~~
plot(mz_data$Zmath_1,mz_data$Zmath_2)
plot(dz_data$Zmath_1,dz_data$Zmath_2)
~~~

The scatterplots will appear in the bottom right panel. You can use the blue arrows at the top to move back and forth between plots you've created. The twin 1 scores are arrayed along the horizontal x-axis and the twin 2 scores are arrayed along the vertical y-axis. You can see that the MZ twin data form a straighter/tighter line than the DZ twin data, indicating a stronger correlation (that is, you'd be better at predicting Twin 2's score from Twin 1's score if they're MZ twins than if they're DZ twins).

## Step 8

Calculate Falconer variance components. You can either do this by putting your numbers from Step 6 into the equations (A = 2*(rMZ-rDZ); C = 2\*rDZ - rMZ; E = 1 - rMZ), or by putting the correlation calculations directly into the formula, as in:

~~~
2*(cor(mz_data$Zmath_1,mz_data$Zmath_2)-cor(dz_data$Zmath_1,dz_data$Zmath_2))   # A estimate
2*cor(dz_data$Zmath_1,dz_data$Zmath_2) - cor(mz_data$Zmath_1,mz_data$Zmath_2)   # C estimate
1 - cor(mz_data$Zmath_1,mz_data$Zmath_2)   # E estimate
~~~

Hint: The three numbers should add up to around 1.0 - they might not be exact, but they should be close. Here, I get A = 0.54 or 54%, C = 0.21 or 21%, and E = 0.25 or 25%. Any text that comes after a # on a line is a comment - it will not be run as code.

## Step 9

Install the 'umx' package (a bundle of functions).

~~~
install.packages("umx")   # This will take a minute, don't panic
library("umx")   # After it's installed, you need to tell R that you want to use it
~~~

Windows users: You may get an error if there's a space in your username (e.g. "Jaime's Computer"). Here's two rstudio support forum posts with suggested fixes: thread 1, thread 2

## Step 10

Run the standard twin ACE variance components model.

~~~
umxACE(selDVs = "Zmath", sep = "_", dzData = dz_data, mzData = mz_data)
~~~

You'll get a bunch of output printed on the console, including the path estimates; look for a table that looks like this: 

~~~
| | a1| c1| e1|

|:------|---:|-----:|-----:|

|Zmath_ | 0.7| 0.498| 0.512|
~~~

Note that these numbers do NOT sum to 1.0; you'll need to square them (number^2) to transform them into the variance component (%) metric. So here, A = 0.7^2 = 49%, C = 0.498^2 = 25%, E = 0.512^2 = 26%.

If you also want to view the path diagram version of the result in the right-side viewer panel, you'll need to add the umxPlotACE() command as a wrapper on the code you just ran, like this:

~~~
umxPlotACE(umxACE(selDVs = "Zmath", sep = "_", dzData = dz_data, mzData = mz_data))
~~~

## Submission Instructions

Once you have completed the above steps analyzing your selected phenotype (readings, writing, or grammar - NOT math), answer the following questions:

1. Which phenotype did you look at - reading, writing, or grammar?
2. What was the MZ twin correlation for your phenotype? What was the DZ twin correlation? (from Step 6)
3. What were the Falconer ACE estimates for your phenotype? (from Step 8)
4. What were the structural equation model ACE estimates for your phenotype? (from Step 10)
5. In no more than 1-2 sentences, what do you conclude about the influence of additive genetic, shared environmental, and non-shared environmental factors on your phenotype?

--------

Home: [Table of Contents](../README.md)