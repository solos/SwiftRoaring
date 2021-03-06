# SwiftRoaring
<a href="https://developer.apple.com/swift"><img src="https://img.shields.io/badge/Swift4-compatible-green.svg?style=flat" alt="Swift 4 compatible" /></a>
<a href="https://github.com/apple/swift-package-manager"><img src="https://img.shields.io/badge/Swift%20Package%20Manager-compatible-brightgreen.svg"/></a>
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Build Status](https://travis-ci.org/piotte13/SwiftRoaring.svg?branch=master)](https://travis-ci.org/piotte13/SwiftRoaring)
[![codecov](https://codecov.io/gh/piotte13/SwiftRoaring/branch/master/graph/badge.svg)](https://codecov.io/gh/piotte13/SwiftRoaring)



Swift wrapper for CRoaring (a C/C++ implementation at https://github.com/RoaringBitmap/CRoaring)

Roaring bitmaps are used by several important systems:

*   [Apache Lucene](http://lucene.apache.org/core/) and derivative systems such as Solr and [Elastic](https://www.elastic.co/),
*   Metamarkets' [Druid](http://druid.io/),
*   [Apache Spark](http://spark.apache.org),
*   [Netflix Atlas](https://github.com/Netflix/atlas),
*   [LinkedIn Pinot](https://github.com/linkedin/pinot/wiki),
*   [OpenSearchServer](http://www.opensearchserver.com),
*   [Cloud Torrent](https://github.com/jpillora/cloud-torrent),
*   [Whoosh](https://pypi.python.org/pypi/Whoosh/),
*   [Pilosa](https://www.pilosa.com/),
*   [Microsoft Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/),
*   eBay's [Apache Kylin](http://kylin.io).

Roaring bitmaps are found to work well in many important applications:

> Use Roaring for bitmap compression whenever possible. Do not use other bitmap compression methods ([Wang et al., SIGMOD 2017](http://db.ucsd.edu/wp-content/uploads/2017/03/sidm338-wangA.pdf))


### Benchmarking

There is an entire repository dedicated to benchmarking.  You can find it [here](https://github.com/piotte13/SwiftRoaringBenchmarks).

> The following benchmarks were produced using this CPU model: <b>Intel(R) Core(TM) i7-4770 CPU @ 3.40GHz</b>
* [Comparison table](http://htmlpreview.github.io/?https://github.com/piotte13/SwiftRoaringBenchmarks/blob/master/Graphs/Intel(R)%20Core(TM)%20i7-4770%20CPU%20%40%203.40GHz/census-income/comparison-table.html)
* [Bar chart](http://htmlpreview.github.io/?https://github.com/piotte13/SwiftRoaringBenchmarks/blob/master/Graphs/Intel(R)%20Core(TM)%20i7-4770%20CPU%20%40%203.40GHz/census-income/bar-chart.html)

> The following benchmarks were produced using this CPU model: <b>Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz</b>
* [Comparison table](http://htmlpreview.github.io/?https://github.com/piotte13/SwiftRoaringBenchmarks/blob/master/Graphs/Intel(R)%20Core(TM)%20i7-8700%20CPU%20%40%203.20GHz/census-income/comparison-table.html)
* [Bar chart](http://htmlpreview.github.io/?https://github.com/piotte13/SwiftRoaringBenchmarks/blob/master/Graphs/Intel(R)%20Core(TM)%20i7-8700%20CPU%20%40%203.20GHz/census-income/bar-chart.html)

### Dependencies

Swift 4.0 or higher

### Usage

#### 1. Intall SwiftRoaring

* ##### With [Swift Package Manager](https://github.com/apple/swift-package-manager):
    Edit ``Package.swift`` so that it reads something like this:
    ```swift
    import PackageDescription

    let package = Package(
        name: "foo",
        dependencies: [
            .package(url: "https://github.com/piotte13/SwiftRoaring",  from: "1.0.4")
        ],
        targets: [
            .target(
                name: "foo",
                dependencies: ["SwiftRoaring"]),
        ]
    )
    ```

* ##### With [Carthage](https://github.com/Carthage/Carthage):
    ```swift
    github "piotte13/SwiftRoaring"
    ```
#### 2. Import SwiftRoaring in your project

```swift
import SwiftRoaring;

....
```

### Example

Here is a simplified but complete example:

```swift
import SwiftRoaring

//Create a new Roaring Bitmap
let bitmap = RoaringBitmap()

//Example: Add Range
bitmap.addRange(min: 0, max: 500)

//Example: copy
let cpy = bitmap.copy()

//Example: Operators
let and = bitmap && cpy

//Example: Iterate
for i in bitmap {
    print(i)
}

//See documentation for more functionalities!

```

### Documentation

https://piotte13.github.io/SwiftRoaring/

### Development

You can build using Swift Package Manager as follows:

```bash    
swift build  -Xcc -march=native  --configuration release
$(swift build   --configuration release  --show-bin-path)/fun
```
You can run tests using Swift Package Manager as follows:
```bash    
swift test
```

### Interactive use

```
$ swift build  -Xcc -march=native  --configuration release
$ swift -I .build/release -L .build/release -lSwiftRoaringDynamic
  1> import SwiftRoaring
  2> let bitmap = RoaringBitmap()
  3> bitmap.add(1)
```

### Mailing list/discussion group

https://groups.google.com/forum/#!forum/roaring-bitmaps

### Compatibility with Java RoaringBitmap library

You can read bitmaps in Go, Java, C, C++ that have been serialized in Java, C, C++.

### References

-  Daniel Lemire, Owen Kaser, Nathan Kurz, Luca Deri, Chris O'Hara, François Saint-Jacques, Gregory Ssi-Yan-Kai,  Software: Practice and Experience Volume 48, Issue 4 April 2018 Pages 867-895 [arXiv:1709.07821](https://arxiv.org/abs/1709.07821)
-  Samy Chambi, Daniel Lemire, Owen Kaser, Robert Godin,
Better bitmap performance with Roaring bitmaps,
Software: Practice and Experience Volume 46, Issue 5, pages 709–719, May 2016
http://arxiv.org/abs/1402.6407 This paper used data from http://lemire.me/data/realroaring2014.html
- Daniel Lemire, Gregory Ssi-Yan-Kai, Owen Kaser, Consistently faster and smaller compressed bitmaps with Roaring, Software: Practice and Experience Volume 46, Issue 11, pages 1547-1569, November 2016 http://arxiv.org/abs/1603.06549
