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
