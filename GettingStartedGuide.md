# H.API Getting started Guide

Three distinct options are available to data providers for their submission of Heritage Gateway Record (HGR) standard compliant records to Historic England (HE) for validation and inclusion in the Heritage Gateway. Offering these three approaches allows for differing levels of technical input on the part of the data provider. These three options are:

## 1. Direct API Submission

The first approach, Direct API Submission, requires some technical input on the data provider's side to write an integration that will submit HGR standard compliant records directly to HE through a RESTFul API provided by HE. This push approach, managed by the data provider, allows for HGR standard compliant records to be submitted to HE from any system.

## 2.External API Harvesting

The second approach, External API Harvesting, operates as an automated retrieval process, with HE pulling data providers’ HGR compliant records at scheduled intervals. This method requires the data provider to give HE access to an API which we can use to fetch HGR compliant records on an agreed schedule. If you have such an API available already then all you need to do is send us details of that API.

## 3. FTP Server Access for File Uploads

The third approach, FTP Server Access, offers a more traditional route, resembling a familiar file-sharing system. Here, data providers can upload data files with HGR compliant records onto HE’s Heritage Gateway FTP server periodically. It’s a simple and effective means for data submission and can be done either manually or by developing functionality into your existing system to send the HGR standard compliant data automatically at scheduled intervals.

Together, these varied approaches cater to diverse user preferences and provide options for an easy submission of HGR standard compliant records to HE.

### 1. Direct API Submission Instructions:

#### Access the Historic England API Documentation:
+	Review the [HE API documentation](DirectAPISubmissionDocumentation.md).

#### Obtain Access Credentials:
+	Contact HE’s Heritage Gateway support team to acquire your access credentials via heritagegateway@HistoricEngland.org.uk 
+	Follow the outlined procedure to authenticate and obtain an access token required for the data submission.

#### Prepare Your Data:
+	Organise your data into a submission batch according to the API documentation.
+	Ensure your data structure aligns with the [schema](HGRSchemaDocumentation.md).

#### Submit Your Data:
+	Use tools like cURL or Postman to interact with the HE Heritage Gateway API endpoints.
+	Authenticate using the obtained access token and follow the documented steps to submit your prepared data.

#### Verify Submission:
+	Check the HE Heritage Gateway API response for confirmation of the successful submission.

### 2. External API Harvesting Instructions:

**Detail TBC**

### 3. FTP Server Access for File Uploads Instructions:

#### Access the HE Heritage Gateway FTP Server:
+	Detail TBC

#### Prepare Your Data Files:
+	Organise your data (detail TBC)
+	Ensure your data structure aligns with the [schema](HGRSchemaDocumentation.md).

#### Upload Your Data:
+	Open your FTP client and enter the server details (host, username, password) to establish a connection.
+	Navigate to the designated folder or directory and upload your prepared data files using the FTP client interface.

#### Confirmation and Monitoring:
+	Verify successful file uploads by checking the uploaded files' presence in the specified folder on the server.
+	Monitor the upload process periodically to ensure continuous and error-free submission of data files.
