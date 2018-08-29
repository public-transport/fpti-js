# `stations.search(query, [opt])` / `stops.search(query, [opt])` / `regions.search(query, [opt])`

Search stations/stops/regions by *query*.

## Input parameters

### `query`

Non-empty `string`.

### `opt = {}`

`Required` options are supported by every module. For non-`required` options, the main FPTI principle still applies: If a certain feature/option is available, it must be provided as described below.

Note that modules might provide additional options as long as they don't use reserved option attributes.

Attribute | Description | Required\* | Value type | Default
----------|-------------|------------|------------|--------
`results` | Max. number of results returned | ✅ | `Number` | `null`

## Output

Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) that resolves in an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/array) of [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) FPTF objects.

## Example

```js
const module = require('fpti-module')

const matchingStations = module.stations.search('Paris Montparnasse')
const matchingStops = module.stops.search('Stadtmitte U2')
const matchingRegions = module.regions.search('Paris', {moduleSpecificOption: 'value'})

matchingStations.then(data => {
    // data is an array of FPTF station objects
    console.log(data)
})
```
