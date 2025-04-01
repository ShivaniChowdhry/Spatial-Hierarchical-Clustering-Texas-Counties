# Spatial-Hierarchical-Clustering-Texas-Counties
Decoding Socio-Political Landscape of Texas Counties Using Spatial Hierarchical Clustering

The objective of this study is to identify homogeneous regions in Texas, which comprise of similar and spatially adjacent counties. These regions should be homogenous with respect to their [a] cultural, [b] political, [c] socio-economic, [d] demographic and [e] residential characteristics. This classification can be used by either a political scientist or strategist or a public health administrator to know which clusters are common in terms of the demographic and socioeconomic factors and how they can target them to achieve greater vote share by addressing their specific issue in election campaigns or how they can design better insurance program or vaccination rollout campaigns for them. Economists and policymakers can also use this clustering information to know the socioeconomic conditions and demographic profiles of people living in each cluster.

Data and idea of the project provided by Dr. Michael Tiefelsdorf, Associate Professor of Geospatial Information Sciences at University fo Texas at Dallas. More information about the data and the Texas counties can be found at Disparities in COVID-19 Vaccination Rates among the Counties of Texas (spatialfiltering.com). Study the article by M. Chavent, V. Kuentz-Simonet, A. Labenne, J. Saracco. ClustGeo: An R package for hierarchical clustering with spatial constraints.

For spatial clustering of the counties in Texas, I have included the following 19 variables/features across 3 domains:

**[a] Demographic features: **
* WHINOHISP : Proportion of White non-Hispanic population (Caucasian population)
* HISPORG : Proportion of population with Hispanic ethnic background
* PARTASIAN : Proportion of any part Asian population
* PARTBLACK : Proportion of any part Afro-American population
* MEDAGE : Median age of population in county

**[b] Socio-economic features: **
* FullVacRate : % of population with full vaccination for Covid-19
* CrudeMort : Crude mortality arte for covid-19 in each county
* UNINSURED : Proportion of uninsured population
* MEDVALHOME : Median value in $ of owner-occupied housing units
* OWNOCCPCT : Percent of owner-occupied housing unit
* INCOME : Per capita income ($)
* UNEMPL : Proportion of population in labor force who are currently unemployed
* COLLEGEDEG : Proportion of population 25+ who do have a college degree and above
* CRIMERATE : Crime rate per 100.000 population in a county (2015)
* POP2020 : Total population by county as of 2020

**[c] Electoral features relating to 2016 and 2020 presidential elections:**
* TRUMPPCT20 : Trump vote percent in 20202 elections
* REPDIFF : Difference in Vote % for Trump or GOP in 2020 and 2018 presidential elections
* DEMDIFF : Difference in vote % of democratic party candidates in 2020 and 2016 presidential elections
* TURNOUTDIFF : Difference in turnout between 20202 and 2016 elections

I converted all the count variables into rates using the formulas described in the code in the appendix below, before using them to calculate feature dissimilarity matrix. 

**Outputs & process of updating of clusters based on parameter tuning:**
Screeplot with K=12: First starting with 12 clusters, and inspecting the dendrogram and screeplot scree plot in top left figure shows the plot of normalized proportion of explained inertias by D1 and D0. The plot suggests retaining alpha=0.1 to 0.17. The value of 0.1 favors the socio-economic homogeneity vs. geographical homogeneity as shown in the clustering in top left map of Texas, in which many clusters are not contiguous. If we give more priority to geographical contiguity and have alpha=0.15, then portioning is shown in top right map of Texas, in which clusters are more contiguous than in LHS figure. From visual inspection of the dendrogram for k=12, some clusters are very small that means relatively homogenous elements are grouped in different clusters. So, we can cut the tree at k=10 and check. 

Screeplot with K=10 & dendrogram with alpha=0.15: It seem from the clustering like we can increase spatial homogeneity now and decrease feature homogeneity.

Screeplot with K=9 & dendrogram with alpha=0.15: It looks like from this clustering that some regions are not contiguous and are very small. So, we can improve performance by reducing K=8.

Screeplot with K=8 & dendrogram with alpha=0.15: This is the final clustering which has most contiguous clusters but also clear distinction in their feature space

**Electoral factors:**
Highest increase in Republican vote percent over 2016-2020 was seen in region 7 and a decrease in Trump vote percent was seen in cluster 8. On the contrary, Democrats vote percent change over 2016-2020 saw highest increase in cluster 8 and lowest in cluster 7. This was true as some counties in the cluster 7 (represented by the South Texas belt bordering Mexico with a high Hispanic population) turned “red” (won by Republican Party) in the 2020 election, and Democrat vote share increased in the three metropolitan regions of Dallas, Austin, and Houston (Cluster 8, hereafter called “metropolitan cities cluster”).

In case of turnout change from 2016-2020, increase in turnout was seen in clusters 6 and 8 and a decrease was seen in cluster 7. Trump vote percent in 2020 was highest in the Texas Panhandle region or Cluster 4 and lowest in clusters 7 (South Texas & big bend county) and 8 (metropolitan cities cluster).

**Demographic factors:**
In terms of demographics, White population is highest in clusters 1, 4 and 6, and lowest in cluster 7. 

Hispanic population is highest in cluster 7 (bordering Mexico) followed by clusters 2 & 3 (bordering Mexico), and lowest in cluster 1.

Asian population is highest in the metropolitan cluster 8, followed by cluster 5. 

Black population is highest in clusters 5 and 1, followed by the metropolitan cluster 8. Clusters 1 & 5 are closest to the historically slave owning regions of Texas, so they have a high Black population. 

Median age is highest in clusters 6 an lowest in cluster 8, followed by clusters 7 and 2. 

**Health-related factors:**
Vaccination rate for Covid 19 was highest in clusters in 6, 7, & 8. It seems reasonable because cluster 6 has a high median age of population who were more at risk for dying from Covid-19, and cluster 7 & 8, representing Rio Grande Valley and the 3 metropolitan cities lead the way in vaccinations. Full vaccination rate was towards the lower end in the cluster 1 which has a high black population. 

Number of uninsured people are highest in cluster 7, which can be due to high number of undocumented immigrants or high joblessness in these areas bordering Mexico.

**Socioeconomic factors:**
Median value of homes was highest in clusters 6 & 8. It seems reasonable since these are the clusters representing the hill country region and the 3 metropolitan cities of Austin, Dallas, and Houston which have seen a greater growth in population in recent years with people moving to these areas in high numbers, which explains the increase in demand and hence the house prices. 

In terms of income, clusters 6 & 8 had the highest income and employment rate. Cluster 5 is closer to the metropolitan areas so is the hub of transportation between the major economic centers of Texas and therefor has more income than cluster 1.

Unemployment rate is less in clusters 2, 4 and 6. Cluster 2 is the oil country, and cluster 4 & 6 are the industrial belt of Texas, including the agricultural plains which are hub for wheat and cotton production. 

Unemployment rate is high in bordering counties represented in cluster 7, followed by cluster 3 and 1, which are all bordering counties and have high population of Hispanic-origin immigrants and Black population.  

College education is highest in clusters 8 and 6 which are metropolitan and metropolitan-surrounding regions and have a high presence of universities. It is lowest in cluster 7 bordering Mexico and also low in clusters 1 & 2, the eastern border region and the oil country, respectively. 

Crime rate is high in clusters 2 & 7, and less in clusters 4 & 6.

And the population is highest in the metropolitan cities (cluster 8) and the counties connecting them (cluster 5). 

**Description of each identified region in terms of its profile of characteristic:**
Region 1: The region bordering the Eastern states of Louisiana, Arkansas, and Oklahoma, has been a historically slave-owning belt and has a high concentration of Black population along with the White population. It has high timber production, but also has high unemployment, low percent of people with college degree, low income, a high Republican voter base, and low Covid-19 full vaccination rates.

Region 2: The oil country of Texas which has an abundance of oil fields. It is characterized by low unemployment, low percent of people with college education, high percent of Trump voters, has some counties with a high Hispanic population.

Region 3: It is segregated into 2 parts: Gulf coastal plain region and the big bend country. The characteristics of this region are High Hispanic population but not as high as cluster 7, high unemployment rate, with mostly Republican voters but some counties turning Blue in 2020 presidential elections, shown in a little drop in republican vote % and increase in Democrat vote % compared to 2016.

Region 4: The part of panhandle plains which is the main agricultural region of Texas. It is characterized by high Trump voter % in 2020 elections, high White population, higher median age or people, slightly lower median home values, average median income but low unemployment rate because of cotton industry and croplands.

Region 5: The region connecting the 3 big metro cities, it also has a high population but not as high as the 3 metro cities. It has a high Asian and Black population, and some features common with the big metropolitan regions but they have a more Republican voter base (it’s turning blue from 2016-2020). 

Region 6: Has a high white population, it is the neighboring region of the Austin metroplex. It has a high republican vote %. It has among the highest median home value (almost at par with the 3 metropolitan cities) and high median age as well as a high Covid full vaccination rate. It has high income, low unemployment, low crime rate and a high % of college educated population.

Region 7: It is segregated into 2 non-contiguous parts: the south Texas plains and upper part of the Big Bend country. It has the highest Hispanic population as it is bordering Mexico. It has the highest vaccination rate for Covid 19, but also the highest number of uninsured people.

The reason why it is segregated from region 3 is because it has higher Hispanic population and very less White population compared to cluster 3. It also has a low median age with a very low % of them having a college education or a health insurance. They have the lowest income and a high unemployment rate. They have a lower % of owner-occupied homes and lower median value of homes. It saw an increase in Republican vote share in 2020 though it is traditionally a blue or democrat voter base, it also saw a fall in voter turnout in 2020.  

Region 8: It is the metropolitan cluster comprising of 3 big metropolitan regions of Dallas, Austin, and Houston. Their characteristics are low median age, very high income, highest population and population density in Texas, a high vaccine rate for Covid-19, highest median home values in Texas, highest number of people with a college degree and highest increase in democratic vote share % from 2016-2020 and high % of democratic party voters in 2020. In terms of demographics, it has a high white population but not as high as certain other clusters because it has a more diverse population comprising of Black, Hispanic, and Asian populations.

