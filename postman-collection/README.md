# 📬 Spotify Integration Testing - Postman Collection

This directory contains the Postman collection and environment variables designed to test and validate Spotify's Web API integration flows using the **OAuth 2.0 Client Credentials Flow**.

## 🛠️ Features Included (Senior Level QA)

- **Automated Handshake:** The authorization request automatically captures the short-lived `access_token` and updates the environment variables dynamically.
- **Data Persistence & Chaining:** Responses from sequential endpoints (User Profile and Search) are parsed to store IDs (`userId`, `lastTrackId`) and feed them into dependent requests (`Create Playlist`, `Add Track`).
- **Contract Testing (JSON Schema Validation):** Uses embedded validation libraries to ensure the backend payload strictly adheres to Spotify's technical contract specifications.
- **Robustness & Negative Tests:** Includes security edge-case scenarios validating exact `401 Unauthorized` structures when no authorization headers are present.
- **Automated Teardown:** Features a Cleanup request using a `DELETE` implementation to automatically unfollow and remove generated test metadata from the active account.

---

## 🚀 How to Import and Run this Collection

To run these tests locally on your Postman desktop client or CLI (Newman), follow these architectural steps:

### 1. Import Files into Postman

1. Download or clone this repository.
2. Open Postman and click on the **Import** button (top left).
3. Drag and drop both files located in this folder:
   - `spotify-api-playwright-postman.postman_collection.json`
   - `spotify-Dev.postman_environment.json`

### 2. Configure Environment Secrets (Security Check)

For strict security standards, real API credentials have been omitted from the shared environment parameters. You must provision your local workspace manually:

1. Ensure the `spotify-Dev` environment is active in the top-right dropdown.
2. Click the **Environment Quick Look** (eye icon).
3. Insert your Spotify Developer application keys **ONLY inside the `Value` (Current Value) column** to prevent accidental credential leakage to remote repositories:
   - `clientId` -> _Your Spotify Client ID_
   - `clientSecret` -> _Your Spotify Client Secret_
4. Leave `accessToken`, `userId`, and `currentPlaylistId` blank; the pre-request and testing scripts will populate them dynamically.

### 3. Execution Flow

1. Execute the `Auth - Get Token` request first. Ensure it returns a `200 OK` status and updates your local variables grid.
2. Open the **Collection Runner** by selecting the collection root and clicking **Run**.
3. Click **Run spotify-api-playwright-postman** to trigger the end-to-end cascading validation flow.
