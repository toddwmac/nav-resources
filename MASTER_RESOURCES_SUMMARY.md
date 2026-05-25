# Master Resources Consolidation

## What Was Done

Created **`master-resources.json`** - a unified, consolidated database combining all resources from:
- `Opus-nav-database.json` (40 resources)
- `western-nav-resources-json.json` (60 resources)  
- `lmc-western-nav-data.json` (17 resources)
- `overland_resources.json` (11 resources)

**Total: 95 unique resources** (after deduplication and intelligent merging)

## Unified Schema (v2.0.0)

The master schema combines the best fields from all source formats:

### Metadata Section
```json
{
  "schemaVersion": "2.0.0",
  "lastVerified": "2026-05-24",
  "lastUpdated": "2026-05-24",
  "metadata": {
    "title": "...",
    "version": "2.0.0",
    "description": "...",
    "totalResources": 95,
    "vehicleProfile": { ... }
  }
}
```

### Resource Fields
| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Stable unique identifier |
| `name` | string | Resource name |
| `category` | string | Primary category |
| `subcategory` | string | Secondary organization |
| `type` | string | App, Web, Hardware, API, PDF, etc. |
| `url` | string | Primary link |
| `platforms` | array | Supported platforms |
| `states` | array | State coverage (US or specific states) |
| `cost` | string | Pricing information |
| `cost_tier` | enum | Free, Freemium, Paid, Free / Low-Cost |
| `offline` | boolean | Offline capability |
| `offlineCapable` | boolean | Alternative offline field |
| `geoFormats` | array | GPX, KML, GeoPDF, etc. |
| `vehicleRouting` | boolean | RV/truck/height routing capability |
| `priority` | enum | critical, high, medium, low |
| `description` | string | What it does |
| `features` | array | Key features list |
| `bestFor` | string | Best use case |
| `tags` | array | Search/filter tags |
| `notes` | string | Operational notes |
| `source_verified` | string | Official source URL |

## Categories (13 total)

1. Height & Clearance Navigation
2. RV & Motorhome Navigation
3. Overlanding & Trail Navigation
4. Adventure Motorcycle
5. Geo-Located PDF Maps
6. Federal Mapping & Public Lands
7. Camping & Boondocking
8. State DOT Road Conditions
9. State OHV & Trail Maps
10. Print Maps & Atlases
11. Trip Planning & Scouting
12. Safety & Communication
13. Weather & Conditions

## Priority Distribution

- **Critical**: 6 resources (Low Clearance Map, Gaia GPS, onX Offroad, Avenza, USFS MVUM)
- **High**: 50+ resources (RV Life, CalTopo, Recreation.gov, iOverlander, etc.)
- **Medium**: 30+ resources
- **Low**: 10+ resources

## Next Steps

To make all HTML applications use this master file:

1. **Update each app's import logic** to handle the unified schema
2. **Add backward compatibility** for `offlineCapable` vs `offline` fields
3. **Update category dropdowns** to include all 13 categories
4. **Add state-based filtering** using the new `states` field
5. **Implement geospatial format filtering** with the `geoFormats` field

## File Comparison

| File | Resources | Lines | Schema Richness |
|------|-----------|-------|-----------------|
| **master-resources.json** | **95** | **2,141** | **★★★★★** |
| western-nav-resources-json.json | 60 | 971 | ★★★☆☆ |
| Opus-nav-database.json | 40 | 938 | ★★★★☆ |
| lmc-western-nav-data.json | 17 | 120 | ★★☆☆☆ |
| overland_resources.json | 11 | 98 | ★★☆☆☆ |

## Notes

- Some resources appear in multiple source files with slight variations
- When duplicates existed, the version with the most complete data was kept
- Resource IDs were standardized (`res-001` format) for consistency
- All URLs validated and kept from original sources
- Category names were standardized across sources
