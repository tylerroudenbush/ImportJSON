# What is ImportJSON?
ImportJSON imports data from public JSON APIs into Google Spreadsheets. It aims to operate similarly to how the native Google Spreadsheet functions ImportData and ImportXML work.

# Functions & USage
The ImportJSON library contains four public functions:

- ImportJSON
Use to import a JSON feed from a URL.
- ImportJSONViaPost
Use to import a JSON feed from a URL using POST parameters.
- ImportJSONAdvanced
Use if you are a script developer and want to easily extend the functionality of this library.
- URLEncode
Use to URL encode a string to concatenate it to a URL.


## ImportJSON
Imports a JSON feed and returns the results to be inserted into a Google Spreadsheet. The JSON feed is flattened to create a two-dimensional array. The first row contains the headers, with each column header indicating the path to that data in the JSON feed. The remaining rows contain the data.

ImportJSON takes 3 parameters:

1. url: The URL to a JSON feed.
2. query: A comma-separated list of paths to import. Any path starting with one of these paths gets imported.
3. parseOptions: A comma-separated list of options that alter processing of the data.


By default, data gets transformed so it looks more like a normal data import. Specifically:

Data from parent JSON elements gets inherited to their child elements, so rows representing child elements contain the values of the rows representing their parent elements.
Values longer than 256 characters get truncated.
Headers have slashes converted to spaces, common prefixes removed and the resulting text converted to title case.
To change this behavior, pass in one of these values in the parseOptions parameter:

- noInherit: Don’t inherit values from parent elements
- noTruncate: Don’t truncate values
- rawHeaders: Don’t prettify headers
- noHeaders: Don’t include headers, only the data
- debugLocation: Prepend each value with the row & column it belongs in


### For example, to return all the number of shares and comments for the URL http://www.yahoo.com/ from the Facebook Graph API, you could use:

=ImportJSON(CONCATENATE("http://graph.facebook.com/", URLEncode("http://www.yahoo.com/")),  "", "")
If you wanted to get rid of the headers, you would add a “noHeaders” to the last parameter.

=ImportJSON(CONCATENATE("http://graph.facebook.com/", URLEncode("http://www.yahoo.com/")), "", "noHeaders")
As an advanced example, if you wanted to query YouTube for the most popular videos, but only see the data returned relating to the ‘title’ and the ‘content’, you could use:

=ImportJSON("http://gdata.youtube.com/feeds/api/standardfeeds/most_popular?v=2&alt=json", "/feed/entry/title,/feed/entry/content", "noInherit,noTruncate,rawHeaders")
The “rawHeaders” allows us to see the full path to each column of data in the spreadsheet.


## ImportJSONViaPost
Imports a JSON feed via a POST request and returns the results to be inserted into a Google Spreadsheet. This function works the same as ImportJSON, but allows you to specify a payload and fetch options to perform a POST request instead of a GET request.

To retrieve the JSON, a POST request is sent to the URL and the payload is passed as the content of the request using the content type “application/x-www-form-urlencoded”. If the fetchOptions define a value for “method”, “payload” or “contentType”, these values will take precedent. For example, advanced users can use this to make this function pass XML as the payload using a GET
request and a content type of “application/xml; charset=utf-8”.

ImportJSONViaPost takes 5 parameters:

- url: The URL to a JSON feed.
- payload: The content to pass with the POST request; usually a URL encoded list of name-value parameters separated by ampersands. Use the URLEncode function to URL encode parameters.
- fetchOptions: A comma-separated list of options used to retrieve the JSON feed from the URL.
- query: A comma-separated list of paths to import. Any path starting with one of these paths gets imported.
- parseOptions: A comma-separated list of options that alter processing of the data.
For more information on the available fetch options, see the documentation for UrlFetchApp. At this time the “headers” option is not supported.

For a list of the supported parseOptions and how to use queries, see ImportJSON.


## ImportJSONAdvanced
An advanced version of ImportJSON designed to be easily extended by a script. This version cannot be called from within a spreadsheet.

Imports a JSON feed and returns the results to be inserted into a Google Spreadsheet. The JSON feed is flattened to create a two-dimensional array. The first row contains the headers, with each column header indicating the path to that data in the JSON feed. The remaining rows contain the data.

ImportJSONAdvanced takes 6 parameters:

- url: The URL to a JSON feed.
- fetchOptions: An Object whose properties are the options used to retrieve the JSON feed from the URL.
- query: A comma-separated list of paths to import. Any path starting with one of these paths gets imported.
- parseOptions: A comma-separated list of options that alter processing of the data.
- includeFunc: A function with the signature func(query, path, options) that returns true if the data element at the given path should be included or false otherwise.
- transformFunc: A function with the signature func(data, row, column, options) where data is a 2-dimensional array of the data and row & column are the current row and column being processed. Any return value is ignored. Note that row 0 contains the headers for the data, so test for row==0 to process headers only.

The function returns a two-dimensional array containing the data, with the first row containing headers.

The fetchOptions can be used to change how the JSON feed is retrieved. For instance, the “method” and “payload” options can be set to pass a POST request with post parameters. For more information on the available parameters, see the documentation for UrlFetchApp. The fetchOptions must be an Object.

Use the include and transformation functions to determine what to include in the import and how to transform the data after it is imported.

### For example:

ImportJSON("http://gdata.youtube.com/feeds/api/standardfeeds/most_popular?v=2&alt=json",
          new Object() { "method" : "post", "payload" : "user=bob&apikey=xxxx" },
          "/feed/entry",
          "",
          function (query, path) { return path.indexOf(query) == 0; },
          function (data, row, column) { data[row][column] = data[row][column].toString().substr(0, 100); } )
In this example, the import function checks to see if the path to the data being imported starts with the query. The transform function takes the data and truncates it. For more robust versions of these functions, see the internal code of this library.


## URLEncode
Encodes the given value to use within a URL.

URLEncode takes 1 parameters:

- value: The value to be encoded.

The function returns the given value encoded using the URL encoding scheme.

### For instance:

=URLEncode("Value with spaces")
Returns the value “Value%20with%20spaces”.

You can use the URLEncode function to create URL (GET) and POST parameters by combining it with the CONCATENATE function. For instance:

=CONCATENATE("param1=", URLEncode("Value 1"), "&", "param2=", URLEncode("Value 2"))
Would be encoded as “param1=Value%20&param2=Value%20”. This could then be added to the query of a URL or passed as a payload in the ImportJSONViaPost function.
