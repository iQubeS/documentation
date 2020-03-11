# **getListItems.js**

[Download getListItems.js version 2.21](https://iqubes.signin.no/Project_17-054538/SiteAssets/Releases/getListItems/getListItems.js)

?> This utility function makes it easier to use the [SPServices getListItemsJson function](http://sympmarc.github.io/SPServices/utilities/SPGetListItemsJson.html) in iQS 3/3.5. It allows you to simply list what columns you want from a list with no CAML view field nonsense and handles all the annoying stuff you have to do to fetch IQSAdvancedLookup fields. Another handy thing it does is provide you with column types and other useful metadata.

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

This should be the display name of the list.

### viewName (optional)
- Type: `String`
- Default: none

This should be the display name of the view.

#### CAMLQuery (optional)
- Type: `String`
- Default: none

If you want to specify any filtering with CAML. It's good to use this for any kind of filtering because it makes the request faster and declutters your code.

#### CAMLQueryOptions (optional)
- Type: `String`
- Default: none

Seldomly used. [Read Microsoft docs on queryOptions](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-services/ms774760(v=office.12)) for better info.

#### columns (optional)
- Type: `String[]`
- Default: columns in default view

An array of strings with internal names of all desired columns. 

For example 
```js
columns: ['Title', 'Personnel', 'Department'];
```

### getAllColumns (optional)
- Type: `Boolean`
- Default: false

If set to true, then the columns parameter will be ignored and all non-hidden and non-private columns of the list will be fetched.

## Callback

A callback function that provides 2 parameters:
### Data
An array of objects representing the list items.
### Fields
An object where the keys are the internal names of the list items and the values contain additional metadata for the fields, such as display name, whether it's mandatory, default value, as well as type-specific properties for example lookups have a source list and choice fields have a list of choices.

Example of what it looks like:

```js
{
	Title: {
		displayName: 'Company Name',
		internalName: 'Title',
		readOnly: false,
		required: true,
		type: 'Text'	
	}
}
```


## Examples

Most basic example would be the following, which fetches the "Companies" list with default settings:

```js
getListItems({
	webURL: '/', listName: 'Companies'
}, function(data, fields) {
  console.log(data, fields);
});
```

A more typical usecase example:

```js
var options = {
    webURL: '/SomeSubsite',
    listName: 'Some List',
    CAMLQuery: '<Query><Where><Eq><FieldRef Name="SomeField"/><Value Type="Choice">SomeChoice</Value></Eq></Where></Query>',
    columns: ['Title', 'SomeField'],
};

getListItems(options, setupSomeChart);

function setupSomeChart(data, fields) {
  /* Yay, now I can use item data in my chart 🎉 */
}

```

## Changelog
### Version 2.21: {docsify-ignore}
- `getView` renamed to `getListView` due to naming conflict with the quick search webpart.
### Version 2.20: {docsify-ignore}
- New boolean option: `getAllColumns`.
### Version 2.10: {docsify-ignore}
- Fields properties for MLT/Note fields.
- Code cleanup.
### Version 2.00: {docsify-ignore}
- Support for views via the `viewName` parameter.
- No longer a need to provide a list of IQSAdvancedLookupFields, it sorts that out on it's own.
- Fields info. It supplies the callback with another parameter `fields` which
	has internal name, display name and field type for each field in the list, as well
	as other properties that differ from column types. It's really helpful for creating custom forms, 
	i.e. choices and default choice for choice columns, source list and display fields for lookups.