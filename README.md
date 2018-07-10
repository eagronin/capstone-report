# Recommendations

## Overview
This section reports the results of the analysis and provides recommendations for increasing revenue in a fictitious online game called "Catch the Pink Flamingo". The analysis is based on the final project of the Big Data Specialization by University of California San Diego on Coursera.

The data for the project consists of 9 files with data on in-app purchases, ad clicks and game-specific information as well as 6 files with chat data.  The data were downloaded from the Coursera website.  All the data for the project were generated by a development team of data scientists.  The data were designed to simulate many aspects of game play and in-game user activity.  

The project entails classification analysis by fitting a decision tree and cluster analysis using k-means.  It also uses graph analytics to identify the chattiest users / teams, longest conversations and active user groups. 

The analysis in this project was performed using Spark, Python, Splunk, KNIME and Neo4j.

We will discuss recommendations based on the classification analysis first, then we will proceed with the recommendations based on cluster analysis and graph analytics.

The analysis is described in the [previous section](https://eagronin.github.io/capstone-analyze/).

## Recommendations Based on the Classification Analysis
As we discussed in the [Data Exploration](https://eagronin.github.io/capstone-prepare/) section, in-app purchases of expensive items generate more revenue for Eglence, Inc. than purchases of inexpensive items. Therefore, it is important to identify users who are more likely to purchase expensive items and target such items to these users.  We call the users who tend to pucharase expensive items “HighRollers” and the users who tend to purchase inexpensive items “PennyPinchers”.  Big-ticket items are those with a price of more than $5.00, and inexpensive items are those that cost $5.00 or less.  

In the previous section we performed classification analysis in KNIME to predict who is a HighRoller and who is a PennyPincher based on the known attributes.  The final KNIME workflow is shown below:

![](https://github.com/eagronin/capstone-report/blob/master/KNIME-workflow.png?raw=true)

What makes a HighRoller vs. a PennyPincher?

The single important variable for predicting whether a player is a HighRoller or PennyPincher is the platform type.  While iPhone users tend to be HighRollers, the users of all the other platforms (Windows, Linux, Android and Mac) tend to be PennyPinchers.  The other variables used for training the decision tree (teamLevel, count_gameclicks, count_hits and count_buyId) do not contribute sufficient explanatory power to the model and, therefore, were not included in the resulting tree.

While the platform itself is not likely to be a cause for the players to purchase more expensive or less expensive items, it is likely a proxy for such attributes as the players’ income and tastes, which could be good predictors of whether a player is a HighRoller or a PennyPincher, if available.

Specific Recommendations to Increase Revenue:

1. Expensive items should be targeted to the players who login using their iPhones.  Inexpensive items should be targeted to the players who login using other platforms.
2. The players use predominantly iPhone and Android for playing the game, i.e. they use their mobile phones rather than desktops and laptops.  Therefore, it could potentially be efficient to relocate some of the resources currently allocated to Windows, Linux and Mac into maintaining and developing mobile platforms to increase profitability.

# Recommendations Based on the Cluster Analysis
As we discussed in the [Data Exploration](https://eagronin.github.io/capstone-prepare/) section, groups of users with different attributes (for example, experienced vs. inexperienced players) are likely to have differences in their tendency to make in-app purchases.  Therefore, revenue and profitability can be increased by choosing different strategies for targeting and setting fees for hosting in-app purchase items shown to users from different groups.

We performed cluster analysis in Spark to identify 3 distinct groups of users, as discussed in the [previous section](https://eagronin.github.io/capstone-analyze/).  The recommended actions based on this analysis are listed below:

Action Recommended | Rationale for the action 
:--- | :---
Increase fees for hosting the in-app purchase items shown to players in Cluster 2 | Players in Cluster 2 are the heaviest spenders.  Therefore, showing in-app purchase items to these players is more valuable than showing items to the players in other clusters.  We can increase game's revenue by charging higher fees for hosting the in-app purchase items shown to players in Cluster 2.
Show fewer in-app purchase items to players in Cluster 1 | Players in Cluster 1 (the beginners) spend very little.  This is likely because they are mostly focused on mastering the game rather than on in-app purchase items.  It may make sense to show fewer items to these players so that they are less distracted from the game and get to the intermediate-to-advanced level (i.e., Cluster 2) faster.  Once the players reach that level of experience and improve their accuracy rate, they are expected to make substantial amount of in-app purchases.  Therefore, getting them to that level faster would contribute to increasing revenue.
Provide incentives to players in Cluster 3 | It appears that as players reach the highest level of experience, they reduce their purchasing activity.  It is possible that they become less engaged with the game and, as a result, are less interested in in-app purchases as well.  Further research needs to be conducted to establish if this is indeed the case.  However, if true, incentives should be provided to players in Cluster 3 to increase their interest level and engagement with the game.

## Recommendations Based on the Graph Analytics
As we discussed in the [Data Exploration](https://eagronin.github.io/capstone-prepare/) section, chattier users, initiators of longer conversations and users who belowng to chattier teams and active user groups are likely to be more valuable, because of their potential to spread information to wider audiences.  As a result, Eglence, Inc. can increase its revenue by choosing the right marketing strategy to target such users, for example, showing the more expensive items to such users.  Even if these users are not going to buy these items, they may influence others in their networks to buy such items.

The extent to which chattier users and initiators of longer conversations are more valuable can be calculated using, for example, the difference in per user revenue between the members of these users’ networks / conversation chains and all the other users. Further research needs to be conducted to perform this analysis.

Further, chattier teams and denser groups are likely to be more valuable not only because of a higher likelihood that their members share information with each other but also because such members are likely to be ”similar” to each other in some respects and, as a result, are likely to purchase similar items.  If this hypothesis holds, the items shown to the members of such teams / groups can be selected based on the items that other members of the same team / group purchased.  For example, if one member of such a group makes an in-app purchase of binoculars, then showing binoculars to other members of the same group is more valuable than showing binoculars to randomly selected users.  As a result, Eglence, Inc. can increase its revenue by tailoring items shown to members of chattier teams / denser groups to their preferences.

The extent to which members of such teams / groups are “similar” to each other can be examined by comparing similarity of items purchased within such teams / groups to similarity of items purchased within less chatty teams / less dense groups.  Further research needs to be conducted to perform this analysis.

## Conclusions
As the data exploration stage showed, purchasers of the most expensive items and top users in terms of their spending generate a disproportionately large share of Eglence, Inc. revenue.  Therefore, the ability to identify such users, is criticalfor Eglence, Inc. to identify new revenue opportunities. The analysis shows that purchasers of expensive items tend to use iPhones, and heavy spenders in general are characterized by high accuracy rate and being at an intermediate-to-advanced level in terms of their experience in playing the game.  

Therefore, targeting expensive items to the players who login using their iPhones would increase revenue for Eglence, Inc.  Similarly, increasing fees for hosting in-app purchase items shown to the group of heavy spenders (as long as they remain at an intermediate-to-advanced level of experience and / or their accuracy rate remains high) would increase revenue generated by in-app purchases.

Previous step: [Analysis](https://eagronin.github.io/capstone-analyze/)
