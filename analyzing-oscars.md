### predicting oscar winners
*there are a lot of steps on the way to logistic regression*

- obtain 15 years of data of nominations, winners
	+ oscars, golden globes, bafta...sag, dag
	+ scrape the web
		* wikipedia, google
		* `curl -k -sA "Chrome" -L 'https://www.google.com/search?hl=en&q=oscar+winner+2014' -o ssearch.html`
			- widget data not show up in html page
			- wikipedia needs follow links
		* http://www.freebase.com/
		* wikidata.org 
		* http://www.omdbapi.com/ open movie database
- clean and structure data 
	+ extract raw data components of html and other crud
	+ split combined columns
	+ categories and nominees names must match across awards
- load into R
	+ load
	+ generate dataframe
	+ dummy variables with binary
		* `2014,best picture, 12 years a slave, [won] Y, [bafta-nominated] Y,...`  
	+ logistic regression to generate probabilities for new data points (the 2016 nominees)

#### obtain data
- watch out for getting IP blocked on google searches
- Java Jsoup not hard to get programmatic results, its an idea

##### wikidata API tutorial
freebase is transferring everything to wikidata

[wikidata API tutorial here](https://www.mediawiki.org/wiki/API:Tutorial)
	
	entry point: https://en.wikipedia.org/w/api.php
	example: api.php?action=query&titles=San_Francisco&prop=images&imlimit=20&format=jsonfm
	Request URL: /w/api.php?action=query&format=json&maxlag=&prop=images&titles=San_Francisco&imlimit=20

##### omdbapi
example api request

	http://www.omdbapi.com/?t=Revenant&y=2015&plot=short&r=json

##### wikipedia scrape
pages for each category are formatted like so, and each page lists all the nominees and winners, and the formatting follows convention with the underscores, sort of.

	https://en.wikipedia.org/wiki/Academy_Award_for_Best_Picture

	Current categories:
	Best Picture
	Best Director
	Best Actor in a Leading Role
	Best Actor in a Supporting Role
	Best Actress in a Leading Role
	Best Actress in a Supporting Role
	Best Animated Feature
	Best Animated Short Film
	Best Cinematography
	Best Costume Design
	Best Documentary Feature
	Best Documentary Short Subject
	Best Film Editing
	Best Foreign Language Film
	Best Live Action Short Film
	Best Makeup and Hairstyling
	Best Original Score
	Best Original Song
	Best Production Design
	Best Sound Editing
	Best Sound Mixing
	Best Visual Effects
	Best Writing (Adapted Screenplay)
	Best Writing (Original Screenplay)

the page has a link for bafta and the rest, `https://en.wikipedia.org/wiki/BAFTA_Award_for_Best_Film`

