# New Heritage Gateway - Overview 

Welcome to the Historic England API (H.API) project, designed to facilitate access to national and local heritage information datasets, including [Historic Environment Records](https://historicengland.org.uk/advice/technical-advice/information-management/hers/) (HERS). 

The project will replace the [current Heritage Gateway](https://www.heritagegateway.org.uk/gateway/) (which is now 15 years old and fails accessibility and cyber essential standards), with a system that ensures users experience reliable and consistent search results. The new Gateway’s user interface will comprise of redesigned search and results display pages on the Historic England website.

Central to the design of a replacement Heritage Gateway is the consolidation of summary data from various providers into a single, searchable GraphDB data store that supports [linked data](https://www.w3.org/wiki/LinkedData) principles and is to be managed by HE. The minimum attributes comprising a CORE Heritage Gateway Record (HGR) have been defined along with additional OPTIONAL attributes. Both sets of attributes have in turn been mapped to the [International Committee for Documentation Conceptual Reference Model](https://cidoc-crm.org/) (CIDOC CRM).  

Data for inclusion in the Heritage Gateway will be made available by providers on a regular update schedule via one of three available [data submission options](DataSubmissionOptions.md):  Direct API Submission, External API Harvesting or FTP Server Access. These will be validated against the core HGR. Valid records will be converted to [Resource Description Framework](https://www.w3.org/RDF/) (RDF) triples/quads conforming to a CIDOC CRM based RDF schema, then imported to the GraphDB RDF triple store. Invalid records will be logged and reported to the relevant data provider. HE will manage this process in close liaison with the data providers. 

The envisaged overall Extract, Transform and Load (ETL) process flow and components is depicted below: 

![image](https://github.com/ember-technology-ltd/H.API/assets/86000238/da935d03-7c5b-46b4-aba9-c71de88df217)

Please visit the [Data Submission Options](DataSubmissionOptions.md) guide for more details on how data providers can submit data for validation and inclusion in the New Heritage Gateway.

For further information or assistance please contact: heritagegateway@HistoricEngland.org.uk
