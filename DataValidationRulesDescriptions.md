# Validation Rules Descriptions

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the Validation Rules Descriptions | Jan Putzan (Ember Technology)

## Overview

The Heritage Gateway Record (HGR) [schema](HeritageGatewayRecordSchemaDocumentation.md) specifies which validation rules will be applied to each of the HGR’s constituent attributes. These rules are described below. 

### `Required`
**What it means**: This field must be filled in. You cannot leave it blank or submit an empty value.  
**Example**: A record without a `primaryReferenceNumber` will fail validation because this field is mandatory.

---

### `RequiredWithout`
**What it means**: This field becomes mandatory if another specified field is missing or empty.  
**Example**: If you don't provide a `bibliographyFootnoteReference`, you must fill in `informationSourceTitle`, `statementOfAuthority`, and `dateOfOrigination`.

---

### `String`
**What it means**: The value must be text (letters, numbers, or symbols). It cannot be a number, true/false value, list, or other data type.  
**Example**: `heritageAssetName` must be text like "Medieval Castle" – not a number like `1234`.

---

### `Date`
**What it means**: The value must be a valid date in **ISO 8601 UTC format** (e.g., `YYYY-MM-DD`). BCE dates use negative years (e.g., `-0500` for 500 BCE).  
**Example**: `lastUpdated: "2023-10-05"` is valid; `lastUpdated: "October 5th"` is not.

---

### `Url`
**What it means**: The value must be a full web address starting with `http://` or `https://`.  
**Example**: `sourceUrl: "https://example.com/resource"` is valid; `sourceUrl: "example.com"` is not.

---

### `Min`
**What it means**: A list must contain at least the specified number of items.  
**Example**: `descriptions` requires at least 1 description entry. An empty list will fail.

---

### `In`/`InCaseInsensitive`
**What it means**: The value must match one of the predefined options (case-sensitive or case-insensitive).  
**Example**: For `description.type`, only `Full` or `Summary` are allowed. `FULL` would fail if case-sensitive.

---

### `Array`
**What it means**: The value must be a list of items (enclosed in `[]`).  
**Example**: `monumentDatedTypes` must be a list of objects – a single object without brackets will fail.

---

### `Numeric`
**What it means**: The value must be a number (whole or decimal).  
**Example**: `xCoordinate: 51.5074` is valid; `xCoordinate: "51.5074"` (as text) is invalid.

---

### `SpatialCoordinate`
**What it means**: Coordinates must match the specified reference system:  
- **EPSG 27700 (British National Grid)**: Whole numbers or decimals (e.g., easting `530000`, northing `180000.777`).  
- **EPSG 4326 (WGS84)**: Decimal latitude/longitude (e.g., `51.5074, -0.1278`).  

---

### `SchemeConcept`
**What it means**: The value must come from a specific controlled list (thesaurus or taxonomy). Use exact terms from the linked scheme.  
**Example**: For `monumentDatedTypes.type`, valid terms include "Castle" or "Roman Villa" from the [FISH Monument Types Thesaurus](https://heritagedata.org/live/schemes/eh_tmt2.html).

---

### `DateFormats`
**What it means**: Dates must use one of these formats:  
- Full date: `YYYY-MM-DD` (e.g., `1066-10-14`)  
- Year-month: `YYYY-MM` (e.g., `1066-10`)  
- Year only: `YYYY` (e.g., `1066`, `966`, `1`)  
- BCE: `-YYYY` (e.g., `-500` for 500 BCE).  

---

### `SpatialFeatureGeometry`
**What it means**: Geometry data must be formatted as:  
- **WKT (Well-Known Text)**: e.g., `POINT (530000 180000)`  
- **GeoJSON**: A structured object like `{"type": "Point", "coordinates": [530000, 180000]}`.  

---

### `DigitalObjectIdentifier`
**What it means**: The value must be a valid DOI URL starting with `https://doi.org/`.  
**Example**: `sourceDigitalObjectIdentifier: "https://doi.org/10.5284/1092416"`.

---

### `HeritagePeriodRequired`
**What it means**: If you don’t provide `startDate` and `endDate`, you must include at least one period (e.g., "Medieval"). If a period is "UNCERTAIN", dates must be omitted.

---

### `HeritageDatesRequired`
**What it means**: If you don’t provide periods, you must include both `startDate` and `endDate`.

---

### `HeritageDatesOmitted`
**What it means**: If any period is "UNCERTAIN", you cannot include `startDate` or `endDate`.

---

### `DateInPast`
**What it means**: Dates cannot be in the future. For example, `startDate: "2050-01-01"` will fail.

---

### `DatesOrder`
**What it means**: `startDate` must be earlier than or equal to `endDate`.  
**Example**: `startDate: "1066-10-14"` and `endDate: "1100"` is valid. `startDate: "1500"` with `endDate: "1400"` is invalid.

---

### `PrimaryReferenceNumberUnique`
**What it means**: Each record’s `primaryReferenceNumber` must be unique within your submission. Duplicate IDs will cause errors.

---

### `Boolean`
**What it means**: The value must represent true/false. Acceptable inputs: `true`, `false`, `1`, `0`, `"1"`, `"0"`.  
**Example**: `delete: true` marks a record for deletion. `delete: "yes"` is invalid.

