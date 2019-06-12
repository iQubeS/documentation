# **getListItems.js**

?> This utility function makes it easier to use the [SPServices getListItemsJson function](http://sympmarc.github.io/SPServices/utilities/SPGetListItemsJson.html) in iQS. It allows you to simply list what columns you want from a list with no CAML view field nonsense and handles all the annoying stuff you have to do to fetch IQSAdvancedLookup fields.

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

Can be the internal name of the desired list or the GUID. Internal names do not always work, so GUID is recommended.

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
getListItems({ listName: 'Companies' }, function(data) {
    console.log(data);
});
```

A more complex example:

```js
var someListGUID = '45DE91DA-A897-41CF-B657-18B3315A5BAD';
var options = {
    webURL: '/SomeSubsite',
    listName: someListGUID,
    CAMLQuery: '<Query><Where><Eq><FieldRef Name="SomeField"/><Value Type="Choice">SomeChoice</Value></Eq></Where></Query>',
    columns: ['Title', 'SomeField'],
    advancedLookupFields: ['SomeAdvancedLookupField']
};

getListItems(options, setupChart);

function setupChart(data) {
    /* Setup some chart with the data */
}

```