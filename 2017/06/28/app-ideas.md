# App Ideas
A list of app ideas from Treehouse and FreeCodeCamp.  

Also see [awesome-app-ideas](https://github.com/tastejs/awesome-app-ideas) from the TodoMVC guys.

## FreeCodeCamp

### JavaScript/jQuery

1. Random Quotes
   * Click a button to display a new quote.
   * Add a button to tweet the quote.
   * **TIP:** Use the Quotes on Design [API](https://quotesondesign.com/api-v4-0/).
   * **BONUS:** Use `setInterval` to show a new quote every few seconds.
2. Local Weather
   * Show the weather for your current location (`window.navigator.geolocation.getCurrentPosition()`)
   * Show an icon or background image depending on the weather conditions.
   * Add a button to toggle between Fahrenheit and Celsius.
   * **TIP:** Use the Apixu [API](https://www.apixu.com/) for an easy way; use Dark Sky [API](https://darksky.net/dev/) and their [Skycons](https://github.com/darkskyapp/skycons) for a better way.
   * **BONUS:** Add a clock.
   * **BONUS:** Show recent news headlines.
3. Wikipedia Reader
   * Search Wikipedia articles and display a list of results.
   * Add a button to show a random article.
   * **BONUS:** Get the article text from the API and display in the app.
4. Twitch Viewer
   * Show a list of Twitch streamers with online/offline status.
   * Make sure users who don't exist (or closed their accounts) are displayed differently.
   * **BONUS:** Use a responsive iframe to embed the video of the stream in your app.
5. Calculator
   * Add basic arithmetic operations (add, subtract, multiply, divide).
   * Be able to clear the screen.
   * Be able to chain operations together until the user presses the equals button.
   * **BONUS:** Add pi, square root, and exponent.
6. Pomodoro Timer
   * Be able to set work time and break time (default is 25 minutes work and 5 minutes break).
   * Display an alert when the timers go off.
   * Be able to reset the timers.
   * **BONUS:** Use system notifications (`Notification.requestPermission()`).
7. Tic Tac Toe
   * Play against the computer.
   * Reset the game automatically.
   * Be able to choose to play as either X or O.
   * **TIP:** Check out the official React [tutorial](https://facebook.github.io/react/tutorial/tutorial.html), which makes a Tic Tac Toe game.
   * **TIP:** Research the Minimax algorithm to create the computer opponent's logic.
   * **BONUS:** Display a winner screen.
   * **BONUS:** Be able to select to play against a human or computer.
8. Simon
   * Add an off/on toggle button.
   * Add start and restart buttons.
   * Be presented with a series of button presses.
   * Each time you input the correct series of presses, the same series is played back with an extra step.
   * Play a sound that corresponds to each button press.
   * Play a sound and display a visual notification when you get the series wrong.
   * Display the number of steps in the current series.
   * Be able to enable strict mode which restarts the game when you get a press wrong.
   * Win the game if you get 20 steps correct.
   * **TIP:** Use the CSS from this [pen](https://codepen.io/Em-Ant/pen/QbRyqq).

### React

1. Markdown Previewer
   * Be able to type Markdown in one panel and show the rendered output in another.
   * **BONUS:** Use a browser code editor like Code Mirror or Ace instead of a plain input field.
2. FreeCodeCamp Leaderboard
   * Show a table of the top 100 FreeCodeCamp users with columns for past 30 days and all time points.
   * Be able to toggle the list by either past 30 days or all time.
   * **BONUS:** Be able to sort the lists (by most points or fewest points).
   * **BONUS:** Add pagination (let the user determine how many results to display per page).
3. Recipe List
   * Display a list of recipe names.
   * Show the ingredients when click on a list item.
   * Be able to add new recipes.
   * Be able to delete recipes.
   * Use `window.localStorage` to persist recipes.
   * **TIP:** Use a modal for the recipe input form.
   * **BONUS:** Instead of 1 input field for all ingredients, be able to add each ingredient individually.
4. Game of Life
   * Generate the grid on load.
   * Add start, pause, and clear buttons.
   * Be able to add new cells by clicking squares on the grid.
   * Display how many generations have gone by.
   * **BONUS:** Be able to change the grid dimensions.
   * **BONUS:** By able to change the simulation speed.
5. Roguelike Dungeon Crawler
   * Have health, a level, and a weapon.
   * Be able to pick up health items and weapons.
   * All of the items and enemies are randomly spawned.
   * Most of the dungeon map is hidden.
   * Be able to move throughout the dungeon map.
   * Be able to battle enemies.
   * Win the game by beating the boss.

### D3

1. Bar Chart
   * Display US GDP by quarter over time.
   * Be able to mouseover a bar to see a tooltip of the exact amount and year.
2. Scatterplot Graph
   * Display performance over time visualized in a scatterplot.
   * Be able to mouseover plots and see a tooltip with additional details.
3. Heat Map
   * Display a heatmap with an X and Y axis.
   * Each cell is colored based on its relationship to other data.
   * Be able to mouseover a cell to display additional data.
4. Force-directed Graph
   * Show countries that share borders on a force-directed graph.
   * Each country's flag is on it's node.
5. Global Map
   * Show all meteorite landings across the globe.
   * The size of the circle on the map is based on the size of the meteorite.
   * Be able to mouse over circles to see additional information.

### Node

1. Timestamp API
   * Pass a string as a route parameter that is either a UNIX timestamp or a natual language date (e.g., January 1, 2016).
   * Return back the UNIX and natural language date as a JSON object.
   * If the string is invalid, return null (or a 400 - Bad Request error).
2. Request Header Parser API
   * Return a JSON object with the IP Address, language, and operating system of the request.
3. URL Shortener
   * Pass a URL and receive a shortened URL in a JSON response.
   * If the passed URL is invalid, return an error response instead.
   * Visiting the shortened URL redirects to the original link.
