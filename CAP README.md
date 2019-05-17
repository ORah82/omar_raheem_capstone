### PREDICTING THE PERFORMANCE OF MLB PITCHERS WITH MACHINE LEARNING AND BAYESIAN METHODS 

#### Problem Statement:
My project has two aims: One expand on the scientific paper entitled: “Ball Speed and Release Consistency Predict Pitching Success in Major League Baseball” by David Whiteside , Douglas N Martini, Ronald F Zernicke, Grant C Goulet. By using a neural network and an array of features contrary to those used by the authors I aim to expand on their study.

Two: To use Bayesian Inference to predict 2019 season ERA of 3 Hall of Fame pitchers. 

“This study aimed to quantify how ball flight kinematics (i.e., ball speed and movement), release location, and variations therein relate to pitching success in Major League Baseball (MLB). One hundred ninety starting MLB pitchers met the inclusion criteria for this study. Ball trajectory information was collected for 76,000 pitches and inserted into a forward stepwise multiple regression model, which examined how (a) pitch selection, (b) ball speed, (c) ball movement (horizontal and lateral), (d) release location (horizontal and lateral), (e) variation in pitch speed, (f) variation in ball movement, and (g) variation in release location related to pitching success (as measured by fielding independent pitching—FIP). Pitch speed, release location variability, variation in pitch speed, and horizontal release location were significant predictors of FIP and, collectively, accounted for 24% of the variance in FIP. These findings suggest that (a) maximizing ball speed, (b) refining a consistent spatial release location, and (c) using varied pitch speeds should be primary foci for the pitching coach. However, between-pitcher variations underline how training interventions should be administered at the individual level, with consideration given to the pitcher's injury history. Finally, despite offering significant predictors of success, these three factors explained only 22% of the variance in FIP and should not be considered the only, or preeminent, indicators of a pitcher's effectiveness. Evidently, traditional pitching metrics only partly account for a pitcher's effectiveness, and future research is necessary to uncover the remaining contributors to success.”

The Whiteside study (as it will be referenced to in this document) used to Statcast data to analyze pitching data. It measured success by using FIP as the measurement of success. Fielding Independent Pitching is an advanced metric that aims to improve on the classic Earned Run Average as the benchmark of pitcher performance by removing elements of team defense and isolating specific pitching stats to calculate a new number. Specifically: 

“FIP is an attempt to isolate the performance of the pitcher by using only those outcomes we know do not involve luck on balls in play or defense; strikeouts, walks, hit batters, and home runs allowed. Research has shown that pitchers have very little control on the outcome of balls in play, so while we care about how often a pitcher allows a ball to be put into play, whether a ground ball goes for a hit or is turned into an out is almost entirely out of their control. ” (source)

Additionally the Whiteside study focused on four pitches: only fastballs, curveballs, sliders, and change-ups as well as regression analysis to determine success. The Whiteside study isolated these 4 pitches because of their common release point and therefore these are the only pitches that can be compared. However, I found that this is not necessarily always the case or even the case often enough to make this a determining factor. 

My study goes in a different direction to determine success. In some way my study is more narrow and in some ways more verbose. First my study focuses on all pitches from all pitchers from the 2016 - 2018 season. The reason for this directly counters the Whiteside study for the following reasons: 

There are more than one type of fastball. There is the traditional 4 seam fastball, 2 seam fall ball and cuter. The cutter being a blend of a 2 seam fastball and a slider. 
The release point of a four seam fastball is indeed different than that of the curveball however at the major league level it is closer than at other levels of baseball because if it vastly different than pro hitter would be able to detect the difference in arm angle and make the pitcher pay.
With this said pitchers will keep their arm angle in a common window but arm angle does vary from pitcher to pitcher so studying arm angle vs success is valid.

Also my study uses a different measure of success. Instead of using the FIP I selected Events to be the measure of success. Events describes what happens as a result of a play. For instance if the result of a hit was a strikeout then that was marked as a 1 if the result was a homerun then 0. A double play would be a 1 while a Walk would be 0. The reasoning behind this decision is that a by classifying  success by result of play I could accurately find what was working and what was not. The challenge came from using a Binary classification system. Many of these Events are out of the pitcher's hands. The result is we’re back in the same place we were by using ERA to determine success, too many factors are out of the pitchers control. Instead you will see my second model uses a multiclass classification model to determine success my splitting 2 good, 1 bad and 0 not a pitcher effected play. 

Together I ran Three Feed Forward Neural Networks:

Model 1:

Binary Classification 
Train: .82
Test: .82

This was the most accurate model. The test data struggled to find the point to descend but it did converge close to the training data. 

Model 2: 

MultiClass Classification
Train: 65
Test: 65

For this model I  took a different approach and labelled my (y) data with 0, 1, 2 instead of binary.
As a result the test data descended immediately resulting in an accuracy score in of .65.  This model was underfit and needed more data. 

Model 3:

MultiClass Classification

For my final model I doubled the features (mostly pitch tracking stats) and changed my (y) to the launch speed angle. The launch speed angle takes the speed of the ball off the bat along with the angle of the ball off the bat and gives it a score. The higher the number the more likely it was a hit. 

New features: 

-Plate x
-Plate z 
-ax 
-ay 
-Effective speed  
-Release speed 
-Release pos_x
-Release_pos_z
-Release spin rate
-pfx_x 
-pfx_z 
-Launch speed angle


#### Bayesian Inference

In addition to using neural networks to predict pitching success I wanted to use Bayesian Methods to predict pitching success in 3 Hall of Fame pitchers. For this more concentrated study I took a the advanced metrics of Max Scherzer, CC Sabathia and Justin Verlander. These are three pitchers that been very successful in their careers (give stats), they are all in their 30s and still pitching at a very high level (give stats). What is their predicted ERA for the end of the 2019 season? To do this I had develop different methods of calculating the maximum a posteriori (MAP) for the simple reason that the formula to find the MAP of batting does not work for ERA. 


The reason I used ERA as a measure of success in this instance is because FIP take in much more factors than ERA, additionally ERA’s calculation is universal while FIP’s calculation differs depending on who’s using it.



#### Conclusions 

Of the three models I ran can say they were somewhat successful. These scores and the fact that they did coverage are positive indicators of an accurate model that could still take on more data without being overfit.

There was also a small variation between trials even with the randomization. If the data pool is sufficiently large, this should not be an issue but it was not a significant factor for a couple of the trials when most of the 0’s or 2’s ended up in one group or the other. Predicting pitchers who be elite (or poor) would certainly give the most value, however, this model only had limited success for those pitchers. Ultimately a training group of 75% of MLB pitchers and a test group of the other 25% pitchers is enough data to solve this problem.. Expanding the analysis to multiple seasons or changing the selection criteria would increase the amount of data available and might yield better prediction results.

My Baysen formula for finding the MAP of pitchers ERA was successful. Finding the future ERAs for the three pitchers in my study is possible if the MAP formula is tweaked to calculating ERAs 
