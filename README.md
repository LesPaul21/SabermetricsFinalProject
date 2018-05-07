# SabermetricsFinalProject

## Contents

1. Repository Contents
2. Usage Instructions
3. Statistic Explanations
4. Project Proposal
5. Statistic Analysis
6. Acknowledgements

## Repository Contents

- PrOCalculator.ipynb: Main application. Usage is explained in usage instructions.
- PrOData.csv: CSV file containing all relevant data needed for calculation.
- PrODataGeneration.sql: SQL file used to generate the CSV from Retrosheet.
- README.md: This file
- Statistic Proposal.pdf: Explanation of the usefulness of the statistic.

## Usage Instructions

1. Download the PrOCalculator.ipynb file as well as the PrOData.csv file.
2. Open the .ipynb file in Jupyter Notebook. 
3. Run the first cell only.
4. Enter any player's first name followed by the second name who has played between 2010 and 2016.
5. After the data has been displayed, type y if you would like to lookup another player and n if you are done.

Known Issues

- If the kernel dies, the cell needs to be re-run. This is believed to be a bug in Jupyter Notebook and not the program itself.
- Some more obscure players that did have at bats between 2010 and 2016 may not be contained in the database. This is most likely due to a 1000 row limit enforced in the SQL script for efficiency purposes.

## Statistic Explanations

- PrOO: Productive Out Opportunities. Number of at bats with less than two outs and a runner in scoring position.
- PrO: Productive Outs. Productive Out Opportunites that produced a run or advanced a base runner.
- PrO%: Ratio of Productive Outs to Productive Out Opportunities. Main focus of this program and project.
- Pro_RBI: Number of productive outs that produced an RBI.
- Pro_RBI%: Percentage of productive outs that produced an RBI.
- Total SO%: Overall percentage of at bats that resulted in a strikeout.
- PrO SO%: Percentage of Productive Out Opportunites that resulted in a strikeout. 

## Project Proposal

Often in this class we have spent time talking about measuring a players contribution in terms of runs that the player in question is contributing to his team. We have done this in many ways. Some were inefficient such as counting RBIs, while others were better such as calculating how many runs an at bat was worth by run expectancy. One thing that I don’t think we have touched on enough is the ability of a player to create a productive out, meaning an out that resulted in a run or advanced base runner. I will be calling this statistic PrO%, or Productive Out Percentage. I believe this statistic would be an accurate metric to measure a player’s contribution to the “small ball” part of the game.

Given that the data I need will be in the form of play by play information, I will be using the same Retrosheet database that we have been using in the class. I will be pulling all plays in which the batter was up to bat with runners on second or third and less than two outs. I will consider this to be the plays in which a player has an opportunity to create a productive out and will call the total number of these plays per player PrOO or Productive Out Opportunities. I will then count the number of PrOOs in which the batter was ruled out but a run scored or a runner advanced. This count will be called Productive Outs or PrOs. Thus, PrO% will be calculated as indicated below:

PrO% = PrO/PrOO

To expand upon this idea, I am considering evolving the statistic to weight productive outs that result in runs heavier than those that merely advanced the base runner. I would also put emphasis on outs in which runners advanced and runs scored. I do not know what weights I would assign and it would most likely take a fair amount of tinkering to get right. For that reason I consider this to be a stretch goal for the project. I am considering using the ratio of run value for the two different kinds of at bats to weight them but that is just my preliminary idea.

To demonstrate this I am choosing to go with a simple approach. I have not touched web development for three years and will not have the time to refresh myself alongside finishing senior projects. For that reason, I am planning on creating a python application that will exist in the same directory as a csv file that will contain all of the necessary data. The application will prompt the user for the name of a player and will then fetch the PrO, PrOO, and PrO% for that player. The application will also display the percent of PrOs that resulted in runs, the number of that resulted in an advanced runner, and the number that resulted in both. This will be comprehensive for all players with data in the retrosheet regardless of position. To run this, it will be required that the user downloads the python script as well as the csv file and that they are stored within the same directory and the csv file’s name is not changed. This will be detailed in the README.

## Statistic Analysis

When I began evaluating this statistic I was expecting most players to be returing a very high success rate in creating productive outs. I believe this assumption came from my own personal frustrations as a baseball fan. Watching players pop out with a man on third and one out and failing to create that crucial run is one of the greatest frustations of any fan. It was much to my surprise that most players were creating producive outs at a relatively low rate. When looking at players with a minimum of 500 PrOOs (Productive Out Opportunities), Elvis Andrus topped the PrO% (Productive Out Percentage) ranking with 37.8% of his PrOOs resulting in productive at-bats. I was expecting good hitters to be able to create a productive out in about half of their opportunities. After all, all they really need to do is make contact right? Evidently not.

Looking at the statistics, I believe that, at least for most players, the PrO% is being weighed down by the inclusion of the "man on second" scenario. Advancing a man from second is simply not that easy. It most often either requires a decent smack to right field (most often by a left handed batter) or a well hit but slow rolling ground ball to the right side. Given how common this base state is, it is easy to see what may be dragging down the stastics.

 In reality, good PrO% numbers did not look much different than a good batting average and only a little bit lower than a good OBP. The average PrO% for players with at least 500 PrOO is 0.214. This is approximately 40 points below the average league batting average in 2017. Given a batting average Mendoza Line of 0.200 and assuming a proportional relationship to PrO%, this would put a hypothetical PrO% Mendoza Line at approximately 0.160. I would like to note that while I believe in the validity of a productive out metric, I do not believe that the scope of this statistic is large enough to make a strong argument to replace any player by this metric alone. By the logic of the above numbersm I've created the following rough player assessment based on PrO%.

| | Minimum | Maximum |
| --- | --- | --- |
| Good | 0.260 | N/A |
| Average | 0.160 | 0.260 |
| Replacement | 0 | 0.160 |

It is worth nothing that the PrO% tended to unsurprisingly favor contact, "slap", hitters over power hitters. Famed slap hitter Ichiro Suzuki, turned in a phenomenal PrO% of 0.322. A full 79 points above the league average. Meanwhile, the home run hitting machine that is Giancarlo Stanton, turned in a replacement level PrO% of 0.152. I also found below average numbers for Carlos Gonzalez and Edwin Encarnacion while finding great numbers for Joe Mauer and Marco Scutaro. Does this mean that I believe that the Yankees should be shipping Giancarlo Stanton to the minors immediately? Absolutely not, he is one of the best players in baseball. That being said, if you need a sacrifice fly to win the game and have Ichiro on the bench. Giancarlo may not be your guy.

I created a correlation matrix (available in the jupyter notebook) to compare the PrO% statistic to other stats that may be useful in predicting a player's ability to create a productive out. One thing that I was certain I would see would be a strong negative correlation between PrO% and strikeouts. It seemed intuitive that a player's ability to create a productive out would be highly influenced by his ability to put the bat on the ball. Surprisingly, while there was a notable negative correlation coefficient when comparing PrO% to Strike Outs, the R-squared value came out to a mere 0.035. In fact, PrO% seemed to be poorly correlated with the vast majority of other metrics. It's strongest correlation was with RBI% (the precentage of PrO that resulted in RBIs) and even that was only 0.13.

This could draw me to one of two conclusions. First, I could conclude that the loose correlation between PrO% and other commonly accepted metrics of performance is indicative of the poor quality of a productive out metric. Second, I may conclude that this metric is simply along a different line of thinking and player evaluation metrics than those already in place. I do firmly believe that measuring a players ability to be productive, even in an out, is a valuable metric, but I acknowledge that there may be shortcomings in my calculation. I believe that future work on this subject should focus on assigning weights to different types of productive outs. If sabermetrics is about measuring a players ability to create runs and therefore wins for his team, a metric that evaluates the ability for a player to do that, even while creating an out, must hold some value.

## Acknowledgements

- Retrosheet 2010-2016: Provided raw data for calculation.
- Baseball Reference: Provided average statistics used for comparison.
- MySQL Workbench: Used for generation of data tables
- Jupyter Notebook: Used for application of statistic
