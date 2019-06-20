# **getListItems.js**

?> This utility function makes it easier to use the [SPServices getListItemsJson function](http://sympmarc.github.io/SPServices/utilities/SPGetListItemsJson.html) in iQS 3/3.5. It allows you to simply list what columns you want from a list with no CAML view field nonsense and handles all the annoying stuff you have to do to fetch IQSAdvancedLookup fields.

`getListItems` accepts two parameters; options and a callback, both of which are required.

## Options

An `object` with several parameters:

#### webURL (optional)
- Type: `String`
- Default: `'/'`

The subsite the list belongs to. `'/'` is root. For example this could be `'/QHSE'`.

#### listName
- Type: `String`
- Default: none

This *can* be the name of a list, but the best practice would be to use the GUID like so:
```js
var COMPANIES_LIST_GUID = 'F613CF60-16C0-4362-A0B8-E1270669CB91';
getListsItems({ listName: COMPANIES_LIST_GUID }, function(data) {
    /* ... */
});
```
This is to improve readability of the code. All caps snake case used to denote a constant.

The GUID can be found in the URL of list settings. For example the Project General list on iqubes.signin.no:

`https://iqubes.signin.no/_layouts/15/listedit.aspx?List=%7BA79E4113-0149-422E-ADB7-ABA2D5ECE0F4%7D`

The GUID is `A79E4113-0149-422E-ADB7-ABA2D5ECE0F4`, the `%7B` and `%7D` are [URL encoded](https://en.wikipedia.org/wiki/Percent-encoding) `{` and `}`.

#### CAMLQuery (optional)
- Type: `String`
- Default: none

If you want to specify any filtering via CAML. Makes for better performance and less cluttered JavaScript.

#### CAMLQueryOptions (optional)
- Type: `String`
- Default: none

Seldomly used. Read SPServices docs for info.

#### columns (optional)
- Type: `String[]`
- Default: columns in default view

An array of strings with internal names of all desired columns, including IQSAdvancedLookup columns. For example `['Title', 'Personnel', 'Department']`.

#### advancedLookupFields (optional)
- Type: `String[]`
- Default: none

Here you need to specify which of the columns are IQSAdvancedLookup fields because the `getListItems` function does its ✨ magic ✨ on them so that SharePoint doesn't flip out.

## Callback

A callback function with one parameter, which is an array of the items fetched.

## Examples

Most basic example would be the following, which fetches the "Companies" list with default settings:

```js
var COMPANIES_LIST_GUID = 'F613CF60-16C0-4362-A0B8-E1270669CB91';
getListItems({ listName: COMPANIES_LIST_GUID }, function(data) {
    console.log(data);
});
```

A more complex example:

```js
var SOME_LIST_GUID = '45DE91DA-A897-41CF-B657-18B3315A5BAD';
var options = {
    webURL: '/SomeSubsite',
    listName: SOME_LIST_GUID,
    CAMLQuery: '<Query><Where><Eq><FieldRef Name="SomeField"/><Value Type="Choice">SomeChoice</Value></Eq></Where></Query>',
    columns: ['Title', 'SomeField', 'SomeAdvancedLookupField'],
    advancedLookupFields: ['SomeAdvancedLookupField']
};

getListItems(options, setupChart);

function setupChart(data) {
    /* Setup some chart with the data */
}

```