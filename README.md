# Hospital Accessibility Analysis Using Isochrones in QGIS

**Study area:** Districts served by Cordaid in Uganda

## Overview
This project maps how much of the population in Cordaid-supported districts can reach a hospital on foot within 15 and 30 minutes. It shows how to build walking-time isochrones in QGIS and combine them with population data to measure site accessibility.

## Objectives
- Map walkable catchments (15 and 30 minutes) around hospitals
- Estimate the population living inside each catchment
- Identify districts and areas with poor hospital access

## Data Sources
| Data | Source | Notes |
|------|--------|-------|
| Uganda population | [HDX – Uganda population](https://data.humdata.org/dataset/?ext_search_source=main-nav&q=Uganda+population) |
| Uganda subnational districts | [HDX – COD-AB Uganda](https://data.humdata.org/dataset/cod-ab-uga) | Administrative boundaries |
| Hospital locations | [source, e.g. Ministry of Health / OSM] |

## Tools and Software
- QGIS [version]
- **ORS Tools plugin** (OpenRouteService) for isochrones, profile: `foot-walking`, ranges: 900 s (15 min) and 1800 s (30 min)
- **Zonal Statistics** to sum population within each isochrone

## Methodology
1. **Prepare data:** load districts, hospitals and population layers; reproject to a common CRS ([e.g. EPSG:32636 / UTM 36N]).
2. **Filter study area:** select the districts where Cordaid operates.
3. **Generate isochrones:** run ORS Tools (Isochrones from Layer) on the hospital points for 15 and 30 minutes on foot.
4. **Calculate population served:** run Zonal Statistics (sum) of the population raster over the isochrone polygons.
5. **Summarise by district:** [intersect / aggregate results per district].
6. **Map and export:** style the layers and produce the final maps.

## Repository Contents
| File | Description |
|------|-------------|
| `concaid_districts.*` | District boundaries (shapefile) |
| `concaid_hospitals.*` | Hospital point locations |
| `CONCAID_hospital_iscohrones.*` | 15 and 30 minute walking isochrones |
| `*.gpkg` | [describe, e.g. combined outputs] |
| `maps/` | [exported maps] |

## Key Findings
- [e.g. X% of the population lives within a 30-minute walk of a hospital]
- [e.g. Districts A and B have the lowest coverage]

## Limitations
- Isochrones rely on OpenStreetMap road and path data, which may be incomplete in rural areas.
- Walking speed assumptions are ORS defaults and ignore terrain, weather and seasonal access.
- Population data is modelled, not a census count, and reflects [year].
- Only hospitals in the dataset are included; health centres and clinics are not.

## Reproducing This Project
1. Download the datasets listed above.
2. Install the ORS Tools plugin and add your free API key (openrouteservice.org).
3. Follow the methodology steps in order.

<img width="404" height="355" alt="population_density" src="https://github.com/user-attachments/assets/8d7695c2-cb14-45d3-a527-a1d14e2f6a19" />
<img width="371" height="349" alt="image" src="https://github.com/user-attachments/assets/3152d71e-bdc7-4e71-8bee-9483f56965f8" />
