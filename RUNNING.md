# RUNNING.md

## Running FIDO2 DEMO in GitHub Codespace

This guide explains how to set up and run the FIDO2 DEMO project in a GitHub Codespace, including IBM Verify configuration and environment setup.

---

## 1. Configure FIDO2 Settings on IBM Verify
- Log in to your IBM Verify admin console.
- Navigate to **Authentication > FIDO2 settings**.
- Create new Relying Party
  - Step 2 Device page, for POC, check Include All Device Metadata and Metadata service
  - Step 3 Allowed origins, should add your application URL (in this case, github CodeSpace Application url, can be obtained later)
- Save your changes.

## 2. Create Applications on IBM Verify
- Go to **Applications** in IBM Verify.
- Create a new [OpenID Conntection] application for FIDO2 DEMO.
  - For POC, use GCS_Themes_SignIn theme
  - Application URL: your application URL (can be obtain later)
  - Redirect URIs: for this POC, your_application_url/callback
- Note the client ID, client secret, and redirect URIs.


## 3. Change .env Settings
- In your Codespace, create or edit the `.env` file from `.env.example`.
- Set the following variables using your IBM Verify details:
  - `CI_TENANT_ENDPOINT` (IBM Verify tenant URL ex: https://asdf.sandbox.xyz)
  - `OAUTH_CLIENT_ID` (This is ADMIN API Client ID from IBM Verify **Security > API Access**)
  - `OAUTH_CLIENT_SECRET` (This is ADMIN API Client Secret)
  - `LOCAL_SSL_SERVER` false, for this POC running on GitHub CodeSpace
  - `RPID` this is Relying party identifier from **Configure FIDO2 Settings on IBM Verify**
  - `SERVER_URL` the url of your codespace running server (obtain later)
  - `OIDC_CLIENT_ID` This is Application Client ID you created from **Create Applications on IBM Verify**
  - `OIDC_CLIENT_SECRET` This is Application Client Secrete you created from **Create Applications on IBM Verify**


## 4. Install Dependencies and Start Local Server
```bash
npm install
npm run start_local
```
- The server will start and display the local URL in the terminal output.
- From GitHub Code space you should make the Port **Public**
- Go to Port tab, and copy the url ex: https://xyz-qppv4cxrq9-3000.app.github.dev
  - This url and hostname will be set in **Allow Origins** from **Configure FIDO2 Settings on IBM Verify**
  - **Application URL** and **Redirect URIs** from **Create Applications on IBM Verify**

## 5. Pick Up Codespace URL and Reset .env
- Update your `.env` file to set `SERVER_URL` with ths HOSTNAME obtained from last step.
- Restart the server if you change `.env`.

## 6. What's Working and What's Not
### Working:
- OIDC LOGIN
- ADD/REMOVE Passkey device

### Not Working / Limitations:
- Logiin with PassKey (not running yet)
- Username/password login (not tested yet)
---

For more details, see the [README.md](README.md) and IBM Verify documentation.