# `stations.get([opt])` / `stops.get([opt])` / `regions.get([opt])`

Get details for a specific station/stop/region.

## Input parameters

### `station`/`stop`/`region`

FPTF@1 [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) `id` or object.

### `opt = {}`

There are currently no standardized options for this method. However, note that modules might provide additional options as long as they don't use reserved option attributes.

#### `features`

The `features` object would look like this for a module which only supports the required options:

```js
{
    // no required options for this method
    // additionalOption: 'description of this option'
}
```

## Output

Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) that resolves in a [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) FPTF@1 object **or rejects with an `FPTFObjectNotFound` error if no match was found**.

## Example

```js
const module = require('fpti-module')

const station = module.stations.get('stationId123')
const stop = module.stops.get({type: 'stop', id: 'stopId123'})
const region = module.regions.get('regionId123', {moduleSpecificOption: 'value'})

station
	.then(data => {
		// data is an FPTF station object
		console.log(data)
	})
	.catch(error => {
		// FPTFObjectNotFound if no matching object was found
		console.error(error)
	})

console.log(module.stations.get.features) // all options
```
