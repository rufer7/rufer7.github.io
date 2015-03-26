---
layout: post
category: out-of-the-www
title: Swissunihockey key matcher
date: 26 Mar 2015
tags: swissunihockey sports Java
---

In my position as a participant of the committee of the floorball club [Hornets Regio Moosseedorf Worblental](http://www.hornets.ch) I had to deal with a challenge. To overcome with the challenge I wrote a little program, which I want to present here.


#### Challenge
The floorball club got the game schedules for the U21 league and the 1st league for the season 2015/2016. In both schedules the teams of the corresponding weren't filled in directly. For every game day there were combinations of keys, where every key will be replaced with a team. Now every club, which has a team in these leagues has to tell the [swiss floorball association](http://www.swissunihockey.ch), which key should represent their team.

Below you can see an excerpt of such a game schedule

**19.09.2015**

Home | Away
:----------- | :-----------
0 | 1
2 | 3
4 | 5
6 | 7

This means at September 19 the key 0 has home game against key 1.

For planning purposes the challenge was to figure out which key combinations would be best, so that the two teams playing in different leagues would have as many home games as possible at the same date.


#### Solution
First I tried to figure it out by taking a piece of paper and going through the combinations. After a few minutes I recognized that this approach is consuming too troublesome and time consuming, so I decided to write a java program, which will do the work for me.

The program I wrote consists of the following components

* domain
  * League
  * MatchingResult (Matches per key combination)
* KeyMatcher (Logic to calculate the matching results)
* MatchingPrinter (Prints out the results to the console)

It took me several hours to write this program, but it avoids additional work in the future.


#### How to use
The following code snippet shows, how to use the swissunihockey key matcher

{% gist ff4ddeb7ea2fb037b664 %}

As you can see the two leagues have to be created by passing the amount of teams and a map containing `home game keys` per `date`. These leagues then have to be passed to the `findMatchesForTwoLeagues` method of a `KeyMatcher` instance. The matching result will be generated and can then be printed to the console by calling the static `printResult`-method of the `MatchingPrinter`.

The printed result looks as follows

{% gist a070a84083e88de2f205 %}

The program is freely available on [GitHub](https://github.com/rufer7/swissunihockey-key-matcher)