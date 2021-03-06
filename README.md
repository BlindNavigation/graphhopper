# GraphHopper Route Planner

[![Build Status](https://secure.travis-ci.org/graphhopper/graphhopper.png?branch=master)](http://travis-ci.org/graphhopper/graphhopper)

GraphHopper is a fast and memory efficient Java road routing engine released under Apache License 2.0.
Per default it uses OpenStreetMap data but can import other data sources.

## GraphHopper for the Web

See GraphHopper in action on [GraphHopper Maps](https://graphhopper.com/maps)

[![GraphHopper Maps](https://karussell.files.wordpress.com/2014/12/graphhopper-maps-0-4-preview.png)](https://graphhopper.com/maps)

GraphHopper Maps uses the [Directions API for Business](https://graphhopper.com/#directions-api) under the hood, which provides 
a Routing API via GraphHopper, a Route Optimization API via [jsprit](http://jsprit.github.io/), a fast Matrix API
and an address search via [Photon](https://github.com/komoot/photon). Additionally the map tiles from various providers are used 
where the default is [Omniscale](http://omniscale.com/), and all is available for free, via encrypted connections and from German servers
for a nice and private route planning experience!


## GraphHopper for Mobile

There are subprojects to make GraphHopper working offline
on [Android](https://github.com/graphhopper/graphhopper/tree/master/android)
and [iOS](http://github.com/graphhopper/graphhopper-ios)

# Community

We have a prosper community and welcome everyone. Let us know your problems, use cases or just [say hello](https://discuss.graphhopper.com/). Please see our [community guidelines](https://graphhopper.com/agreements/cccoc.html).

## Get Started

To get started read through our documentation ([0.6](https://github.com/graphhopper/graphhopper/blob/0.6/docs/index.md), [unstable](https://github.com/graphhopper/graphhopper/blob/master/docs/index.md)). 

## Questions

All questions can go to our [forum](https://discuss.graphhopper.com/) where we also have subsections specicially for developers, mobiles usage (iOS&Android) and our map matching component. Another place to ask questions would be on [Stackoverflow](http://stackoverflow.com/questions/tagged/graphhopper) but please do NOT use our issue section. Create new issues ONLY if you are sure that this is a bug and see how to contribute in the next section.

## Contribute

Read through [how to contribute](.github/CONTRIBUTING.md)
like finding and fixing bugs and improving our documentation or translations!


# Technical Overview

GraphHopper supports several routing algorithms like 
<a href="https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm">Dijkstra</a> and 
<a href="https://en.wikipedia.org/wiki/A*_search_algorithm">A</a>`*` and its bidirectional variants. 
Furthermore it allows you to use 
<a href="https://en.wikipedia.org/wiki/Contraction_hierarchies">Contraction Hierarchies</a> (CH) very easily, we call this 
**speed mode** and in contrast to the speed mode we call everything without CH the
**flexibility mode**. BTW: This does not mean that the flexibility mode is *slow*.

The speed mode comes with much faster and lightweight (less RAM) responses and it does not use heuristics in its default settings.
The downsides are that the speed mode allows only pre-defined vehicle profiles (multiple possible in GraphHopper) and requires a time consuming and resource intense preparation. And implementing certain features are not possible or very complex compared to the flexibility mode. Since 0.4 you can use both modes at the same time. 
See [here](https://github.com/graphhopper/graphhopper/pull/631) for more details.

## License

We chose the Apache License to make it easy for you to embed GraphHopper in your products.
We suggest to contribute back your changes, as GraphHopper will evolves fast,
but of course this is not necessary.

## OpenStreetMap Support

OpenStreetMap is directly supported from GraphHopper. Without the amazing data from
OpenStreetMap GraphHopper wouldn't be possible at all.
Other map data will need a custom import procedure, see e.g. <a href="https://github.com/graphhopper/graphhopper/issues/277">Ordnance Survey</a>,
<a href="https://github.com/graphhopper/graphhopper/pull/616">Shapefile like ESRI</a> or <a href="https://github.com/knowname/morituri">Navteq</a>.

## Written in Java

GraphHopper is written in Java and runs on Linux, Mac OS X,
Windows, BSD, Solaris, Raspberry Pi,  Android, Blackberry and even iOS. Other 
environments which supports at least Java 5 will work too.

## Customizable

We've build the GraphHopper class which makes simple things easy and complex things like multi-modal routing possible. Still you can use the low level API of GraphHopper and you'll see that
it was created to allow fast and memory efficient use of the underlying datastructures and algorithms.

### Android / Blackberry

On Android and Blackberry (since 10.2.1) we provide an integration with Mapsforge which makes offline navigation one step closer.
Due to the usage of memory mapped files and Contraction Hierarchies
we avoid allocating too much memory which makes it possible to run Germany-wide queries with only 
32MB in a few seconds. We provide an Android studio project as well as the Maven-Android integration to be 
used in other IDEs.

### Web UI and API

With the web module we provide code to query GraphHopper over HTTP and decrease bandwidth usage as much as possible.
For that we use the polyline encoding from Google, the Ramer–Douglas–Peucker algorithm and a simple 
GZIP servlet filter.                 
On the client side we provide Java and JavaScript code (via Leaflet) to consume that service and 
visualize the routes.

### Desktop

GraphHopper also runs on the Desktop in a Java application without internet access.
E.g. you could use the rough user interface called MiniGraphUI provided in the tools module, see some
visualizations done with it [here](https://graphhopper.com/blog/2016/01/19/alternative-roads-to-rome/).
A fast and production ready map visualization for the Desktop can be easily implemented via mapsforge.

# Features

Here is a list of the more detailed features including a link to the documentation:

 * [Simple start for users](./docs/web/quickstart.md) - just Java necessary! [Simple start for developers](./docs/core/quickstart-from-source.md) due to Maven.
 * Works out of the box with OpenStreetMap (osm and pbf) but can be adapted to use your own data
 * OpenStreetMap integration: Takes care of the road type, the surface, barriers, access restrictions, ferries, [conditional access restrictions](https://github.com/graphhopper/graphhopper/pull/621), ...
 * GraphHopper is fast. And with the so called "Contraction Hierarchies" it can be even faster (enabled by default).
 * Memory efficient data structures, algorithms and [the low and high level API](./docs/core/low-level-api.md) is tuned towards ease of use and efficiency
 * Provides a simple [web API](./docs/web/api-doc.md) including JavaScript and Java clients
 * Offers turn instructions in more than 30 languages, contribute or improve [here](./docs/core/translations.md)
 * Displays and takes into account [elevation data](./docs/core/elevation.md) (per default disabled)
 * Can apply [real time changes to edge weights](https://graphhopper.com/blog/2015/04/08/visualize-and-handle-traffic-information-with-graphhopper-in-real-time-for-cologne-germany-koln/) (flexibility only)
 * Customized routing profiles per request (flexibility only)
 * Possibility to specify a '[heading parameter](./docs/core/routing.md)' for start, end and via points for navigation applications via `pass_through` or `favoredHeading` parameters (flexibility only)
 * [alternative routes](https://discuss.graphhopper.com/t/alternative-routes/424) (flexibility only)
 * [turn costs and restrictions](https://github.com/graphhopper/graphhopper/pull/55#issuecomment-31089096) (flexibility only)
 * multiple profiles and weightings (flexibility and speed mode since 0.5)
 * several pre-built routing profiles: car, bike, racingbike, mountain bike, foot, motorcycle
 * the core uses only a few dependencies (trove4j and slf4j)
 * scales from small indoor- to world-wide-sized graphs
 * [map matching component](https://github.com/graphhopper/map-matching) (flexibility only)
