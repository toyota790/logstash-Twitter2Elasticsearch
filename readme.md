###Big Data Analytics - Assignment 1 : Data Collection and Persistence
This project is the first assignment of Big Data Analytics course in NTUST CSIE department. 

* Name: 羅智晟
* Student ID: M10415010

#Using the Logstash to get data from Twitter, and output to Elasticseach and JSON file


This project is using the Logstash to get data from Twitter. It tracks the Twitter Streaming API for keywords and directly indexes the documents in Elasticsearch and output the JSON file at the same time.


##Data Source
The data source is from the [Twitter Streaming API.](https://dev.twitter.com/streaming/overview)

##Topic
The topic is [Panama Papers](https://en.wikipedia.org/wiki/Panama_Papers).

##Search Keywords
<ol>
	<li>"#panamapapers"</li>
	<li>"panamapapers"</li>
	<li>"panama paper"</li>
	<li>"the panama paper"</li>
</ol>

##Data Format
The data set is using the JSON format.

##Dataset Size
The total data size is 2.1 GB.

##JSON Schema

|     Field     |    Type    |             Description                     |
| ------------- | :--------- | :----------------------------------------   
|  created\_at   |   String   | UTC time when this Tweet was created.       | 
|      id       |   Int64    | The integer representation of the unique identifier for this Tweet. |
|     id\_str    |   String   | The string representation of the unique identifier for this Tweet.|
|     text      |   String   | The actual UTF-8 text of the status update. |
|  source  |  String  | Utility used to post the Tweet, as an HTML-formatted string. Tweets from the Twitter website have a source value of web.|
|   truncated   |   Boolean  | Indicates whether the value of the text parameter was truncated.|
| in\_reply\_to\_status\_id  |  Int64 |  Nullable. If the represented Tweet is a reply, this field will contain the integer representation of the original Tweet’s ID.        | 
| in\_reply\_to\_status\_id\_str |  String  |  Nullable. If the represented Tweet is a reply, this field will contain the string representation of the original Tweet’s ID.   |
|  in\_reply\_to\_user\_id  |  Int64  | Nullable. If the represented Tweet is a reply, this field will contain the integer representation of the original Tweet’s author ID. |
| in\_reply\_to\_user\_id\_str  |  String  |  Nullable. If the represented Tweet is a reply, this field will contain the string representation of the original Tweet’s author ID. |
|  in\_reply\_to\_screen\_name  |  String  | Nullable. If the represented Tweet is a reply, this field will contain the screen name of the original Tweet’s author. |
| user  | Users |  The user who posted this Tweet. [More details.](https://dev.twitter.com/overview/api/users)|
|  geo  | Object | **Deprecated.** Nullable. Use the “coordinates” field instead. |
| coordinates |  Coordinates  | Nullable. Represents the geographic location of this Tweet as reported by the user or client application. [More details.](https://dev.twitter.com/overview/api/tweets#obj-coordinates)|
| place | Places  | Places	Nullable. When present, indicates that the tweet is associated (but not necessarily originating from) a Place. [More details.](https://dev.twitter.com/overview/api/places)|
| contributors | Collection of [Contributors](https://dev.twitter.com/overview/api/tweets#obj-contributors)  |  Nullable. An collection of brief user objects (usually only one) indicating users who contributed to the authorship of the tweet, on behalf of the official tweet author. |
| retweeted_status  |  [Tweet](https://dev.twitter.com/overview/api/tweets)  | Users can amplify the broadcast of tweets authored by other users by retweeting. Retweets can be distinguished from typical Tweets by the existence of a **retweeted_status** attribute. This attribute contains a representation of the original Tweet that was retweeted. |
| retweet_count | Int | Number of times this Tweet has been retweeted.|
| favorite_count | Integer | Nullable. Indicates approximately how many times this Tweet has been “liked” by Twitter users.|
| entities | Entities  | Entities which have been parsed out of the text of the Tweet. [More details.](https://dev.twitter.com/overview/api/entities)|
| favorited | Boolean  | Nullable. Perspectival. Indicates whether this Tweet has been liked by the authenticating user.|
| retweeted | Boolean | Perspectival. Indicates whether this Tweet has been retweeted by the authenticating user.|
| possibly_sensitive | Boolean  | Nullable. This field only surfaces when a tweet contains a link. The meaning of the field doesn’t pertain to the tweet content itself, but instead it is an indicator that the URL contained in the tweet may contain content or media identified as sensitive content.|
| filter_level | String |  Indicates the maximum value of the filter_level parameter which may be used and still stream this Tweet. So a value of medium will be streamed on none, low, and medium streams. |
| lang |  String  | Nullable. When present, indicates a [BCP 47](http://tools.ietf.org/html/bcp47) language identifier corresponding to the machine-detected language of the Tweet text, or “und” if no language could be detected. 

Reference from [Twitter Developer Document](https://dev.twitter.com/overview/api/tweets).


##Environment
*   [Logstash 2.3.1] (https://www.elastic.co/products/logstash)
*   [Elasticsearch 2.3.1] (https://www.elastic.co/products/elasticsearch)
*   JAVA Version 8 Update 77	

##Configuration

Required configuration options in "/crawler/twitter2elastic\_and\_json.conf" file:

	twitter {
	    consumer_key => ...
	    consumer_secret => ...
	    oauth_token => ...
	    oauth_token_secret => ...
	}

Set up the JSON output file path:
	
	output{
		file {
			codec => "json"
			path => ["JSON output file path"]
		}
	}



You need to create an application on Twitter, and paste the key on it. For more informations, you can follow the link:
[https://apps.twitter.com/app/new](https://apps.twitter.com/app/new)

##Running Command

	logstash -f twitter2elastic\_and\_json.conf
	
(Note: -f, it means that load the Logstash config from a specific file, directory. )