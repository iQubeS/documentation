# **getListItems.js**

?> This utility function makes it easier to use the [SPServices getListItemsJson function](http://sympmarc.github.io/SPServices/utilities/SPGetListItemsJson.html) in iQS. It allows you to simply list what columns you want from a list with no CAML view field nonsense and handles all the annoying stuff you have to do to fetch IQSAdvancedLookup fields.

`getListItems` accepts two parameters; options and a callback, both of which are required.

## Options

An `object` with several parameters:

### webURL (optional)
- Type: `String`
- Default: `'/'`

The subsite the list belongs to. `'/'` is root. For example this could be '`/QHSE`'

### listName
- Type: `String`
- Default: none

Can be the internal name of the desired list or the GUID. Internal names do not always work, so GUID is recommended.

### CAMLQuery (optional)
- Type: `String`
- Default: none

If you want to specify any filtering via CAML. Makes for better performance and less cluttered JavaScript.

### CAMLQueryOptions
- Type: `String`
- Default: none

Seldomly used. Read SPServices docs for info.

### columns
- Type: `String[]`
- Default: columns in default view

An array of strings with internal names of all desired columns, except for IQSAdvancedLookup columns. For example `['Title', 'Personnel', 'Department']`.

### advancedLookupFields
- Type: `String[]`
- Default: none

Here you'll put the IQSAdvancedLookup columns. They are separated in their own array because the `getListItems` function does its ✨ magic ✨ on them so that SharePoint doesn't flip out.