 | **Dataset Name** |	**Submission Batch ID** |	**Primary Reference Number** |	Attribute	Candidate Term Submitted	|  Scheme	| Candidate Term Status	| Preferred Term	| Status Updated |




# REJECTED Candidate Term Status Report Guidance
SchemeConcept data validation errors are reviewed by Historic England as Candidate Terms. Candidate Terms REJECTED by Historic England are reported separately for each dataset from which records failed SchemeConcept data validation . These reports contain the following information to help data providers identify the affected records and update these with the relevant Preferred Term 

## Dataset name
The name of the dataset specified at registration for which data validation errors have been logged. For example: *H&BC Historic Environment Record*
## Submission Batch ID
A unique system generated identifier for the batch of submitted records for which a SchemeConcept data validation error (i.e., a Candidate Term) was logged
## Primary Reference Number.
The unique identifier allocated to each entry in the source database and included in the corresponding records submitted for inclusion in the Heritage Gateway. The repeat of the Primary Preference Number 790001 and Primary reference Number 790005 above indicates that more than one Candidate Term has been process and rejected by HE for each of those records.
## Attribute
This indicates which attribute in the submitted record’s JSON file failed SchemeConcept data validation and has been processed by Historic England as a Candidate Term. 
### Single attribute with multiple values
All Heritage Gateway Record attributes that are subject to SchemeConcept data validation may have multiple values. 
For example, each record may include one or more protectedStatuses. The protectedStatuses values are held in a simple array in the submitted JSON file. Each element in the array is indexed; 0 (zero) indicating the first element in the array, 1 the second and so on. 
So, record.protectedStatuses.0 indicates that the first of the protectedStatuses specified for the record failed validation and has been processed by Historic England as a Candidate Term.
### Multiple attribute object, attribute with single value
In addition to simple arrays, records contain objects that have multiple constituent attributes. For example, each record may have one or more MonumentDatedType objects each comprising values for different attributes (monument type, start date, end date, period, materials etc.) that describe the different construction and use phases of the Heritage Asset. 
Again, the information for each MonumentDatedType (i.e., construction and use phase) is held in an array in the submitted JSON file. Again, each element in the array is indexed; 0 (zero) indicating the first element in the array, 1 the second and so on. This time, however, the constituent attribute that failed validation and has been processed as a Candidate Term is also specified. 
So, record.monumentDatedTypes.0.type indicates that the type (monument type) value specified for the record’s first monumentDatedTypes (i.e., construction and use phase) failed validation and has been processed as a Candidate Term.

## Multiple attribute object, attribute with multiple values
Although each monumentDatedTypes (i.e., construction and use phase) will only have one type value, other constituent attributes held in arrays may contain multiple values. For example, each monumentDatedTypes (i.e., construction and use phase) may have one or more materials (building material) values recorded or similarly one or more different evidences (types of evidence) values recorded. These instances of multiple values are handled by nested arrays indexed in the same manner as above.
Thus, record.monumentDatedTypes.0.materials.1 indicates that second materials (building materials) listed for the record’s first monumentDatedTypes (i.e., construction and use phase) has failed validation and has been processed as a Candidate Term.
Similarly, record.monumentDatedTypes.2.evidences.0 indicates that the first evidences type cited for the third monumentDatedTypes (i.e., construction and use phase) has failed validation and has been processed as a Candidate Term.
## Candidate Term Submitted
The value submitted that failed SchemeConcept data validation and has been processed by Historic England as a Candidate Term
## Scheme
The name of the controlled vocabulary or thesaurus against which records are validated.
## Candidate Term Status
Candidate Terms that have been processed and rejected by Historic England are logged with the status of rejected and a Preferred Term indicated (see below)
## Preferred Term
Where a Candidate Term has been rejected, a Preferred Term existing in the relevant scheme (e.g. monument types thesaurus) is recommended to index the record. 
## Status Updated
The date and time that the Candidate Term’s status was confirmed by Historic England.

