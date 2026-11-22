# Still Supported 2.0 — Epistemic Decision-Support & Redline Review in Jira

**15-second judge walkthrough on ANY Jira issue:**
1. Open **any** Jira issue assigned to you whose status is **Done** (no special Jira label required).
2. Open **Still Supported** and click **Seed 1-Click Live Linked Demo (8D + Linked Lab Issue)** *(or **Initialize Local 8D Case** if you prefer zero extra tickets)*.
3. Click **Simulate upstream lab amendment (24 → 12 cartons)** *(or edit the newly created `[LAB-SC20]` Jira issue yourself!)*.
4. Watch the **3-column Epistemic Support Graph**, **Quantitative Drift Detector (`24 → 12 cartons, -50%`)**, **Word-Level LCS Redline Diff**, **Rovo Inspector**, and **SHA-256 Audit Evidence Pack** react in real time—without silently altering Jira status or forging human sign-offs.

---

## Why Still Supported Exists (Specialized Regulated Industries)

In regulated engineering and quality workflows—**Medical Devices (ISO 13485 CAPA)**, **Automotive & Aerospace (IATF 16949 / AS9100 8D)**, **Pharma Cold-Chain**, and **SOC 2 Change Governance**—a Jira work item is often closed (`Done`) on the strength of laboratory or field evidence `@1`. Weeks later, an amended laboratory report `@2` narrows the verified scope (for example, cold-storage telemetry confirms only `12` of `24` cartons underwent `-20 °C` conditioning).

Teams face a dangerous blind spot:
- **Jira status still reads `Done`**, masking that the evidence cited by `D6 Effectiveness`, `D8 Closure`, and historical customer acceptance has shifted underneath them.
- **Auto-reopening tickets or letting AI rewrite decisions breaks audit compliance**: regulated standards require preserving historical sign-offs verbatim, distinguishing editorial typo fixes (`0` numeric drift) from quantitative scope contractions (`-50%`), and requiring an attributed human reviewer to sign a new disposition on `@current`.

**Still Supported 2.0** solves this natively on Atlassian Forge.

---

## What's New in Still Supported `2.0.0`

- **Works on ANY Jira Work Item**: No `still-supported-demo` label lock. Open any closed (`Done`) Jira issue assigned to you and start immediately, with 100% backward compatibility for existing stored cases.
- **Atlassian Design System (`ADS`) Custom UI Cockpit (`viewportSize: large` + `jira:issueContext` glance)**:
  - **Top Epistemic Status Bar**: Live Jira status, `DECISIONS TO REVIEW` vs `ALL DECISIONS SUPPORTED`, `CUSTOMER CITES @1`, active stock holds (`HOLD H20`), case revision `#n`, and 1-click Rovo Inspector launch.
  - **Tab 1 — Interactive 3-Column Vector SVG Support Graph**: Maps `Evidence Records & Linked Jira Issues` → `Signed Supplier Decisions` → `Customer History, Holds & Audit Pack` with solid green edges when `@cited === @current` and animated dashed crimson edges when upstream evidence advances or `D6 → D8` prerequisites break.
  - **Tab 2 — Word-Level LCS Redline Diff & Teamwork Graph Sources**: Unified and side-by-side redline (`#FFD5D2` removals / `#BAF3DB` additions), deterministic **Quantitative Drift Detector** (`24 cartons → 12 cartons (-50%)`), SHA-256 version digests, and live **Jira + Atlassian Teamwork Graph (`requestTeamworkGraph`)** source binding.
  - **Tab 3 — Examine & Sign (Separation of Duties)**: Explicit human reviewer role assignment, `D6` / `D8` disposition signing (`Reaffirm on @current` / `Withdraw support` / `Reopen closure review`), mandatory engineering rationale, and cryptographic citation sealing.
  - **Tab 4 — Handover, SHA-256 Audit Pack & GDPR Controls**: Automatic `STALE` handover detection, 1-click **ISO 13485 / IATF 16949 / SOC 2 Audit Evidence Pack** (`.json`, `.md`, printable `.html`) with canonical SHA-256 verification, plus self-service account redaction (`[erased]`) and tombstone case erasure (`CASE_ERASED`).
- **Automated Upstream Jira Watcher (`avi:jira:updated:issue`, `avi:jira:commented:issue`)**: Editing a linked upstream Jira lab ticket automatically records `@v+1` in downstream cases via conditional KVS transactions—flagging dependent decisions `TO REVIEW` and handovers `STALE` without touching Jira status.
- **Read-Only Rovo Agent (`Still Supported Inspector`) & Forge Remote MCP (`still-supported-mcp`)**:
  - Exposes 3 strictly read-only (`GET`) tools shared between **Rovo Chat** and **Atlassian MCP** (`Claude Code`, `Cursor`, `Rovo Studio`): `inspect-decision-support`, `diff-evidence-versions`, and `discover-teamwork-context`.
  - Open-source Agent Skill included at [`skills/still-supported-mcp/SKILL.md`](skills/still-supported-mcp/SKILL.md).

---

## Install & Evaluate

[Install Still Supported in Jira](https://developer.atlassian.com/console/install/a02e8917-1f2e-4737-a4d5-5a858b729799?signature=AYABeJTZWerkMRhm5PczaHBwKcoAAAADAAdhd3Mta21zAEthcm46YXdzOmttczp1cy13ZXN0LTI6NzA5NTg3ODM1MjQzOmtleS83MDVlZDY3MC1mNTdjLTQxYjUtOWY5Yi1lM2YyZGNjMTQ2ZTcAuAECAQB4CxqLTo9l4lqXuFjNim1xJM%2Bp%2F3TVP9xHS2BrU5DRRucBemLYfBVOTT4z9noIJHgIdgAAAH4wfAYJKoZIhvcNAQcGoG8wbQIBADBoBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDAQf%2FM2cE7ANsfLowQIBEIA7EyM8qV2rip5NRO0Q0ZvFBtzXw99T7TMezShSnYJRnvUhLjqi5uZVP9jagKmN6dgYnetrB%2BBsHv0sHkMAB2F3cy1rbXMAS2Fybjphd3M6a21zOmV1LXdlc3QtMTo3MDk1ODc4MzUyNDM6a2V5LzQ2MzBjZTZiLTAwYzMtNGRlMi04NzdiLTYyN2UyMDYwZTVjYwC4AQICAHi9bVMAkme4qVQX1fQHo6ePw3H40A7cGfz7yrmSfBWMXgGGviZ33UZi0BqmZy4iH76kAAAAfjB8BgkqhkiG9w0BBwagbzBtAgEAMGgGCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMbGPGvz8qnH8rU5f%2BAgEQgDuXbWkXFRt9GrlLF4rYjDIgf%2FIPMmRb2hiqZgHoWyiocb9MoxN%2Bj6u4YpLO5EjPm9AwwzEUMa%2FE%2Ft4ZuQAHYXdzLWttcwBLYXJuOmF3czprbXM6dXMtZWFzdC0xOjcwOTU4NzgzNTI0MzprZXkvNmMxMjBiYTAtNGNkNS00OTg1LWI4MmUtNDBhMDQ5NTJjYzU3ALgBAgIAeDYASx0XCjkny4iLV6vz%2BKtEGSGT6kdt0QRpkn6D%2FlVEAREzFCxCGb6JIK%2B99pkhNzYAAAB%2BMHwGCSqGSIb3DQEHBqBvMG0CAQAwaAYJKoZIhvcNAQcBMB4GCWCGSAFlAwQBLjARBAy%2FlIfoNba19Kv3UO8CARCAO1A7EEOAj6SzBUrYEzu7LElQrZE0JLaYC5aT8RnJxcWncnLspLa1ljYOIPWB8dSex%2F%2FqGVjb8U7F33cZAgAAAAAMAAAQAAAAAAAAAAAAAAAAACU9%2BwB3fJH%2FSBkeiaNeL4r%2F%2F%2F%2F%2FAAAAAQAAAAAAAAAAAAAAAQAAADIP1aLkv2hDEHxo7%2F0FzXNXRj3Yl%2BCf95Z0Z0mjMjqD9D%2BArL2CGx%2BVjNn7YhyJTcUbluZwf8KJTjDOiM2T6jvVj%2BY%3D&product=jira)

Additional documentation in this repository:
- [Rehearsal & Synthetic Counterexamples (`CQ-18`, `CQ-19`, `CQ-20`)](REHEARSAL.md)
- [Atlassian MCP Skill (`skills/still-supported-mcp/SKILL.md`)](skills/still-supported-mcp/SKILL.md)
- [Atlassian Marketplace Listing Specification (`MARKETPLACE-LISTING.md`)](MARKETPLACE-LISTING.md)

---

## Privacy Notice

Effective 22 November 2026. Developer: Yann Abadie, independent personal Codegeist project. Contact: yann.abadie@gmail.com.

- **100% Runs on Atlassian (Zero External Egress)**: `permissions.external` is completely absent from `manifest.yml`. No external AI API, external database, CDN asset, telemetry, or analytics service is ever contacted.
- **Minimal Scopes & Explicit User Control**:
  - `read:jira-work` & `read:graph:issue:jira`, `read:graph:page:confluence`, `read:graph:goal:atlassian`: user-scoped reads of the current Jira issue, linked Jira evidence issues, and Teamwork Graph context.
  - `write:jira-work`: invoked **only** when an operator explicitly clicks *Seed 1-Click Live Linked Demo* or *Simulate upstream lab amendment* to create/amend a synthetic upstream lab issue. Existing customer/user Jira issue statuses are never silently modified.
  - `storage:app`: stores versioned cases, SHA-256 digests, dispositions, and the GDPR account-reference register in Forge Custom Entity Store (`case-state`), isolated per tenant installation.
  - `read:chat:rovo`: powers the read-only `Still Supported Inspector` Rovo Agent.
- **Account Minimization & Self-Service GDPR Erasure**: Only opaque Atlassian account IDs are stored in structured attribution slots—never names, email addresses, or avatars. Automated trigger syncs use a non-personal marker (`[jira-trigger]`). Any user can redact their own account ID (`[erased]`) and the assigned custodian can permanently erase an entire case (`CASE_ERASED` tombstone) directly from Tab 4. Uninstallation follows [Atlassian's Forge hosted-storage lifecycle](https://developer.atlassian.com/platform/forge/storage-reference/hosted-storage-data-lifecycle/).

---

## Evaluation Terms

Effective 22 November 2026.

You may install and use Still Supported free of charge for evaluation and Codegeist judging with synthetic/non-confidential data. Still Supported is an epistemic decision-support and audit-trail visibility tool; it is not an automated certification engine, medical device, or substitute for qualified human engineering and quality sign-off. No warranty or SLA is implied.

Support & privacy inquiries: yann.abadie@gmail.com.
