# fpti-js

**FPTI-JS (_Friendly Public Transport Interface_)** describes a standardized API for public transportation client libraries in JavaScript. See **[the spec](#api)** and the [list of JS modules](modules.md).

**_Proposal, work in progress!_**

[![license](https://img.shields.io/github/license/juliuste/fpti-js.svg?style=flat)](license)
[![chat on gitter](https://badges.gitter.im/juliuste.svg)](https://gitter.im/juliuste)

## API

The purpose of this specification is to outline a standardized API for the *most common* features of public transportation libraries, such as *Journey planning*, *Departures/Arrivals* or *Station search*. While most libraries certainly don't cover all of the following features, the basic principle for modules complying to `fpti-js` is that **if a certain feature is available, it must be provided with the API described below**. Some modules may also include **additional functionalities** that are not covered within this specification, **as long as they don't use the reserved `fpti-js` method names**.

Furthermore, even for additional features that are not covered within the following spec, `fpti-js` modules **return data in the [Friendly Public Transport Format](https://github.com/public-transport/friendly-public-transport-format/) `v1.1.2` wherever possible**.

### Method overview

Method | Feature description | Returns
-------|---------------------|--------
[`stations([opt])` / `stops([opt])` / `regions([opt])`](docs/stations-stops-regions.md) | **All** stations/stops/regions of the network. | [`Readable`](https://nodejs.org/api/stream.html#stream_readable_streams) → [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`region`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region)
[`stations.search(query, [opt])` / `stops.search(query, [opt])` / `regions.search(query, [opt])`](docs/stations-stops-regions.search.md) | Search stations/stops/regions by *query*. | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) → [`[station]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`[stop]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`[region]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region)
[`stations.nearby(location, [opt])` / `stops.nearby(location, [opt])` / `regions.nearby(location, [opt])`](docs/stations-stops-regions.nearby.md) | Search stations/stops/regions by *location*. | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) → [`[station]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station) / [`[stop]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop) / [`[region]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#region)
[`journeys(origin, destination, [opt])`](docs/journeys.md) | Journeys between stations (or optionally other locations) | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) → [`[journey]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#journey)
[`stopovers(station, [opt])`](docs/stopovers.md) | Departures and arrivals at a given station (or optionally other location) | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) → [`[stopover]`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stopover)

<!--[`locations([opt])`](docs/locations) | **All** locations (stations, stops, POI, addresses) of the network. | [`Readable`](https://nodejs.org/api/stream.html#stream_readable_streams) -> [`location`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#location), [`station`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#station), [`stop`](https://github.com/public-transport/friendly-public-transport-format/blob/master/spec/readme.md#stop)
[`locations.search(query, [opt])`](docs/locations.search) | Search locations (stations, stops, POI, addresses) by *query*. | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) -> `[location, station, stop]`
[`locations.nearby(location, [opt])`](docs/locations.search) | Search locations (stations, stops, POI, addresses) by *location*. | [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) -> `[location, station, stop]`-->


## Contributing

We are looking forward to discuss & extend this format further! If you have a question or want to propose changes, visit [the issues page](https://github.com/juliuste/fpti-js/issues). Keep our [contributing guidelines in mind](contributing.md). Note that, by participating in this project, you commit to the [code of conduct](code-of-conduct.md).
