# Beach Volleyball Match Data

This repository contains **most** beach volleybal men's and women's match data from the FIVB tour between April 2013 and July 2017 and the AVP tour between April 2014 and June 2017. FIVB includes pool and elimination matches. AVP includes pool, elimination, loser's bracket, winner's bracket, and qualifying matches (as applicable).

**Some notes:**

The team names have been cleaned (some special chars remain in FIVB dataset) and sorted. 
*"Sorting"* means that a team will always appear based on the alphabetic order of the player names. For example, Dalhauser/Lucena will not appear as Lucena/Dalhauser. All teams have been standardized in this way.

The FIVB does not follow a naming convention that can be identified (sometimes last name only, sometimes last name first initial, etc.). The AVP appears to have the full name. Parse at your leisure :)

The **dataset** variable in FIVB is used to better identify where the data came from. Note that in dataset 2, ranking is missing (future update) and the **round** names are different. The round names are consistent within a tournament, and generally the lowest number pool corresponds to A, the next lowest number to B, etc.

The **score** will indicate which team won. It should be read from left to right. For example, "21-19 21-19" signifies team_a won vs. "19-21 19-21" signifies team_b won.

Tournament type is based on FIVB designation:

WCH=World Championship, GS=Grand Slam, MJS = Major Series, WTF = World Tour Finals, WT5*=World Tour 5 Stars, WT4*=World Tour 4 Stars,  etc., SAT=Satellite, CHAL=Challenger, MST=Master, CCH=Continental Championship, NT = National Tour, U19 = Under 19, 

2 AVP tournaments include the country name in the team names as I have yet to try and parse it out. Good Luck :)

Rank in the AVP set follows the convention "[rank or seed, qualifier]". Unsure of qualifier interpretability.

# License
Attribution required. Non-commercial use only
