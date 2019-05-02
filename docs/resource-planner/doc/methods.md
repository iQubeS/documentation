# Methods

## Usage

The Resource Planner has two methods that can be very useful for paging and such.

To use them it's best to initialize the plugin as such:

```js
var planner = $('#planner').ResourcePlanner(options);
```

Then you can re-setup the planner with the methods. For example filtering the data with a button:

```js
$('#filter-button').on('click', function() {
    planner.set({
        data: filteredData
    });
    planner.restart();
});
```

This will change the data and update the view.

## set(options)
- Parameter: options(Type: `Object`)

Set the options of the planner. The view needs to be updated for this to do anything.

Example:
```js
planner.set({
    viewStart: dayjs('2019/05/01'),
    viewEnd: dayjs('2019/08/01')
});
planner.restart();
```

## restart()
- Parameters: None

Restarts/updates the view. Used mostly for updating the view after the options have been changed. Is used internally to resize the planner on window resizing.