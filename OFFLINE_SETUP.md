# Offline operation

1. Enable GitHub Pages on the main branch, root directory.
2. Open the site online on the event device and allow the service worker to install. Then test airplane mode and refresh.
3. In **Offline Tools**, import a CSV with columns `id,name,type,family`. One row per person; type must be exactly `Patient` or `Companion`. Use only authorized event devices.
4. Use attendee IDs manually for check-in and claims. On browsers supporting the native BarcodeDetector API, camera scanning can read QR codes whose entire payload is an attendee ID. The on-screen QR design is not a real QR code.
5. Export a JSON backup and attendance CSV frequently. Keep backups secure.

## Important limitations

- This is an offline **single-device** implementation. Local data is stored in browser localStorage, unencrypted and device-specific. Clearing browser storage, private mode, device loss, or storage eviction can erase it.
- No online synchronization, staff authentication, role-based access, cross-device duplicate detection, or secure backend yet.
- Use fictional test data until proper access controls and privacy safeguards are established for real patient/companion information.
- The browser must load the site once while online before offline caching can work. Native camera scanning requires HTTPS and browser support; manual ID entry is the fallback.
- Existing Google Sheet responses are **not automatically imported**. Export an appropriate minimized CSV and import it manually after reviewing privacy requirements.
- For production, use a secure backend, authenticated staff devices, offline transaction logs, encryption at rest where appropriate, and conflict resolution.
