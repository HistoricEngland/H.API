# Historic England API (H.API) Documentation

# Overview
Welcome to the Historic England API (H.API) project, designed to facilitate access to national and local heritage information datasets, including Historic Environment Records (HERs) https://historicengland.org.uk/advice/technical-advice/information-management/hers/. 

The project will replace the current Heritage Gateway (https://www.heritagegateway.org.uk/gateway/), which is now 15 years old and fails accessibility and cyber essential standards, with a system that ensures users experience reliable and consistent search results. The new Gateway’s user interface will comprise redesigned search and results display pages on the Historic England website.

Central to the design of a replacement Heritage Gateway is the consolidation of summary data from various providers into a single, searchable GraphDB data store which supports linked open data (LOD) standards and is to be managed by HE. The minimum units of information comprising a core Heritage Gateway Record (HGR) have been defined along with additional optional units. Both sets of units have in turn been mapped to the International Committee for Documentation Conceptual Reference Model (CIDOC CRM).  

Data for inclusion in the Heritage Gateway will be made available by providers on a regular update schedule via a published API or export file. These will be validated against the core HGR. Valid records will be converted to Resource Description Framework (RDF) triples/quads conforming to a CIDOC CRM based RDF schema, then imported to the GraphDB RDF triple store. Invalid records will be logged and reported to the relevant data provider. HE will manage this process in close liaison with the data providers. 

The envisaged overall Extract, Transform and Load (ETL) process flow and components is depicted below: 

![image](https://github.com/ember-technology-ltd/H.API/assets/86000238/da935d03-7c5b-46b4-aba9-c71de88df217)


# Accessing Heritage Gateway Record Submission
This API enables the submission of Heritage Gateway Records (HGRs). Below are the key components and resources available for integration:

1. File Upload API Documentation
File: [File Upload API Documentation](FileUploadDocumentation.md)
Description: Details on accessing the web service used for submitting Heritage Gateway Records.
2. HGR Schema Documentation
File: [HGR Schema Documentation](HGRSchemaDocumentation.md)
Description: Technical documentation outlining the required format and structure of the Heritage Gateway Record for submission via the web service.
3. Example JSON Record of HGR Schema
File: [HGR shema in JSON format](HeritageGatewayRecord.json)
Description: An example JSON record demonstrating the structure and content expected for the Heritage Gateway Record, aligned with the specified schema.

# Usage Instructions

To interact with the Historic England API and submit Heritage Gateway Records, follow these steps:

1) Review Documentation: Study the provided documentation to understand the API endpoints and the structure of the data required for submission.
2) Access API Endpoints: Utilize the File Upload API to submit Heritage Gateway Records to the Historic England system.
3) Ensure Data Format: Prepare HGR data in accordance with the defined schema outlined in the HGR Schema Documentation.
4) Testing & Validation: Test the submission process using the provided example JSON record to ensure compatibility and proper handling.
5) Error Handling: Implement error handling mechanisms as described in the API documentation to manage any issues during data submission.
6) Feedback & Support: Reach out to the Historic England support team for any assistance or inquiries regarding API integration or data submission.

Additional Resources
For further information or assistance, refer to the following resources:

Historic England Website: https://historicengland.org.uk/
Support and Contact Information: 

