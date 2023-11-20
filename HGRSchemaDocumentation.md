# Heritage Gateway Technical Documentation 

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the Heritage Gateway Schema| Jan Putzan (Ember Technology)


# Overview 

Historic Environment Records (sometimes referred to as Sites and Monuments Records) may be held by County Councils, District Councils or Unitary Authorities. In each case, the record will cover the whole of the local authority area. Selected major historic towns and cities are covered by Urban Archaeological Databases (UADs). In many cases, UADs are held as part of, and are accessible via, the local Historic Environment Record. 

Historic England have made available a web service which can be used to submit the UAD information into the Heritage Gatewway through a REStful API. Details can be found here: [https://github.com/ember-technology-ltd/H.API/blob/master/FileUploadDocumentation.md]

The information submitted through the API must be compliant with the Heritage Gateway Record Schema for the purposes of processing and validating the information submitted. This documents is a detailed description of that schema. 


# Heritage Gateway Record (HGR) Schema Documentation
The Heritage Gateway Record (HGR) schema comprises several attributes, each with specific requirements and characteristics.\
This documentation outlines the key aspects of these attributes.


### Attribute: `metadata`
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: The metadata attribute is a fundamental part of the HGR schema and is mandatory for all records. It is an object that encapsulates various metadata elements. The creation and validation of this attribute require a third-party process to ensure its accuracy and integrity. This process is essential for maintaining the reliability of the HGR records.

```
{
	"metadata": {
		"extractedAtTimestamp": "timestamp",
		"source": "string",
		"sourceID": "string"
	},
	"record": { ... }
}
```
---

### Attribute: `metadata.extractedAtTimestamp`
**Mandatory in HGR**: Y\
**Data Type**: ISO 8601 UTC\
**Description**: The metadata.extractedAtTimestamp attribute, also mandatory, records the timestamp when the data was extracted. This attribute follows the ISO 8601 UTC format and adheres to a strict validation rule that requires the timestamp to be in the 'Y-m-d H:i:s' format. The precision and standardisation of this timestamp are crucial for maintaining the consistency of temporal data across the HGR system.\
**Validation Rules**: required, date format:Y-m-d H:i:s

---

### Attribute: `metadata.source`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Mandatory attribute, it's a string that represents the Historic Environment Record (HER) identifier. It is subject to validation rules that require it to be alphanumeric.\
**Validation Rules**: required, alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `meatadata.sourceID`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: The metadata.sourceID attribute serves as a critical identifier within the Heritage Gateway Record (HGR) schema. This field holds a unique identifier which correlates directly to the original source of the data. The value for this attribute is expected to match one of the predefined values from a dictionary, ensuring that each entry is consistent with a controlled vocabulary or set of identifiers that have been established prior.\
**Validation Rules**: must be one of the following predefined values: predefined dictionary\
**Acceptable Values**: Predefined dictionary

---

### Attribute: `record`
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: The record attribute is a core object in the HGR schema and is mandatory. It serves as a container for the primary data of the HGR record. The integrity and structure of this attribute are pivotal in maintaining the overall coherence and utility of the HGR system.

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
		"maritimeCraft": { ... },
		"historicAircraft": { ... },
		"relatedRecords": [ ... ],
		"relatedEvents": [ ... ],
		"compiler":{ ... },
		"typeOfRecord": "string",
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
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: It is a key attribute within the record object and is part of the CORE record structure. It is a mandatory string that holds the primary reference number for the record. The data type is a string, and it must adhere to a validation rule that restricts it to alphanumeric characters, explicitly excluding slashes and spaces. This requirement aligns with best practices for open linked data, where URIs are used, and slashes in reference numbers can complicate data management and retrieval.\
**Validation Rules**: required, alpha\
**Acceptable Values**: Numeric or alphanumeric, must not contain slash characters

---

### Attribute: `record.heritageAssetName`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the name of the heritage asset of the record and while not mandatory for all records, is a core part of the schema when included. The attribute accepts alphanumeric values, and it follows a validation rule that ensures it contains only alphabetic characters. For records where the data provider does not hold a specific name for the asset, a generated or default name should be used to maintain consistency in the dataset.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.descriptions`
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: This attribute is an essential array-type attribute that is mandatory for all records. It consists of one or more description objects that provide detailed information about the heritage asset. Each object within this array must adhere to specific structure and content requirements, ensuring comprehensive and uniform descriptions across all records.\
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
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: Within each description object, the attribute is a string that specifies the type of description, with allowable values including 'Full' and 'Summary'. This categorization facilitates the appropriate representation and interpretation of the description content.\
**Validation Rules**: required, must be one of the following predefined values: Full,Summary\
**Acceptable Values**: Full,Summary

---

### Attribute: `record.descriptions.*.description`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: It is designed to hold textual information that provides detailed narratives or explanations about the heritage asset. This field is versatile, accepting both rich text and plain text formats. Rich text can include additional formatting such as bolding, italics, bullet points, and other text structuring features, which can enhance the readability and presentation of the information. Plain text, on the other hand, is unformatted and is used for simple, straightforward descriptions without the need for additional text styling.\
**Validation Rules**: required\
**Acceptable Values**: Summary: Alphanumeric (255 characters for Summary, truncate if greater).

---

### Attribute: `record.monumentDatedTypes`
**Mandatory in HGR**: Y \
**Data Type**: Array\
**Description**: This attribute captures the historical or archaeological classification of a monument or heritage asset, linked to specific time periods. This field includes information that identifies the monument type with corresponding dates or historical periods.\
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
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: It is a string that identifies the monument type, adhering to the FISH Thesaurus of Monument Types. This attribute is crucial for categorising the heritage asset accurately, and it requires validation to ensure consistency and accuracy in the classification of assets.\
**Validation Rules**: required, alpha\
**Acceptable Values**: FISH Thesaurus of Monument Types: https://heritagedata.org/live/schemes/eh_tmt2.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.startDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the beginning of the relevant time period for the monument type. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.monumentDatedTypes.*.endDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute represents the endDate of the record. It also adheres to the ISO 8601 UTC date format (YYYY-MM-DD) and signifies the end of the heritage asset's relevant time period. The inclusion of both start and end dates, when available, offers a comprehensive temporal picture of the asset.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.monumentDatedTypes.*.period`
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: It is a string that represents the historical period of the heritage asset, aligning with the Historic England Periods. This attribute provides a broader temporal context when specific dates are not available and is vital for classifying assets into historical timelines.\
**Validation Rules**: required, alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.displayDate`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: It is a string intended to provide a human-readable date or date range, capped at a maximum of 40 alphabetic characters. This attribute enhances the user-friendliness of the record by providing a simplified date display, making it easier for non-specialists or the general public to understand the temporal context of the heritage asset.\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.monumentDatedTypes.*.material`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute details the material associated with the heritage asset. It plays a vital role in understanding the construction and preservation state of the asset.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.monumentDatedTypes.*.evidence`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: It contains evidence type related to the heritage asset.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Evidence Thesaurus: https://heritagedata.org/live/schemes/eh_evd.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.pointGeometry`
**Mandatory in HGR**: Y\
**Data Type**: Object\
**Description**: It  is responsible for storing the geographical coordinates that define the precise location of a heritage asset. This attribute encompasses a set of numerical values representing latitude and longitude (or absolute easting and norting, depending on the reference system in use), which together describe a singular point in a spatial reference system.

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
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: This attribute denotes the spatial reference system used, crucial for ensuring the geographical data's accuracy and interoperability.\
**Validation Rules**: required, must be one of the following predefined values: EPSG 27700 , WGS84\
**Acceptable Values**: Valid spatial reference system name

---

### Attribute: `record.pointGeometry.xCoordinate`
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: This attribute represents the xCoordinate of the record. Depending on the spatial reference system it either stands for latitude or easting values.\
**Validation Rules**: required, numeric

---

### Attribute: `record.pointGeometry.yCoordinate`
**Mandatory in HGR**: Y\
**Data Type**: Decimal|integer\
**Description**: This attribute represents the yCoordinate of the record. Depending on the spatial reference system it either stands for longitude or northing values.\
**Validation Rules**: required, numeric

---

### Attribute: `record.complexGeometries`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute denotes more sophisticated spatial data than a simple point location. This attribute would store information on the shape and boundaries of a heritage asset, potentially encompassing various geometric forms such as polygons, lines, or complex curves that outline the asset's physical footprint.\
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
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: This attribute specifies the type of spatial feature, such as point, line, or area, representing the asset's physical dimensions or boundaries.\
**Validation Rules**: required, must be one of the following predefined values: point, polygon, multipoint, multipolygon, collection\
**Acceptable Values**: point|polygon|multipoint|multipolygon|collection

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometryFormat`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: This attribute specifies the format of the spatial feature geometry, such as WKT (Well-Known Text) or GeoJSON, crucial for data standardisation and software compatibility.\
**Validation Rules**: required, must be one of the following predefined values: wkt, geojson\
**Acceptable Values**: wkt|geojson

---

### Attribute: `record.complexGeometries.*.referenceSystem`
**Mandatory in HGR**: nan\
**Data Type**: String\
**Description**: This attribute denotes the spatial reference system used, crucial for ensuring the geographical data's accuracy and interoperability.\
**Validation Rules**: required, must be one of the following predefined values: EPSG 27700 , WGS84

---

### Attribute: `record.complexGeometries.*.spatialFeatureGeometry`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: This attribute contains the actual spatial geometry data of the heritage asset, encoded in the specified format.\
**Validation Rules**: required, string\
**Acceptable Values**: WKT or geojson representation

---

### Attribute: `record.monumentSources`
**Mandatory in HGR**: Y\
**Data Type**: Array\
**Description**: This attribute is an array detailing the sources of information for the monument. It includes various sub-attributes like source title, authority statement, and source reference, providing a comprehensive understanding of the asset's informational background.\
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
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: This attribute represents the source title of the information.\
**Validation Rules**: required without:bibliographyFootnoteReference, alpha, max:255

---

### Attribute: `record.monumentSources.*.statementOfAuthority`
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: String\
**Description**: This attribute represents the statement of authority.\
**Validation Rules**: required without:bibliographyFootnoteReference, alpha, max:255

---

### Attribute: `record.monumentSources.*.sourceReference`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the source reference.\
**Validation Rules**: alpha, max:255

---

### Attribute: `record.monumentSources.*.dateOfOrigination`
**Mandatory in HGR**: Y (if attribute bibliographyFootnoteReference is empty)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute represents the date of origination.\
**Validation Rules**: required without:bibliographyFootnoteReference, date format:YYYY-MM-DD

---

### Attribute: `record.monumentSources.*.sourceDigitalObjectIdentifier`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the source digital object indentifier of the record.\
**Validation Rules**: url\
**Acceptable Values**: Must have text segment "doi" in URL

---

### Attribute: `record.monumentSources.*.bibliographyFootnoteReference`
**Mandatory in HGR**: Y (if attributes informationSourceTitle, statementOfAuthority, sourceReference are empty)\
**Data Type**: String\
**Description**: This attribute represents the bibliography footnote reference.\
**Validation Rules**: required without:informationSourceTitle,statementOfAuthority,sourceReference, max:255

---

### Attribute: `record.monumentSources.*.sourceURL`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the source URL.\
**Validation Rules**: url

---

### Attribute: `record.objectFinds`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This is an array-type attribute that documents any objects found in association with the heritage asset. It contains sub-attributes detailing the type of objects, their production and use dates, materials, etc.\
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
**Mandatory in HGR**: Y\
**Data Type**: string\
**Description**: It is a string that identifies the object finds type, adhering to the FISH Thesaurus of Archaeological Objects. This attribute is crucial for categorising the heritage asset accurately, and it requires validation to ensure consistency and accuracy in the classification of assets.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Archaeological Objects Thesaurus: https://heritagedata.org/live/schemes/mda_obj.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.startDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the beginning of the relevant time period for the object find. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.objectFinds.*.endDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the end of the relevant time period for the object find. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.objectFinds.*.period`
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: It is a string that represents the historical period of the heritage asset, aligning with the Historic England Periods. This attribute provides a broader temporal context when specific dates are not available and is vital for classifying assets into historical timelines.\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.objectFinds.*.displayDate`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: It is a string intended to provide a human-readable date or date range, capped at a maximum of 40 alphabetic characters. This attribute enhances the user-friendliness of the record by providing a simplified date display, making it easier for non-specialists or the general public to understand the temporal context of the heritage asset.\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.objectFinds.*.material`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute details the material associated with the object find. It plays a vital role in understanding the construction and preservation state of the asset.\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft`
**Mandatory in HGR**: N\
**Data Type**: Object\
**Description**: This attribute represents the maritimeCraft of the record.\
**Validation Rules**: No specific validation rules apply.\
**Acceptable Values**: MaritimeCraft object

```
{
	"metadata": { ... },
	"record": {
		...
		"maritimeCraft": {
			"type": "string",
			"startDate": "YYYY-MM-DD",
			"endDate": "YYYY-MM-DD",
			"period": "string",
			"displayDate": "string",
			"material": "string"
		}
		...
	}
}
```
---

### Attribute: `record.maritimeCraft.type`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: It is a string that identifies the maritime craft type, adhering to the FISH Thesaurus of Maritime Craft types.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Maritime Craft Types: https://heritagedata.org/live/schemes/eh_tmc.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft.startDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the beginning of the relevant time period for the maritime craft. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.maritimeCraft.endDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the end of the relevant time period for the maritime craft. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.maritimeCraft.period`
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: It is a string that represents the historical period of the maritime craft, aligning with the Historic England Periods. This attribute provides a broader temporal context when specific dates are not available and is vital for classifying assets into historical timelines.\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.maritimeCraft.displayDate`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: It is a string intended to provide a human-readable date or date range, capped at a maximum of 40 alphabetic characters. This attribute enhances the user-friendliness of the record by providing a simplified date display, making it easier for non-specialists or the general public to understand the temporal context of the heritage asset.\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.maritimeCraft.material`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute details the material associated with the maritime craft. It plays a vital role in understanding the construction and preservation state of the asset.\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft`
**Mandatory in HGR**: N\
**Data Type**: Object\
**Description**: This attribute represents the historicAircraft of the record.\
**Validation Rules**: No specific validation rules apply.\
**Acceptable Values**: HistoricAircraft object

```
{
	"metadata": { ... },
	"record": {
		...
		"historicAircraft": {
			"type": "string",
			"startDate": "YYYY-MM-DD",
			"endDate": "YYYY-MM-DD",
			"period": "string",
			"displayDate": "string",
			"material": "string"
		}
		...
	}
}
```
---

### Attribute: `record.historicAircraft.type`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: It is a string that identifies the historic aircraft craft type, adhering to the FISH Thesaurus of Historic Aircraft types.\
**Validation Rules**: alpha\
**Acceptable Values**: FISH Historic Aircraft Types: https://heritagedata.org/live/schemes/225.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft.startDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the beginning of the relevant time period for the maritime craft. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.historicAircraft.endDate`
**Mandatory in HGR**: Y (if attribute period is not provided, omitted if period = UNCERTAIN)\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute marks the end of the relevant time period for the maritime craft. The use of a standardised date format is vital for consistency and facilitates comparative historical analysis.\
**Validation Rules**: date format:YYYY-MM-DD, YYYY-MM, YYYY

---

### Attribute: `record.historicAircraft.period`
**Mandatory in HGR**: Y (if attribute startDate and endDate have been omitted, if 'UNCERTAIN' then attribute startDate and endDate must have been omitted)\
**Data Type**: String\
**Description**: It is a string that represents the historical period of the historical aircraft, aligning with the Historic England Periods. This attribute provides a broader temporal context when specific dates are not available and is vital for classifying assets into historical timelines.\
**Validation Rules**: alpha\
**Acceptable Values**: Historic England Periods: https://heritagedata.org/live/schemes/eh_period.html (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.historicAircraft.displayDate`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: It is a string intended to provide a human-readable date or date range, capped at a maximum of 40 alphabetic characters. This attribute enhances the user-friendliness of the record by providing a simplified date display, making it easier for non-specialists or the general public to understand the temporal context of the heritage asset.\
**Validation Rules**: alpha, max:40

---

### Attribute: `record.historicAircraft.material`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute details the material associated with the historic aircraft. It plays a vital role in understanding the construction and preservation state of the asset.\
**Validation Rules**: alpha\
**Acceptable Values**: - FISH Building Materials Thesaurus: https://heritagedata.org/live/schemes/eh_tbm.html (including narrower concepts) prefLabel or altLabel.

- Historic England Maritime Object Material: https://heritagedata.org/live/schemes/73.html
 (including narrower concepts) prefLabel or altLabel.

---

### Attribute: `record.relatedRecords`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute is an array-type that references other records related to the heritage asset. It includes sub-attributes like primary reference number, heritage asset name, description, and URL, facilitating a networked understanding of related heritage assets.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"relatedRecords": [
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

### Attribute: `record.relatedRecord.primaryReferenceNumber`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the primaryReferenceNumber of the related record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedRecord.heritageAssetName`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the heritageAssetName of the related record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedRecord.description`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the description of the related record.\
**Validation Rules**: alpha\
**Acceptable Values**: Phil to check with Jane - regarding max characters

---

### Attribute: `record.relatedRecord.url`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the url of the related record.\
**Validation Rules**: url\
**Acceptable Values**: Must be a HE gateway URL

---

### Attribute: `record.relatedEvents`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute represents an array of the related event objects for the record.\
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

### Attribute: `record.relatedEvent.primaryReferenceNumber`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the primaryReferenceNumber of the related event record.\
**Validation Rules**: alpha\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvent.name`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the name of the related event record.\
**Validation Rules**: alpha, max:100\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.relatedEvent.description`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the description of the related event record.\
**Validation Rules**: alpha\
**Acceptable Values**: Phil to check with Jane - regarding max characters

---

### Attribute: `record.relatedEvent.url`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the url of the related event record.\
**Validation Rules**: url

---

### Attribute: `record.compiler.organisationName`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the organisationName of the compiler.\
**Validation Rules**: max:100\
**Acceptable Values**: Alphanumeric

---

### Attribute: `record.typeOfRecord`
**Mandatory in HGR**: Y\
**Data Type**: String\
**Description**: This attribute represents the typeOfRecord of the record.\
**Validation Rules**: No specific validation rules apply.\
**Acceptable Values**: Default to Monument

---

### Attribute: `record.parish`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the parish of the record.\
**Validation Rules**: max:100

---

### Attribute: `record.streetMapLink`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the streetMapLink of the record.\
**Validation Rules**: url

---

### Attribute: `record.images`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute represents the images of the record.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"images": [
			{
				"url": "url",
				"caption": "string"
			}
		],
		...
	}
}
```
---

### Attribute: `record.images.*.url`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the url of the image.\
**Validation Rules**: url

---

### Attribute: `record.images.*.caption`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the caption of the image.\
**Validation Rules**: max:100

---

### Attribute: `record.protectedStatuses`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute represents the protected statuses of the record.\
**Validation Rules**: array

---

### Attribute: `record.protectedStatuses.*`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the actual protected status object.\
**Validation Rules**: alpha\
**Acceptable Values**: OASIS Protection Status: https://heritagedata.org/live/schemes/ef5ebc5b-abd6-44c5-a9d6-83a16f2b66ae.html (including narrower concepts) prefLabel or altLabel.

```
{
	"metadata": { ... },
	"record": {
		...
		"protectedStatuses": [
			{
				"description": "string",
				"url": "url"
			}
		],
		...
	}
}
```
---

### Attribute: `record.otherStatuses`
**Mandatory in HGR**: N\
**Data Type**: Array\
**Description**: This attribute represents the other statuses of the record.\
**Validation Rules**: array

```
{
	"metadata": { ... },
	"record": {
		...
		"otherStatuses": [
			{
				"description": "string",
				"url": "url"
			}
		],
		...
	}
}
```
---

### Attribute: `record.otherStatuses.*`
**Mandatory in HGR**: N\
**Data Type**: String\
**Description**: This attribute represents the actual other status object.\
**Validation Rules**: alpha

---

### Attribute: `record.lastUpdated`
**Mandatory in HGR**: Y\
**Data Type**: ISO 8601 UTC\
**Description**: This attribute represents the lastUpdated of the record.\
**Validation Rules**: required, date format:Y-m-d H:i:s
