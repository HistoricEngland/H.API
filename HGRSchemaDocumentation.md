# Heritage Gateway Technical Documentation 

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the Heritage Gateway Schema| Jan Putzan (Ember Technology)
1.1  | Addition of Overview section and updates to attribute descriptions | Jan Putzan (Ember Technology)

## Overview
Historic Environment Records (sometimes referred to as Sites and Monuments Records) may be held by County Councils, District Councils or Unitary Authorities. In each case, the record will cover the whole of the local authority area. Selected major historic towns and cities are covered by Urban Archaeological Databases (UADs). In many cases, UADs are held as part of, and are accessible via, the local Historic Environment Record. 

Historic England have made available a web service that can be used to submit the UAD information into the Heritage Gatewway through a REStful API. Details can be found here: [https://github.com/ember-technology-ltd/H.API/blob/master/FileUploadDocumentation.md]

The information submitted through the API must be compliant with the Heritage Gateway Record Schema for the purposes of processing and validating the information submitted. This documents is a detailed description of that schema. 

# Heritage Gateway Record (HGR) Schema Documentation
The Heritage Gateway Record (HGR) schema comprises several attributes, each with specific requirements and characteristics.\
This documentation outlines the key aspects of these attributes.


### Attribute: `metadata`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: Object serving as a container for the Heritage Gateway Record’s metadata

```
{
	"metadata": {
		"extractedAtTimestamp": "timestamp",
		"compilerOrganisationName": "string",
		"dataSource": "string",
		"dataSourceID": "string",
		"typeOfRecord": "string"
	},
	"record": { ... }
}
```
---

### Attribute: `metadata.extractedAtTimestamp`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: ISO 8601 UTC\
**Description**: Records the timestamp when the data were extracted.\
**Validation Rules**: required, date, format:Y-m-d H:i:s

---

### Attribute: `metadata.compilerOrganisationName`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The name of the organisation responsible for the compilation or curation of entries in a dataset. (MIDAS)\
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `metadata.dataSource`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The name of the resource i.e. the dataset from which the HGR is extracted.\
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `meatadata.dataSourceID`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: A unique number, or number and character combination, used to identify the resource.\
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `meatadata.typeOfRecord`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Type of the record, programmatically defaulted to MONUMENT \
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: Object serving as a container for the primary data of the Heritage Gateway Record.

```
{
	"metadata": { ... },
	"record": {
		"primaryReferenceNumber": "string",
		"heritageAssetName": "string",
		"descriptions": [ ... ],
		"monumentDatedTypes": [ ... ],
		"pointGeometry": { ... },
		"complexGeometries": [ ... ],
		"monumentSources": [ ... ],
		"objectFinds": [ ... ],
		"maritimeCrafts": [ ... ],
		"historicAircrafts": [ ... ],
		"relatedRecords": [ ... ],
		"relatedEvents": [ ... ],
		"parish": "string",
		"streetMapLink": "url",
		"images": [ ... ],
		"protectedStatuses": [ ... ],
		"otherStatuses": [ ... ],
		"lastUpdated": "YYYY-MM-DD"
	}
}
```
---

### Attribute: `record.primaryReferenceNumber`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: A unique number, or number and character combination, allocated to identify one entry in an information system. (MIDAS)\
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.heritageAssetName`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A free-text field that records the name by which a Heritage Asset is most commonly known. (MIDAS)\
For records where the data provider does not hold a specific name for the asset, generate Heritage Asset Name by concatenating Period and Monument Type. Always use the earliest Period and Monument type available.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.descriptions`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: An array recording free text describing the Heritage Asset. Description Type is used to specialise the nature of the description. For example to distinguish non-technical summary text from more detailed synthesised works.\
**Validation Rules**: required, array\
**Acceptable Values**: An array that contains one or more Description objects

```
{
	"metadata": { ... },
	"record": {
		...
		"descriptions": [
			{
				"type": "Full|Summary",
				"description": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.descriptions.*.type`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Allows a description to be specialised by level of detail or intended use. Used to distinguish brief summaries from more detailed full descriptions. (MIDAS)\
**Validation Rules**: required\
**Acceptable Values**: Full,Summary

---

### Attribute: `record.descriptions.*.description`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Free-text description of the Heritage Asset. (MIDAS)\
**Validation Rules**: required\
**Acceptable Values**: Alphanumeric (255 characters for Summary, truncate if greater).

---

### Attribute: `record.monumentDatedTypes`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y \
**Data Type**: Array\
**Description**: An array recording information that describes the construction and use phases of the Heritage Asset.\
**Validation Rules**: required, array\
**Acceptable Values**: An array that contains a combination of one or more MonumentDatedType objects.

```
{
	"metadata": { ... },
	"record": {
		...
		"monumentDatedTypes": [
			{
				"type": "string",
				"startDate": "YYYY-MM-DD",
				"endDate": "YYYY-MM-DD",
				"period": "string",
				"displayDate": "string",
				"material": "string",
				"evidence": "string"

			}
		],
		...
	}
}
```
---

### Attribute: `record.monumentDatedTypes.*.type`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Term or terms that classify the monument principally with reference to its function or use. (MIDAS)\
**Validation Rules**: required, alpha\
**Acceptable Values**: FISH Thesaurus of Monument Types: https://heritagedata.org/live/schemes/eh_tmt2.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. (MIDAS)\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.monumentDatedTypes.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. (MIDAS)\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.monumentDatedTypes.*.period`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS).\
**Validation Rules**: required, alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.monumentDatedTypes.*.material`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Heritage Asset is composed. (MIDAS)\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.evidence`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A description of the existing physical remains of a Heritage Asset when investigated, or the means by which it was identified where no remains exist or are visible. (MIDAS)\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Evidence Thesaurus: https://heritagedata.org/live/schemes/eh_evd.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.pointGeometry`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: An object recording simple point spatial object information used to depict the spatial element of a Heritage Asset.

```
{
	"metadata": { ... },
	"record": {
		...
		"pointGeometry": {
			"referenceSystem": "string",
			"xCoordinate": "numeric",
			"yCoordinate": "numeric",
		},
		...
	}
}
```
---

### Attribute: `record.pointGeometry.referenceSystem`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The spatial reference system (or coordinate reference system) framework used to measure the Heritage Asset’s location(s) on the surface of Earth as coordinates.\
**Validation Rules**: required\
**Acceptable Values**: EPSG 27700 | EPSG 4326

---

### Attribute: `record.pointGeometry.xCoordinate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: The numerical easting (X) coordinate for a feature (MIDAS). Depending on the spatial reference system it either stands for longitude or easting values.\
**Validation Rules**: required, numeric\
If record.pointGeometry.referenceSystem = EPSG 4326 must be decimal LONGITUDE value\
If record.pointGeometry.referenceSystem =  EPSG 27700  must be absolute EASTING co-ordinate value

---

### Attribute: `record.pointGeometry.yCoordinate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: The numerical northing (Y) coordinate for a feature (MIDAS). Depending on the spatial reference system it either stands for latitude or northing values.\
**Validation Rules**: required, numeric\
If record.pointGeometry.referenceSystem = EPSG 4326 must be decimal LATITUDE value\
If record.pointGeometry.referenceSystem =  EPSG 27700  must be absolute NORTHING co-ordinate value

---

### Attribute: `record.complexGeometries`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An optional array recording more complex spatial object information used to depict the spatial element of a Heritage Asset.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"complexGeometries": [
			{
				"spatialFeatureType": "string",
				"referenceSystem": "string",
				"spatialFeatureGeometryFormat": "string",
				"spatialFeatureGeometry": "string",
			}
		],
		...
	}
}
```
---

### Attribute: `record.complexGeometries.*.spatialFeatureType`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The spatial object type used to depict the spatial element of a feature. (MIDAS)\
**Validation Rules**: required\
**Acceptable Values**: point|polygon|multipoint|multipolygon|collection

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometryFormat`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Standard format such as WKT (Well-Known Text) or GeoJSON used to describe the specified spatial reference system depicting the spatial feature type.\
**Validation Rules**: required\
**Acceptable Values**: wkt|geojson

---

### Attribute: `record.complexGeometries.*.referenceSystem`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The spatial reference system (or coordinate reference system) framework used to measure the Heritage Asset’s location(s )on the surface of Earth as coordinates.\
**Validation Rules**: required\
**Acceptable Values**: EPSG 27700 | EPSG 4326

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometry`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Records the spatial geometry data describing the Heritage Asset’s locations, encoded in the specified format.\
**Validation Rules**: required, string\
**Acceptable Values**: WKT or geojson representation

---

### Attribute: `record.monumentSources`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: An array documenting references to sources of information about the Heritage Asset.\
**Validation Rules**: required, array\
**Acceptable Values**: An array that contains one or more MonumentSource objects

```
{
	"metadata": { ... },
	"record": {
		...
		"monumentSources": [
			{
				"informationSourceTitle": "string",
				"statementOfAuthority": "string",
				"sourceReference": "string",
				"dateOfOrigination": "YYYY-MM-DD",
				"sourceDigitalObjectIdentifier": "url",
				"bibliographyFootnoteReference": "string",
				"sourceURL": "url"
			} 
		],
		...
	}
}
```
---

### Attribute: `record.monumentSources.*.informationSourceTitle`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: A name assigned to an information source, generally by its creator, to assist in identification. (MIDAS)\
**Validation Rules**: required without:bibliographyFootnoteReference, alpha, max:255

---

### Attribute: `record.monumentSources.*.statementOfAuthority`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: A statement of the origin of an information source. (Statement of Responsibility - MIDAS). Typically, this will be personal names for the author, editor, photographer, cartographer, etc., but may also be used for publishers or issuing organisation names if individual names are not known.\
**Validation Rules**: required without:bibliographyFootnoteReference, alpha, max:255

---

### Attribute: `record.monumentSources.*.sourceReference`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Specific reference within a bibliographic or archive item. (MIDAS). Used to record details specific to the volume number, chronological designation, page numbers, figures and plates etc.\
**Validation Rules**: alpha, max:255

---

### Attribute: `record.monumentSources.*.dateOfOrigination`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: ISO 8601 UTC\
**Description**: The date of creation of an information Source. The year of publication or issue of a bibliographic item.\
**Validation Rules**: required without:bibliographyFootnoteReference, date format:YYYY-MM-DD

---

### Attribute: `record.monumentSources.*.sourceDigitalObjectIdentifier`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A unique set of letters, characters and numbers that gives a persistent link to a resource on the internet, e.g. https://doi.org/10.5284/1092416.\
**Validation Rules**: url\
**Acceptable Values**: Must have text segment "doi" in URL

---

### Attribute: `record.monumentSources.*.bibliographyFootnoteReference`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attributes informationSourceTitle, statementOfAuthority, dateOfOrigination are empty)\
**Data Type**: String\
**Description**: A free text source reference.\
**Validation Rules**: required without:informationSourceTitle,statementOfAuthority,dateOfOrigination, max:255

---

### Attribute: `record.monumentSources.*.sourceURL`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A unique set of letters, characters and numbers referencing a web resource that specifies its location and a mechanism for retrieving it.\
**Validation Rules**: url

---

### Attribute: `record.objectFinds`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An optional array documenting artefacts and ecofacts found in association with the Heritage Asset. \
**Validation Rules**: array\
**Acceptable Values**: An array that contains one or more ObjectFinds objects

```
{
	"metadata": { ... },
	"record": {
		...
		"objectFinds": [
			{
				"type": "string",
				"startDate": "YYYY-MM-DD",
				"endDate": "YYYY-MM-DD",
				"period": "string",
				"displayDate": "string",
				"material": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.objectFinds.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: string\
**Description**: A description of the form, function or type of artefact/ecofact. (MIDAS)\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Archaeological Objects Thesaurus: https://heritagedata.org/live/schemes/mda_obj.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of manufacture, deposition or death (for biological materials).(MIDAS)\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.objectFinds.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of manufacture, deposition or death (for biological materials). (MIDAS)\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.objectFinds.*.period`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the period of manufacture, deposition or death (for biological materials).\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given. (MIDAS)\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.objectFinds.*.material`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which the Object is composed. (MIDAS)\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCrafts`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array used to record information about watercraft (vessels of every description that ply on or in the water) associated with the Historic Asset. \
**Validation Rules**: No specific validation rules apply.\
**Acceptable Values**: An array that contains one or more MaritimeCraft object

```
{
	"metadata": { ... },
	"record": {
		...
		"maritimeCrafts": [
			{
				"type": "string",
				"startDate": "YYYY-MM-DD",
				"endDate": "YYYY-MM-DD",
				"period": "string",
				"displayDate": "string",
				"material": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.maritimeCrafts.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: A term describing a watercraft by form or function.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Maritime Craft Types: https://heritagedata.org/live/schemes/eh_tmc.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCrafts.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: ISO 8601 UTC\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.maritimeCrafts.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: ISO 8601 UTC\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.maritimeCrafts.*.period`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCrafts.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.maritimeCrafts.*.material`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Maritime Craft is constructed.\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircrafts`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array used to record information about aircraft (all heavier-than-air flying machines including airships, balloons, unmanned aerial vehicles etc.) associated with the Historic Asset\
**Validation Rules**: No specific validation rules apply.\
**Acceptable Values**: An array that contains one or more HistoricAircraft objects

```
{
	"metadata": { ... },
	"record": {
		...
		"historicAircrafts": [
			{
				"type": "string",
				"startDate": "YYYY-MM-DD",
				"endDate": "YYYY-MM-DD",
				"period": "string",
				"displayDate": "string",
				"material": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.historicAircrafts.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: A term describing an aircraft by form or function.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Historic Aircraft Types: https://heritagedata.org/live/schemes/225.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircrafts.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: ISO 8601 UTC\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.historicAircrafts.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: ISO 8601 UTC\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY\
BCE dates are represented using a negative year format. For example, 500 BCE becomes -499 (this is because there is no year 0 in the Gregorian calendar). The negative year indicates it's a BCE date.

---

### Attribute: `record.historicAircrafts.*.period`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircrafts.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.historicAircrafts.*.material`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Historic Aircraft is constructed.\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.relatedMonumentRecords`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array recording information on records of Monument Heritage Assets related to the Heritage Asset in question.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"relatedMonumentRecords": [
			{
				"primaryReferenceNumber": "string",
				"heritageAssetName": "string",
				"description": "string",
				"url": "url"
			}
		],
		...
	}
}
```
---

### Attribute: `record.relatedMonumentRecords.*.primaryReferenceNumber`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The primaryReferenceNumber of the related Monument Heritage Asset record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedMonumentRecords.*.heritageAssetName`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The heritageAssetName of the related Monument Heritage Asset record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedMonumentRecords.*.description`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text description of the related Monument Heritage Asset.\
**Validation Rules**: alpha\
**Acceptable Values**: Phil to check with Jane - regarding max characters

---

### Attribute: `record.relatedMonumentRecords.*.url`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The URL of the related Monument Heritage Asset record.\
**Validation Rules**: url\
**Acceptable Values**: Must be a HE gateway URL

---

### Attribute: `record.relatedEvents`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array recording events (i.e., investigative activities) associated with the Historic Asset.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"relatedEvents": [
			{
				"primaryReferenceNumber": "string",
				"name": "string",
				"description": "string",
				"url": "url"
			}
		],
		...
	}
}
```
---

### Attribute: `record.relatedEvents.*.primaryReferenceNumber`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The primaryReferenceNumber of the related event record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvents.*.name`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name of the related event record.\
**Validation Rules**: alpha, max:100\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvents.*.description`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The free text description of the related event record.\
**Validation Rules**: alpha\
**Acceptable Values**: Phil to check with Jane - regarding max characters

---

### Attribute: `record.relatedEvents.*.url`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The url of the related event record.\
**Validation Rules**: url

---

### Attribute: `record.parish`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name of the parish type administrative area within which the Heritage Asset is located.\
**Validation Rules**: max:100

---

### Attribute: `record.streetMapLink`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: streetMapLink  e.g. http://www.streetmap.co.uk/map?x=501003&y=228939&title=HER+number+962 \
**Validation Rules**: url

---

### Attribute: `record.images`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array of displayed images and captions. \
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"images": [
			{
				"url": "url",
				"caption": "string",
				"copyright": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.images.*.url`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The url of the image.\
**Validation Rules**: url

---

### Attribute: `record.images.*.caption`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The caption of the image.\
**Validation Rules**: max:100

---

### Attribute: `record.images.*.copyright`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The copyright text of the image.\
**Validation Rules**: max:100

---

### Attribute: `record.protectedStatuses`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array of protected statuses (e.g. Conservation Area, Listed Building etc.) to which the Heritage Asset is subject.\
**Validation Rules**: array

---

### Attribute: `record.protectedStatuses.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The protected status of the Heritage Asset.\
**Validation Rules**: alpha\
**Acceptable Values**: OASIS Protection Status: https://heritagedata.org/live/schemes/ef5ebc5b-abd6-44c5-a9d6-83a16f2b66ae.html (including narrower concepts) prefLabel or altLabel.

```
{
	"metadata": { ... },
	"record": {
		...
		"protectedStatuses": [
			"string"
		],
		...
	}
}
```
---

### Attribute: `record.otherStatuses`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array recording combinations of text and links, including those that are dead or redirected, e.g.: http://pastscape.english-heritage.org.uk/hob.aspx?hob_id=1003343 \
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"otherStatuses": [
			"string"
		],
		...
	}
}
```
---

### Attribute: `record.otherStatuses.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A combination of text and links, including those that are dead or redirected, e.g.: http://pastscape.english-heritage.org.uk/hob.aspx?hob_id=1003343 \
**Validation Rules**: alpha

---

### Attribute: `record.lastUpdated`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: ISO 8601 UTC\
**Description**: The date on which an inventory entry was most recently revised or updated (MIDAS)\
**Validation Rules**: required, date format:Y-m-d H:i:s
