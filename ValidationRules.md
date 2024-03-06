# Validation Rules Explanation

## `required`
The `required` rule means that the field must be present in the input data and cannot be empty. This ensures that a value for the specified field is provided and is not null or an empty string.

## `string`
The `string` rule checks that the field's value is a string. This means that the value must consist of text and cannot be a number, boolean, array, or any other non-string data type.

## `date`
The `date` rule ensures that the field contains a valid date. The value must be a recognizable date format by the system, allowing for consistent date-related operations.

## `url`
The `url` rule verifies that the field's value is a valid URL. This means that the value must follow the standard URL format, including the scheme (http or https) and the domain.

## `in`
The `in` rule checks if the field's value is within a specific set of values. This rule is used to validate that the value is one of the allowed options.

## `array`
The `array` rule ensures that the field's value is an array. This is useful for validating fields that are expected to contain multiple values or a list of items.

## `numeric`
The `numeric` rule verifies that the field's value is numeric. This includes integers and floating-point numbers, allowing for validation of numeric data.

## `coordinates_4326`
The `coordinates_4326` rule is specific to geographic data, ensuring that the field contains a valid set of coordinates (latitude and longitude) in the WGS84 coordinate system (EPSG:4326). This system is commonly used for global positioning.

## `coordinates_27700`
Similar to `coordinates_4326`, the `coordinates_27700` rule validates that the field contains a valid set of coordinates, but in the British National Grid (BNG) system (EPSG:27700), which is specific to mapping in Great Britain.

## `file`
The `file` rule checks that the field contains a file. This validation is useful for ensuring that an upload input contains an actual file.

## `json_file`
The `json_file` rule ensures that the uploaded file is a JSON file. This includes checking the file format and potentially validating the JSON structure within the file.

## `scheme_concept`
The `scheme_concept` rule is designed to ensure that the value provided in the field adheres to a predefined set of concepts within a specific scheme.

## `date_formats`
The `date_formats` rule verifies that the field's value matches one of the specified date formats. This allows for flexible date input that can accommodate multiple formats.

## `wkt`
The `wkt` (Well-Known Text) rule validates that the field contains a geometric object described in the WKT format, which is a text markup language for representing vector geometry objects.

## `geojson`
The `geojson` rule ensures that the field contains a valid GeoJSON object. GeoJSON is a format for encoding a variety of geographic data structures.

## `date_within_period`
The `date_within_period` rule checks that the date provided falls within a specified period. This can be useful for ensuring that dates are within acceptable ranges for events or data collection periods.

## `required_date_without_period`
This rule seems to ensure that a date is provided and is valid, even if no specific period is set for it. It combines the requirements of being a date and being required.

## `doi`
The `doi` (Digital Object Identifier) rule verifies that the field contains a valid DOI. DOIs are standardized identifiers used to uniquely identify and provide a permanent link to digital objects, such as academic publications.
