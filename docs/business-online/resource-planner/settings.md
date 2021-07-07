# Settings

The Resource Planner takes 1 object as a parameter on initialization, which is the settings. All the available settings and their defaults are listed here:

## container
- Type: DOM element
- Default: `document.querySelector('body')`

This is the element that the Resource Planner will be appended to. Ideally an empty div.

## data (required)
- Type: `Object[]`
- Default: `undefined`

This array of objects is for the tasks to be displayed. The tasks being the objects. The task schema is as follows:

```js
{
	title: 'Task title',
	resource: {
		name: 'John Smith',
		id: 1
	},
	startDate: new Date(), 
	endDate: dayjs().add(2, 'days'),
}
```

In the example above, the `startDate` is a JavaScript Date and the `endDate` is a dayjs object. This is just to show that internally the Resource Planner converts all dates to dayjs objects. So these date properties can be any kind of date that dayjs supports. (Check the [Parse chapter](https://day.js.org/docs/en/parse/now) in dayjs documentation for more information)

### Passing extra data to the task

You can pass as much data as you want with a task if you need, for example, some extra data to display in a tooltip. You do this by just adding properties to the task:
```js
{
	title: 'Task title',
	resource: {
		name: 'John Smith',
		id: 1
	},
	startDate: new Date(), 
	endDate: dayjs().add(2, 'days'),
	favoriteAnimal: 'cat'
	shoeSize: 42
}
```
This data can then be accessed with event handlers through the `task.data` property, like so:

```js
onTaskClick: task => {
	console.log(`${task.resource.name}'s favorite animal is a ${task.data.favoriteAnimal}`);
	console.log(`${task.resource.name}'s shoe size is ${task.data.shoeSize}`);
}
```

### Example
```js
data: [
	{
		title: 'John\'s task',
		resource: {
			name: 'John Smith',
			id: 1
		},
		startDate: new Date(), 
		endDate: dayjs().add(2, 'days'),
	},
	{
		title: 'Jane\'s task',
		resource: {
			name: 'Jane Smith',
			id: 2
		},
		startDate: dayjs().add(2, 'days'), 
		endDate: dayjs().add(7, 'days'),
	}
]
```
## filteredData (only used when using the `update` method)
- Type: `Object[]`
- Default: `undefined`

Used for filtering data.

## dataMapping
- Type: `Object`
- Default:
```js
dataMapping: {
		title: 'title',
		resource: 'resource',
		startDate: 'startDate',
		endDate: 'endDate',
		id: 'id'
	}
```
The dataMapping can be used to map your data to the task schema.

### Example
```js
dataMapping: {
		title: 'Title',
		resource: 'AssignedTo',
		startDate: 'Start',
		endDate: 'End',
		id: 'ID'
	}
```

### draggableHorizontal (not in use)
- Type: `Boolean`
- Default: `false`

(Since the Resource Planner on Business Online doesn't allow manipulating tasks at the moment, this is not used. The logic for it is still in there but might need to be updated if this is to be used)

Whether tasks should be draggable horizontally or not. Essentially moving the task backwards or forwards in the time.

### draggableVertical (not in use)
- Type: `Boolean`
- Default: `false`

(Since the Resource Planner on Business Online doesn't allow manipulating tasks at the moment, this is not used. The logic for it is still in there but might need to be updated if this is to be used)

Whether tasks should be draggable vertically or not. Essentially re-assigning tasks to other resources.

### overlap
- Type: `Boolean`
- Default: `true`

Whether multiple tasks with the same resource should be able to overlap each other.

### taskHeight
- Type: `Number`
- Default: `48`

Height of a task, or actually the height of a row. (Tasks are actually not as tall because of spacing)

### plannerHeight
- Type: `Number`
- Default: `800`

Height of the whole planner. This can of course be a calculated value based on the browser dimensions.

### viewStart
- Type: dayjs `object`
- Default: `dayjs()`

The start date of the timeline.

### viewEnd
- Type: dayjs `object`
- Default: `dayjs().add(1, 'months')`

The end date of the timeline.

### locale
- Type: `String`
- Default: `nb`

Locale for datepicker. `nb` is Norwegian Bokmål.

### toolbar
- Type: `String[]`
- Default: 
```js
toolbar: [
	'back',
	'forward',
	'daterangepicker',
	'zoomtofit',
]
```
What buttons to show in the toolbar and in what order. See documentation on toolbar for more information.

### palette
- Type: `String[]`
- Default: 
```js
palette: [
	'hsl(206, 81%, 58%)',
	'hsl(0, 75%, 60%)',
	'hsl(193, 8%, 27%)',
	'hsl(247, 80%, 74%)',
	'hsl(39, 100%, 65%)',
	'hsl(168, 75%, 46%)',
]
```

Color palette for tasks. Need to be CSS colors. Currently only the first and last colors are used (blue and red).

### taskClass
- Type: `String`
- Default: `undefined`

If you want to add a specific class to the tasks.

### customTaskRendering
- Type: `Function`
- Default: `undefined`

If you want to customize the rendering of tasks. This function needs to return valid HTML as a string. The function has 2 parameters: `task` and `numMonthsInView` (for having different levels of detail depending on zoom level).

