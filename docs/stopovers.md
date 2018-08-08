# `stopovers(station, [opt])`

Stopovers (departures and arrivals) at a given station (or optionally other location).

## Input parameters

### `station`

[FPTF `station` object or `id`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station). Modules might optionally also accept other FPTF object types like `location` or `stop`, however only stopovers at `station`s will be supported by **every module**.

### `opt = {}`

`Required` options are supported by every module. For non-`required` options, the main FPTI principle still applies: If a certain feature/option is available, it must be provided as described below.

Note that modules might provide additional options as long as they don't use reserved option attributes.

Attribute | Description | Required\* | Value type | Default
----------|-------------|------------|------------|--------
`when` | Stopover date | ✅ | [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/date) | `new Date()`
`results` | Max. number of results returned | ✅ | `Number` | `null`
`interval` | Results for how many minutes after `when` | ✅ | `Number` | `null`
`direction` | Only show departures heading to this station | ❌ | [`station` object or `id`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station)\* | `null`

\*Or other FPTF types, if the module supports it..

## Output

Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) that resolves in an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/array) of [`stopover` FPTF objects](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stopover).

## Example

```js
const module = require('fpti-module')

const station = {
    type: 'station',
    id: '123456'
}
const otherStation = '234567' // station id

const stopovers = module.stopovers(station)
const stopoversWithOptions = module.stopovers(otherStation, {
    when: new Date('2019-03-01T12:00+01:00'),
    interval: 6*60, // 6 hours
    direction: {type: 'station', id: '345678'}
})

stopovers.then(data => {
    // data is an array of FPTF stopover objects
    console.log(data)
})
```
