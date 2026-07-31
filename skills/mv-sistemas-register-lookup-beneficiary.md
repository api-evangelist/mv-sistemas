---
name: Register and look up a beneficiary
description: Create a beneficiary/insurance record in MV Global Health and retrieve it by document (CPF) or insurance card number.
api: openapi/mv-sistemas-gestao-beneficiarios-openapi.json
operations: [addPerson, findPersonByDocumentNumberOrInsuranceCardNumber, findPersonsByDocumentNumberOrInsuranceCardNumber]
---

# Register and look up a beneficiary

Use the Gestão de Beneficiários API (base `https://api.globalhealth.mv/health-insurance-store`, or `/hml/...` for staging). Every request needs the `x-api-key` header. This API is rate-limited to 1 request/second.

## Steps
1. **Create the beneficiary** — call `addPerson` (POST) with the person's registration data (document number / CPF, insurance card number, and cadastral fields).
2. **Look up one beneficiary** — call `findPersonByDocumentNumberOrInsuranceCardNumber` (GET) passing the CPF or insurance card number to fetch the current record.
3. **Look up multiple matches** — call `findPersonsByDocumentNumberOrInsuranceCardNumber` (GET) when a document may map to more than one beneficiary.

## Rules
- Respect the 1 req/s limit — serialize calls and back off on 403.
- Handle 400 (invalid payload), 404 (not found), and 500 per errors/mv-sistemas-problem-types.yml.
- Validate in the `/hml` environment before production.
