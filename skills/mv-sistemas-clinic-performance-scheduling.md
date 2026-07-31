---
name: Schedule a clinic performance appointment
description: List performance-scheduling availability, create a scheduling, and update its status via Clinic Connect.
api: openapi/mv-sistemas-clinic-connect-performance-schedule-openapi.yml
operations: [listPerformanceSchedules, createScheduling, updateSchedulingStatus]
---

# Schedule a clinic performance appointment

Use the Clinic Connect – Agendamento de performance API (base `https://api.globalhealth.mv/clinic-connect/api/`, `/hml/...` for staging). All requests require the `x-api-key` header.

## Steps
1. **List availability** — `listPerformanceSchedules` (GET) to retrieve schedulable performance slots for providers.
2. **Create the scheduling** — `createScheduling` (POST) with the chosen slot and patient/provider references; expect 201 on success.
3. **Update status** — `updateSchedulingStatus` (PUT/PATCH) to confirm, complete, or cancel the scheduling.

## Rules
- Validate the slot is still listed before creating (availability can change).
- Handle 400 (invalid request) and 404 (slot/scheduling not found).
- The outbound webhook (openapi/mv-sistemas-performance-schedule-webhook-openapi.yml) notifies external systems of availability; consume it if you mirror schedules.
- Test in `/hml` before production.
