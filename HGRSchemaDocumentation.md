# Heritage Gateway Technical Documentation 

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the Heritage Gateway Schema | Jan Putzan (Ember Technology)
1.1  | Addition of Overview section and updates to attribute descriptions | Jan Putzan (Ember Technology)
1.2  | Changes following the review of the Heritage Gateway Schema | Jan Putzan (Ember Technology)

## Overview
The submitted records must be compliant with the Heritage Gateway Record Schema for the purposes of processing and validating. This documents is a detailed description of that schema. 

# Heritage Gateway Record (HGR) Schema Documentation
The Heritage Gateway Record (HGR) schema comprises several attributes, each with specific requirements and characteristics.\
This documentation outlines the key aspects of these attributes.\
The minimum attributes comprising a CORE HGR are defined along with additional OPTIONAL attributes.

### Attribute: `record`
**CORE HGR attribute or OPTIONAL attribute**: N/A\
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: Object serving as a container for the primary data of the Heritage Gateway Record.

```
{
	"record": {
		"primaryReferenceNumber": "string",
		"heritageAssetName": "string",
		"descriptions": [ ... ],
		"monumentDatedTypes": [ ... ],
		"pointGeometry": { ... },
		"complexGeometries": [ ... ],
		"monumentSources": [ ... ],
		"objectFinds": [ ... ],
		"maritimeCraft": [ ... ],
		"historicAircraft": [ ... ],
		"relatedMonumentRecordPrimaryReferenceNumbers": [ ... ],
		"relatedEvents": [ ... ],
		"images": [ ... ],
		"protectedStatuses": [ ... ],
		"otherStatuses": [ ... ],
		"lastUpdated": "string"
	}
}
```
---

### Attribute: `record.primaryReferenceNumber`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: A unique number, or number and character combination, allocated to identify one entry in an information system. (MIDAS)\
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.heritageAssetName`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A free-text field that records the name by which a Heritage Asset is most commonly known. (MIDAS)\
For records where the data provider does not hold a specific name for the asset, HE will generate the Heritage Asset Name by concatenating Period and Monument Type using the earliest Period and Monument type available.\
**Validation Rules**: [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.descriptions`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: An array recording free text describing the Heritage Asset. Description Type is used to specialise the nature of the description. For example to distinguish non-technical summary text from more detailed synthesised works.\
**Validation Rules**: [Required](ValidationRules.md#required), [Array](ValidationRules.md#array), [Min:1](ValidationRules.md#min)

```
{
	"record": {
		...
		"descriptions": [
			{
				"type": "string",
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
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string), [In](ValidationRules.md#in)\
**Acceptable Values**: Full|Summary

---

### Attribute: `record.descriptions.*.description`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Free-text description of the Heritage Asset. (MIDAS)\
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric. Either rich text format or plain text format is acceptable.

---

### Attribute: `record.monumentDatedTypes`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y \
**Data Type**: Array\
**Description**: An array that contains a combination of one or more MonumentDatedType objects and recording information that describes the construction and use phases of the Heritage Asset.\
**Validation Rules**: [Required](ValidationRules.md#required), [Array](ValidationRules.md#array), [Min:1](ValidationRules.md#min)

```
{
	"record": {
		...
		"monumentDatedTypes": [
			{
				"type": "string",
				"startDate": "string",
				"endDate": "string",
				"displayDate": "string",
				"periods": [
					"string"
				],
				"materials": [
					"string"
				],
				"evidences": [
					"string"
				]
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
**Validation Rules**: [Required](ValidationRules.md#required), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Thesaurus of Monument Types: https://heritagedata.org/live/schemes/eh_tmt2.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: String\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. (MIDAS)\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.monumentDatedTypes.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: String\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. (MIDAS)\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.monumentDatedTypes.*.periods`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing periods for Herritage Asset. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.monumentDatedTypes.*.periods.*`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS).\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.monumentDatedTypes.*.materials`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing basic materials and media of which Herritage Asset is composed. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.monumentDatedTypes.*.materials.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Heritage Asset is composed. (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.evidences`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing evidence of Herritage Asset remains. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.monumentDatedTypes.*.evidences.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A description of the existing physical remains of a Heritage Asset when investigated, or the means by which it was identified where no remains exist or are visible. (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Evidence Thesaurus: https://heritagedata.org/live/schemes/eh_evd.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.pointGeometry`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: An object recording simple point spatial object information used to depict the spatial element of a Heritage Asset.

```
{
	"record": {
		...
		"pointGeometry": {
			"referenceSystem": "string",
			"xCoordinate": "decimal|integer",
			"yCoordinate": "decimal|integer",
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
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string), [In](ValidationRules.md#in)\
**Acceptable Values**: EPSG 27700 | EPSG 4326

---

### Attribute: `record.pointGeometry.xCoordinate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: The numerical easting (X) coordinate for a feature (MIDAS). Depending on the spatial reference system it either stands for longitude or easting values.\
**Validation Rules**: [Required](ValidationRules.md#required), [Numeric](ValidationRules.md#numeric), [SpatialCoordinate](ValidationRules.md#spatialcoordinate)\
**Acceptable Values**: If record.pointGeometry.referenceSystem = EPSG 4326 must be decimal LONGITUDE value\
If record.pointGeometry.referenceSystem =  EPSG 27700  must be absolute EASTING co-ordinate value

---

### Attribute: `record.pointGeometry.yCoordinate`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: The numerical northing (Y) coordinate for a feature (MIDAS). Depending on the spatial reference system it either stands for latitude or northing values.\
**Validation Rules**: [Required](ValidationRules.md#required), [Numeric](ValidationRules.md#numeric), [SpatialCoordinate](ValidationRules.md#spatialcoordinate)\
**Acceptable Values**: If record.pointGeometry.referenceSystem = EPSG 4326 must be decimal LATITUDE value\
If record.pointGeometry.referenceSystem =  EPSG 27700  must be absolute NORTHING co-ordinate value

---

### Attribute: `record.complexGeometries`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An optional array recording more complex spatial object information used to depict the spatial element of a Heritage Asset.\
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"complexGeometries": [
			{
				"spatialFeatureType": "string",
				"referenceSystem": "string",
				"spatialFeatureGeometryFormat": "string",
				"spatialFeatureGeometry": "string|object",
			}
		],
		...
	}
}
```
---

### Attribute: `record.complexGeometries.*.spatialFeatureType`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.complexGeometries` attribute is present)\
**Data Type**: String\
**Description**: The spatial object type used to depict the spatial element of a feature. (MIDAS)\
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string), [In](ValidationRules.md#in)\
**Acceptable Values**: point|polygon|multipoint|multipolygon|collection

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometryFormat`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.complexGeometries` attribute is present)\
**Data Type**: String\
**Description**: Standard format such as WKT (Well-Known Text) or GeoJSON used to describe the specified spatial reference system depicting the spatial feature type.\
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string), [In](ValidationRules.md#in)\
**Acceptable Values**: wkt|geojson

---

### Attribute: `record.complexGeometries.*.referenceSystem`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.complexGeometries` attribute is present)\
**Data Type**: String\
**Description**: The spatial reference system (or coordinate reference system) framework used to measure the Heritage Asset’s location(s )on the surface of Earth as coordinates.\
**Validation Rules**: [Required](ValidationRules.md#required), [String](ValidationRules.md#string), [In](ValidationRules.md#in)\
**Acceptable Values**: EPSG 27700 | EPSG 4326

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometry`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.complexGeometries` attribute is present)\
**Data Type**: String|object\
**Description**: Records the spatial geometry data describing the Heritage Asset’s locations, encoded in the specified format.\
**Validation Rules**: [Required](ValidationRules.md#required), [SpatialFeatureGeometry](ValidationRules.md#spatialfeaturegeometry)\
**Acceptable Values**: WKT string or GeoJSON object

---

### Attribute: `record.monumentSources`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: An array documenting references to sources of information about the Heritage Asset.\
**Validation Rules**: [Required](ValidationRules.md#required), [Array](ValidationRules.md#array), [Min:1](ValidationRules.md#min)

```
{
	"record": {
		...
		"monumentSources": [
			{
				"informationSourceTitle": "string",
				"statementOfAuthority": "string",
				"sourceNo": "string",
				"sourceReference": "string",
				"dateOfOrigination": "string",
				"sourceDigitalObjectIdentifier": "string",
				"bibliographyFootnoteReference": "string",
				"sourceUrl": "string"
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
**Validation Rules**: [RequiredWithout:bibliographyFootnoteReference](ValidationRules.md#requiredwithout), [String](ValidationRules.md#string)

---

### Attribute: `record.monumentSources.*.statementOfAuthority`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: A statement of the origin of an information source. (Statement of Responsibility - MIDAS). Typically, this will be personal names for the author, editor, photographer, cartographer, etc., but may also be used for publishers or issuing organisation names if individual names are not known.\
**Validation Rules**: [RequiredWithout:bibliographyFootnoteReference](ValidationRules.md#requiredwithout), [String](ValidationRules.md#string)

---

### Attribute: `record.monumentSources.*.sourceNo`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Descriptions often include numbered references to a bibliographic, archival, or personal communication source. The number relates to the sources listed in association with the record and helps indicate which part of the description relates to which source.\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.monumentSources.*.sourceReference`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Specific reference within a bibliographic or archive item. (MIDAS). Used to record details specific to the volume number, chronological designation, page numbers, figures and plates etc.\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.monumentSources.*.dateOfOrigination`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: The date of creation of an information Source. The year of publication or issue of a bibliographic item.\
**Validation Rules**: [RequiredWithout:bibliographyFootnoteReference](ValidationRules.md#requiredwithout), [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)

---

### Attribute: `record.monumentSources.*.sourceDigitalObjectIdentifier`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A unique set of letters, characters and numbers that gives a persistent link to a resource on the internet, e.g. https://doi.org/10.5284/1092416. \
**Validation Rules**: [Url](ValidationRules.md#url), [DigitalObjectIdentifier](ValidationRules.md#digitalobjectidentifier)\
**Acceptable Values**: Must have text segment "doi" in URL

---

### Attribute: `record.monumentSources.*.bibliographyFootnoteReference`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attributes informationSourceTitle, statementOfAuthority, dateOfOrigination are empty)\
**Data Type**: String\
**Description**: A free text source reference.\
**Validation Rules**: [RequiredWithout:informationSourceTitle,statementOfAuthority,dateOfOrigination](ValidationRules.md#requiredwithout)\
**Acceptable Values**: Alphanumeric. Either rich text format or plain text format is acceptable.

---

### Attribute: `record.monumentSources.*.sourceUrl`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: A unique set of letters, characters and numbers referencing a web resource that specifies its location and a mechanism for retrieving it.\
**Validation Rules**: [Url](ValidationRules.md#url)

---

### Attribute: `record.objectFinds`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An optional array documenting artefacts and ecofacts found in association with the Heritage Asset. \
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"objectFinds": [
			{
				"type": "string",
				"startDate": "string",
				"endDate": "string",
				"displayDate": "string",
				"periods": [
					"string"
				],
				"materials": [
					"string"
				]
			}
		],
		...
	}
}
```
---

### Attribute: `record.objectFinds.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.objectFinds` attribute is present)\
**Data Type**: String\
**Description**: A description of the form, function or type of artefact/ecofact. (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Archaeological Objects Thesaurus: https://heritagedata.org/live/schemes/mda_obj.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.objectFinds` attribute is present AND if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: String\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of manufacture, deposition or death (for biological materials).(MIDAS)\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.objectFinds.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.objectFinds` attribute is present AND if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: String\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of manufacture, deposition or death (for biological materials). (MIDAS)\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.objectFinds.*.periods`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing periods for Herritage Asset. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.objectFinds.*.periods.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.objectFinds` attribute is present AND if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the period of manufacture, deposition or death (for biological materials).\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given. (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.objectFinds.*.materials`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing basic materials and media of which the Object is composed. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)


---

### Attribute: `record.objectFinds.*.materials.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which the Object is composed. (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.\
Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array used to record information about watercraft (vessels of every description that ply on or in the water) associated with the Historic Asset. \
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"maritimeCraft": [
			{
				"type": "string",
				"startDate": "string",
				"endDate": "string",
				"displayDate": "string",
				"periods": [
					"string"
				],
				"materials": [
					"string"
				]
			}
		],
		...
	}
}
```
---

### Attribute: `record.maritimeCraft.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.maritimeCraft` attribute is present)\
**Data Type**: String\
**Description**: A term describing a watercraft by form or function.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Maritime Craft Types: https://heritagedata.org/live/schemes/eh_tmc.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.maritimeCraft.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.maritimeCraft.*.periods`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing periods for Herritage Asset. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.maritimeCraft.*.periods.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.maritimeCraft.*.materials`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing basic materials and media of which Maritime Craft is composed. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)


---

### Attribute: `record.maritimeCraft.*.materials.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Maritime Craft is constructed.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.\
Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array used to record information about aircraft (all heavier-than-air flying machines including airships, balloons, unmanned aerial vehicles etc.) associated with the Historic Asset\
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"historicAircraft": [
			{
				"type": "string",
				"startDate": "string",
				"endDate": "string",
				"displayDate": "string",
				"periods": [
					"string"
				],
				"materials": [
					"string"
				]
			}
		],
		...
	}
}
```
---

### Attribute: `record.historicAircraft.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.historicAircraft` attribute is present)\
**Data Type**: String\
**Description**: A term describing an aircraft by form or function.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Historic Aircraft Types: https://heritagedata.org/live/schemes/225.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft.*.startDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The earliest date of a date range. Associated with an End Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.historicAircraft.*.endDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The latest year of a date range. Associated with a Start Date entry. Used together, they provide a range of dates within which something has taken place (where this is not precisely known) or to indicate the span of dates over which a longer event has taken place. Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [DateFormats:YYYY-MM-DD, YYYY-MM, YYYY, -YYYY](ValidationRules.md#dateformats)\
**Acceptable Values**: BCE dates are represented using a negative year format.

---

### Attribute: `record.historicCraft.*.periods`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing periods for Herritage Asset. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)

---

### Attribute: `record.historicAircraft.*.periods.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The name given to the period when an event in the history of a Heritage Asset is thought to have occurred, or the archaeological period to which it is thought to belong (MIDAS). Most significantly the dates of construction, loss or recovery.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft.*.displayDate`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: Free-text field used to qualify or expand upon the date information recorded in Start Date and End Date, or Period (Name). May also include a brief description of what is referred to by the date given (MIDAS)\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.historicAircraft.*.materials`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array that contains one or more strings representing basic materials and media of which Historic Aircraft is composed. (MIDAS)\
**Validation Rules**: [Array](ValidationRules.md#array)


---

### Attribute: `record.historicAircraft.*.materials.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The basic materials and media of which a Historic Aircraft is constructed.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.\
Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.relatedMonumentRecordPrimaryReferenceNumbers`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array containing primaryReferenceNumbers of Monument Heritage Assets related to the Heritage Asset in question.\
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"relatedMonumentRecordPrimaryReferenceNumbers": [
			"string"
		],
		...
	}
}
```
---

### Attribute: `record.relatedMonumentRecordPrimaryReferenceNumbers.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.relatedMonumentRecordPrimaryReferenceNumbers` attribute is present)\
**Data Type**: String\
**Description**: The primaryReferenceNumber of the related Monument Heritage Asset record.\
**Validation Rules**: [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvents`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array recording events (i.e., investigative activities) associated with the Historic Asset.\
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"relatedEvents": [
			{
				"primaryReferenceNumber": "string",
				"type": "string",
				"name": "string",
				"description": "string",
				"url": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.relatedEvents.*.primaryReferenceNumber`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.relatedEvents` attribute is present)\
**Data Type**: String\
**Description**: The primaryReferenceNumber of the related event record.\
**Validation Rules**: [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvents.*.type`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.relatedEvents` attribute is present)\
**Data Type**: String\
**Description**: The type of the related event record.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: Historic England Event Types: https://heritagedata.org/live/schemes/agl_et.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.relatedEvents.*.name`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.relatedEvents` attribute is present)\
**Data Type**: String\
**Description**: The name of the related event record.\
**Validation Rules**: [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvents.*.description`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The free text description of the related event record.\
**Validation Rules**: [String](ValidationRules.md#string)\
**Acceptable Values**: Alphanumeric. Either rich text format or plain text format is acceptable.

---

### Attribute: `record.relatedEvents.*.url`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The url of the related event record.\
**Validation Rules**: [Url](ValidationRules.md#url)

---

### Attribute: `record.images`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array of displayed images and captions. \
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
	"record": {
		...
		"images": [
			{
				"url": "string",
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
**Mandatory in HGR**: Y (if `record.images` attribute is present)\
**Data Type**: String\
**Description**: The url of the image.\
**Validation Rules**: [Url](ValidationRules.md#url)

---

### Attribute: `record.images.*.caption`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.images` attribute is present)\
**Data Type**: String\
**Description**: The caption of the image.\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.images.*.copyright`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: Y (if `record.images` attribute is present)\
**Data Type**: String\
**Description**: The copyright text of the image.\
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.protectedStatuses`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: Array of protected statuses (e.g. Conservation Area, Listed Building etc.) to which the Heritage Asset is subject.\
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
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

### Attribute: `record.protectedStatuses.*`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: The protected status of the Heritage Asset.\
**Validation Rules**: [String](ValidationRules.md#string), [SchemeConcept](ValidationRules.md#schemeconcept)\
**Acceptable Values**: OASIS Protection Status: https://heritagedata.org/live/schemes/ef5ebc5b-abd6-44c5-a9d6-83a16f2b66ae.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.otherStatuses`
**CORE HGR attribute or OPTIONAL attribute**: OPTIONAL\
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: An array recording combinations of text and links, including those that are dead or redirected, e.g.: http://pastscape.english-heritage.org.uk/hob.aspx?hob_id=1003343 \
**Validation Rules**: [Array](ValidationRules.md#array)

```
{
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
**Validation Rules**: [String](ValidationRules.md#string)

---

### Attribute: `record.lastUpdated`
**CORE HGR attribute or OPTIONAL attribute**: CORE\
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The date on which an inventory entry was most recently revised or updated (MIDAS)\
**Validation Rules**: [Required](ValidationRules.md#required), [Date](ValidationRules.md#date)\
**Acceptable Values**: A date represented in ISO 8601 UTC format
