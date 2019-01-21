# Get started

## Basic setup

```js
$('#empty-div').ResourcePlanner({
  data: data,
  dataMapping: {
    title: 'title',
    resource: 'resource',
    startDate: 'startDate'
  }
});
```

The above snippet is the most basic setup for the Resource Planner, given that `data` is setup with the following schema:

```js
[
  {
    title: 'Some title',
    resource: 'Some resource',
    startDate: '2019/02/23',
  },
  ...
]
```