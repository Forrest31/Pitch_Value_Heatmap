# Pitch_Value_Heatmap

##Overview

Oftentimes we see heatmaps for pitchers display the number of pitches they throw in certain locations, with the most frequent locations having a deep red color while the least frequent locations are shown in blue. While useful in particular applications, this visualization gives the reader no idea of what happened on each of those pitches.  Did they result in whiffs, homeruns, weak contact?  We don't know.  This project seeks to answer that question by shwowing a pitcher's results as a heat map with his best outcomes become shown in blue and his worse outcomes shown in red.  

##Pitch Scoring Methodology
A widely-accepted method of valuing pitches is assigning it the change in the run expectancy table from that pitch. A run expectancy table shows the average number of runs scored in each of the 288 possible game states (12 possible counts x 8 possible base states x 3 possible out states).  Each value comes from adding all of the runs scored after this state and dividing it by the number of times the state occured.   
This file creates a weighted heat map for Paul Dolander's pitches vs. LSU on 30 March 2023. Rather than frequency of pitches, this heat map will assign a run value to each pitch and this run value will be represented on the heat map.

This project requires pitch location which we can get from the Synergy API. First step is to find the synergy game ID. First, we find UT's team ID in the teams table (145958) and the 2023 season ID for D1 baseball in the seasons table (41). 

UT was the visitor in this game so we query the games table where visitor_team = 145958 and season_id = 41 to find the 643 game id (200150).  The 643 game_id is passsed into the bridge_synergy_games table to pull the synergy game id (63cf97261078b38d56abe480).  

I take this synergy game id to postman where I input my OAuth2.0 credentials in the authorization tab.  After input, I click "Get New Access Token". I click use token, copy the name of the token into token name and proceed to pass in my search parameters (the synergy game) {
    'gameIds': ['63cf97261078b38d56abe480'],
    'take': 10000 }
into the body    
    
I change "Get" to "Post" at this endpoint: https://baseball.synergysportstech.com/external/api/events/filter and send. 

A JSON is returned in the body which is copy and pasted into a text file, saved as "all files" with a .json suffix and saved into my working directory.  

JSON packages and libraries are installed to convert into a data frame.
