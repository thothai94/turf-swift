# Turf for Swift 
Turf for Swift is **experimental** and its public API is subject to change. Please use with care and open issues for any problems you see or missing features that should be added.

## Why have we forked

We wanted to upgrade the SDK from iOS 9.0 to 12.0.

## What have we changed

Upgrade iOS version from 9.0 to 12.0.

## Requirements 

Turf is written in Swift 4. It requires Xcode 9.x and supports the following minimum deployment targets:

* iOS 12.0 and above
* macOS 10.10.0 (Yosemite) and above
* tvOS 9.0 and above
* watchOS 2.0 and above

Alternatively, you can incorporate Turf into a command line tool without Xcode on any platform that [Swift](https://swift.org/download/) supports, including Linux.

If your project is written in Objective-C, you’ll need to write a compatibility layer between turf-swift and your Objective-C code. If your project is written in Objective-C++, you may be able to use [spatial-algorithms](https://github.com/mapbox/spatial-algorithms/) as an alternative to Turf.

## Installation

Although a stable release of this library is not yet available, prereleases are available for installation using any of the popular Swift dependency managers.

### CocoaPods

To install Turf using [CocoaPods](https://cocoapods.org/):

1. Specify the following dependency in your Podfile:
   ```rb
   pod 'Turf', '~> 0.2'
   ```
1. Run `pod repo update` if you haven’t lately.
1. Run `pod install` and open the resulting Xcode workspace.
1. Add `import Turf` to any Swift file in your application target.

### Carthage

To install Turf using [Carthage](https://github.com/Carthage/Carthage/):

1. Add the following dependency to your Cartfile:
   ```
   github "mapbox/turf-swift" ~> 0.2
   ```
1. Run `carthage bootstrap`.
1. Follow the rest of [Carthage’s integration instructions](https://github.com/Carthage/Carthage#adding-frameworks-to-an-application). Your application target’s Embedded Frameworks should include Turf.framework.
1. Add `import Turf` to any Swift file in your application target.

### Swift Package Manager

To install Turf using the [Swift Package Manager](https://swift.org/package-manager/), add the following package to the `dependencies` in your Package.swift file:

```swift
.Package(url: "https://github.com/mapbox/turf-swift.git", .upToNextMinor(from: "0.2"))
```

Then `import Turf` in any Swift file in your module.


## Available functionality

This work-in-progress port of [Turf.js](https://github.com/Turfjs/turf/) contains the following functionality:

Turf.js | Turf-swift
----|----
[turf-along](https://github.com/Turfjs/turf/tree/master/packages/turf-along/) | `LineString.coordinateFromStart(distance:)`
[turf-area](https://github.com/Turfjs/turf/blob/master/packages/turf-area/) | `Polygon.area`
[turf-boolean-point-in-polygon](https://github.com/Turfjs/turf/tree/master/packages/turf-boolean-point-in-polygon) | `Polygon.contains(point:ignoreBoundary:)`
[turf-destination](https://github.com/Turfjs/turf/tree/master/packages/turf-destination/) | `CLLocationCoordinate2D.coordinate(at:facing:)`<br>`RadianCoordinate2D.coordinate(at:facing:)`
[turf-distance](https://github.com/Turfjs/turf/tree/master/packages/turf-distance/) | `CLLocationCoordinate2D.distance(to:)`<br>`RadianCoordinate2D.distance(to:)`
[turf-helpers#polygon](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers/#polygon) | `Polygon(outerRing:innerRings:)`
[turf-helpers#lineString](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers/#linestring) | `LineString(_:)`
[turf-helpers#degreesToRadians](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers/#degreesToRadians) | `CLLocationDegrees.toRadians()`
[turf-helpers#radiansToDegrees](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers/#radiansToDegrees) | `CLLocationDegrees.toDegrees()`
[turf-helpers#convertLength](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers#convertlength)<br>[turf-helpers#convertArea](https://github.com/Turfjs/turf/tree/master/packages/turf-helpers#convertarea) | `Measurement.converted(to:)`
[turf-length](https://github.com/Turfjs/turf/tree/master/packages/turf-length/) | `LineString.distance(from:to:)`
[turf-line-intersect](https://github.com/Turfjs/turf/tree/master/packages/turf-line-intersect/) | `Turf.intersection(_:_:)`
[turf-line-slice](https://github.com/Turfjs/turf/tree/master/packages/turf-line-slice/) | `LineString.sliced(from:to:)`
[turf-line-slice-along](https://github.com/Turfjs/turf/tree/master/packages/turf-line-slice-along/) | `LineString.trimmed(from:distance:)`
[turf-nearest-point-on-line](https://github.com/Turfjs/turf/tree/master/packages/turf-nearest-point-on-line/) | `LineString.closestCoordinate(to:)`
— | `CLLocationCoordinate2D.direction(to:)`<br>`RadianCoordinate2D.direction(to:)`
— | `CLLocationDirection.difference(from:)`
— | `CLLocationDirection.wrap(min:max:)`


## GeoJSON

turf-swift also contains an experimental GeoJSON encoder/decoder with support for Codable.

```swift
// Decode unknown GeoJSON type
let geojson = try! GeoJSON.parse(data: data)

// Decode known GeoJSON type
let geojson = try! GeoJSON.parse(data: data, as: FeatureCollection.self)

// Initialize a PointFeature and encode as GeoJSON
let coordinate = CLLocationCoordinate2D(latitude: 0, longitude: 1)
let point = Point(coordinate)
let pointFeature = PointFeature(point)
let data = try! JSONEncoder().encode(pointFeature)
let json = String(data: data, encoding: .utf8)
print(json)

/*
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [
      1,
      0
    ]
  }
}
*/

```

Copyright (c) 2023 MapLibre contributors
