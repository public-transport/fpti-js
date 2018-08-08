# `stations([opt])` / `stops([opt])` / `regions([opt])`

Get **all** stations/stops/regions of the network.

## Input parameters

### `opt = {}`

There are currently no standardized options for this method. However, note that any `fpti-js` module might provide custom options as long as they don't use reserved option attributes.

## Output

Returns a [`Readable`](https://nodejs.org/api/stream.html#stream_readable_streams) stream in object mode that emits [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region) FPTF objects.

## Example

```js
const module = require('fpti-module')

const stationStream = module.stations()
const stopStream = module.stops()
const regionStream = module.regions({moduleSpecificOption: 'value'})

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
```
