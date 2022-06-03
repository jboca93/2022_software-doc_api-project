# GetMyWeather API

## Contents

- [GetMyWeather API and the getWeather Method](#intro)
- [Get Started](#get-started)
  - [Register for an API Key](#key)
  - [Embed Initialization and Call Code](#embed)
- [Call getWeather API](#call)
  - [Parameters](#parameters)
  - [Sample getWeather API Call](#sample-call)
- [Understand Your API Return Package](#return)
  - [Return Values](#return-values)
  - [Sample Return Package](#sample-return)
- [Error Conditions](#errors)

<a id="intro"/>

## GetMyWeather API and the getWeather Method

Using GetMyWeather's API, **getWeather**, you can retrieve hyper-local weather data for your web applications or websites. For example, if you are developing a web application for outdoor adventurers, getWeather allows you to provide them with a weather forecast for a specific day, at a specific time and within a specific region. With your forecast, getWeather provides a *trust* value, a value that indicate's GetMyWeather's confidence in the accuracy of the forecast based on how far in the future or how large a region the user has specified.

getWeather is supported by all modern web browsers that support Javascript. You must enable Javascript to use getWeather.

<a id="get-started"/>

## Get Started

Before you can call weather data, you must register for an API key and embed the initialization and call code in your web application.

<a id="key"/>

### Register for an API Key

Visit [getmyweather.com](https://www.getmyweather.com) and select **Create an Account.** You may then use a credit card to pay for a subscription based on how many API calls you intend to make per day. If you intend to make less than 1,000 calls per day, you may sign up for a free account. You may also sign up for a free account for application development and testing.

Once you create an account, GetMyWeather will provide you with a unique API Key.

<a id="embed"/>

### Embed Initialization and Call Code

Embed the following Javascript samples in your web application to initialize and call getWeather. You must initialize getWeather once per session to establish a connection with the GetMyWeather server.

For information about the parameters within the call code, review [Call getWeather API](#call).

**Initialization Code**

```
<script type="text/javascript">
var weatherForecast;
function init() {
weatherForecast =
new getWeather(document.getElementById('forecast')}
</script>
```

<a id="call-code"/>

**Call Code**

```
<script async defer
src="https://www.getmyweather.com/getWeather?
key=<YOUR_KEY>&
callback=init&
location=<LATITUDE>:<LONGITUDE>&
specificity=<SPECIFICITY>&
time=<TIME>">
</script>
```

<a id="call"/>

## Call getWeather API

If you haven't already, embed the [call code](#call-code) into your web application or website.

<a id="parameters"/>

### Parameters

Parameter | Necessity | Description
-----|---------|------
**Location** | *required* | Indicate location using *latitude/longitude* in ISO 6709 format.
**Specificity** | *optional* | Define the area of the forecast as a circle around the *Location.* Indicate specificity as a *radius* in meters. Range: 10-10,000 meters. 
**Time** | *required* | Indicate time in hours from the current date and time (decimals will be accepted). For example, if a user submitted a forecast request at 1 p.m. today for the weather tomorrow at 3 p.m., the time would be 26 hours.
**Key** | *required* | Review [Register for an API Key](#key) to get your unique key.

<!--- For specificity, add note about what happens if you don't enter a value - what's getWeather's default? --->

Time necessary to call getWeather is negligible. You will not need a GUI indication that the application is waiting for a result.

<a id="sample-call"/>

### Sample getWeather API Call

The below represents a getWeather API call for a user wishing to receive a weather forecast for Schenley Park (a public park in Pittsburgh, Pennsylvania, United States) within a 1,000 meter radius on May 12, 2022 at noon. 

The user is requesting the forecast on May 10 at 10 a.m. ET. 

The developer's key is A341055662sse5g.

```
<script async defer
src="https://www.getmyweather.com/getWeather?
key=A341055662sse5g&
callback=init&
location=40.4367:79.9448&
specificity=1000&
time=50">
</script>
```

<a id="return"/>

## Understand Your API Return Package

getWeather delivers your weather data in JSON.

<a id="return-values"/>

### Return Values

Value | Description
-----|------
**temperature** | Indicated in degrees celcius.
**windspeed** | Indicated in kilometers per hour.
**chanceRain** | Indicated as a percentage.
**trust** | Represents GetMyWeather's confidence in the accuracy of the forecast. Trust is a value between 1 and 100, and can be interpreted as a percentage. 

**More on Trust**

Trust is dependent on the time and specificity paremeters included in the API call. The farther in the future the time, and/or the higher the specificity value, the lower the trust. For example, if a user requested a forecast for one month in advance for a radius of 10,000 meters within a location, getWeather would return a low trust value.

Forecasts greater than 240 hours (10 days) in the future are generally unreliable. 

If a user requests a forecast that is too far in the future or for too large a radius within a location, getWeather will return historical weather data with a low trust value.

<a id="sample-return"/>

### Sample Return Package

The below represents a return package indicating a forecast of 21 degrees celcius, 15 kilometer per hour winds and a 30% chance of rain. getWeather shares its trust, or confidence in this forecast as 80%.

```
<div class="forecast">
<div class="temperature">21</div>
<div class="windspeed">15</div>
<div class="chanceRain">30</div>
<div class="trust">80</div>
</div>
```

<a id="errors"/>

## Error Conditions

Error Message | Description and Resolution
-----------|--------------
**Invalid Key** | You entered your unique getWeather API key with an error. Review your key for accuracy in the [call code](#call-code).
**Invalid Paramater Format** | You entered a parameter using an incorrect format. Review the formatting requirements for [parameters](#parameters).
**Parameter Out of Range** | You entered a value that is outside the legal range of the given parameter. Review ranges for [parameters](#parameters).
**Server Unavailable** | getWeather is experiencing server issues, or your connection to the getWeather server was broken. Initialize getWeather again. If you receieve the same error, contact GetMyWeather for assistance.







