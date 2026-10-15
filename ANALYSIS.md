# Geospatial MCP landscape: strategic overview

Snapshot of the catalog on 2026-10-15: 106 servers, health checked 2026-10-15.
The tables in `README.md` are generated and stay current. This file is a hand-written analysis and does not update itself, so re-run the numbers before relying on them later.

## Summary

The catalog shows a market that is broad but uneven. Everyday location tasks (geocoding, routing, place search, weather) are well covered, mostly by open-source servers over OpenStreetMap and public data. Commercial value is concentrating in two places: hosted servers run by data vendors, and the large mapping platforms, which now publish their own servers. Analysis-heavy work (spatial databases, desktop GIS, geoprocessing) has fewer servers and almost no vendor involvement. Some capability areas have no servers in the catalog at all.

| Measure | Value |
| --- | --- |
| Servers | 106 across 12 categories |
| Access | 48 open · 4 free · 47 commercial · 7 paywalled |
| Published by the vendor (`official`) | 41 (39%) |
| Health | 63 active · 22 hosted · 18 stale · 2 pending · 1 archived |
| Delivered as a hosted endpoint | 24 (22 live, 2 in early access) |
| Implementation language, where known | Python 38 · TypeScript 24 · JavaScript/Node 4 · other 5 |

## Coverage by category

| Category | Servers | Open or free | Commercial or paywalled | Official | Stale or archived |
| --- | ---: | ---: | ---: | ---: | ---: |
| Maps, tiles & commercial platforms | 18 | 0 | 18 | 12 | 6 |
| Geocoding & place search | 17 | 9 | 8 | 5 | 5 |
| Remote sensing (STAC / EO) | 16 | 6 | 10 | 8 | 1 |
| Weather & climate | 12 | 12 | 0 | 1 | 2 |
| Desktop & enterprise GIS | 9 | 5 | 4 | 0 | 3 |
| Geospatial data access & catalogs | 8 | 5 | 3 | 6 | 0 |
| GIS / geoprocessing toolkits | 7 | 7 | 0 | 2 | 0 |
| Aviation & maritime tracking | 6 | 3 | 3 | 1 | 0 |
| Parcels & property | 4 | 0 | 4 | 3 | 0 |
| Other (IP geolocation, misc) | 4 | 1 | 3 | 2 | 1 |
| Spatial databases | 3 | 2 | 1 | 1 | 0 |
| Routing, isochrones & navigation | 2 | 2 | 0 | 0 | 1 |

The category counts understate some capabilities. Routing is the clearest case: only 2 servers sit in the routing category, but 14 servers carry the `routing` tag, because most mapping platforms bundle routing with geocoding and search.

## Patterns

### Commodity location services are saturated

Geocoding, reverse geocoding, place search and routing appear in more servers than any other capability: 21 servers carry the `geocoding` tag. Seven of the 17 geocoding servers wrap OpenStreetMap services (Nominatim or Overpass), and they overlap heavily. Five of the 17 are stale. A new geocoding server adds little unless it brings different data or a different way of working, such as Overture places (PlaceRoot), US address verification (Smarty) or fully offline lookups from a local file (GridPin, the catalog's first offline geocoder).

### The major platforms have arrived, with gaps

12 of the 18 mapping-platform servers are official, including Mapbox, TomTom, MapQuest, CARTO, Felt, Cesium and an Esri beta. Two large ecosystems still depend on community work:

- **Google Maps** has four entries and none is official. The reference server has been archived, and the remaining three are community wrappers.
- **Esri / ArcGIS** has seven entries across categories. One is an official beta (ArcGIS Location Services). The rest are community servers or third-party platforms, including both ArcGIS Pro integrations.

Being official does not guarantee upkeep. The Baidu, Foursquare and Stadia Maps servers are official but stale.

Vendors are also starting to replace community wrappers of their own APIs. Geoapify now publishes an official hosted server, which sits beside the older community server for the same API. That community server is stale.

### Data vendors prefer hosted servers

Of the 24 hosted servers, nearly all come from vendors selling data or a platform: parcel data (Regrid, LandRecords.us, MAIA), imagery (Vexcel, Planet, Planetary Computer Pro), address data (Smarty), location services (Geoapify), mobility and foot-traffic data (Factori) and cloud GIS (CARTO, Felt, GIS Cloud). A hosted server keeps the vendor's data and API keys on their side and lets them update tools without users reinstalling anything. We expect this to become the default delivery model for commercial geodata. It also changes what the catalog can check: a hosted server has no source code to scan, so trust rests on the vendor's domain.

### Earth observation is the most commercially varied area

Remote sensing has the widest spread of access models in the catalog: open STAC and NASA/ESA access, Earth Engine wrappers, imagery marketplaces (SkyFi), and paid-only vendor platforms. Three of the catalog's seven paywalled servers are here. Newer entries go beyond search and download to embeddings and similarity search (LGND) and array-data queries over Zarr (Arraylake), which suggests the area is moving from data access towards analysis. Discovery is improving too: AWS now publishes an official server for its Registry of Open Data, which finds datasets with STAC endpoints and previews public S3 buckets.

### Weather is open and US-heavy

All 12 weather servers are open or free. Most of them draw on NOAA and the US National Weather Service, or on Open-Meteo for global coverage. Outside the US, only Canada has a national service in the catalog. European services such as ECMWF open data, DWD and the Met Office do not appear, except through Open-Meteo's ERA5 data. A search for European options on 2026-10-15 found no official servers: Rainbow.ai offers a precipitation nowcasting API but no MCP server, and the one Buienradar server is a small, unmaintained community project.

### Analysis tools are thin and community-built

Spatial databases (3 servers), desktop GIS (9) and geoprocessing toolkits (7) together make up less than a fifth of the catalog. No desktop GIS server is official: all five QGIS servers and both ArcGIS Pro servers come from the community. For agents that do GIS analysis beyond lookups, this is the least mature part of the market and the most open to new work.

## Gaps

These capabilities have no dedicated server in the catalog. Some may exist but not be listed yet, so each gap is a prompt to search before it is a conclusion.

| Capability | What the catalog has today |
| --- | --- |
| Public transit (GTFS, schedules, real-time) | Nothing |
| Fleet and logistics optimisation (vehicle routing, dispatch) | Trip optimisation inside OSRM MCP only |
| Cloud warehouse spatial SQL (BigQuery, Snowflake, Databricks) | Wherobots (Apache Sedona), plus warehouse access through CARTO and Felt |
| Natural hazards (wildfire, flood, earthquake) as a focus | Wildfire inside weather-mcp; earthquakes inside God's Eye View and the EarthScope server |
| Demographics and census data | Demographics derived from mobility data in Factori (paid), and census enrichment inside Smarty |
| Elevation and terrain as a service | Spread across MapTiler, TerraLab, MapSmith and Open-Meteo |
| 3D, point clouds and digital twins | Cesium and one module of the Kiro power pack |
| Parcels and property outside the US and Canada | Nothing |
| National weather services outside North America | Nothing (see above) |

## Implications

For someone choosing servers: commodity lookups are a solved problem, so choose on data quality, licence and vendor support rather than features. Prefer official or actively maintained servers. For hosted servers, check who runs the domain.

For someone building servers: the open opportunities are in analysis and in under-served data. Desktop GIS automation, cloud warehouse spatial SQL, transit and hazard data have the clearest demand and the least supply. Another OSM geocoder does not.
