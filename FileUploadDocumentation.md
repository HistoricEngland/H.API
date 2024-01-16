
# Direct API Submission Documentation

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the API for the submission of the Heritage Gateway File | Jan Putzan (Ember Technology)
1.1  | Addition of the dataset creation endpoint | Jan Putzan (Ember Technology)
1.2  | Addition of Swagger API documentation  | Jan Putzan (Ember Technology)


## Overview

This document outlines the steps required to submit files to our service using OAuth authentication into the Heritage Gateway.

## Authentication

### Obtaining an Access Token

- **Endpoint**: `https://api.example.com/oauth/token`
- **Method**: `POST`
- **Headers**: 
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "username": "your_username",
    "password": "your_password"
  }
  ```
- **Response**: A JSON object containing the `access_token` required for file upload.
  ```json
  {
    "access_token": "YOUR_ACCESS_TOKEN",
    "token_type": "Bearer",
    "expires_in": 3600
  }
  ```

## Dataset Creation

To initiate the file upload process, begin by generating a new dataset. This is achieved by submitting the current counts of monument records to the designated endpoint. Upon successful creation, the system will return a unique DATASET_ID. This DATASET_ID must be included in all subsequent API requests related to the current batch, whether you are performing single file uploads or bulk uploads. Note that for each new batch of files, a fresh DATASET_ID is required. This necessitates the resubmission of the latest monument record counts to generate a new ID. Ensure that the counts are updated accurately with each new batch submission.

### Creating a New Dataset

- **Endpoint**: `https://api.example.com/api/dataset/create`
- **Method**: `POST`
- **Headers**:
  - `Authorization: Bearer YOUR_ACCESS_TOKEN`
  - `Content-Type: application/json`
- **Body**:
  ```json
  {
    "total_count": integer,
    "published_count": integer,
    "submitted_count": integer
  }
  ```
- **Response** A JSON object containing the `dataset_id` required for file upload.
  ```json
  {
    "dataset_id": "DATASET_ID"
  }
  ```

## File Upload

### Uploading Files

- **Endpoint**: `https://api.example.com/dataset/upload`
- **Method**: `POST`
- **Headers**: 
  - `Authorization: Bearer YOUR_ACCESS_TOKEN`
  - `Content-Type: multipart/form-data`
- **Body**:
```json
  {
    "dataset_id": "DATASET_ID"
  }
  ```
  - Include an array of files in the request as form-data.

### Steps

1. Obtain an access token from the OAuth endpoint.
2. Construct a POST request to the dataset creation endpoint with the appropriate headers and dataset details.
3. Process the API's response to retrieve the DATASET_ID for the newly created dataset.
4. Prepare the file for upload according to the API's specifications.
5. Construct a POST request to the file upload endpoint with the appropriate headers, DATASET_ID and file data.
6. Process the API's response to determine the success or failure of the upload.

### Examples of cURL Commands

```bash
curl -X POST https://api.example.com/oauth/token \
  -H "Content-Type: application/json" \
  -d '{"username": "your_username","password": "your_password"}'
```

```bash
curl -X POST https://api.example.com/api/dataset/create \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"total_count": 100, "published_count": 50, "submitted_count": 30}'
```

```bash
curl -X POST https://api.example.com/api/dataset/upload \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: multipart/form-data" \
  -d '{"dataset_id": DATASET_ID}' \
  -F "files[]=@path_to_your_first_file" \
  -F "files[]=@path_to_your_second_file" \
  ...
  -F "files[]=@path_to_your_last_file"

```

## Error Handling

- **401 Unauthorized**: Your access token is invalid or expired.
- **400 Bad Request**: The request is improperly formatted.
- **413 Payload Too Large**: The file size exceeds the allowed limit.
- **500 Internal Server Error**: An unexpected error occurred on the server.

## Swagger API documentation

https://hapi-platform-staging.embertech.link/api/documentation

## Security Notes

- Securely store your access tokens and credentials.
- Communicate over HTTPS to protect the data in transit.

## Support

For support, contact `support@ember.ltd`.
