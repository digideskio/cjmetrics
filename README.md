# cjmetrics
This is a wrapper for Chartbeat and SiteCatalyst analytics for Courier-Journal offsite pages. This single script is designed to provide everything needed for analytics tracking on offsite pages with an emphasis on speed, efficiency, and most importantly a *minimal amount of setup*. The script contains the most recent implementations of Adobe's App Measurement plugin and Chartbeat's bootstrap code.

# Setup
When you open the script the very first variable you run into is an object called `options`. This is the base configuration that's used whenever the script is first run. You can change any of the values in this to be the default. If you are a Gannett property but not the Courier-Journal and are looking to customize this for your needs, replace anything beginning with `gpaper` to your own SC siteID as well as replacing any instance of `courier-journal.com` with your own domain. The name of the function as well as the filename can easily be changed to something besides `cjmetrics` if you wish. Once you change the options variable, save the .js file on a common server and simply call to it on each page you need analytics.

Installation on any page is as simple as adding the following lines of code at the bottom of the html:
```HTML
<script src="{YOUR-PATH}/cjmetrics.js"></script>
<script>cjmetrics();</script>
```


# How it works
When the script is inialized by calling `cjmetrics()` it goes through a couple of steps:

  * set the default the default values in the `options` variable 
  * check for the pagename by searching for specific tags in the page and going on to the next one if it doesn't exist
  * check for the author by searching for specific tags in the page and going on to the next one if it doesn't exist
  * overwriting any of the base options with custom options *if* they are specified
  * calling the respective SC and CB plugins and passing this data into them
  


# The good stuff - recipes
Any of the default options can be overridden by passing in new values when you call `cjmetrics()`. SiteCatalyst values are prefixed with `sc_`, chartbeat is prefixed with `cb_` and generic values that can be used by both have no prefixes. All of the available options can be seen by simply looking at the `options` object.

**Set a custom pagename and author for the page**
```javascript
cjmetrics({
    'pagename': 'My custom page name',
    'author': 'John Doe'
});
```
**Set a custom pagename and change prop17 and 18 which is the section and sub-section of the SSTS**
```javascript
cjmetrics({
    'pagename': 'My custom page name',
    'sc_prop17': 'Interactives',
    'sc_prop18': 'Sports'
});
```

**Use default SiteCatalyst values and disable chartbeat completely**
```javascript
cjmetrics({
    'cb_enable': false
});
```

**Disable SiteCatalyst, pass a custom SSTS and pagename into chartbeat**
```javascript
cjmetrics({
    'sc_enable': false,
    'cb_sections': 'Interactives/Sports/Longform/Football',
    'pagename': 'My custom page name'
});
```

