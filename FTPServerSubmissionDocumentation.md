# FTP Server Submission Documentation

## Version History 

Version| Description | Author 
--- | --- | --- 
1.0  | Initial version of the instructions for the FTP Server submission of the Heritage Gateway Record | Jan Putzan (Ember Technology)
1.1  | Added sFTP server url and port | Jan Putzan (Ember Technology)

## Overview

This document outlines the steps required to submit Heritage Gateway Record (HGR) compliant records to Historic England (HE) via a FTP Server provided by HE using an FTP client of your choice.

---

## Authentication

- **Host**: sftp://he-sftp.embertech.link
- **Port**: 2022
- **Credentials**: Use the username and password created during your HE portal registration.
- **Protocol**: Connect via **SFTP/FTPS** for encrypted file transfer.
- **No token required**: Unlike the API method, authentication is handled directly through your FTP credentials.

---

## Batch Creation

1. **Create a submission folder**:
   - Log into the FTP server and create a **new folder** for your submission batch.
   - Folder names are arbitrary but must be **unique** (duplicate names are not allowed).
   - Example valid folder name: `submission_batch_01`

2. **Folder restrictions**:
   - No deleting, renaming, or moving folders/files after creation
   - Only new folders and files may be created

---

## Batch Submission

1. **Upload records**:
   - Navigate to your newly created folder.
   - Upload **individual HGR records** as separate JSON files.
   - File naming convention: `<primaryReferenceNumber>.json` (e.g., `HGR-12345.json`).

2. **Finalize submission**:
   - After **all records** are uploaded, add an `index.json` file to the folder:
     ```json
     {
         "total_count": 100,
         "published_count": 50,
         "submitted_count": 10
     }
     ```
   - The `index.json` triggers the ETL - upload this **LAST**.

---

### Record Counts Explained

- **Total Count**: Total monument records in your entire dataset.
- **Published Count**: Publicly visible records in your dataset.
- **Submitted Count**: Records being uploaded in this batch.

---

## Workflow Example

1. Create folder `submission_batch_01`.
2. Upload files:
   - `HGR-12345.json`
   - `HGR-12346.json`
   - `HGR-12347.json`
3. Add `index.json` with `"submitted_count": 3`.
4. HE systems automatically process the batch at the end of the day.

## Security Requirements

1. Use **SFTP/FTPS** - plain FTP is strictly prohibited.
2. Never share credentials via email/unsecured channels.
3. Rotate passwords every 90 days (per HE security policy).
