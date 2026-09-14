# Public Portfolio Security Review Checklist

Do not make the development repository public until every relevant item is reviewed.

## Secrets
- [ ] No database passwords
- [ ] No OIDC / Keycloak client secrets
- [ ] No JWT signing secrets
- [ ] No API tokens
- [ ] No GitHub tokens
- [ ] No cloud credentials
- [ ] No private keys / certificates
- [ ] No `.env` files with real credentials

## Personal / customer data
- [ ] No real resident/patient names
- [ ] No real employee names unless explicitly intended
- [ ] No personal addresses
- [ ] No private emails or phone numbers
- [ ] No employer-internal information
- [ ] No screenshots containing private browser/account information

## Development-only material
- [ ] Exclude private handoff documents
- [ ] Exclude raw ChatGPT/Codex transcripts
- [ ] Exclude local DB dumps
- [ ] Exclude acceptance DB dumps
- [ ] Exclude runtime logs that contain sensitive context
- [ ] Exclude local filesystem paths where unnecessary
- [ ] Exclude protected stashes/backups from export

## Demo fixtures
- [ ] Use fictional organization name
- [ ] Use fictional Facility name
- [ ] Use fictional worker names
- [ ] Use synthetic employee codes
- [ ] Use synthetic requests / leave
- [ ] Do not reuse real care-work resident data

## Source publication
- [ ] Decide whether source is full, partial, or case-study-only
- [ ] Confirm third-party dependency licenses
- [ ] Add an appropriate LICENSE only after that decision
- [ ] Run secret scanning before first public push

## Screenshots / video
- [ ] Candidate Review hero screenshot anonymized
- [ ] Planning screenshot anonymized
- [ ] Staffing Demand screenshot anonymized
- [ ] Requests / Leave screenshot anonymized
- [ ] Workforce / Setup screenshot anonymized
- [ ] My Schedule screenshot only after accepted implementation
- [ ] Technical IDs hidden unless intentionally demonstrated
- [ ] Video contains no local secrets, browser-account information or private data
