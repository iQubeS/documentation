# **updateListItems.js**

?> This script makes it easier to use th SPServicese [UpdateListItems](http://sympmarc.github.io/SPServices/core/web-services/Lists/UpdateListItems.html) and [AddAttachment](https://sympmarc.github.io/SPServices/core/web-services/Lists.html#:~:text=Introduced-,AddAttachment,-%5BwebURL%5D%2C%20listName%2C%20listItemID) in iQS 3/3.5.

## updateItem

Has three parameters, `option`, `success` and `error`.

##### Example usage
```js
 updateItem({
	webURL: '/',
	listName: 'Some List Name',
	id: 5,
	fields: [['Title', 'Fannar Freyr Kristinsson'], ['BirthDate', '1992/07/16']],
	attachments: someAttachments
}, function(id, response) {
	console.log(id, response);
}, function(errorResponse) {
	console.log(errorResponse);
});
```

### options

Type: `Object`

Has 5 properties:

##### webURL

- Type: `String`

Subsite URL where the list that contains the item you want to update is.

##### listName

- Type: `String`

Display name of the list that contains the item you want to update.

##### fields

- Type: Array of arrays containing key and value

The columns and values you want to set.

Example:
```js
fields: [['Title', 'Fannar Freyr Kristinsson'], ['BirthDate', '1992/07/16']]
```

##### attachments (optional)

- Type: `blob[]`

An array of [`blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) objects for attachments.

### success

Type: `Function`

Callback function. Has two parameters: ItemID and the server response.

Example:
```js
success: function(id, response) {
	console.log('Updated item ID: ' + id);
	console.log('Server response: ' + response);
}
```

### error

Type: `Function`

Error callback function. Has a single parameter: the server response.

Example:
```js
error: function(response) {
	console.log('Oh no! Something has gone terribly awry! 😢');
}
```

## createItem

Has three parameters, `option`, `success` and `error`.

##### Example usage
```js
 createItem({
	webURL: '/',
	listName: 'Some List Name',
	fields: [['Title', 'Fannar Freyr Kristinsson'], ['BirthDate', '1992/07/16']],
	attachments: someAttachments
}, function(id, response) {
	console.log(id, response);
}, function(errorResponse) {
	console.log(errorResponse);
});
```

### options

Type: `Object`

Has 4 properties:

##### webURL

- Type: `String`

Subsite URL where the list you want to create an item in is.

##### listName

- Type: `String`

Display name of the list you want the item to be added to.

##### fields

- Type: Array of arrays containing key and value

The columns and values you want to set.

Example:
```js
fields: [['Title', 'Fannar Freyr Kristinsson'], ['BirthDate', '1992/07/16']]
```

##### attachments (optional)

- Type: `Blob[]`

An array of [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) objects for attachments.

### success

Type: `Function`

Callback function. Has two parameters: ItemID and the server response.

Example:
```js
success: function(id, response) {
	console.log('Created item ID: ' + id);
	console.log('Server response: ' + response);
}
```

### error

Type: `Function`

Error callback function. Has a single parameter: the server response.

Example:
```js
error: function(response) {
	console.log('Oh no! Something has gone terribly awry! 😢');
}
```

## attachToItem

Attach a file to a list item.

##### Example usage
```js
 attachToItem(file, 5, { webURL: '/', listName: 'Some List' });
```

### file

Type: `Blob`

### id

Type: `Number`

### options

Type: `Object`

Has two parameters:

##### webURL

- Type: `String`

Subsite URL where the list that contains the item you want to attach a file to is.

##### listName

- Type: `String`

Display name of the list that contains the item you want attach a file to.