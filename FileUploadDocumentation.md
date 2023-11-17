
# File Upload API Documentation

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the API for the submission of the Heritage Gateway File | Jan Putzan (Ember Technology)


## Overview

Historic Environment Records (sometimes referred to as Sites and Monuments Records) may be held by County Councils, District Councils or Unitary Authorities. In each case, the record will cover the whole of the local authority area. Selected major historic towns and cities are covered by Urban Archaeological Databases (UADs). In many cases, UADs are held as part of, and are accessible via, the local Historic Environment Record.

This document outlines the steps required to upload files to our service using OAuth authentication into the Heritage Gateway.

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

## File Upload

### Uploading a File

- **Endpoint**: `https://api.example.com/upload`
- **Method**: `POST`
- **Headers**: 
  - `Authorization: Bearer YOUR_ACCESS_TOKEN`
  - `Content-Type: multipart/form-data`
- **Body**: Include the file in the request as form-data.

### Steps

1. Obtain an access token from the OAuth endpoint.
2. Prepare the file for upload according to the API's specifications.
3. Construct a POST request to the file upload endpoint with the appropriate headers and file data.
4. Process the API's response to determine the success or failure of the upload.

### Example cURL Command

```bash
curl -X POST https://api.example.com/upload   -H "Authorization: Bearer YOUR_ACCESS_TOKEN"   -H "Content-Type: multipart/form-data"   -F "file=@path_to_your_file"
```

## Error Handling

- **401 Unauthorized**: Your access token is invalid or expired.
- **400 Bad Request**: The request is improperly formatted.
- **413 Payload Too Large**: The file size exceeds the allowed limit.
- **500 Internal Server Error**: An unexpected error occurred on the server.

## Security Notes

- Securely store your access tokens and credentials.
- Communicate over HTTPS to protect the data in transit.

## Support

For support, contact `support@ember.ltd`.
