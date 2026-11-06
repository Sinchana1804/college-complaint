# CampusCare — Render-ready College Complaint Management System

## Deploy to GitHub and Render (manual setup)

1. Extract this ZIP. The `node_modules` folder is intentionally excluded.
2. Create a GitHub repository and upload/commit all files from this folder (including `render.yaml`). Do not upload `.env` or runtime `data/*.json`.
3. In Render, choose **New + → Blueprint** and connect the GitHub repository. Render reads `render.yaml`.
4. When prompted for `ADMIN_PASSWORD` (marked `sync: false`), enter a strong password. The service receives a generated `SESSION_SECRET`.
5. Deploy. Open the service URL. Admin login is the value of `ADMIN_EMAIL` (default `admin@college.edu`) and the password you entered.
6. Students use **Create account** to register.

### If creating a Render Web Service manually
- Runtime: **Node**
- Root Directory: leave blank (repository root)
- Build Command: `npm install`
- Start Command: `npm start`
- Environment variables: `NODE_ENV=production`, `SESSION_SECRET` (long random value), `ADMIN_EMAIL=admin@college.edu`, `ADMIN_PASSWORD` (strong password), `DATA_DIR=/var/data`
- Attach a persistent disk mounted at `/var/data` (1 GB). Without a persistent disk, JSON records may be lost on redeploy/restart.
- Health check path: `/api/me`

## Local run
```bash
npm install
npm start
```
Open http://localhost:3000.

## Note
This academic demo stores records in JSON files. The persistent Render disk keeps data across deployments but is attached to a paid disk-capable service. For a production multi-instance application, migrate to a managed database and persistent session store.
