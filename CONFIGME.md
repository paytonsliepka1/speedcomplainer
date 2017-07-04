## Twitter app setup
This must be done before configuring the JSON file in the next step.
1. (Optional but recommended) Create a Twitter account to only be used to tweet at your Internet Service Provider (in this case, Charter Spectrum). You must have a phone number linked to this account. 2-Factor Authentication is not required, but I recommend using 2FA for all of your online accounts. Ex. @hatespectrumbot
2. Create a Twitter app at https://apps.twitter.com/app/new. You must have a Twitter account. If you created a second Twitter account for use with speedcomplainertwc, it's a good idea to log in with that same account to keep everything together.
3. Fill in the details of your new Twitter Developers app. 
    It's important to note that you can't use "speedcomplainer" or "speedcomplainertwc" as a name for your Twitter app. You must come up with something unique.
    The description for the Twitter app is "Hi, I'm a bot that tweets @AskSpectrum when my connected download speeds fall."
    The website for the Twitter app is paytonsliepka1.github.io/speedcomplainertwc
4. Click on "Create your Twitter application"
5. Details of your new app will be shown along with your consumer key and consumer secret.
6. Scroll down and click "Create my access token"
7. Details of your new Twitter app access tokens will be shown along with your consumer API key and consumer secret.
Keep this tab open! You'll need all of these strings when you go to configure the JSON file.

## Configuration
Configuration is handled by a basic JSON file. Things that can be configured are:
* twitter
 * twitterToken: This is your app access token
 * twitterConsumerKey: This is your Consumer Key (API Key)
 * twitterTokenSecret: This is your Access Token Secret
 * TwitterConsumerSecret: This is your Consumer Secret (API Secret)
* tweetTo: This is a account (or list of accounts) that will be @ mentioned (include the @!)
* internetSpeed: This is the speed (in MB/sec) you're paying for (and presumably not getting).
* tweetThresholds: This is a list of messages that will be tweeted when you hit a threshold of crappiness. Placeholders are:
 * {tweetTo} - The above tweetTo configuration.
 * {internetSpeed} - The above internetSpeed configuration.
 * {downloadResult} - The poor download speed you're getting

Threshold Example (remember to limit your messages to 140 characters or less!):
```
    "tweetThresholds": {
        "5": [
            "Hey {tweetTo} I'm paying for {internetSpeed}Mb/s but getting only {downloadResult} Mb/s?!? Shame.",
            "Oi! {tweetTo} $100+/month for {internetSpeed}Mbit/s and I only get {downloadResult} Mbit/s? How does that seem fair?"
        ],
        "12.5": [
            "Uhh {tweetTo} for $100+/month I expect better than {downloadResult}Mbit/s when I'm paying for {internetSpeed}Mbit/s. Fix your network!",
            "Hey {tweetTo} why am I only getting {downloadResult}Mb/s when I pay for {internetSpeed}Mb/s? $100+/month for this??"
        ],
        "25": [
            "Well {tweetTo} I guess {downloadResult}Mb/s is better than nothing, still not worth $100/mnth when I expect {internetSpeed}Mb/s"
        ]
    }
```

Logging can be done to CSV files, with a log file for ping results and speed test results. 

CSV Logging config example:
```
"log": {
    "type": "csv",
    "files": {
        "ping": "pingresults.csv",
        "speed": "speedrestuls.csv"
    }
}
```

## Usage
> python speedcomplainer.py

Or to run in the background:

> python speedcomplainer.py > /dev/null &
