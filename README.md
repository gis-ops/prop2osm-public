# `prop2osm` converter for road & address data for TomTom & HERE

CLI tool to create OSM files from a variety of proprietary street network & address data sources, and specifically from TomTom and HERE data.

Converting your proprietary street data into the OSM data model has the following advantages:

- FOSS routing engines work out-of-the-box with your custom street data (e.g. [Valhalla](https://github.com/valhalla/valhalla), [GraphHopper](https://github.com/graphhopper/graphhopper/), [OSRM](https://github.com/Project-OSRM/osrm-backend/) and others)
- FOSS geocoding engines work out-of-the-box, such as [Pelias](https://github.com/pelias/pelias) and [Nominatim](https://github.com/osm-search/Nominatim)
- the entire OSM software ecosystem can be used for data processing (`osmium`, `osmosis`, `osm2pgsql` etc.)
- Storage-efficient protobuf (PBF) format to store the data which also allows for metadata tags

<!---
On https://converter.gis-ops.com you can see a demo with Valhalla & TomTom/HERE covering small regions in Austria and the US. We also provide the setup of this whole application ready-to-use with docker in this repository: https://github.com/gis-ops/osm-converter-demo.
-->

We provide more information in [this article](https://gis-ops.com/open-source-routing-engines-with-tomtom-and-here-data/). In case of further interest or questions, please contact us on enquiry@gis-ops.com.

> **Disclaimer**
> The converter has been designed to only work with street network and address data and is **not** suitable to produce OSM files for rendering or any other purpose.

## Contact

Please contact us on enquiry@gis-ops.com in case of questions or interest.

## General

#### Supported providers:

- TomTom (including historical traffic data and the MNL datasets, i.e. logistics: width/height/hazmat etc.)
- HERE (also including truck attributes), not including traffic & address data (yet)

#### Supported transporation profiles

Generally the software can be used to output data suitable for **any** transportation profile. **Note** however, that most proprietary street datasets are optimized for motorized vehicles.

`prop2osm` has special support for truck/hgv, where both TomTom & HERE offer extensively attributed datasets for truck restrictions, such as `maxheight`, `maxweight`, truck-specific speed limits etc.

#### Historical Traffic in Valhalla

We provide support to convert TomTom's historical traffic patterns to Valhalla's expected format.

#### Live Traffic in Valhalla

Additionally Valhalla can ingest dynamic live traffic (e.g. from TomTom). 

## Customization

The software was designed to provide least resistance to extensibility, both in terms of extending functionality for already implemented providers and/or implementing a new data provider, other than TomTom or HERE.

## OSM tags supported

The following is a (not comprehensive) list of the general OSM tags we create/use for e.g. TomTom data:

- [name](https://wiki.openstreetmap.org/wiki/Key:name)
- [highway](https://wiki.openstreetmap.org/wiki/Key:highway)
- [oneway](https://wiki.openstreetmap.org/wiki/Key:oneway)
- [maxspeed](https://wiki.openstreetmap.org/wiki/Key:maxspeed) (including `:hgv`, `:forward`, `:backward` and others)
- Access restrictions [motor_vehicle](https://wiki.openstreetmap.org/wiki/Key:motor_vehicle), [motorcar](https://wiki.openstreetmap.org/wiki/Key:motorcar), [bus](https://wiki.openstreetmap.org/wiki/Key:bus), [psv](https://wiki.openstreetmap.org/wiki/Key:psv) etc
- All turn restrictions (including `restriction:hgv`, but not time-dependent ones)
- [bridge](https://wiki.openstreetmap.org/wiki/Key:bridge)
- [tunnel](https://wiki.openstreetmap.org/wiki/Key:tunnel)
- [toll](https://wiki.openstreetmap.org/wiki/Key:toll)
- [ferry](https://wiki.openstreetmap.org/wiki/Tag:route%3Dferry)
- [hazmat](https://wiki.openstreetmap.org/wiki/Key:hazmat) (for truck profiles)
- [maxweight](https://wiki.openstreetmap.org/wiki/Key:maxweight) (for truck profiles)
- [maxheight](https://wiki.openstreetmap.org/wiki/Key:maxheight) (for truck profiles)
- [maxwidth](https://wiki.openstreetmap.org/wiki/Key:maxwidth) (for truck profiles)
- [incline](https://wiki.openstreetmap.org/wiki/Key:incline) (for pedestrian)
- etc.

## Compatibility

The output OSM files have been validated against:

- Valhalla
- OSRM
- Graphhopper
- OpenRouteService
- JOSM
- QGIS
- osmosis
- osmium
