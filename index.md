---
layout: default
title: Home - IBM Data Science Capstone March 3, 2019
---

![Image of Phoenix from Mountain Trail](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/KfBjNBvg.png?raw=true "Title")
<center><span style="font-family:Papyrus; font-size:2em;">The Battle of Neighborhoods in Phoenix</span></center>

***

## Table of Contents
* [Introduction](#introduction)
* [Problem Statement](#problem)
* [Data Description](#data)
* [Methodology](#methodology)
* [Results and Discussion](#results)
* [Conclusion](#conclusion)
* [References](#references)

---

## Introduction <a name="introduction"></a>
Based on Wikipedia<sub>[[1]](https://en.wikipedia.org/wiki/Phoenix_metropolitan_area)</sub> and an article published in 2017 on AZ Central<sub>[[2]](https://www.azcentral.com/story/news/local/phoenix/2017/06/11/phoenix-nation-5th-largest-but-real-city/369917001/)</sub>, Phoenix is one of the fastest growing metro areas within recent years and earned “two national distinctions with the U.S. Census Bureau numbers released Thursday [June 8, 2017]: Fifth-largest city and fastest-growing city.” However, due to its vast land mass within the [Metropolitan Statistical Area (MSA)](https://en.wikipedia.org/wiki/Metropolitan_area) boundaries, this got some thinking it to be rather atypical of a “true city,” like New York City. Key neighborhoods being miles apart don’t fit together well for people seeking a traditional sense of one big city. Having been in the area a short while, I find that the uniqueness of the area is very much appreciated in recent urban developments that have injected pieces of the real city in many neighborhoods surrounding the urban core.  

## Problem Statement <a name="problem"></a>
If naysayers' opinions about the city of Phoenix as described above remains pervasive, it may discourage some city seekers like new families and young professionals to dismiss the opportunities that lies within Arizona. One way to help new prospects better appreciate the area is to explore the various neighborhoods with geolocation data from Foursquare and supplemental local datapoints to illuminate the social composition of top activities, popular venues, and businesses within key neighborhoods. We can then compare these areas to those within a big city like New York City for context. With growth, comes economic development and increased business opportunities. Any similarities/differences found during the exploration could be leveraged to help identify potential pockets of opportunities. Let's see what the data can tell us during this data exploration exercise.

## Data Description <a name="data"></a>
### *Objectives*
* Gain better insight into Phoenix and the local neighborhoods of Maricopa County.
* Compare/Contrast Phoenix's mix of popular venue preferences focusing on Maricopa county versus those of a more established city, NYC's Manhattan borough (county equivalent).
* Based on similarities/differences to Manhattan, are there potential business opportunities for the Phoenix metro area neighborhoods.

### *Sources*
* Foursquare<sub>[[3]](https://foursquare.com/)</sub> geolocation datasets will be used to pull sample sets of top venues within the radius of the main metro areas. Categories of these venues will be used to cluster like activities and provide some contextual understanding within each neighborhood based on matches to the dataset with neighborhoods and their identified lat/long coordinates.
   * Phoenix (County: Maricopa)
   * New York City (Borough: Manhattan)
* US state-county<sub>[[4]](https://www.geonames.org/)</sub> latitutude/longitude dataset will provide the set of county ZIP codes along with their lat/long coordinates that are needed to match to the Foursquare data.
* Supplemental manual neighborhood identification lookups will provide name identification of Phoenix neighborhoods since a set list is not readily available online. Any additional local statistics if pertinent to the analysis may be included from Phoenix local government sites.
   * US ZIP code lookups<sub>[[5]](https://www.unitedstateszipcodes.org/)</sub> for neighborhood names
   * Local AZ demographics data<sub>[[6]](https://arizona.hometownlocator.com/)</sub>
* United States Census Bureau<sub>[[7]](https://www.census.gov/data/data-tools.html/)</sub> will provide some national census related business statistics at the zip code level that may be pertinent to the evaluation exercise.
    * Business Statistics
* Given the shorten timeframe to turn around this analysis, supplemental location intelligence produced by Esri<sub>[[8]](https://www.esri.com/en-us/home)</sub> (an expert in geographic science and the builder of ArcGIS, a powerful mapping and spatial analytics software) will be used to help fill in characteristics about certain neighborhood segments within this study.
    * Esri's Tapestry Segmentation provides community lifestyle and demographic information

### *Challenges*
To note upfront, I did encounter a few challenges in the acquisition of ZIP code neighborhood data as well as the completeness of key indicators at that level code level for the Maricopa neighborhoods. This took a lot of set up time to structure the master datasets before any exploration could be conducted for the area. I ended up with 50 neighborhoods for Maricopa County and 40 for Manhattan with the matched venue data retrieved from Foursquare API eventually in this format:

![Manhattan Clusters](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_lat-longDataset.png?raw=true "Title")

Although there are plenty of great data around, much of it is available at the county level, FIPS, or by census block and not directly for zip codes. Many sources that had zip code data were either selling them in bulk packages or selling a platform, sorftware, or database just to receive simple counts or statistics for a couple hundred ZIP codes. Therefore, I had to go the manual route and collect a few measures where I could to test viability for enhancing the analytics. 

Typically, I would do a much more expansive exploratory analysis with thousands of variables and feature sets to iterate through and boil down to key components for modeling, but unfortunately this was not possible for this quick study. Even with the minimal data points not in excess of a few thousand rows, I was already running up against the dreaded IBM Watson message of using more than my monthly system quota and randomly getting kicked off the system. This definitely slowed my progress and I had to cut my evaluations short before this write up since I was unable to technically continue vetting the data and finish within the week. Despite the inability to be more exhaustive, I believe some interesting insights did emerge to pave the path for future work.

## Methodology <a name="methodology"></a>
GitHub will be used as the main collaborative repository with a web based graphical interface to host the files for this project. The majority of the processing will be conducted from a Python notebook on the IBM Watson platform. The base geolocation files will be built off of publicly available neighborhood latitude/longitude for each area. A simple clustering exercise employing K-means algorithms will first be conducted on Foursquare social networking data to compare top activities within Phoenix versus those within New York City for observations of basic behavior differences. Key points of differentiation from Manhattan will be leveraged to further build out segmentation for the Phoenix Maricopa area to help identify pockets of potential opportunity within like neighborhoods with some demographics overlay for context.

K-means is one of the simplest and popular unsupervised machine learning algorithms meant to derive common themes based on inputs or features with unlabeled or unknown outcomes. I used this to cluster the Foursquare neighborhood activities in hopes of deriving common themes to better understand the preferences of people within each region. Since the data to be clustered are unlabeled, first objective is to determine the best number of clusters or 'k' to kick off the unsupervised modeling process. Typically, the elbow method and silhouette scores could be employed to help pick the best 'k'. However, these are not fool proof methods, especially if the data points are fairly homogenous or doesn't cluster well into distinct groups. Both the Elbow method and Silhouette scoring provided minimal assistance in selecting the optimum k using Foursquare venue category data. As you can see here, after several iterations, a definitive bend was not found in either the Maricopa or Manhanttan charts during the investigation.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_elbow.png?raw=true" width="425">
        <p align="center"><sub>Maricopa (Phoenix) showed a weak elbow curve</sub></p></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_elbow.png?raw=true" width="425">
        <p align="center"><sub>Manhattan (NYC) definitely did not show much of an elbow</sub></p></td>
    </tr></table></center>
    
In this case, with limited time and stubborn data points, I did have to seek additional business context from Esri's Tapestry Segmentation to determine which groupings are more viable for this study. While observing the visualization of the Foursquare segmented venue clusters for Manhattan, they do to a certain degree, resemble the shapes of the Tapestry Segmentation (pictured below). With the limited amount of time for this study, I took advantage of this alignment and applied the basic demoographics findings from Esri to help explain the additional nuances of our newly formed venue based segments.

![Manhattan Clusters](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_Cluster_Map.png?raw=true "Title")

As you can see, the plotted clusters above aligned fairly well with those of the Esri Tapestry segments in Manhattan for Laptops and Lattes (light blue blocks) and High Rise Renters (purple blocks). Cluster 1 (red pins) appeared to match more so to the High Rise Renters. Cluster 2 (purple pins) mapped more to the Laptops and Lattes group.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-Esri-Segs.png?raw=true" width="275"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Esri-LL.png?raw=true" width="300"></td>
      <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Esri-HR.png?raw=true" width="300"></td>
    </tr></table></center>
    
According to Esri, Laptops and Lattes folks are said to be more upscale, mid-career professionals, and likely to be single householders with an average household size of 1.87. These are health-conscious consumers, who exercise regularly and pay attention to the nutritional value of the food they purchase. Additional demographics to note:

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-LL-Age.png?raw=true" width="400"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-LL-DiversityIndex.png?raw=true" width="400"></td>
      <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-LL-Income.png?raw=true" width="400"></td>
        <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-LL-RentOwn.png?raw=true" width="400"></td>
    </tr></table></center>

The other dominant segment that is less of an interest for this study are the High Rise Renters. High Rise Renters are said to be less well off, more likely multicultural and multigenerational households with an average household size of 2.82. These are family oriented people, risk takers spending beyond their means to make ends meet and like to explore other interests to make life enjoyable.  Additional demographics for comparison:

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-Age.png?raw=true" width="400"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-DiversityIndex.png?raw=true" width="400"></td>
      <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-Income.png?raw=true" width="400"></td>
        <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-RentOwn.png?raw=true" width="400"></td>
    </tr></table></center>

With guidance from this source, two segments were teased out for Manhattan and eventually up to six were forced within Maricopa county in order to find a group that fits loosely to characteristics for a potential up and coming "Laptops and Lattes"-like segment to target. 

## Results and Discussion <a name="results"></a>
As mentioned earlier, there were many unexpected challenges to completing this study in a more thorough manner. Phoenix is a large city with a growing population across a huge land mass. Many neighborhoods are very widespread with their own distinct flavors, which is why the clustering exercise during this study has shown difficulties in merging groups for segmentation. The urban core or downtown Phoenix is not as densely populated as they are within NYC. In fact, some surrounding neighborhoods have a higher population density per capita than the center.  

Unlike Manhattan, where the culture has been pretty established, patterns were not as easy to pick up for the Phoenix area either, even within the select county of Maricopa. Referring back to the Tapestry Segmetation schematics, you can see the visual differences here by the amount of different segment shadings across the two regions:

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX-Esri-Segs.png?raw=true" width="425">
        <p align="center"><sub>Maricopa (Phoenix) has upwards of 10+ segments</sub></p></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-Esri-Segs.png?raw=true" width="425">
        <p align="center"><sub>Manhattan (NYC) has basically two main segments</sub></p></td>
    </tr></table></center>

One other thing to consider is that the individuals here in Phoenix may not be as avid Foursquare users to check-in everywhere they go either. Given the amount of traveling by car versus public transportation like the metro in NYC, individuals are less likely to always be glued to their phones to be mindful of using the Foursquare app if at all. Therefore, inherent biases and flaws already exist with the venue visitation data and could partially contribute to difficulties of breaking up the neighborhood groups. The variety of neighborhoods in Maricopa and the complexity of the make up did require a lot more data and processing time to drill in and test different approaches for a more informed study. 

Cluster 2 for Maricopa showed some promising indications for providing services that would cater to younger, career-focused professionals with a busy lifestyle. Perhaps busines service around health and fitness or special quality dry cleaning services would support an active, on-the-go lifestyle for these individuals. With the lack of publicly available data readily available for the Phoenix neighborhoods, these opportunity suggestions are not fail proof. A lot of time was spent on manual collections of the minimal additional data points used to supplement the Foursquare venue data in the study. In future work, information that can programmatically be retrieved from paid platforms would be much more fruitful in conducting this type of work.

Additional data with respect to age, income, household size and ownership was manually compiled along with specific geo coordinates for key neighborhoods to assist in analyzing and translating the Maricopa County data. There is definitely a lot more intelligence to unearth for Phoenix with so much more opportunity for growth in both business and investments if key nuggets of information can be gained for analytics.

## Conclusion <a name="conclusion"></a>
The Phoenix metropolitan region is definitely unique and marches to the beat of it's own drums. It is a new type of city and should be appreciated for what it is becoming instead of forcing it to replicate another New York, LA, or even Chicago. With dispersed areas of city living, this adds a different kind of urban flavor that takes a typical city adventure beyond a congested concrete jungle. There's obviously plenty of room for growth, development, and a ton of indoor/outdoor adventures to be had.

## References
[1] ["Wikipedia - Phoenix Metropolitan Area"](https://en.wikipedia.org/wiki/Phoenix_metropolitan_area/)

[2] ["Phoenix is the nation's 5th largest — but is it a 'real' city?"](https://www.azcentral.com/story/news/local/phoenix/2017/06/11/phoenix-nation-5th-largest-but-real-city/369917001/)

[3] [*Foursquare*](https://foursquare.com/)

[4] [US State-County Latitutude/Longitude Dataset](https://www.geonames.org/)

[5] [*United States Zip Codes.org*](https://www.unitedstateszipcodes.org/)

[6] [*AZ HometownLocator*](https://arizona.hometownlocator.com/)

[7] [*United States Census Bureau*](https://www.census.gov/data/data-tools.html/)

[8] ["Esri Tapestry Segmentation"](https://www.esri.com/en-us/home)
