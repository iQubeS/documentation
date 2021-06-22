# **updateListItems.js**

?> This utility function makes it easier to use the [SPServices getListItemsJson function](http://sympmarc.github.io/SPServices/utilities/SPGetListItemsJson.html) in iQS 3/3.5. It allows you to simply list what columns you want from a list with no CAML view field nonsense and handles all the annoying stuff you have to do to fetch IQSAdvancedLookup fields. Another handy thing it does is provide you with column types and other useful metadata.

`updateListItems` accepts two parameters; options and a callback, both of which are required.

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