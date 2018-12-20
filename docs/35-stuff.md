# Things to keep in mind
## Redundant scripts
Remove redundant references to javascript libraries e.g. jQuery and SPServices. These libraries are used by so many different webparts and scripts throughout iQS that they should just be referenced directly on the master pages themselves. There is no need to reference them inside different components.

For example: The current status of jQuery and SPServices on [iQS 3.5 projects](https://iqs35t.signin.no/Project_18-000130/SitePages/DefaultHome.aspx):

- **jQuery** is referenced 8 times and loaded 4 times (*4 of the requests return 404 because the files don't exist*)
	- v3.3.1 (*39KB*)
    - v1.7.1 (*41.8KB*)
    - v1.11.3 (*33.2KB*)
    - v1.12.4 (*87.1KB*)
    - **Total of 201.1KB (*162.1KB more than needed*)**
- **SPServices** is referenced 5 times and loaded 3 times (*2 of the requests return 404 because the files don't exist*)
    - V0.7.2 (*51.1KB*)
    - v2014.02 (*20.1KB*)
    - v2014.02 (*27.2KB*)
    - **Total of 98.4KB (*78.3KB more than needed*)**

## Minification
Minify scripts and stylesheets to reduce file sizes, which reduces download time, script parse time and bandwidth usage. This isn't really needed for very small scripts, but it's best to make sure to do this with bigger scripts and to use minified versions of dependencies such as jQuery, Fabric, Angular etc.

## CSS Scope
The best way to make sure that new CSS added to the site doesn't overwrite pre-existing default styles is to wrap the webpart/component in a div with some identifying class and specifying that class in all the CSS rule-sets. For example:

This would overwrite default styles for `ul` and `li` elements on the page:

```html
<ul>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
</ul>
<style>
ul {
    font-size: 16px;
}

li {
    text-decoration: none;
}
</style>
```

This would make sure the default styles won't be overwritten:
```html
<div class="custom-webpart">
    <ul>
        <li>List item 1</li>
        <li>List item 2</li>
        <li>List item 3</li>
    </ul>
</div>
<style>
.custom-webpart ul {
    font-size: 16px;
}

.custom-webpart li {
    text-decoration: none;
}
</style>
```