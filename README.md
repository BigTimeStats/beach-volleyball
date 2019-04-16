# Beach Volleyball Match Data and Statistics

This repository contains **most** beach volleyball men's and women's match data and match statistics from the AVP & FIVB tours. Archive contains matches from September 2000 to July 2017. Updated files published periodically with match dates in filenames.

**Notes:**

Date represents tournament date and is typically the first day of the tournament.

The winning team is denoted by "w_" and the losing team is denoted by "l_". 

The player names have been sorted alphabetically for a winning or losing team. This means that "Nick Lucena" should always appear in "w_player1" and "Phil Dalhausser" should appear in "w_player2", regardless of the data source order.

Age is represented in years and is calculated as: (event date - birthdate) / 365.25, rounded to 7 decimals.

Height is represented in inches.

"w_rank" and "l_rank" follow the convention "seed, qualifier". If players have individual seeds (e.g. in a King of Beach tournament), only the second player's seeding is retained at the time of the data pull, but before the players have been sorted alphabetically. This means that for these matches, the seeding may not correspond to the correct player.

Duration is represented as "h:mm" (hours:minutes)

Match stats (columns 34:65) represent match totals. Available for Contender's Bracket and above for about 20 FIVB and most AVP tournaments. "Hitpct" represents (kills - errors) / attacks. 

# Example Work

Using this data, I created a beach volleyball Tableau dashboard to summarize some key metrics:

https://public.tableau.com/views/AVPFIVBPlayerInteractiveResultsandStats/Dashboard3

[Tableau Dashboard]("Tableau Dashboard Preview.png")

Read more on my blog here: https://bigtimestats.wordpress.com/2017/09/18/avp-fivb-beach-volleyball-match-database/


## Python

Here is some starter Python code to download the data into memory and query it with SQL. This code was run in [Google Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb) and prints the top 10 teams with the highest winning percentage:

```
import pandas as pd
# !pip install pandasql
import pandasql as ps

url = ['https://raw.githubusercontent.com/BigTimeStats/beach-volleyball/master/match_archive_2000_to_2017_v2.csv',
       'https://raw.githubusercontent.com/BigTimeStats/beach-volleyball/master/match_update_20170729_to_20170912.csv',
       'https://raw.githubusercontent.com/BigTimeStats/beach-volleyball/master/match_update_20170913_to_20180314.csv',
       'https://raw.githubusercontent.com/BigTimeStats/beach-volleyball/master/match_update_20180315_to_20180821.csv',
       'https://raw.githubusercontent.com/BigTimeStats/beach-volleyball/master/match_update_20180822_to_20190409.csv'
      ]        
      
li = []
for i in range(len(url)):
    temp = pd.read_csv(url[i], index_col=None, header=0)
    li.append(temp)

df = pd.concat(li, axis=0, ignore_index=True)

df.head(5)

q1 = """
select player1, player2, 
count(*) as matches_played, 
round(AVG(Win) * 100, 0) as win_pct
FROM
(select w_player1 as player1, w_player2 as player2, 1 as Win from df
UNION ALL
select l_player1 as player1, l_player2 as player2, 0 as Win from df) a
group by player1, player2
having count(*) > 100
order by AVG(Win) desc
limit 10
"""

print(ps.sqldf(q1, locals()))
```
Output:
```
                player1               player2  matches_played  win_pct
0  Kerri Walsh Jennings     Misty May-Treanor             846     92.0
1            April Ross  Kerri Walsh Jennings             241     88.0
2        Larissa Franca        Talita Antunes             194     86.0
3       Phil Dalhausser           Todd Rogers             689     85.0
4    Juliana Felisberta        Larissa Franca             622     84.0
5         Elaine Youngs          Holly McPeak             259     83.0
6      Ana Paula Henkel          Sandra Pires             106     82.0
7      Jonas Reckermann          Julius Brink             186     80.0
8         Elaine Youngs        Nicole Branagh             369     79.0
9          Emanuel Rego        Ricardo Santos             567     79.0
```


# License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

Non-commercial use only. Attribution required.
