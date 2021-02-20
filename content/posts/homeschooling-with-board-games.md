---
title: "Homeschooling With Board Games: Pandemic Edition"
date: 2021-02-19
draft: true
---

A lot has changed in the last year. I started a new job in April 2020.
My 8-year old daughter started homeschooling. I started hoarding wine (who needs toilet paper?).
And we play a lot more board games.

Appropriately, one of those board games is called Pandemic.

For those unfamiliar with the game, Pandemic is a co-operative game ...

_TODO: summary of game mechanics_

Which city is the most important?
---------------------------------

_me: Which city do you think is the most important in the game?_

_daughter: London_

_me: Why?_

_daughter: Because we live there!_

Before we can answer "which city is the most important", we need to decide what
"importance" means. The city you live in is the most important for your own survival, but
which cities are the most important for winning the game? The answer to that question will
depend on what players are trying to do and what has happened so far in the game.

Let's focus on a single scenario: Bogotá and Santiago are on the verge of an outbreak (i.e.
have three infection cubes), and a player can only intervene in one of the cities in this
turn. Which city should the player prioritise?

*insert images here*

Bogotá is connected to Buenos Aires, Sáo Paulo, Miami, Mexico City, and Lima. So the
yellow infection will spread to five new cities if there is an outbreak in Bogotá. On the
other hand, Santiago is connected to only Lima. So an outbreak in Santiago will lead to
only one extra infected city. From this perspective Bogotá seems more important than
Santiago and Santiago can be sacrificed.

In network analysis, each city on the board is called a **node** and the connections
between the cities are called **links**. The importance of a node within a network is
called **centrality** (think of the person at the centre of the party). There are many
ways to define importance, but like in our example above, one way is to rank them by the
number of links connecting to each node. The number of links connecting to a node is
called it's **degree**, so the measure of importance based on the number of links is
called **degree centrality**. In our board game, degree centrality would give us a ranking
like this:

| Rank | City         | Degree |
|------|--------------|--------|
| 1    | Istanbul     | 6      |
| =2   | Karachi      | 5      |
| =2   | Bogotá       | 5      |
| ⋮    | ⋮            | ⋮      |
| =5   | Johannesburg | 2      |
| =5   | Lima         | 2      |
| 6    | Santiago     | 1      |

By this measure of importance, Istanbul is the most important city in the game and
Santiago is the least important. However, using degree centrality to measure importance
has some limitations.

Firstly, there are many cities with the same rank because the degree of the nodes in
this network are in the range 1 to 6. Looking at the network's **degree distribution**, we
can see that there are 17 cities with degree 4, all of which would be ranked the same.

{{<svg "pandemic-degree-distribution.svg">}}

Secondly, centrality measures the __topological__ importance of a node, but within a
dynamic system like a board game we need to think about what could happen in subsequent
turns.  For example let's compare what happens if there is an outbreak in Istanbul vs
Karachi.

*insert images here*

Six cities will be infected if there is an outbreak in Istanbul, but only five cities will
be infected if there is an outbreak in Karachi. But what happens in the next turn? Let's
imagine a pretty bad scenario: we're too far away to do anything about the infected cities
and we draw an epidemic card. How likely is it that another outbreak occurs when we draw a
card from the bottom of the infection deck?

An outbreak occurs when adding an infection cube to a city results in more than three
infection cubes of a single colour. And during an epidemic we add three cubes to the city
drawn from the bottom of the infection deck. So an outbreak will occur if the infection
card matches any city with one or more infection cubes of that city's colour.

If there are no other infected cities, and there are _N_ cards in the infection deck, then
there is a _5/N_ chance that another outbreak occurs in the turn after an outbreak in
Karachi. However, two of the cities connected to Istanbul are blue instead of black. If we
draw one of these blue cards, we will add three blue infection cubes but _not_ trigger an
outbreak in that city because there are still no more than three of any single colour.
Therefore, in the Istanbul scenario there is only a _4/N_ chance of an outbreak in the
next turn.

_insert images here_

This entire scenario is pretty unlikely, but it did play out in a real life game that
inspired this homeschooling lesson. We're already stretching my daughter's knowledge of
probability, so let's not worry too much about the exact likelihood of the scenario until
we have covered some more of the basics of probability. However, we can say that
everything else being equal, in-group degree centrality matters more than overall degree
centrality if we're trying to prevent an outbreak. Ranking by in-group degree centrality,
gives us something like:

_insert table_

After ranking with in-group degree centrality, there are still a lot of very similarly
ranked cities. For example, should we prioritise Bogotá or Karachi if both are on the
verge of an outbreak? Can we find a metric to differentiate between them?

- eigenvector centrality
