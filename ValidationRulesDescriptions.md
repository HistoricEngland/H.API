# Validation Rules Descriptions

The Heritage Gateway Record (HGR) [schema](HeritageGatewayRecordSchema.md) specifies which validation rules will be applied to each of the HGR’s constituent attributes. These rules are described below. 

## `Required`
The `Required` rule means that the field must be present in the input data and cannot be empty. This ensures that a value for the specified field is provided and is not null or an empty string.

## `RequiredWithout`
The `RequiredWithout` rule when applied to a field specifies that the field under validation must be present and not empty only if any of the other specified fields are not present or empty in the input data.

## `String`
The `String` rule checks that the field's value is a string. This means that the value must consist of text and cannot be a number, boolean, array, or any other non-string data type.

## `Date`
The `Date` rule ensures that the field contains a valid date. The value must be a recognizable date format by the system, allowing for consistent date-related operations.

## `Url`
The `Url` rule verifies that the field's value is a valid URL. This means that the value must follow the standard URL format, including the scheme (http or https) and the domain.

## `Min`

The rule `Min` when applied to an array ensures that the array contains at least a minimum specified number of elements.

## `In`
The `In` rule checks if the field's value is within a specific set of values. This rule is used to validate that the value is one of the allowed options.

## `Array`
The `Array` rule ensures that the field's value is an array.

## `Numeric`
The `Numeric` rule verifies that the field's value is numeric. This includes integers and floating-point numbers, allowing for validation of numeric data.

## `SpatialCoordinate`
The `SpatialCoordinate` rule is specific to geographic data, ensuring that the field contains a valid set of coordinates (latitude and longitude in the WGS84 coordinate system EPSG:4326 or easting and northing in British National Grid BNG system EPSG:27700).

## `SchemeConcept`
The `SchemeConcept` rule is designed to ensure that the value provided in the field adheres to a predefined set of concepts within a specific scheme.

## `DateFormats`
The `DateFormats` rule verifies that the field's value matches one of the specified date formats. This allows for flexible date input that can accommodate multiple formats.

## `SpatialFeatureGeometry`
The `SpatialFeatureGeometry` rule validates that the field contains a geometric string|object described in either WKT (Well-Known Text) or GeoJSON format, depending on provided format.

## `DigitalObjectIdentifier`
The `DigitalObjectIdentifier` rule verifies that the field contains a valid DOI. DOIs are standardized identifiers used to uniquely identify and provide a permanent link to digital objects, such as academic publications.
