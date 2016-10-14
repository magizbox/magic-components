# Magic Components: Semantic and Beautiful Web UI

**What is a magic component?**

A magic component is an web component with minimal dom

```
<div class="component-type" gid="google-spreadsheet-id"></div>
```

It will load data from google spreadsheet via *google-spreadsheet-id*.

![](http://i.imgur.com/72DEC8O.png)

Then render a beautiful UI

![](http://i.imgur.com/X9scMZ1.png)

The idea behind magic component is ["The Next Web" proposed by Tim Berners-Lee](https://www.ted.com/talks/tim_berners_lee_on_the_next_web?language=en)

## Story

Recently, I developed some web components, which is load data from google spreadsheet.

It has some advantages

*Simple and Secure*

With google spreadsheet, It allow me get rid of database and CRUD. I simply edit data via google docs UI and then publish it to the world, such as https://docs.google.com/spreadsheets/d/140x82v0b2qnuuuy2NVvKQTyEZtM5G1zhHYq3OU_LaiU/pubhtml

I write simple script to load data from spreadsheet via docs api

```
function getJSONFromGoogleSpreadsheet(spreadsheetID, callback){
  // author: Brother Rain
  // date  : Sep 2015
  
  // get json from Google Spreadsheet

  // dependencies: jquery
  // dependencies: underscore

  function convertItem(item){
      var result = {};
      var keys = _.keys(item);
      _.each(keys, function(key){
        if(_.contains(key, "$")){
           var realKey = key.split("$")[1];
           result[realKey] = item[key]["$t"];
        }  
      });
    return result;  
  }
  var spreadsheetURL = "https://spreadsheets.google.com/feeds/list/" + spreadsheetID + "/od6/public/values?alt=json";    
  $.getJSON(spreadsheetURL, function(data){ 
      var items = data.feed.entry;
      var items = _.map(items, convertItem);
      callback(items);
  });
};
```

*Sematic & Open*

Each component has component-type, so if a crawler crawl this site, It will read component-type and get data from spreadsheet. I kind of sematic web, right? Correct me if I am wrong? 

**This is still in progress and please don't hesitate to give me your opinion.**

## Components List

* [Video Component](#video-component)
* [Book Component](#book-component)
* [Course Component](#course-component)
* [Paper Component](#paper-component)
* [Benchmark Component](#benchmark-component)

## Showcase

### Video Component Example ([fork me](https://github.com/magizbox/magiz-c-video))

![](https://camo.githubusercontent.com/ca4dca90c449272a766b7b7720acccce4d465ced/687474703a2f2f692e696d6775722e636f6d2f785744314c78452e706e67)

### Book Component Example ([fork me](https://github.com/magizbox/magiz-c-book))

![](https://camo.githubusercontent.com/32594a65d967549f44cc12b5bcad2772c7267f17/687474703a2f2f692e696d6775722e636f6d2f69384c416639562e706e67)

### Course Component ([fork me](https://github.com/magizbox/magiz-c-course))

![](https://camo.githubusercontent.com/52ee4f14ce0eea2edbe8f8d4240e5749c8b33e3e/687474703a2f2f692e696d6775722e636f6d2f356e7733624f672e706e67)

### Paper Component ([fork me](https://github.com/magizbox/magiz-c-paper))

![](https://camo.githubusercontent.com/697466b7892ba72032feaef838835bc1a0854a89/687474703a2f2f692e696d6775722e636f6d2f6c7766475051452e706e67)

### Benchmark Component ([fork me](https://github.com/magizbox/magiz-c-benchmark))

![](https://camo.githubusercontent.com/6b19e193c994153fd4cf5997c29b57f3f490862c/687474703a2f2f692e696d6775722e636f6d2f6a37496342456c2e706e67)
)
