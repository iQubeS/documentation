# Options

## data
- Type: `Array`
- Default: none

An `Array` of `Objects` that define the items in the Resource Planner. The values used are:

- title: `String` (Default: `''`)
    - For title of item *Optional*
    - This will, by default, be the text on the item itself. Can be omitted if the item has custom rendering.
- resource: `String`
    - Title of the resource responsible for the item.
    - Resources are the values on the y-axis of the grid. For example a bar or an oilrig.
- startDate: `Date`
    - Start date for the item (DayJS compliant)
- endDate: `Date` (Default: Same as `startDate`)
    - End date of the item (DayJS compliant) *Optional*
    - If omitted it will be set to the same date as the start date.

Any other properties can be included for custom functionality or custom rendering.

## dataMapping
- Type: `Object`
- Default: none

Properties can(and will almost certainly be needed) to be mapped to fit the item schema.

For example if you have a database of items where each item has this schema:

```js
{
    event: 'Some sales event',
    department: 'Sales',
    personResponsible: 'Arnold',
    numAttendees: 42
    startOfEvent: '2018/11/21',
    endOfEvent: '2018/11/23'
}
```

The `dataMapping` should be like this

```js
{
    title: 'event',
    resource: 'personResponsible',
    startDate: 'startOfEvent',
    endDate: 'endOfEvent'
}
```

Then the Resource Planner will see that item as this:

```js
{
    title: 'Some sales event',
    resource: 'Arnold',
    startDate: '2018/11/21',
    endDate: '2018/11/23'
    department: 'Sales'
    numAttendees: 42
}
```

## draggableHorizontal
- Type: `Boolean`
- Default: `true`

If true, then items can be moved horizontally in the grid, back and forth in the timeline within a resource's row.

## draggableVertical
- Type: `Boolean`
- Default: `true`

If true, then items can be moved vertically in the grid, between resource rows.

## resizable
- Type: `Boolean`
- Default: `true`

If true, then items can be resized horizontally.

## overlap
- Type: `Boolean`
- Default: `true`

If true, then items in the same row can overlap in the timeline. Row height is expanded to compensate.

## itemHeight
- Type: `Number`
- Default: `32`

The height of items in the grid in pixels.

## plannerHeight
- Type: `Number`
- Default: `500`

The height of the Resource Planner in pixels.

For a dynamic height, something like this can be done. `headerOffset` is used to offset the height incase there is a header/toplink bar.
```js
plannerHeight: window.innerHeight - $('#planner').position().top - headerOffset
```

## viewStart
- Type: `String` | `Number` | `Date` | `Dayjs`
- Default: `dayjs()` (today)

The first day of the month of the date chosen is the starting point of the timeline when initialized. Takes native Javascript Date objects, ISO 8601 strings and Unix timestamps(ms). See [DayJS documentation](https://github.com/iamkun/dayjs/blob/master/docs/en/API-reference.md#constructor-dayjsexisting-string--number--date--dayjs) for more info.


## verticalGridlines

- Type: `Boolean`
- Default: `true`

If true, displays vertical gridlines.

## palette
- Type: `Array`
- Default: `['#3d9fea', '#e54c4c', '#3f474a', '#fec04c', '#9487f1', '#1ad9b3']`

Array of CSS color values. These colors are equally distributed to resources. So items for each resource all have the same color.

## color
- Type: `String`
- Default: none

Background color of items. Has to be a CSS color. Can be dynamic by making it a function that returns a string. The function has 1 parameter that is the item. Example where items that have Dickens as a resource get colored orange, otherwise they keep their default color from the palette:
```js
color: function(item) {
    if (item.resource.title === 'Dickens') return 'orange';
    return item.color;
},
```

## customItemRendering
- Type: `Function`
- Default: none

This function takes 1 parameter: an Item instance. This should return a `String` with HTML.

Example: If the PSS data would look something like this:

```js
{
    allocatedResources: 1,
    requiredResources: 2,
    date: '2018-12-21T09:33:56.523Z',
    id: 42,
    resource: 'Dickens',
    department: 'Stavanger'
    // Probably more
}
```
The custom rendering might be defined like this:

```js
function(item) {
    var allocated = item.allocatedResources;
    var required = item.requiredResources;
    var title = allocated + '(' + required + ')';
    var allocationProgress = '';
    if (required > allocated && allocated !== 0) allocationProgress = 'allocation-not-full';
    if (required === allocated) allocationProgress = 'allocation-full';
    if (allocated === 0) allocationProgress = 'allocation-empty';
    return '<div class="item-content ' + allocationProgress + '" id="' + item.id + '">' + title + '</div>';
}
```

which would end up as this HTML:

```html
<div class="item">
    <div class="item-content allocation-not-full" id="42">1(2)</div>
</div>
```

the planner automatically wraps it in an `.item` container which is used for the grid logic of the planner. Everything inside that container can be customized and used in event handlers.

## customResourceRendering
- Type: `Function`
- Default: none

Same as `customItemRendering`, but a bit more restrained.

## onClick
- Type: `Function`
- Default: none
- Available parameters: item, id, event

Click event handler for items.

```js
onClick: function(item, id, event) {
    console.log(item); // Really useful for debugging
    doSomethingWithItem(item);
}
```

## onDoubleClick
- Type: `Function`
- Default: none
- Available parameters: item, id, event

Double click event handler for items.

## onGridDoubleClick
- Type: `Function`
- Default: none
- Available parameters: column, resourceId, resource, event

Double click event handler for grid.

## onMouseEnter
- Type: `Function`
- Default: none
- Available parameters: item, id, event

On mouse enter event handler for items.

## onMouseLeave
- Type: `Function`
- Default: none
- Available parameters: item, id, event

On mouse leave event handler for items.

## initializationDone
- Type: `Function`
- Default: none
- Available parameters: items (array of the items)