# Geospatial and directory functions

Scope: Dremio Enterprise current [26.x]. Directory pages are source/format dependent; an HDFS-specific documented form is not evidence that it runs on every source.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [GEO_BEYOND](https://docs.dremio.com/current/reference/sql/sql-functions/functions/GEO_BEYOND/) | `GEO_BEYOND(latitude1 double, longitude1 double, latitude2 double, longitude2 double, distance double) → boolean` | Distance-threshold predicate | Coordinates and distance use the public page's units. |
| [GEO_DISTANCE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/GEO_DISTANCE/) | `GEO_DISTANCE(latitude1 double, longitude1 double, latitude2 double, longitude2 double) → double` | Distance between points | Latitude/longitude order is fixed. |
| [GEO_NEARBY](https://docs.dremio.com/current/reference/sql/sql-functions/functions/GEO_NEARBY/) | `GEO_NEARBY(latitude1 double, longitude1 double, latitude2 double, longitude2 double, distance double) → boolean` | Nearby predicate | Coordinates and distance use the public page's units. |
| [ST_FROMGEOHASH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ST_FROMGEOHASH/) | `ST_FROMGEOHASH(geohash varchar) → struct<latitude: double, longitude: double>` | Coordinates from geohash | Valid geohash string required. |
| [ST_GEOHASH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ST_GEOHASH/) | `ST_GEOHASH(latitude double, longitude double [, precision integer]) → varchar` | Geohash string | Precision is optional only in this form. |
| [IMAXDIR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IMAXDIR/), [IMINDIR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IMINDIR/), [MAXDIR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/MAXDIR/), [MINDIR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/MINDIR/) | `IMAXDIR\|IMINDIR\|MAXDIR\|MINDIR('dfs', '<parent_path>') → varchar` | Maximum/minimum immediate subdirectory name | HDFS-only documented form; do not generalize to other sources. |
| [LIST_FILES](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LIST_FILES/) | `LIST_FILES(source_path varchar) → table`; use `TABLE(LIST_FILES('@source/path'))` | File rows beneath path | Table binding, source permissions, and path support required. |
