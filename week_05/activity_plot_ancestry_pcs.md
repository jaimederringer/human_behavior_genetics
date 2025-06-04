---

title: Activity, Plot Ancestry Principle Components in R

---

In this activity, you will plot ancestry principal components estimated among a sample of relatively homogeneous Dutch participants, to see how the statistical signal we identify from genotypes aligns with geographic location (at least among groups with limited recent or distant mobility; that is, among participants whose families have pretty much lived in the same place for hundreds of years).

You will be working with Dutch ancestry data described here: https://ibg.colorado.edu/cdrom2019/abdelouia/populationStratification/abdel_pop_strat_boulder_2019.pdf

Specifically, you'll be making the plot on slide 49 using a modified version of the R code posted here: https://ibg.colorado.edu/cdrom2019/abdelouia/populationStratification/results/plot_NL.R

This practical is a subset of a larger activity created by Dr. Abdel Abdellaoui for the 2019 International Behavioral Genetics Workshop, a week-long workshop that trains (mostly) grad students and early career researchers (including me, many years ago) in statistical/computational genetic methods. It's been running since 1990 and is an incredible resource because they make their materials publicly available (now online, but you'll notice the containing folder is labeled cdrom2019 because they used to be mailed to participants on CDs).

You will need two free software packages:

- R, https://www.r-project.org/; and 
- RStudio, https://rstudio.com/products/rstudio/ (the free "desktop" version).
***OR*** A no-downloads-required option, you can use Rstudio in your web browser via the UIUC AnyWare system: https://uiucanyware.cloud.com/; instructions here: https://answers.uillinois.edu/105846

## Step 1

Open RStudio (it is a user-friendly wrapper/organizer for R, which is the base statistical software we're using).

## Step 2

In the left-side console area, paste the following code and hit enter to import two datasets from the web and save them to datasets named 'PCs_NL' (the genomic principal components) and 'province' (a key for which participants live where):

~~~
PCs_NL = read.delim(file="https://ibg.colorado.edu/cdrom2019/abdelouia/populationStratification/results/dutch.R.evec",skip=1,head=FALSE,sep="")
province = read.delim(file="https://ibg.colorado.edu/cdrom2019/abdelouia/populationStratification/results/NL_provinces.txt",skip=1,head=FALSE,sep="")
~~~

In R, when you see something that is text followed by parentheses (eg. read.csv()), that is a function that will operate on the inputs and options specified within the parentheses. You can look up functions in the Help tab in the bottom right panel in RStudio, which will show you the available options, some examples of how to use the function, and often suggest related functions to consider.

Notice after running this line of code that a descriptor has appeared in the upper right corner of the screen listing PCs_NL under the Data header on the Environment tab, identifying 151 obs. (observations, or rows) of 13 variables (or columns), and the province dataset as containing 170 obs. Of 3 variables.

## Step 3

Take a look at the first few rows of the dataset to get a sense of what's in there:

~~~
head(PCs_NL)
head(province)
~~~

This will print to the console area the first six lines of data plus the variable names at the top. 

In both files, the variables named V1 and V2 provide unique identifiers of the individuals. In the PCs_NL dataset, the variables V3 - V12 provide the first 10 genomic principal components (the 10 "largest signals" of genetic similarity among the participants). In the province dataset, the V3 variable provides the mapping of the individuals to the provinces (we'll define the key for labeling these in Step 5).

## Step 4

Look at some distributions of the variables:

~~~
hist(PCs_NL$V3)		# this will make a histogram in the bottom right panel
table(province$V3)	# this will make a table of number of observations per value in the console panel
~~~

I like to plot variables in a new dataset, just to look for weirdnesses or places where I might have misunderstood the data.

Note that the text before the $s in the above statements identifies the dataset where the data are located, and the text after the $s identified the variable name within that dataset. Text after a # is a comment; even if you paste it into the console, R will not attempt to "run" it; very useful for annotating code so you can remember what you've done and why.

## Step 5

Merge the two datasets so you have both the principal components and province information in a single dataset:

~~~
dutch_data = merge(PCs_NL,province,by.x=c("V1","V2"),by.y=c("V1","V2"))
~~~

The 'by' statement tells R which variables should be used to match observations/participants. If you preview the new dataset (head(dutch_data)), you'll see that R has renamed the V3 variables to avoid having multiple variables with the same name in a single dataset: V3.x was the V3 variable from the dataset listed first in the merge command - so the 1st PC from the PCs_NL dataset; V3.y was the province key from the province dataset. You can check this intuition by running hist(dutch_data$V3.x) and table(dutch_data$V3.y) and seeing that they match your results from Step 4.

## Step 6

Rename the variables to be easier to read/remember:

~~~
colnames(dutch_data) = c("FID","IID",paste0("PC",1:10),"V13","province")
~~~

I left V13 as-is; it's a holdover column from creation of the PCs. To check that it worked, run head(dutch_data) again. FID and IID stand for family ID and individual ID; in datasets with only unrelated individuals, they're usually the same, but we tend to include both anyway to maintain standard file formats regardless of data structure.

## Step 7

Define color coding based on province location for the plot (you can copy and paste this whole chunk at one time):

~~~
cls=as.character(dutch_data[,14])	# creating a list of color values for each participant, based on their value in the 14th column of the dutch_data dataset (the province code)
cls[cls=="1"]="#FF82AB"	# Noord-Holland
cls[cls=="2"]="#BF3EFF"	# Zuid-Holland
cls[cls=="3"]="#87CEEB"	# Zeeland 
cls[cls=="4"]="#FFB90F"	# Utrecht
cls[cls=="5"]="#4876FF"	# Noord-Brabant
cls[cls=="6"]="#000080"	# Limburg 
cls[cls=="7"]="#FF7F24"	# Gelderland
cls[cls=="8"]="#8B0000"	# Overijssel
cls[cls=="9"]="#FF0000"	# Flevoland
cls[cls=="10"]="#54FF9F"	# Friesland
cls[cls=="11"]="#32CD32"	# Drenthe
cls[cls=="12"]="#6E8B3D"	# Groningen
~~~

## Step 8

Visualize individuals by a plot of PC1 along the x-axis and PC2 along the y-axis:

~~~
plot(dutch_data$PC1,dutch_data$PC2,col=cls,type="p",pch=20,cex=1,bty="l")
~~~

The 'col' option tells R what color key to use and 'pch' specifies the plotted shape (a filled circle). You can view more options by going through the Help documentation for the plot command.

This is the plot shown on slide 49 at https://ibg.colorado.edu/cdrom2019/abdelouia/populationStratification/abdel_pop_strat_boulder_2019.pdf. Slide 50 shows the same visualization in the whole dataset of >4400 Dutch folks. 

## Step 9

Change something about the plot (the colors, or choose different PCs for the x- and/or y-axis, or the size/shape of the individual dots; something to show that it's not a screengrab of the existing image :) and save the resulting plot by clicking the Export button at the top of the plotting window. 

Need some color ideas for your graph? Check out the [Miyazaki](https://medium.com/@jchen001/r-ggplot2-color-palettes-inspired-by-hayao-miyazakis-animes-f2aeccce45fd) and [Wes Anderson](https://github.com/karthik/wesanderson/blob/master/README.md) palettes for R, and this [maximally-distinct-colors generator](https://mokole.com/palette.html).

## Submission Instructions

Upload and submit the MODIFIED plot that you created in Step 9 for credit on this activity.

-------

Home: [Table of Contents](../README.md)
