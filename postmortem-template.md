# Incident Postmortem Template

> Blameless postmortem. Focus on systems and processes, not individuals.

## Summary
- **Incident ID:**
- **Date / Time (UTC):**
- **Duration:**
- **Severity:** SEV-1 / SEV-2 / SEV-3
- **Author:**
- **Status:** Draft / In Review / Final

## Impact
- Who/what was affected and for how long?
- Error budget consumed:

## Timeline (UTC)
| Time | Event |
|------|-------|
| | Alert fired |
| | On-call acknowledged |
| | Mitigation applied |
| | Service recovered |

## Root Cause
- What was the underlying cause?

## Detection
- How was the incident detected? How long until detection?

## Resolution
- What actions resolved the incident?

## What Went Well
-

## What Went Poorly
-

## Action Items
| Action | Owner | Priority | Due |
|--------|-------|----------|-----|
| | | | |

## HOTFIX: Updated Escalation Policy
The escalation policy has been corrected so that secondary on-call is
paged after **10 minutes** without acknowledgement (previously 30).
SEV-1 incidents now page the incident commander **immediately**.

| Severity | Primary | Escalate to secondary after | Incident commander |
|----------|---------|-----------------------------|--------------------|
| SEV-1 | on-call | immediate | immediate |
| SEV-2 | on-call | 10 min | 30 min |
| SEV-3 | on-call | 30 min | not required |
