Date: 5/11/2017

## National Parks Analysis

As part of my class in R (and Tableau, and technically data visualization), our final project was to create a web app based on the Shiny framework that displayed interesting data visualizations. 

I chose to dig into a data set on National Parks, and the number of visitors each had. Each data set used can be [found on data.world](https://data.world/jonathankkizer/s-17-dv-final-project).

Here's a link to the Shiny webapp: [jonathankizer.shinyapps.io/DVFinal](https://jonathankizer.shinyapps.io/DVFinal)

The Shiny app is interesting because it is so interactive; sliders can be set to different minimal values and points, thus filtering data points (typically outliers) out. Each works relatively simply, with essentially all of the heavy-lifting database work being done on data.world's end -- SQL statements are wonderful.

Perhaps just as interesting is the project notebook (click [here](https://jonathankizer.shinyapps.io/DVFinal), and scroll down; the link is on the lefthand side of your screen), which includes all of the methodology behind finding the data, "cleaning" it, and then using Tableau to quickly find certain aspects that stand out as "interesting."

In particular, the Interesting Visualizations section of the project notebook highlights a number of findings that we considered to be of note. 

One hypothesis I had while looking at the data was the relationship between number of visitors each year and average gas prices. It was my thought that, when gas prices started to rise, visitor numbers dropped. Within the project notebook, I set up a quick correlation test with average gas prices set to 2015 as the constant, to remove the inflationary upward trend that would otherwise heavily skew the test. The hypothesis turns out to not quite be the case, though, as the correlation test was essentially 0, indicating neither a positive or negative relationship.

More time and research (and data points!) are needed to determine the effect of the wider economy on visitor numbers, though.