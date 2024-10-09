# Joining the new Heritage Gateway: information for Data Providers (August 2024) 

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the Joining Instructions | Jane Golding (Historic England)

Welcome to the Heritage Gateway. This short guide takes you through each step to join the Heritage Gateway. 


## Background 

The Heritage Gateway is managed by Historic England in partnership with ALGAO and IHBC. A key objective of this partnership is to provide integrated access to local and national historic environment information resources under the [Heritage Information Access Simplified](https://historicengland.org.uk/research/support-and-collaboration/heritage-information-access-simplified/strategic-background-to-hias/) (HIAS) strategy. We are replacing the current website, now 15 years old, to improve user experience and to meet present-day accessibility and cyber essential standards. 

Data you provide to the new Heritage Gateway will be uploaded to a GraphDB data store before being published to the Heritage Gateway user interface on the Historic England website. Making this change to the Heritage Gateway standardises the data, giving the end user consistent results to search requests. 

We expect to make a beta release of the new Heritage Gateway website in Spring 2025. To prepare, we will assist all current data providers to onboard their datasets to the new Heritage Gateway datastore during the preceding year. This will not change your data service to the existing Heritage Gateway which will continue running in parallel until later next year. 

Historic England does not charge for providing and maintaining the Heritage Gateway. We will fund your implementation costs involved in making a transition to the new site. 

  

## Step 1. Get Ready - Expression of Interest 

During July and August 2024, you should have received an invitation to express interest to join the new Heritage Gateway. If you have not received an invitation or have not yet responded, please get in touch by emailing heritagegateway@historicengland.org.uk  or by completing this [short form](https://forms.office.com/Pages/ResponsePage.aspx?id=RG4RMHlNwESowevAcH2jyZ84nmPTxHdKmvyWkQpA5jpURE5SWDBLNlpSWE5GRDY2M0tVNFdIUjlXSi4u).  

We will ask you when and how you would like to onboard your data to the new Heritage Gateway. This will help us create a schedule to onboard all data providers. 

Three [Data Submission Options](DataSubmissionOptions.md) are available to submit your records to the Heritage Gateway: 

1.  You can push your data to the Heritage Gateway through a RESTful API provided by Historic England **(Direct API Submission)**. Interfaces are being written for Arches and HEROS software systems for this option.

2.  You can give us access to an endpoint of an API we can call to pull your records at scheduled intervals **(External API Harvesting)**. The HBSMR API 2.0 Gateway Service supplied by Idox is utilising this option.

3.  You can upload data files periodically onto an FTP server we provide **(FTP Server Access for File Uploads)**.  

 

The method best suiting your circumstance will depend on factors, such as, the level of in-house IT support you can call on and if you use a third-party service. 

We are supporting the implementation of API services by third-party suppliers (see under options one and two above) who will be able to handle the new process for you.  

Records submitted for validation and inclusion in the Heritage Gateway must be compliant with the Heritage Gateway Record (HGR) schema. Under options one and three, we can help you map your data to the schema. 

You can read more about the background to the redevelopment work and the different methods made available for data supply here.  

Please do contact us at this point to talk through any queries. Once you are happy to proceed, we will send you an invitation to join. 

 

## Step 2. Invitation to Join 

We will send you an email ahead of your actual joining date that will: 

Confirm the date agreed to start your joining process 

Give details of your funding offer. We will request financial information that will allow us to raise a purchase order for you to return a corresponding invoice. 

Contain a link to your Content Provision Agreement (CPA) for reading and signing. The areas that have been updated in this revised CPA will be highlighted to assist with understanding the changes. 

Once you have accepted your funding offer and returned a matching quotation, together with a copy of your signed CPA, we will send you a link to register to submit your data. 

 

## Step 3. Register to Submit Data to the Heritage Gateway 

Registration to submit data is via a secure online form and we will send you a link. To complete your registration, you will need the following information to hand: 

- Dataset name (the formal name of the heritage dataset from which you wish to submit records to the Heritage Gateway. A separate registration is required for each dataset). 

- Technical contact email address (the principal point of contact within your organisation or IT contact for queries and issues related to technical aspects of your data and their submission to Historic England).  

- Data contact email address (the principal point of contact for data content queries and issues, and for receipt of data validation error reports). 

- Your selected data submission method and as applicable:

  - A username and password that will allow you access to the RESTful API provided by Historic England
  - A username and password that will allow you access to Historic England's FTP server 
  - An API endpoint, username and password to provide Historic England with secure access to your API

 

## Step 4. Registration Request Confirmation 

When your registration request has been accepted, we will notify the email contacts. 

You will then be ready to start submitting your first batch of data! 

 

## Step 5. First Data Batch Submission 

See the [Data Submission Options](DataSubmissionOptions.md) for details of how to verify the success of your data submission. 

 

## Step 6. Record Validation and Error Logs 

Records submitted for validation and inclusion in the Heritage Gateway must be compliant with the Heritage Gateway Record (HGR) [schema](HeritageGatewayRecordSchemaDocumentation.md). 

[Validation rules](DataValidationRulesDescriptions.md) are specified for each attribute comprising the Heritage Gateway Record (HGR). Submitted records that do not comply, will be identified as data validation errors. A log of data validation errors identified for each batch of records submitted will be emailed to the data contact specified at registration. These logs will include information to aid identification and rectification of errors in the source data. Guidance on the information contained in the error log report can be found [here](DataValidationErrorReportGuidance.md). 

You will be notified separately of the acceptance or rejection of any Candidate Terms arising from SchemeConcept validation errors identified in your data batch submission. 

## Step 7. Candidate Term Approval. 

Submitted data values that have failed SchemeConcept validation and are reviewed by Historic England as Candidate Terms on behalf of the [FISH Terminology Working Group](https://heritage-standards.org.uk/working-groups/). A Candidate Term is a term (e.g. “Ice cream factory”) that has been used locally in a dataset (e.g. Westshire HER) but has not yet been incorporated into the relevant scheme (e.g. the [FISH Thesaurus of Monument Types](https://heritagedata.org/live/schemes/eh_tmt2.html) ). More information on controlled vocabularies, the FISH thesauri and Candidate Terms is documented [here](https://heritage-standards.org.uk/terminology/). 

Candidate Terms REJECTED by Historic England will be reported directly to your data contact specified at registration. The reports will contain information to help you identify the affected records and update these with the relevant Preferred Term. Once updated, the records will resubmit in your next data batch. Guidance on the information contained in the report can be found [here](RejectedCandidateTermStatusReportGuidance.md)  

 

Records where the Candidate Term is ACCEPTED (and have no other validation errors) are automatically re-submitted to the Heritage Gateway by Historic England. ACCEPTED terms will be reported to all data providers. Guidance on the information contained in the report can be found [here](AcceptedCandidateTermStatusReportGuidance.md) 

 

If you have any queries about Candidate Terms, please contact terminologies@historicengland.org.uk  

 

## Step 8. New and Updated Record Batch Submissions 

Each subsequent batch should exclusively contain records that have either been newly created or updated since the submission of the previous batch. Details of how to initiate batch submission according to your chosen data submission method can be found [here](DataSubmissionOptions.md). 

 

 

Thank you for participating in the Heritage Gateway. If you have any questions, please do not hesitate to email the Heritage Gateway inbox at heritagegateway@historicengland.org.uk .  

 

Best regards,  

The Heritage Gateway Team 
