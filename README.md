#README

mdnCrawl.js is a useful program that was built to facilitate the work of volunteers who want to collaborate on the translation effort of the MDN documentation on JavaScript. Language is still a huge barrier for many people all around the globe. Translating documentation has great value, as it improves the accessibility of valuable knowledge for the persons who need it the most.
mdnCrawl.js employs cheerio.js to scrape one by one the routes of the documentation of the MDN database and search for flags that indicate the existence of a translation on a given language, and its status if it exists. Its output can be useful for obtaining statistics about the state of the translation.

mdnCrawl.js works in three steps:

1. In **Stage 1**, it starts from [the Index of MDN's JavaScript Documentation](https://developer.mozilla.org/en/docs/Web/JavaScript) and scrapes the contents of the `<a>` tags in the `#wikiArticle` element. Each of the urls is pushed as an object with an `enUrl` property equal to the url into an array without including duplicates. This means that the crawler will scrape each of the links until no new links can be found. The resulting array contains all the urls in the English version of MDN's documentation. By default, it only obtains routes nested into `Web/JavaScript`, which contain the JavaScript documentation. You'll find roughly one thousand routes in the MDN Documentation of JavaScript. Take this into account, when changing this parameter, or you'll have to wait a lot to get your results.
2. **Stage 2** takes the array outputted by **stage 1** and, for each element, verifies whether a route for a given language's version (Spanish by default) of the current route exists among the `<a>` tags in the `#translations` element, appending the `esUrl` property to the corresponding route in the array (empty string if the translation in the desired language doesn't exist).
3. Finally, **Stage 3** runs through the urls array again, scraping the urls in the `esUrl` property of each element and verifying the existence of an element with the class `.translationInProgress` for each url. It appends an `esMessage` property to each element including the corresponding text in the element `.translationInProgress`, which is usually employed to leave notes about incomplete translations. jsonfile.js is employed to create a `.json` file containing the data in the array with the url in English and another language, as well as notes for translators for each of the routes in the MDN Documentation. The resulting `.json` file can be used for analytics and to evaluate the state of the translation of the MDN Documentation.

A delay of 10 seconds was introduced between requests to prevent overloading the servers. You can change this parameter to make the process faster or more gentle to the server.

**Caution!** Screen Scraping can have an impact on the website's performance if too many requests are made in a short period of time. We're here to help, not to break the thing. Use it responsibly.

To run it, clone the repository, install all the dependencies, run `mdnCrawl.js`and get yourself a coffee.

See `routes.json` for an example of an output file.

Feel free to clone it, improve it and notify any issue you find.
