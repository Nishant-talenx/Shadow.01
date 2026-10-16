# SHADOW Pilot Upgrade

A local-first prototype for documenting public anti-piracy investigations. It starts with an empty registry and does not include fabricated incidents. No Supabase credentials or server are required.

## Run on Windows

1. Install a current Node.js LTS release if needed.
2. Extract `SHADOW_Pilot_Upgrade.zip` into your Downloads folder.
3. Open PowerShell and run:

```powershell
cd "$HOME\Downloads\SHADOW_Pilot_Upgrade\SHADOW_Pilot"
npm.cmd install
npm.cmd run dev
```

4. Open the local URL Vite prints, normally `http://127.0.0.1:5173`. Keep the PowerShell window open while using the app.

## Team login

Enter a team member's name and the shared demo password `SHADOW12@@##`.

This is a frontend-only prototype access gate, not secure authentication. The password is present in the frontend bundle. Do not use it to protect confidential PW information or deploy this prototype publicly.

## Main workflow

- **Overview:** Actual local-record metrics, status donut, discovery trend and overdue follow-up queue.
- **Investigations:** Search/filter incidents, edit case details, update status, record notes and view activity history.
- **Evidence Submission:** Dedicated sidebar page. Capture source type/name/URL, discovery time, investigator, category, priority, description and notes. Attach up to three PNG/JPG screenshots (maximum 5 MB each) and save the incident plus its evidence in one IndexedDB state write.
- **Evidence Library:** Search/filter saved screenshots by platform, status and submitter. Preview/download images and open the associated case.
- **Team:** Assignment workload counts for the configured team list.
- **Reports:** Weekly summary based on current records, CSV export, JSON backup, and browser Print / Save as PDF.
- **Settings:** Backup/restore and local-storage/security guidance.

## Local data and evidence

Records, evidence data URLs, activity entries and notes are stored together in IndexedDB under the existing `shadow-local-pilot-v1` database. The incident and evidence payload for a new submission is written as one state object so the UI only shows success after the database transaction completes. Existing Shadow.09 records in the same browser profile should remain readable; older records without `source_type` are classified from their URL when displayed.

Use **Export backup** regularly. The JSON backup contains incident records, screenshot payloads, activity history and notes. Restore replaces the current local dataset after confirmation; validate the restored incident count and evidence before deleting the original backup. Browser data is specific to this browser profile and device, and may be removed if browser data is cleared. There is no automatic sync between teammates' devices.

## Important limitations

- The app tracks evidence and reporting progress. It does not contact Telegram/websites, submit takedown reports, or directly control platform enforcement.
- A submitted complaint is not proof of removal. A confirmed removal requires a date and verification notes.
- The local activity history is not a tamper-proof audit log.
- The shared password gate is not production authentication. Use no confidential customer data until server-side authentication, authorization, and shared private storage are implemented.
- Screenshots are stored in IndexedDB as data URLs for compatibility with the current single-state local database and JSON backup format. Browser quotas vary; if storage is full, export a backup and retry with smaller images.
- PDF output uses the browser's print dialog. Choose **Save as PDF** there; the app does not silently create a PDF file.

## Troubleshooting evidence submission

1. Use a current Chrome or Edge browser.
2. Use PNG, JPG, or JPEG files, no larger than 5 MB each.
3. Attach at least one screenshot (maximum three), enter a valid `https://` or `http://` source URL, then click **Save Submission**.
4. Wait for the save operation to finish. A success toast includes the incident ID.
5. Open the created incident and its Evidence tab, then open Evidence Library. Refresh and verify the evidence remains available.
6. If the browser reports quota/storage errors, export a backup, try smaller screenshots, and retry. The form should retain its fields and selected files after a failed submission.

## Build verification

The project uses React, Vite, and lucide-react. Run `npm.cmd install` and `npm.cmd run build` to validate it on your machine. The build could not be run in the authoring environment because package installation did not complete; do not treat this README as a claim that a full browser QA pass has been performed.
