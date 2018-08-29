# `stations.all([opt])` / `stops.all([opt])` / `regions.all([opt])`

Get **all** stations/stops/regions of the network.

## Input parameters

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

Returns a [`Readable`](https://nodejs.org/api/stream.html#stream_readable_streams) stream in object mode that emits [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) FPTF@1 objects.

## Example

```js
const module = require('fpti-module')

const stationStream = module.stations.all()
const stopStream = module.stops.all()
const regionStream = module.regions.all({moduleSpecificOption: 'value'})

stationStream.on('data', item => {
    // item is an FPTF station object
    console.log(item)
})

stopStream.on('data', item => {
    // item is an FPTF stop object
    console.log(item)
})

regionStream.on('data', item => {
    // item is an FPTF region object
    console.log(item)
})

console.log(module.stations.all.features) // all options
```
