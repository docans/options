# Options
Drupal Module to do options data research

The purpose of this module is to have a module that will do a research on the options market to find trades that will be profitable.

The goal of this module is to do an API connection to TD Ameritrade website, Where it will pull the videos option chain according to the selected strategy

This is achieved in five steps

Step One
this is the stage at which you receive input data from the user specifically about the type of strategy to research, the stock or to Ticker symbol, And any other inputs needed to do the research.

step Two
Next step is to make an API Request which will authenticate the Request and then provide a token which can be used for Authentication

step Three
after the authentication token has been generated we will then use the Token to perform an API request And the result of the request will be stored aS JSON DATA which will be used for further calculation

Step For
according to the preselected trading strategy and ticker symbol, we will then perform various calculation and analysis based on the results obtained from the JSON data and outsput out a table which would be used to determine which stock provides a better strategy over another

Step Five
after the Research result has been presented in a tabular format there is a option to either save the research or discarded it

