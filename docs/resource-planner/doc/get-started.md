# Get started

## Data

The minimum amount of data needed for each item is

- Title of the item
- Resource the item is tied to
- Start date of the item

End date can also be provided, and usually is. If it isn't it defaults to the same date as start date.

## Basic setup

Here's a basic setup for the Resource Planner. 

```js
$('#an-empty-div').ResourcePlanner({
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