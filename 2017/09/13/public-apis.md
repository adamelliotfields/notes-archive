# Public APIs
> A curated list of interesting and useful APIs.

Also check out:
 - [https://www.programmableweb.com](https://www.programmableweb.com)
 - [https://github.com/toddmotto/public-apis](https://github.com/toddmotto/public-apis)
 - [https://www.reddit.com/r/webdev/comments/3wrswc/what_are_some_fun_apis_to_play_with/](https://www.reddit.com/r/webdev/comments/3wrswc/what_are_some_fun_apis_to_play_with/)

## Contents
 - [Programming](#programming)
 - [Maps and Geolocation](#maps-and-geolocation)
 - [Weather](#weather)
 - [News](#news)
 - [Finance](#finance)
 - [Images](#images)
 - [Food](#food)
 - [Social](#social)
 - [Entertainment](#entertainment)
 - [Gaming](#gaming)
 - [Sports](#sports)
 - [Misc](#misc)

### Programming
[GitHub API](https://developer.github.com)
 - Searches GitHub users and repositories.

[NPM Registry](https://github.com/npm/registry/blob/master/docs/REGISTRY-API.md)
 - Searches the NPM Registry.

[Libraries.io](https://libraries.io/api)
 - Searches open source projects using a variety of package managers (e.g., NPM, Maven, Homebrew,
etc).

[Verse](https://verse.pawelad.xyz)
 - Gets the latest version for popular open source projects. Can also return the latest version from
GitHub releases.

[LetsValidate](https://github.com/letsvalidate/api)
 - Generates screenshots of websites and also returns a JSON list of the technologies used.
Screenshots are via headless Chrome; technologies are via Wappalyzer. Limited to 100 requests per
minute per IP.

### Maps and Geolocation
[Google Maps API](https://developers.google.com/maps)
 - Embed a Google Map, get street views images, get a static map image, and access Google Places
information.

[Google Geocoding API](https://developers.google.com/maps/documentation/geocoding/start)
 - Converts addresses into coordinates and coordinates into addresses.

[InfoIP](https://infoip.com)
 - Returns geographic information based on IP address. Useful if a user disables GPS in their
browser or mobile device. Note that IP addresses are not a reliable way to locate a user. Best case
scenerio is that your result will be in the same state; worst case scenerio is that your result will
be thousands of miles away.

### Weather
[Dark Sky API](https://darksky.net/dev)
 - The most accurate weather API. Powers Forecast.io and the Forecast Bar apps. Responses include an
ID that maps to an animated weather icon ([Skycon](http://darkskyapp.github.io/skycons/)).

[Apixu](https://www.apixu.com)
 - Alternative weather API that doesn't require any authentication.

### News
[News API](https://newsapi.org)
 - Get news articles from over 70 sources.

[The Guardian Open Platform](http://open-platform.theguardian.com)
 - Access all The Guardian content going back to 1999.

[New York Times Developer Network](https://developer.nytimes.com)
 - APIs for article archive (back to 1851), article search, newswire, books, movies, and more.

### Finance
[IEX Developer Platform](https://iextrading.com/developer)
 - Free stocket market data from the IEX Exchange via JSON or Socket.io. No authorization required.
Throttled to 100 requests per second (!).

[Alpha Vantage](https://www.alphavantage.co)
 - Another free stock market data API.

[Fixer.io](http://fixer.io)
 - Free ForEx rates and currency conversions.

### Images
[Unsplash API](https://unsplash.com/developers)
 - Search for photos by keyword, list new photos, and get random photos (useful for placeholder
images). The random photo API is `http://source.unsplash.com/random/<length>x<width>` (e.g.,
[http://source.unsplash.com/random/1920x1080](http://source.unsplash.com/random/1920x1080)).

[Giphy API](https://developers.giphy.com)
 - Access the GIPHY search, translate words or phrases into GIFs, pull trending GIFs, and get a
random GIF. Also supports search by emoji.

[Robohash](https://robohash.org)
 - Easily generate robotic avatar images based on any text input including IP or email addresses.

[Adorable Avatars](http://avatars.adorable.io)
 - Generates a random cartoon avatar on every request.

### Food
[Nutritionix API](https://www.nutritionix.com/business/api)
 - Get nutrition information for food (including branded food).

[Yummly API](https://developer.yummly.com)
 - Food and recipe data.

[Snooth Wine API](https://api.snooth.com)
 - Free access to the Snooth wine database. Search for wines by price, varietal, region. Get details
like price, reviews, winery information, and store availability.

[TheCocktailDB](http://www.thecocktaildb.com)
 - User-contributed database of cocktail recipes and images.

### Social
[Twitter API](https://dev.twitter.com/rest/public)
 - Access user information and search for tweets. Also offers a streaming API.

[StackExchange API](https://api.stackexchange.com/docs)
 - Search for questions, answers, comments, and posts (question + answers).

[Reddit API](https://www.reddit.com/dev/api)
 - Search Reddit.

[HackerNews API](https://github.com/HackerNews/API)
 - Simple API for accessing everything on HN. All stories and comments have a unique item ID. To get
the most recent item, use https://hacker-news.firebaseio.com/v0/maxitem.json. To access that item,
use https://hacker-news.firebaseio.com/v0/item/<item>.json. Also provides endpoints for new, top,
and best stories.

[FullContact API](https://www.fullcontact.com/developer)
 - Generates a complete social profile from a variety of social networks.

### Entertainment
[YouTube API](https://developers.google.com/youtube)
 - Search YouTube content and also embed a player in your web app.

[Spotify API](https://developer.spotify.com/web-api)
 - Search the Spotify catalog and also embed a player in your web app. The player requires the user
to be authenticated in order to play songs for more than 30 seconds.

[Twitch API](https://dev.twitch.tv)
 - Search Twitch for users, streamers, and games. Also embed a player and chat client into your web
app.

[Goodreads API](https://www.goodreads.com/api)
 - Access Goodreads data like user, author, and book titles.

[OMDb](http://www.omdbapi.com)
 - Search the Open Movie Database. Patrons ($1/mo) have access to movie posters.

[TMDb](https://www.themoviedb.org/documentation/api)
 - Database of movie and TV information.

[TheTVDB](https://api.thetvdb.com/swagger)
 - Database of TV show information.

[SWAPI](https://swapi.co)
 - All data from the Star Wars universe.

### Gaming
[Blizzard APIs](https://dev.battle.net)
 - Access player and game data for WoW, D3, and SC2. The WoW APIs include achievements, auctions,
bosses, leaderboards, items, mounts, pets, quests, recipes, spells, zones, PvP, and character/guild
stats.

[Hearthstone API](http://hearthstoneapi.com)
 - Up-to-date data from all cards in the game, including still and animated images.

### Sports
[MySportsFeeds](https://www.mysportsfeeds.com)
 - Free (for non-commercial use) sports schedules, scores, and stats.

### Misc
[Wikipedia](https://www.mediawiki.org/wiki/API:Main_page)
 - Search Wikipedia and get access to full article texts.

[Yelp](https://www.yelp.com/developers/documentation)
 - Find businesses by keyword, location, category, open status, price level, phone number, and food
delivery/pickup availability. Responses include business information, photos, Yelp rating, and up
to 3 review excerpts. 

[NASA](https://api.nasa.gov)
 - Access APOD (Astronomy Picture of the Day), NEOs (Near Earth Objects), EPIC (Earth Polychromatic
Imaging Camera), EONET (Earth Observatory Natural Event Tracker), Earth imagery (powered by Google
Earth), NASA images and videos, Mars Rover photos, and more.

[Wolfram Alpha](http://products.wolframalpha.com/api)
 - Access all capabilities of Wolfram Alpha. Responses can include screenshots of WA results, summary
boxes, and short text answers.

[Random User Generator](https://randomuser.me)
 - Generate random user data including avatars.

[MailTest](http://mailtest.in)
 - Validates email domains.

[mailboxlayer](https://mailboxlayer.com)
 - Validates email addresses. Free tier is only 250 requests per month.
