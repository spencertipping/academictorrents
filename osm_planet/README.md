# OpenStreetMap planet
Downloads `planet.xml` and produces several derivative outputs, each available
under its own torrent:

- `xml-parts`: the original XML recompressed using LZ4 and split into high-level
  regions:
    - `xml-parts/osm-nodes.lz4`
    - `xml-parts/osm-ways.lz4`
    - `xml-parts/osm-relations.lz4`
- `osm-nodes-packed.QQ`: a 128-bit native-endian binary encoding of nodes as
  `long id, long gh60`
- `way-tiles/[gh4]`: ways indexed by geohash-4 with dereferenced nodes
