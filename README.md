# Pitch_Value_Heatmap

##Overview

Oftentimes we see heatmaps for pitchers display the number of pitches they throw in certain locations, with the most frequent locations having a deep red color while the least frequent locations are shown in blue. While useful in particular applications, this visualization gives the reader no idea of what happened on each of those pitches.  Did they result in whiffs, homeruns, weak contact?  We don't know.  This project seeks to answer that question by shwowing a pitcher's results as a heat map with his best outcomes become shown in blue and his worse outcomes shown in red.  

##Pitch Scoring Methodology
A widely-accepted method of valuing pitches is assigning it the change in the run expectancy table from that pitch. A run expectancy table shows the average number of runs scored in each of the 288 possible game states (12 possible counts x 8 possible base states x 3 possible out states).  Each value comes from adding all of the runs scored after this state and dividing it by the number of times the state occured.   
This file creates a weighted heat map for Paul Dolander's pitches vs. LSU on 30 March 2023. Rather than frequency of pitches, this heat map will assign a run value to each pitch and this run value will be represented on the heat map.


