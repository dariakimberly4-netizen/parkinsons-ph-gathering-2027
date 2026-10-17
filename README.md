# Parkinson's Disease PH Gathering 2027

Mobile-friendly event website starter for patient and companion registration, separate QR passes, attendance, snack, lunch, and gift distribution.

## Status
**Starter interface only.** Registration is deliberately disabled until a secure backend is connected. No real QR codes, check-in records, claims, or database are created by this commit.

## Proposed stack
- GitHub Pages: public website (static frontend)
- Supabase: PostgreSQL database, authentication, row-level security and server-side operations
- Server-side QR issuance with random opaque tokens; never encode medical or contact details
- Authenticated staff-only check-in and distribution endpoints

## Data model
- families (id, created_at)
- patients (id, family_id, name, registration_status)
- companions (id, family_id, patient_id, name, registration_status)
- qr_passes (id, attendee_type, attendee_id, token_hash, issued_at, revoked_at)
- checkins (id, attendee_type, attendee_id, checked_in_at, staff_id)
- benefit_claims (id, attendee_type, attendee_id, benefit_type, claimed_at, staff_id)
- audit_log (id, actor_id, action, target_id, occurred_at)

Create unique constraints on checkins(attendee_type, attendee_id) and benefit_claims(attendee_type, attendee_id, benefit_type). Enforce authorization server-side and use atomic transactions to prevent double claims.

## Next steps
1. Create a Supabase project and define access policies.
2. Configure staff roles and server-side issuance and claim endpoints.
3. Connect the registration form, admin dashboard and scanner.
4. Test with synthetic participant records before handling real data.
5. Enable GitHub Pages from Settings → Pages → Deploy from branch → main / root.

**Privacy:** Do not commit real participant information, passwords, or secret API keys. Health-related data requires special care and appropriate consent.
