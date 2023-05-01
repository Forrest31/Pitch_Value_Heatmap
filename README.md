# Pitch_Value_Heatmap

##Overview

Oftentimes we see heatmaps for pitchers display the number of pitches they throw in certain locations, with the most frequent locations having a deep red color while the least frequent locations are shown in blue. While useful in particular applications, this visualization gives the reader no idea of what happened on each of those pitches.  Did they result in whiffs, homeruns, weak contact?  We don't know.  This project seeks to answer that question by shwowing a pitcher's results as a heat map with his best outcomes become shown in blue and his worse outcomes shown in red.  

##Pitch Scoring Methodology
A widely-accepted method of valuing pitches is assigning it the change in the run expectancy table from that pitch. A run expectancy table shows the average number of runs scored in each of the 288 possible game states (12 possible counts x 8 possible base states x 3 possible out states).  Each value comes from adding all of the runs scored after this state and dividing it by the number of times the state occured from a given period of time.  For example, in 2023, each inning has a run expectancy of 0.7666 runs. This value will change with the result of the subsequent pitch. A ball will increase the run expectancy to 0.8442. The difference in these states, plus the number of runs scored, can be assigned to the pitch; 0.0776 in this case. 

### Data Populating the Heatmap

To demonstrate the concept, I collected all pitches from University of Tennessee's star pitcher Chase Dollander between 3 March - 22 April; a span of 8 games totaling just over 450 pitches. This data comes from https://synergysports.com/ via their API. The data is returned in a JSON file, and is read into R using the jsonlite package. While containing dozens of features, we focus on:

Game state
Horizontal location
Vertical location

A non-trival amount of data wrangling is required to create a game state when the pitch is delivered and the resulting game state. The RE 288 table created from the 6-4-3 charts database is then joined onto Synergy data on the game state to provide the run expectancy of every possible game state. 

### Design Considertions

Several factors must be determined to create this heat map:
Size of mesh grid
Sample of pitches
Number of decrements to each pitch
Decrement methodology (linear or non-linear)
Type of visualization

The size of the grid, sample of pitches, and number of decrements all influence the quality of the resulting visualization. The Syergy data plots the loctation of each pitch on the horizontal axis with coordinates between -2.5 and 2.5 and the vertical axis between 0 and 5. This area is what our mesh grid will represent. I have to determine if each pixel in our grid will 1, 0.1, 0.01 or something else. If it is 1, then the mesh grid will be 5x5. Such a grid would not provide the necessary level of fidelity for pitch location. On the other hand, a pixel size of 0.01 would result in a 500x500 grid and potentially be too large of a space to represent a small number of pitcher. 

I represented this relationship with the following equation (2L + 1)^2 * p /m^2 where L is the number of decrements, p is the number pitches and m is the number of rows/columns of the mesh grid.  
