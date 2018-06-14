# **Dashboard Designer**

?> [The Dashboard Designer documentation](http://www.spchart.com/documentation) has some basic information about how to use it and a few articles with tips and tricks.

## Kendo UI Charts

The Dashboard Designer uses the Kendo UI framework for creating the charts. Therefore the documentation for that framework is applicable for customising the Dashboard Designer charts.

[An overview of the Kendo UI Charts](https://docs.telerik.com/kendo-ui/controls/charts/overview "Kendo UI Charts Overview")

[Kendo UI Charts documentation](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/chart "Kendo UI Charts documentation")

## Drilldowns

Drilling down to a list by clicking elements in a chart is done by using the same way Sharepoint filters lists; by using the `hash` of the `url`.

Here's a function for setting the filter for one or more columns:

```js
// filter is an array of objects with key pair values 'field' and 'value'
function setHashFilter(filter) {
    var wpid = window.ctx.clvp.wpid;
    var filterPrefix = 'InplviewHash' + wpid + '=';   
    var filterString = '';
    $.each(filter, function (index, item) {
        if (typeof item.value === 'string') item.value = item.value.replace(/-/g, '%2D');
        var filterField = 'FilterField' + (index + 1) + '=' + item.field;
        var filterValue = 'FilterValue' + (index + 1) + '=' + item.value;
        filterString += filterField + '-' + filterValue + '-';
    });
    window.location.hash = filterPrefix + encodeURIComponent(filterString);
}
```
Here's an example of how it's used in Dashboard Designer to filter on the department clicked and the current year:

?> The following code snippet is inside the `preRender()` function in `Dashboard > Advanced`. The `setHashFilter` function can either be put inside that tab or in a content editor or script editor on the webpart page.

```js
var filtrationApplied = false;

config.seriesClick = function (e) {
    setHashFilter([
        { 
            field: 'Department',
            value: e.category
        },
        {
            field: 'Year',
            value: new Date().getFullYear()
        }
    ]);
    filtrationApplied = true;
}

// Clear the filter when clicked outside chart elements
config.plotAreaClick = function (e) {
    if (!filtrationApplied) {
        window.location.hash = '';
    }
    filtrationApplied = false;
}
```

## Color theme

The color theme for a chart can be changed in the *__Advanced tab__* in the *__Dashboard tab__* by setting the `config.seriesColors` to an `array` of [CSS colors](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

```js
var colors = [ 
    '#3498db', // Blue 
    '#e74c3c', // Red 
    '#f1c40f', // Yellow 
    '#28b463', // Green 
    '#2e4053', // Black 
    '#e67e22' // Orange 
]; 
 
config.seriesColors = colors; 
```

To set a certain series' color: 
 
```js
// Setting the 0th series color.
config.series[0].color = '#3498db'; 
```
 
To set a certain data item's color: 
 
 ```js
config.series[0].colorField = 'color'; 
config.series[0].data.color = '#f1c40f'; 
```