# `stations.nearby(location, [opt])` / `stops.nearby(location, [opt])` / `regions.nearby(location, [opt])`

Search stations/stops/regions by *location*.

## Input parameters

### `location`

[FPTF `location` object](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#location-objects).

### `opt = {}`

Note that any `fpti-js` module might provide custom options as long as they don't use reserved option attributes.

Attribute | Description | Required\* | Value type | Default
----------|-------------|------------|------------|--------
`distance` | Maximum distance in meters | ❌ | `number` | `null`

\*Required options are supported by every `fpti-js` module that provides this method.



## Output

Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) that resolves in an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/array) of [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) FPTF objects.

## Example

```js
const module = require('fpti-module')

const location = {
    type: 'location',
    longitude: 13.369,
    latitude: 52.525
}

const nearbyStations = module.stations.nearby(location)
const nearbyStops = module.stops.nearby(location, {distance: 1500}) // max. distance: 1.5km
const nearbyRegions = module.regions.nearby(location, {distance: 1000, moduleSpecificOption: 'value'})

nearbyStations.then(data => {
    // data is an array of FPTF station objects
    console.log(data)
})
```
