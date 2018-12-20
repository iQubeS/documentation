# Forms Designer

Get an array of values selected in a multi choice field.

```js
function getMultiChoiceValues(fieldName) {
    var selectedValues = [];
    $.each(fd.field(fieldName).value(), function(index, value) {
        var value = fd.field(fieldName).control()._el().find('input[type="checkbox"]').eq(value).next().text();
        selectedValues.push(value);
    });
    return selectedValues;
}
```