# Data Submission Options

Three options are available to data providers for their submission of Heritage Gateway Record (HGR) standard compliant records to Historic England (HE) for validation and inclusion in the Heritage Gateway. These three approaches allow for differing levels of technical input on the part of the data provider. To maintain the integrity and relevance of the data received, it is critical that each submitted batch solely comprises records that are either newly created or have been updated following the last submission. By adhering to this practice, data providers ensure that all information added to the Heritage Gateway is current, reducing unnecessary duplication and emphasizing the latest developments or contributions.

The three data submission options:

- Direct API Submission
- External API Harvesting
- FTP Server Access for File Uploads

are outlined below:

## 1. Direct API Submission

Direct API Submission requires the data provider to write an integration that will submit HGR compliant [JSON](https://www.json.org/json-en.html) files directly to HE through a RESTFul API provided by HE. A separate JSON file generated from the datasets maintained by a provider is required for each monument record in the provider’s datasets. These files must conform to the HGR standards as defined in the [schema documentation](HGRSchemaDocumentation.md) which will involve mapping providers’ current data to the HGR schema. This push approach, managed by the data provider, allows for HGR standard compliant records to be submitted to HE from any system.

## 2.External API Harvesting

External API Harvesting, operates as an automated retrieval process, with HE pulling data providers’ HGR compliant records at scheduled intervals. This method requires the data provider to give HE access to an API with an endpoint that EH can call and which will return HGR compliant JSON records on an agreed schedule. If you have such an API available already then all you need to do is provide us with the details.

## 3. FTP Server Access for File Uploads

The third approach, FTP Server Access, offers a more traditional route, resembling a familiar file-sharing system. Here, data providers can upload data files with HGR compliant records onto HE’s Heritage Gateway FTP server periodically. It’s a simple and effective means for data submission and can be done either manually or by developing functionality into your existing system to send the HGR standard compliant data automatically at scheduled intervals. As with the Direct API Submission option, HGR compliant JSON files will need to be generated from the datasets maintained by a provider with a separate JSON file required for each monument record.

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

#### Provide API details
+ Contact HE’s Heritage Gateway support team via heritagegateway@HistoricEngland.org.uk to provide URL of the API endpoint and the frequency of data gathering.

#### Prepare Your Data
+ Ensure your data structure aligns with the [schema](HGRSchemaDocumentation.md).

#### API Preparation Guidelines
+ Ensure your API supports a paginated retrieval of compliant HGR records and allows `page` and `per_page` parameters within the request structure to facilitate efficient data navigation and extraction.
+ Ensure your API supports an `updated_since` query parameter, allowing for the refinement of result sets based on the temporal attribute indicating the last modification timestamp. The ETL process operates on the assumption that only new/updated records are submitted.
+ Your API's response payload should include a `metadata` object, detailing the counts of monument records (`total_count`, `published_count`, `submitted_count`). This should dynamically adjust in accordance with the `updated_since` parameter, providing a granular view of the dataset's state over time.

#### Monitoring and Error Handling
+ Implement a monitoring strategy for your API, prioritizing the assurance of uninterrupted and faultless data transmission processes. This involves real-time surveillance of API performance metrics and operational health indicators.
+ Implement the error handling mechanism by providing detailed and informative error messages upon request failures.

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
