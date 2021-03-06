# Deadly Earthquakes
*Analysis of deadly earthquakes and correlation with other natural features to predict where deadly earthquakes are most likely to occur*

## Background
The ability to know when and where deadly earthquakes will occur would be hugely valuable but has so far eluded prediction. This is largely due to the inability to separate the signal from the noise in the data. To address this question we scraped a list of <a href="https://en.wikipedia.org/wiki/List_of_deadly_earthquakes_since_1900" target="_blank">deadly earthquakes since 1990</a> and attempted to identify any trends or insights that could help predict when and where future deadly earthquakes may occur. 

## Methodology
To get the data we used <a href="https://www.crummy.com/software/BeautifulSoup/bs4/doc/" target="_blank">BeautifulSoup</a> to scrape the wikipedia page and convert to a <a href="https://pandas.pydata.org/pandas-docs/version/0.22.0/" target="_blank">pandas</a> dataframe. We then used <a href="https://docs.python.org/3/howto/regex.html" target="_blank">regex</a> to clean the data and then converted dtypes to appropriate formats. There were a number of fields with missing data and for some of them we were able to manually input the information. For columns with many missing values we either removed the column or only focused on rows where all data were complete. We also simplified fields that calculated total deaths differently by selecting the largest value across all death calculations. 

## Adding in new data and plotting
At this point we supplemented our main data by finding other sources with information that may be relevant to when and where deadly earthquakes occur, specifically data about <a href="http://volcano.oregonstate.edu/volcano_table" target="_blank">volcanoes</a> and <a href="https://github.com/fraxen/tectonicplates" target="_blank">tectonic plate boundaries</a>. In an attempt to see if there were any correlations . We then used <a href="http://geopandas.org/" target="_blank">geopandas</a> to overlay the data points over a <a href="https://github.com/Stefie/geojson-world" target="_blank">world map</a>. We were able to see trends but needed to quantify the relationship with earthquakes. <br>
<br>
![world_map](/images/quakes_world_map.png)

We calculated the nearest of each of our new features using <a href="http://www.numpy.org/" target="_blank">numpy</a> and used that to visualize the trends of the nearest volcano and tectonic boundary type using <a href="https://matplotlib.org/" target="_blank">matplotlib</a>. 

## Are earthquakes associated with fracking in the same areas as natural ones
With all this information we train a supervised machine learning model of where deadly earthquakes occur using <a href="http://scikit-learn.org/stable/index.html" target="_blank">scikit-learn</a>. We then tested the ability of the model to predict earthquakes which occur in areas where fracking is performed (Oklahoma and northern Texas). We found that the model was not able to predict earthquakes that occurred in the <a href="https://github.com/johan/world.geo.json/tree/master/countries" target="_blank">USA</a>, possibly indicating that earthquakes associated with fracking occur due to factors beyond natural ones. The model likely needs to be tuned to ensure no overfitting has occurred. This process was also repeated on a more extensive <a href="https://volcano.si.edu/E3/" target="_blank">list of earthquakes</a> to consider all earthquakes, not just deadly ones. <br>
<br>
![us_map](/images/quakes_USA_map.png)

***
This project was part of a data science bootcamp at <a href="http://nashvillesoftwareschool.com/" target="_blank">Nashville Software School</a>
