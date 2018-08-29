# `journeys(origin, destination, [opt])`

Journeys between stations (or optionally other locations).

## Input parameters

### `origin` and `destination`

[FPTF `station` objects or `id`s](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station). Modules might optionally also accept other FPTF object types like `region` or `stop`, however only journeys between `station`s will be supported by **every module**.

### `opt = {}`

`Required` options are supported by every module. For non-`required` options, the main FPTI principle still applies: If a certain feature/option is available, it must be provided as described below.

Note that modules might provide additional options as long as they don't use reserved option attributes.

Attribute | Description | Required | Value type | Default
----------|-------------|------------|------------|--------
`when` | Journey date, synonym to `departureAfter` | ✅ | [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/date) | `new Date()`
`results` | Max. number of results returned | ✅ | `Number` | `null`
`interval` | Results for how many minutes after / before `when` (depending on `whenRepresents`) | ✅ | `Number` | `null`
`transfers` | Max. number of transfers | ✅ | `Number` | `null`
`departureAfter` | List journeys with a departure (first leg) after this date, mutually exclusive with `arrivalBefore` | ✅ | [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/date) | `new Date()`
`arrivalBefore` | List journeys with an arrival (last leg) before this date, mutually exclusive with `departureAfter` | ❌ | [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/date) | `null`
`via` | Via station | ❌ | [`station` object or `id`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station)\* | `null`
`currency` | Currency for `journey.price` | ❌ | [ISO 4217 code](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) | `null`

\*Or other FPTF types, if the module supports it. Similar to [`origin` and `destination`](#origin-and-destination).

#### `features`

The `features` object would look like this for a module which only supports the required options:

```js
{
    when: 'Stopover date, synonym to `departureAfter`',
    results: 'Max. number of results returned',
    interval: 'Results for how many minutes after `when`',
    transfers: 'Max. number of transfers',
    departureAfter: 'List stopovers with a departure after this date'
    // additionalOption: 'description of this option'
}
```

## Output

Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) that resolves in an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/array) of [`journey` FPTF objects](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#journey).

## Example

```js
const module = require('fpti-module')

const origin = {
    type: 'station',
    id: '123456'
}
const destination = '234567' // station id

const journeys = module.journeys(origin, destination)
const journeysWithOptions = module.journeys(origin, destination, {
    when: new Date('2019-03-01T12:00+01:00'),
    whenRepresents: 'arrival',
    interval: 6*60, // 6 hours
    transfers: 0, // direct connections only
    via: {type: 'station', id: '345678'},
    currency: 'EUR'
})

journeys.then(data => {
    // data is an array of FPTF journey objects
    console.log(data)
})

console.log(module.journeys.features) // all options
```
