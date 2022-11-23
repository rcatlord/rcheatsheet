## Querying OpenStreetMap

- [OSM map features](https://wiki.openstreetmap.org/wiki/Map_features)
- [overpass turbo](https://overpass-turbo.eu/)

```
// bike racks
node
({{bbox}})
["amenity"="bicycle_parking"];
out;
```

```
// zero waste shops
node
({{bbox}})
["shop"]["zero_waste”=“yes”];
out;
```
