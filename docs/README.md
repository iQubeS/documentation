<!-- # **Style Guide**

Yo sup, don't make stuff look ugly pls thx

<div style="text-align: center; color: white; box-sizing: border-box; display: inline-flex; align-items: center; font-weight: bold; justify-content: center; width: 49.8%; height: 200px; border-radius: 2px; background-color: #ff4477">This is html</div>
<div style="text-align: center; color: white; box-sizing: border-box; display: inline-flex; align-items: center; font-weight: bold; justify-content: center; width: 49.8%; height: 200px; border-radius: 2px; background-color: #11ccff">and this is too</div>

!> use `!>` before a line to do this

?> use `?>` before a line to do this

> use `>` before a line to do this -->
# **Dashboard Designer**

?> [The Dashboard Designer documentation](http://www.spchart.com/documentation) has some basic information about how to use it and a few articles with tips and tricks.

## Kendo UI Charts

The Dashboard Designer uses the Kendo UI framework for creating the charts. Therefore the documentation on that site is applicable for customising the Dashboard Designer charts.

[An overview of the Kendo UI Charts](https://docs.telerik.com/kendo-ui/controls/charts/overview "Kendo UI Charts Overview")

[Kendo UI Charts documentation](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/chart "Kendo UI Charts documentation")

## Drilldowns

Drilling down to a list by clicking elements in a chart is done by using the same way Sharepoint filters lists; by using the `hash` of the `url`.

?> The following code snippet is inside the `preRender()` function in `Dashboard > Advanced`

```js
var filtrationApplied = false;

config.seriesClick = function (e) {
    var filter = 'FilterField1=Department-FilterValue1=' + e.category;
    var wpid = window.ctx.clvp.wpid;
    var inplviewHash = 'InplviewHash' + wpid + '=';
    window.location.hash = inplviewHash + encodeURIComponent(filter);
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

It's possible to have more `FilterField`s. Just put a `-` in between. For example:

```js
var filter = 'FilterField1=Department-FilterValue1=' + department
            + '-FilterField2=Customer-FilterValue2=' + customer;
```

* The `e` parameter of the functions are the event `object`s  and contain information about the event, such as the value or category of the clicked `element`. 

* `wpid` is the webpart ID of the listview webpart. It is stored in the `window` `object`.

* `encodeURIComponent()` encodes UTF-8 characters. [encodeURIComponent on MDN web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

## Styling

### Color theme

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

### Gridline colors

I like making the gridlines a bit lighter.

```js
config.valueAxis.majorGridLines.color = '#eaeaea';
```

# **SPForms**

## Tooltips

Tooltips using the [jQuery tooltip plugin](https://jqueryui.com/tooltip/).

Set up a tooltip in the HTML:

```html
<div id="id" class="tooltip" title="title">
	<span class="ui-icon ui-icon-help"></span>
</div>
```

A nice base style for a tooltip:

```css
.tooltip {
	background-color: #e5e5e5;
	user-select: none;
	border-radius: 50%;
	float: left;
}

.tooltip > span {
	user-select: none;
}

.ui-tooltip {
	border: none;
	border-radius: 2px;
	box-shadow: 1px 1px 5px 1px rgba(0, 0, 0, 0.2);
	padding: .5rem;
}
```

Initialize the tooltip like this:

```js
$(function () {
    $('#id').tooltip({
        content: '<h1>Whatever HTML in here</h1>,
        position: {
            my: 'left center',
            at: 'right center'
        },
        show: { duration: 100 },
        hide: { duration: 100 }
    });
});
```

# **Sharepoint ( ͡° ͜ʖ ͡°)**

## Setting up theme for new site

* Open `styles/custom.css` and replace the primary and/r secondary color codes.

* Replace `images/logo.png` with said companies logo.

* Replace iQubeS logo on `settings/iQubeSImages/QHSE.png` with said companies logo

* Replace slideshow images in `settings/RollingPictures`. Changing number of pictures is done on master page.


## Testing

And some random JavaScript `codaroni` for the road:

?> **Tip:** You can hover of the top right corner and click to copy a code snippet.

```js
function functionName(parameter) {
    return parameter + ' is the parameter that I used.';
}

console.log(functionName('Sample parameter'));
```
