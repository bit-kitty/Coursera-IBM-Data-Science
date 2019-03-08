---
layout: default
title: Home - IBM Data Science Capstone March 3, 2019
---

![Image of Phoenix from Mountain Trail](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/KfBjNBvg.png?raw=true "Title")
<center><span style="font-family:Papyrus; font-size:2em;">The Battle of Neighborhoods in Phoenix</span></center>
<center>(as a New Metro)</center>

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
Is Phoenix a true city? If naysayers' opinions about the city of Phoenix as described above remains pervasive, it may discourage some city seekers like new families and young professionals to dismiss the opportunities that lies within Arizona. One way to help new prospects better appreciate the area is to explore the various neighborhoods with geolocation data from Foursquare and supplemental local datapoints to illuminate the social composition of top activities, popular venues, and businesses within key neighborhoods. We can then compare these areas to those within a big city like New York City for context. With growth, comes economic development and increased business opportunities. Any similarities/differences found during the exploration could be leveraged to help identify potential pockets of opportunities. Let's see what the data can tell us during this data exploration exercise.

## Data Description <a name="data"></a>
### *Objectives*
* Gain better insight into Phoenix and the local neighborhoods of Maricopa county.
* Compare/Contrast Phoenix's mix of popular venue preferences focusing on Maricopa county versus those of a more established city, NYC's Manhattan borough (county equivalent).
* Based on similarities/differences to Manhattan, are there potential business opportunities for the Phoenix metro area neighborhoods.

### *Sources*
* Foursquare<sub>[[3]](https://foursquare.com/)</sub> geolocation data for mid-February 2019 will be used to pull sample sets of top venues within the radius of the main metro areas. Categories of these venues will be used to cluster like activities and provide some contextual understanding within each neighborhood based on matches to the dataset with neighborhoods and their identified lat/long coordinates.
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
To note upfront, I did encounter a few challenges in the acquisition of ZIP code neighborhood data as well as the completeness of key indicators at the ZIP code level for the Maricopa neighborhoods. This took a lot of set up time to structure the master datasets before any exploration could be conducted for the area. I ended up with 50 neighborhoods for Maricopa County and 40 for Manhattan with the matched venue data retrieved from Foursquare API eventually in this format:

![Manhattan Clusters](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_lat-longDataset.png?raw=true "Title")

After matching to the Foursquare venue data, the resulting top 10 occurrences of venue categories for each area ranked as below.  Seeing that Phoenix is located in a state closer to the borders of Mexico, it is not surprising to see Mexican Restaurant as top listed.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_top10venues.png?raw=true" width="300">
        <p align="center"><sub>Data covers 50 neighborhoods</sub></p></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_top10venues.png?raw=true" width="300">
        <p align="center"><sub>Data covers 40 neighborhoods</sub></p></td>
    </tr></table></center>

Although there are plenty of great data around, much of it is available at the county level, FIPS, or by census block and not directly for zip codes. Many sources that had zip code data were either selling them in bulk packages or selling a platform, sorftware, or database just to receive simple counts or statistics for a couple hundred ZIP codes. Therefore, I had to go the manual route to collect the few extra measures where I could to test viability for enhancing the analytics. 

Typically, I would do a much more expansive exploratory analysis with thousands of variables and feature sets to iterate through and boil down to key components for modeling, but unfortunately this was not possible for this quick study. Even with the minimal data points not in excess of a few thousand rows, I was already running up against the dreaded IBM Watson message of using more than my monthly system quota and randomly getting kicked off the system. This definitely slowed my progress and I had to cut my evaluations short before this write up since I was unable to technically continue vetting the data and finish within the week. Despite the inability to be more exhaustive, I believe some interesting insights did emerge to pave the path for future work.

## Methodology <a name="methodology"></a>
GitHub was used as the main collaborative repository with a web based graphical interface to host the files for this project. The majority of the processing will be conducted from a Python notebook on the IBM Watson platform. The base geolocation files will be built off of publicly available neighborhood latitude/longitude for each area. A simple clustering exercise employing K-means algorithms will first be conducted on Foursquare social networking data to compare top activities within Phoenix versus those within New York City for observations of basic behavior differences. Key points of differentiation from Manhattan will be leveraged to further build out segmentation for the Phoenix Maricopa area to help identify pockets of potential opportunity within like neighborhoods with some demographics overlay for context.

K-means is one of the simplest and popular unsupervised machine learning algorithms meant to derive common themes based on inputs or features with unlabeled or unknown outcomes. I used this to cluster the Foursquare neighborhood activities in hopes of deriving common themes to better understand the preferences of people within each region. Since the data to be clustered were unlabeled, first objective is to determine the best number of clusters or 'k' to kick off the unsupervised modeling process. Typically, the elbow method and silhouette scores could be employed to help pick the best 'k'. However, these are not fool proof methods, especially if the data points are fairly homogenous or doesn't cluster well into distinct groups. Both the Elbow method and Silhouette scoring provided minimal assistance in selecting the optimum k using Foursquare venue category data. As you can see here, after several iterations, a definitive bend was not found in either the Maricopa or Manhanttan charts during the investigation.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_elbow.png?raw=true" width="425">
        <p align="center"><sub>Maricopa (Phoenix) showed a weak elbow curve</sub></p></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_elbow.png?raw=true" width="425">
        <p align="center"><sub>Manhattan (NYC) definitely did not show much of an elbow</sub></p></td>
    </tr></table></center>
    
In this case, with limited time and stubborn data points, I did have to seek additional business context from Esri's Tapestry Segmentation to determine which groupings and how many are more viable for this study. For the Manhattan area, there appears to be two main segments so I followed suit in breaking Manhattan into two clusters and plotted them. While observing the visualization of the Foursquare segmented venue clusters for Manhattan, they do to a certain degree, resemble the shapes of the Tapestry Segmentation (pictured below). With the limited amount of time for this study, I took advantage of this alignment and applied the basic demographics findings from Esri to help explain the additional nuances of our newly formed venue based segments.

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

The other dominant segment that is less of an interest for this study are the High Rise Renters. To round out observations, High Rise Renters are said to be less well off, more likely multicultural and multigenerational households with an average household size of 2.82. These are family oriented people, risk takers spending beyond their means to make ends meet and like to explore other interests to make life enjoyable.  Additional demographics for comparison:

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-Age.png?raw=true" width="400"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-DiversityIndex.png?raw=true" width="400"></td>
      <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-Income.png?raw=true" width="400"></td>
        <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-HR-RentOwn.png?raw=true" width="400"></td>
    </tr></table></center>

With guidance from this source, two segments were teased out for Manhattan and eventually up to six were forced within Maricopa county in order to find a group that fits loosely to characteristics for a potential up and coming "Laptops and Lattes"-like segment to target. Manhattan's Foursquare Cluster 2 did show support of the Laptops and Lattes Tapestry Segment. This cluster, accounted for 22 neighborhoods around Manhattan with indication of higher occurrences of gyms, fitness centers, spas, and yoga studios visited among the top venue categories along with Coffee Shops and Cafes. Hotels are more frequented as well, mostly likely due to business travelers, consultants, and tourists that can afford the luxury of the area. Fancier cuisines like Italian, Sushi, Japanese, French appear on the top 20 list more so than the areas within Cluster 1.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_Cluster2TopCat.png?raw=true" width="175"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh_Cluster2TopCatByHood.png?raw=true" width="675"></td>
    </tr></table></center>

For Maricopa county, out of six clusters, I also landed on Cluster 2 (purple pins) as best fit to compare with Manhattan's Cluster 2. Cluster 1 (red pins) was more of the 'Multi Cultural Urban Quarters' where diversity is high, with larger families and lower income. Cluster 3 (blue pin) was more of a 'Blended New Family Area' with larger average household size and mid to upper income earnings. Clusters 4-6 (turquoise, green, orange pins) are the upper echelon of neighborhoods encompassing the likes of Paradise Valley and DC Ranch Scottsdale where individuals are likely to be more settled and focus on home improvement and raising families. Here's how they mapped out for the region:

![Maricopa Clusters](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_Cluster_Map.png?raw=true "Title")

I would describe the segment of focus, Cluster 2, as more of the 'Restless "On-the-Go" Young Professionals' group. This segment encompasses 19 neighborhoods netting a relatively high diversity index, averaging 68.5 across the area with 78.3 within the top quartile (0 = not very diverse and 100 = extremely diverse). This is roughly 7% higher than the US average and 36% higher than Manhattan's Cluster 2 (proxied by Laptop and Latte segment's diversity index). Income is higher than the poorest neighborhoods within Maricopa. Not the richest group, but folks in this area of Phoenix appear to be earlier in their careers. Average household size is smaller than the rest of the neighborhood clusters in the study making this group more likely to be single households or not yet with children. Percent of home ownership is the lowest in comparison to other neighborhood segments. 

![Maricopa Cluster 2 Stats](https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX-Cluster2Stats.png?raw=true "Title")

Mexican food tops the list, but that may be due to the abundance of them in Phoenix due to the vicinity to the borders as was pointed out earlier. Easy access makes for easy check-ins. We also see check-ins more often at gas stations, quick eateries and restaurants. Although not the same exact characteristics of the Laptops and Lattes group of Manhattan's Cluster 2, the neighborhoods within this cluster would be closest to compare and contrast for opportunities to provide additional services targeting these mobile young professionals.

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_Cluster2TopCat.png?raw=true" width="175"></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX_Cluster2TopCatByHood.png?raw=true" width="675"></td>
    </tr></table></center>

## Results and Discussion <a name="results"></a>

As mentioned earlier, there were many unexpected challenges to completing this study in a more thorough manner. Phoenix is a large city with a growing population across a huge land mass. Many neighborhoods are very widespread with their own distinct flavors, which is why the clustering exercise during this study has shown difficulties in merging groups for segmentation. The urban core or downtown Phoenix is not as densely populated as they are within NYC. In fact, some surrounding neighborhoods have higher population density per capita than downtown.  

Unlike Manhattan, where the culture has been pretty well established as an urban center, patterns were not as easy to pick up for the Phoenix area either, even within the select county of Maricopa. Referring back to the Tapestry Segmetation schematics, you can see the visual differences here by the amount of different segment shadings across the two regions:

<center><table><tr>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/PHX-Esri-Segs.png?raw=true" width="425">
        <p align="center"><sub>Maricopa (Phoenix) has upwards of 10+ segments</sub></p></td>
    <td align="center"><img src="https://github.com/bit-kitty/Coursera_Capstone/blob/master/ProjectData/images/Manh-Esri-Segs.png?raw=true" width="425">
        <p align="center"><sub>Manhattan (NYC) has basically two main segments</sub></p></td>
    </tr></table></center>

One other thing to consider is that the individuals here in Phoenix may not be as avid Foursquare users to check-in everywhere they go either. Given the amount of traveling by car versus public transportation like the metro in NYC, individuals are less likely to always be glued to their phones to be mindful of using the Foursquare app if at all. Therefore, inherent biases and flaws already exist with the venue visitation data and could partially contribute to difficulties of breaking up the neighborhood groups. 

The variety of neighborhoods in Maricopa and the complexity of the make up did require a lot more data and processing time to drill in and test different approaches for a more informed study. During this quick study, additional ZIP code statistics were manually compiled to supplemental the intelligence for learning. 

Cluster 2, the 'Restless "On-the-Go" Young Professionals', within Maricopa showed some promising indications for providing services that would cater to younger, career-focused professionals with a busy lifestyle. In comparison to Manhattan's Cluster 2 ("Laptops and Lattes" group), there were 73% less check-ins at Italian restaurants and gyms were no where at the top. Perhaps this could be an opportunity to invest in opening up quality Italian venues within these neighborhoods. Other services around health and fitness or maybe even for special quality dry cleaning services would support an active, on-the-go lifestyle for these up and coming career oriented folks and could be an areas of opportunity as well. Of course, more input data would be needed to understand if there is a need for more quality Italian cuisine, gyms, spas, or dry cleaning within any of the neighborhoods that fell within this cluster. 

In future work, additional overlay for daytime demographics as well as residential demographics will help decipher work related commuting activities as well as industry business statistics to understand types of business established and where within proximity to targeted locations for opening new businesses would take this evaluation much further. Information that can programmatically be retrieved from paid platforms would be much more fruitful in conducting this type of work as well. Additonal plotting of density features using heatmaps or choropleth maps with segments superimposed could add more visual context as well. If only I had more time and bandwidth left for processing. Not being limited in processing space on a platform could take this analysis to the next level. There is definitely a lot more intelligence to unearth for Phoenix with so much more opportunity for growth in both business and investments opportunities if key nuggets of information can be gained for analytics.

## Conclusion <a name="conclusion"></a>
The Phoenix metropolitan area is definitely unique and marches to the beat of it's own drums. It is a new type of city with a different vibe and behavior patterns. Thus, it should be appreciated for what it is becoming instead of forcing it to replicate another New York, LA, or even Chicago. Although we can borrow ideas from other cities, whether it is successful or not remains to be seen. With dispersed areas of city living, this adds a different kind of urban flavor that takes a typical city adventure beyond a congested concrete jungle. There's obviously plenty of room for growth, development, and a ton of indoor/outdoor adventures to be had.

## References
[1] ["Wikipedia - Phoenix Metropolitan Area"](https://en.wikipedia.org/wiki/Phoenix_metropolitan_area/)

[2] ["Phoenix is the nation's 5th largest — but is it a 'real' city?"](https://www.azcentral.com/story/news/local/phoenix/2017/06/11/phoenix-nation-5th-largest-but-real-city/369917001/)

[3] [*Foursquare*](https://foursquare.com/)

[4] [US State-County Latitutude/Longitude Dataset](https://www.geonames.org/)

[5] [*United States Zip Codes.org*](https://www.unitedstateszipcodes.org/)

[6] [*AZ HometownLocator*](https://arizona.hometownlocator.com/)

[7] [*United States Census Bureau*](https://www.census.gov/data/data-tools.html/)

[8] ["Esri Tapestry Segmentation"](https://www.esri.com/en-us/home)

***

<span style="font-family:Bebas Neue; font-size:1em;">*Author: Pam Vongboupha*</span>

>Thanks for reading! Feel free to [email me](mailto:bit-kitty@gmail.com) with any questions or comments.
