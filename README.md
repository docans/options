# Options
Drupal Module to do options data research

The purpose of this module is to 
1. Make an API call
2. Get a JSON response 
3. Loop through that JSON data To retrieve specific data 
4. Use the data retrieved to perform calculations
5. present the results To the user.

The goal of this module is to do an API connection to TD Ameritrade website, Where it will pull the videos option chain according to the selected strategy

This is achieved in five steps

App Workflow 
# Step One
this is the stage at which you receive input data from the user specifically about the type of strategy to research, the stock or to Ticker symbol, And any other inputs needed to do the research.

# Step Two
Next step is to make an API Request which will authenticate the Request and then provide a token which can be used for Authentication

# Step Three
after the authentication token has been generated we will then use the Token to perform an API request And the result of the request will be stored aS JSON DATA which will be used for further calculation

# Step Four
according to the preselected trading strategy and ticker symbol, we will then perform various calculation and analysis based on the results obtained from the JSON data and outsput out a table which would be used to determine which stock provides a better strategy over another

# Step Five
after the Research result has been presented in a tabular format there is a option to either save the research or discarded it

To be able to achieve this, we will pull data from TD Ameritrade API. To pull data from TD Ameritrade API we need to first of all authenticate, secondly we need to generate an access token, then we will use our access talking to create a request.
TD Ameritrade does not have a detailed documentation on how to get the process done, but the links below are the few documentation provided.

We will therefore use the Limited documentation provided below And combine it with sample code from another API which is tradier

# TD AMERITRATDE Setup
Connecting to the TD ameritrade API - https://developer.tdameritrade.com/content/getting-started

# Authentication
Simple Auth for Local Apps - https://developer.tdameritrade.com/content/simple-auth-local-apps
Web Server Authentication (Node.js) - https://developer.tdameritrade.com/content/web-server-authentication-nodejs

# Token
Post Access Token - https://developer.tdameritrade.com/authentication/apis/post/token-0

# Option Chain
Get Option Chain - link https://developer.tdameritrade.com/option-chains/apis/get/marketdata/chains
Resource URL
https://api.tdameritrade.com/v1/marketdata/chains


# TRADIER Sample code
Get an option chain  - https://documentation.tradier.com/brokerage-api/markets/get-options-chains
  #PHP
```
<?php
// Version 7.2.17-0ubuntu0.18.04.1
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, 'https://api.tradier.com/v1/markets/options/chains?symbol=VXX&expiration=2019-05-17&greeks=true');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'GET');

$headers = array();
$headers[] = 'Authorization: Bearer <TOKEN>';
$headers[] = 'Accept: application/json';

curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);

$result = curl_exec($ch);
$http_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
if (curl_errno($ch)) {
    echo 'Error:' . curl_error($ch);
}
curl_close ($ch);
echo $http_code;
echo $result;
```

# NODE.JS
```
// Version 10.15.2    
const request = require('request');

request({
    method: 'get',
    url: 'https://api.tradier.com/v1/markets/options/chains',
    qs: {
       'symbol': 'VXX',
       'expiration': '2019-05-17',
       'greeks': 'true'
    },
    headers: {
      'Authorization': 'Bearer <TOKEN>',
      'Accept': 'application/json'
    }
  }, (error, response, body) => {
      console.log(response.statusCode);
      console.log(body);
  });
  ```

# Module Setup with HTTP client
In order to write this module we will need to use the Drupal::httpClient. 
Documentation on how to use Drupal::httpClient can be located at https://drupalize.me/blog/201512/speak-http-drupal-httpclient
Guzzle gitub at https://github.com/guzzle/guzzle
Guzzle Documentation is at http://docs.guzzlephp.org/en/latest/



