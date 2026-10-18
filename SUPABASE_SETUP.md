# Supabase connection — Gathering 2027

Supabase project: **GET TOGETHER 2027 E-Raffle** (`allltrsiqauixobewipm`)

Project URL: `https://allltrsiqauixobewipm.supabase.co`

## Created tables
- `g27_attendees`: patient and companion records
- `g27_checkins`: one check-in per attendee
- `g27_benefit_claims`: one claim per attendee per snack/lunch/gift
- `g27_audit_log`: staff activity
- `g27_staff_access`: allowlist of authenticated staff

Existing raffle tables are untouched.

## Security
RLS is enabled and table access is revoked from anonymous and authenticated client roles. The server-side RPC functions `g27_staff_checkin(p_code)` and `g27_staff_claim(p_code,p_benefit)` require an authenticated user who has been explicitly granted active access in `g27_staff_access`. No staff members are automatically enrolled.

## Before live operation
1. Set up Supabase Auth for staff and explicitly approve staff UUIDs in `g27_staff_access`.
2. Implement authenticated, least-privilege attendee lookup and import endpoints; do not expose the full participant list publicly.
3. Review and import the existing Google Sheet records with consent, and assign distinct opaque codes to each attendee.
4. Wire the GitHub frontend to secure APIs and test QR scanning and atomic claims.
5. Design and test offline sync and conflict resolution. Current browser-local offline records do **not** sync with Supabase.
6. Use only a publishable key in frontend code; never publish a service-role key.
7. Test end-to-end on authorized devices before using real participant information.

**Status:** Database schema is live, but frontend-to-Supabase integration and data migration are pending. The existing website still operates as a local offline interface.
