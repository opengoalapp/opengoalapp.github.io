---
layout: post
title: Applied Tracking - Pressure
categories: [Tracking]
---

Whilst the public analytics movement has barely scratched the surface in terms of realising the potential of event data, the use of tracking data in tandem with events undoubtedly offers additional context to the analysis in many situations. This is the first in a series of articles which will take a practical look at how tracking data can be applied to pre- or post-game analysis, with the aim of gaining actionable insight on our own team or an opponent.

This article will take a look at an example workflow for a pre-game analysis scenario. Here we focus on the characteristics of a team's application of pressure on an opponent in receipt of the ball and also identify situations in a match where opponent pressure was invited in high-risk situations.


### A fluid definition of pressure


One aspect of StatsBomb's event data specification that makes it stand out from other data providers is the inclusion of a "pressure" action. This off-the-ball action allows an analyst to examine at both an individual and team level how and where defensive pressure is being applied to an opponent in possession of the ball. From this data you can identify a forward who is regularly putting in a shift as a first line of defence or a team that stands off opponents noticeably more than other teams in the league, to name just two examples. This has clearly added a valuable layer to the kinds of analysis possible with event data. However, the standard drawback applies that you are at the mercy of the data provider for defining what actually constitutes the action in question, in this case pressure.

​
Using tracking data which has been synced to an event data feed you not only gain the ability to define pressure in terms that you decide, and indeed in multiple ways depending on application, but you can unlock all of the context stemming from the remaining players on the pitch that is missing from event level data. Let's now look at just one of the many ways you could analyse a team's tendency to apply pressure using a game from the open tracking data set provided by Metrica Sports.


### Ball Receipts Under Pressure

Let's say we are conducting a data-driven review of our last game as part of post-match evaluation process. As part of this we can plot all the pass receipts that we conceded against our opponent. This is a pretty standard event based analysis which can be derived from the x,y co-ordinates of the end location of successful passes by our opponent. We can however augment this data with tracking information, specifically the distance of our nearest defender when the opponent received the ball.

<p align="center">
 <img src="/images/Tracking - pressure/pass_receipts.png" />
</p>

Here we've used the distance between the ball receipt and the nearest defender as a proxy for how much pressure our team applied on each pass that was conceded. In general our opponent was mostly receiving the ball in areas that posed little immediate danger as we would hope, with pressure applied well into our opponent's half at times. The sliding scale used immediately reveals some interesting additional insights, some of which should instigate further investigation:

-   The opponent's right flank was aggressively pressured, even at deeper locations near the half way line. The left flank conceded a number of passes in more advanced areas, with a significant number of unpressured receipts in positions that are undesirable to leave an opponent time and space.
    
-   There were a number of instances where the attacker was allowed 7-10m distance (equal to 150-315 sqm of space!) in "zone 14" type positions upon receipt of the ball.
    
-   A number of passes were conceded around the right post (in the attacking direction) despite a defender in very close proximity. Is this aerial duels being lost, attackers losing their markers, or something else?

### Too Much Time?

Let's now home in on some of the potential concerns raised above, namely looking at times when an undesirable amount of time and space was given to the opponent in dangerous areas. With a simple query of the data set we can apply a cut-off distance to filter the passes which we've deemed as being of concern. We can then use the full extent of the tracking data available to build a more complete picture of how and why these situations developed. This in turn can flag situations where corrective action might be required at a strategic level or indeed if certain players haven't been following instructions as desired. Let's filter all pass receive points where >7.5m of distance was allowed to the nearest defender.

<p align="center">
 <img src="/images/Tracking - pressure/in_space.png" />
</p>

We can clearly see a handful of instances where the opponent was given time and space around the edge of the penalty area. We have the opportunity to easily look into how these situations arose as all of these receive events are timestamped. So let's recall the full positional information for all 22 players for these particularly dangerous passes conceded. We'll simply add a constraint to our query which selects passes which were received <35m from goal. Four of these are shown.

<p align="center">
 <img src="/images/Tracking - pressure/att_focus.png" />
</p>

We can of course select the series of frames immediately before and after the single frame selected to view the whole attacking sequences. The more powerful workflows will also have the corresponding video footage tagged with the tracking timestamps so these sequences can be called upon with a single click. In the examples above, whilst the intent of tactical setup is unknown, it looks as though the defenders nearest the ball have been too passive in reading the danger and closing space in at least the top two and bottom right examples.

### Wing Imbalance?

Another notable feature of the plot of passes into space was that our right flank was giving away more passes in advanced positions compared to the left, despite considerable attacking activity on both wings by our opponent. Is our right back a touch off the pace in closing down? How do these situations materialise? Let's now filter passes into >7.5m space by location on the pitch and take a look at where these passes originated.

<p align="center">
 <img src="/images/Tracking - pressure/left_wing.png" />
</p>

We can see that we were caught out twice by long cross-field diagonals leading to dangerous situations. There is also a clear hub of pass making and receiving activity where our opponent has been productive in deeper left-side half space areas. Analysis of additional games and relevant video clips would give insight as to whether defensive resources need bolstering in this region, if players weren't positioned as intended, or if our opponent was simply extremely creative in developing space for this game.

### Looking for Trouble?

If we now flip our scenario around and use our data set to imagine we are now the home team, attacking left to right, performing the same post-match analysis. We can identify all the passes that we made where the receiver was under intense pressure and as such the player receiving will need to take instant action to redistribute the ball or evade the defender. For many of these occasions we would expect this such as when in advanced attacking positions. However there will be times when we will be under intense pressure deep into our own half. Given the events we are observing are a result of passes made, it means the decision has been made by a player to pass and put the receiver under immediate pressure. It would be useful to take a deeper dive into these situations.

<p align="center">
 <img src="/images/Tracking - pressure/closed_down.png" />
</p>

Here we can easily identify at least half a dozen occasions where a pass has been chosen where there is potentially significant risk of a turnover in a highly dangerous position. Like before we can pinpoint the timestamps of these passes to gain the full situational context to evaluate whether a clearance or alternative options would have been more appropriate, considering of course the general tactical outlook of the team. We'll again focus on four examples here.

<p align="center">
 <img src="/images/Tracking - pressure/def_focus.png" />
</p>

Here we can see in the top two occasions there is space for the receiver to work with and evade the pressure, even though risk of mis-control remains. It can certainly be argued these passes were risk-reward appropriate for a possession based playing style. The bottom two examples however are clearly extremely dangerous passes where superior alternatives were available. A turnover here would probably lead to a goal-scoring opportunity for the opponent with attackers free centrally and at the back post for the bottom left and bottom right examples respectively.

### In Conclusion

One of the clear advantages of data driven analysis is the ability to instantly recall all instances of a scenario of our choosing from a match or selection of matches. In the above examples we have essentially said "show me all of the occasions where the opponent received the ball with at least/at most n metres distance from the nearest defender". We can select any value of n, and from here we can inspect how each event developed, what the outcomes were, and easily use these event sequences to build a top-down animation or video clip package for further analysis of root causes and identification of team and player level issues that need addressing.

The above examples using distance to nearest defender demonstrate just one variation on the theme of defensive pressure. There are of course countless alternatives made possible with a synchronised tracking and event data set.

### Acknowledgements

This work has been made possible due to the open tracking data set provided by Metrica Sports. Effortless plotting capability provided by the incredible  [mplsoccer](https://github.com/andrewRowlinson/mplsoccer)  Python library by Andrew Rowlinson.