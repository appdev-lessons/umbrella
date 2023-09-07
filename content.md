# Umbrella

[Here is a video for this lesson](https://share.descript.com/view/7C8WxEg694l). You should not rely entirely on the video. PLEASE READ the below lesson as you are going through the steps, since there is much more detail in the text than in the video.

In this project, we'll write a Ruby program that uses the Google Maps API and Pirate Weather API to tell the user whether or not they should carry an umbrella with them when they leave home.

## Set up codespace

Since this project is not graded, you can [visit this link to fork the repository yourself](https://github.com/appdev-projects/umbrella/fork).

Once forked, set up a Codespace.

## Solution

There is a solution in the file called `possible_solution.rb`.

- You can run it to see how the program should behave:

    ```
    ruby possible_solution.rb
    ```
- Before it will work, you need to create two **environment variables** in your GitHub settings.
    - [Read how to create environment variables here.](https://learn.firstdraft.com/lessons/52-storing-credentials-securely)
    - You need to create env vars called `GMAPS_KEY` and `PIRATE_WEATHER_KEY`. You'll find the values to assign in the assignment in Canvas.
    - _Don't forget to restart your Codespace after the variables have been saved._
- Then, try running `possible_solution.rb` and enter some rainy locations — [you should be able to find some using this live radar](https://www.rainviewer.com/weather-radar-map-live.html).
- Don't peek at the solution until you've tried things yourself.

## Program outline

Here is a suggested outline for your program:

- Ask the user for their location. (Recall `gets`.)
- Get and store the user's location.
- Get the user's latitude and longitude from the Google Maps API.
- Get the weather at the user's coordinates from the Pirate Weather API.
- Display the current temperature and summary of the weather for the next hour.

If you get that far, then stretch further:

- For each of the next twelve hours, check if the precipitation probability is greater than 10%.
    - If so, print a message saying how many hours from now and what the precipitation probability is.
- If any of the next twelve hours has a precipitation probability greater than 10%, print "You might want to carry an umbrella!"

    If not, print "You probably won't need an umbrella today."

## Useful links

Some handy links:

 - [Hoppscotch](https://hoppscotch.io/): a great, free, online tool that makes it easy to experiment with API calls and see the JSON reponses nicely formatted.

### Pirate Weather links

 - [Pirate Weather forecast at the Merchandise Mart for humans](https://merrysky.net/forecast/merchandise%20mart/us)
 - Pirate Weather forecast at the Merchandise Mart for machines:
 
```
https://api.pirateweather.net/forecast/REPLACE_THIS_PATH_SEGMENT_WITH_YOUR_API_TOKEN/41.8887,-87.6355
```

  **You'll need an access token to view this page. Find it in the assignment on Canvas.**
 - [Pirate Weather API docs](https://docs.pirateweather.net/en/latest/Specification/)
 
### Google Maps links

 - [Map of Merchandise Mart for humans](https://goo.gl/maps/2mXdvBnHSGuMq98m6)
 - Map of Merchandise Mart for machines:

```
https://maps.googleapis.com/maps/api/geocode/json?address=Merchandise%20Mart%20Chicago&key=REPLACE_THIS_QUERY_STRING_PARAMETER_WITH_YOUR_API_TOKEN
```

  **You'll need an access token to view this page. Find it in the assignment on Canvas.**
 - [Google Geocoding API docs](https://developers.google.com/maps/documentation/geocoding/start)

## Useful methods

Most of working with APIs boils down to working with [`Array`s](https://learn.firstdraft.com/lessons/73-ruby-intro-array) and [`Hash`es](https://learn.firstdraft.com/lessons/77-ruby-intro-hash).

You will likely also need to use:

- [`if` statements](https://learn.firstdraft.com/lessons/74-ruby-intro-conditionals) 
- [loops](https://learn.firstdraft.com/lessons/75-ruby-intro-loops)
- [Array#each](https://learn.firstdraft.com/lessons/76-ruby-intro-each)

Most useful programs do.

Here are some less familiar methods that will be useful:

- `HTTP.get()`: The argument to `HTTP.get()` should be a `String` containing a URL. The method will then read the page at the provided URL and return it as an `HTTP::Response`.
    - In order to use this method, we must include the `gem "http"` in our `Gemfile`, `bundle install`, and `require "http"`.
- `HTTP::Response#to_s`: If you call `.to_s` on an instance of `HTTP::Response`, it will return the body of the response as a `String`.
- `JSON.parse()`: The argument to `JSON.parse` should be a `String` containing valid JSON. The method will transform the JSON objects into Ruby objects.
    - In order to use this method, we must `require "json"`.
- `Time.at()`: The argument to `Time.at` should be an `Integer` representing the [Epoch time](https://en.wikipedia.org/wiki/Unix_time). The method will transform the `Integer` into an instance of `Time`.

    You could also try [this online epoch time converter](https://www.epochconverter.com/).
- You can use [a `Range`](https://www.rubyguides.com/2016/06/ruby-ranges-how-do-they-work/) along with the `[]` method to access a specific set of elements within an `Array`:

    ```ruby
    array = [8, 3, 1, 19, 23, 3]

    pp array[2..4] # => [1, 19, 23]
    ```
    
## Stretch goal
  
Use [the ascii_charts gem](https://github.com/benlund/ascii_charts) to produce output that includes a chart, like this:
  
```
========================================
    Will you need an umbrella today?    
========================================

Where are you?
brooklyn
Checking the weather at Brooklyn....
Your coordinates are 40.6781784, -73.9441579.
It is currently 51.33°F.
Next hour: Possible light rain starting in 25 min.
 
Hours from now vs Precipitation probability
 
80|                                    
75| *                                  
70| *                                  
65| *                                  
60| *                                  
55| *                                  
50| *                                  
45| *                                  
40| *                                  
35| *                                  
30| *                                  
25| *                             *  * 
20| *                          *  *  * 
15| *              *  *  *  *  *  *  * 
10| *           *  *  *  *  *  *  *  * 
 5| *  *  *  *  *  *  *  *  *  *  *  * 
 0+-*--*--*--*--*--*--*--*--*--*--*--*-
    1  2  3  4  5  6  7  8  9 10 11 12 
 
You might want to take an umbrella!
```
