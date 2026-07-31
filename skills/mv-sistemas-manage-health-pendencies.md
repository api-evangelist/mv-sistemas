---
name: Manage patient health pendencies
description: Create, search, and update clinical pending items (pendências de saúde) and their exam items for a beneficiary.
api: openapi/mv-sistemas-pendencias-saude-openapi.json
operations: [addHealthPendency, findHealthPendencies, getHealthPendencyById, updateHealthPendencyByHashKey, getHealthPendencyExamItemByHashKey, updateHealthPendencyExamItemByHashKey]
---

# Manage patient health pendencies

Use the Gestão de Pendências de Saúde API (base `https://api.globalhealth.mv/health-insurance-store`). All requests require the `x-api-key` header.

## Steps
1. **Create a pendency** — `addHealthPendency` (POST) registers a clinical pending item for the beneficiary.
2. **Search** — `findHealthPendencies` (GET) lists pendencies with `page`/`size` pagination and period filters.
3. **Read one** — `getHealthPendencyById` (GET) fetches a single pendency.
4. **Update status** — `updateHealthPendencyByHashKey` (PUT) updates a pendency by its hash key.
5. **Exam items** — `getHealthPendencyExamItemByHashKey` (GET) then `updateHealthPendencyExamItemByHashKey` (PUT) to read and resolve associated exam items.

## Rules
- Pass the hash key returned on create when updating; do not fabricate keys.
- Handle 404 (unknown pendency) gracefully.
- No idempotency-key contract exists — avoid blind retries of POST/PUT.
