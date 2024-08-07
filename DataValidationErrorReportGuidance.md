# Data Validation Error Report Guidance

Validation rules are specified for each attribute comprising the Heritage Gateway Record. Non-compliance with these rules, in records submitted for inclusion in the Heritage Gateway, results in the identification of data validation errors.
A log of data validation errors identified for each batch of records submitted for inclusion in the Heritage Gateway is emailed to the data contact specified at registration for your organisation.
The data validation error logs include the following information to aid identification and rectification of errors in the source data:

## Error ID
A unique system generated identifier for each data validation error which has been logged.

## Dataset Name
The name of the dataset specified at registration for which data validation errors have been logged. For example: *H&BC Historic Environment Record*

## Submission Batch ID
A unique system generated identifier for the batch of submitted records for which data validation errors have been logged

## Primary Reference Number
The unique identifier allocated to each entry in the source database and included in the corresponding records submitted for inclusion in the Heritage Gateway.

## Attribute
This indicates which attribute in the submitted record’s JSON file has failed validation 

### Single attribute object with one value
Some Heritage Gateway Record attributes have a single value.
For example, **record.primaryReferenceNumber** indicates that the value submitted for the record’s primary reference number attribute  has failed validation.
Similarly, **record.pointGeometry.referenceSystem** indicates that the reference system specified for the record’s point geometry has failed validation

### Single attribute with multiple values
Submitted records also contain multiple values for certain attributes. 
For example, each record may include one or more **protectedStatuses**. The **protectedStatuses** values are held in a simple array in the submitted JSON file. Each element in the array is indexed; 0 (zero) indicating the first element in the array, 1 the second and so on.

Thus, **record.protectedStatuses.0** indicates that the *first* of the **protectedStatuses** specified for the record failed validation; **record.protectedStatuses.1** would indicate that that the *second* of the **protectedStatuses** specified for the record failed validation and so on.

### Multiple attribute object, attribute with single value
In addition to simple arrays, records contain objects that have multiple constituent attributes. For example, each record may have one or more **monumentDatedType** objects each comprising values for different attributes (monument type, start date, end date, period, materials etc.) that describe the different construction and use phases of the Heritage Asset.

Again,the information for each **monumentDatedType** (i.e., construction and use phase) is held in an array in the submitted JSON file. Each element in the array is indexed; 0 (zero) indicating the first element in the array, 1 the second and so on. This time however, the constituent attribute that failed the validation is also specified. 

So, **record.monumentDatedTypes.0.type** indicates that the type (monument type) value specified for the record’s first **monumentDatedTypes** (i.e., construction and use phase) has failed validation.

Similarly **record.monumentDatedTypes.1.startDate** indicates that the startDate specified for the record’s second **monumentDatedTypes** (i.e., construction and use phase) has failed validation.

### Multiple attribute object, attribute with multiple values

Although each **monumentDatedTypes** (i.e., construction and use phase) will only have one type value, other constituent attributes held in arrays may contain multiple values. For example, each **monumentDatedTypes** (i.e., construction and use phase) may have one or more **materials** (building material) values recorded or similarly one or more different **evidences** (types of evidence) values recorded. These instances of multiple values are handled by nested arrays indexed in the same manner as above.

Thus, **record.monumentDatedTypes.0.materials.1** indicates that second **materials** (building materials) listed for the record’s first **monumentDatedTypes** (i.e., construction and use phase) has failed validation.

Similarly, **record.monumentDatedTypes.2.evidences.0** indicates that the first **evidences** type cited for the third **monumentDatedTypes** (i.e., construction and use phase) has failed validation.

## Error Type
The type of validation rule which has been breached. For example, *Required* i.e. the attribute must be present in the submitted data and cannot be empty

## Value
The data value submitted. For example: FIBRE CEMENT SLATE; E263; 10-20016 

## Error Message
A description of the error identified. For example, *“the type field must be a valid concept for MONUMENT_TYPE”*

## Candidate Term
This column records submitted data values that have failed SchemeConcept validation and are reviewed by Historic England as *Candidate Terms* on behalf of the [FISH Terminology Working Group](https://heritage-standards.org.uk/working-groups/). A *Candidate Term* is a term (e.g. “Ice cream factory”) that has been used locally in a dataset (e.g. Westshire HER) but has not yet been incorporated into the relevant scheme (e.g. monument types thesaurus). More information on controlled vocabularies, the FISH thesauri and Candidate Terms is documented [here](https://heritage-standards.org.uk/terminology/).

## Candidate Term Status
The initial status of all *Candidate Terms* is *pending* (i.e., pending Historic England’s review of the term). Candidate Terms identified in the submission batch that have previously been reviewed and rejected by Historic England will be logged with the status of *rejected* and a *Preferred Term* indicated (see below)

## Preferred Term
Where a *Candidate Term* has been rejected, a *Preferred Term* existing in the relevant scheme (e.g. monument types thesaurus) will be recommended to index the record. A *Preferred Term* is a term that has been chosen to represent the concept being indexed. 

## Reported at
The date and time that the error was logged.
