# Still Supported 2.0 — Epistemic Decision-Support & Redline Review in Jira

**90-second live judge walkthrough on ANY fresh Jira project (zero hardcoded path — no Confluence or Rovo required):**
1. **Seed (`~20 s`)**: Assign any Jira issue to yourself, set its status to **Done**, open **Still Supported**, and click **Seed 1-Click Live Linked Demo (8D + Linked Lab Issue)** to create and link a real upstream Jira lab ticket (`[LAB-SC20]`, baseline `24 cartons`, `72 hours`, `releaseGate: CLEAR`).
2. **Free-edit in Jira (`~35 s`)**: Click that newly linked `[LAB-SC20]` ticket in Jira's **Linked work items** right above the panel, **edit its Description with any numbers of your choice**—for example, change `all 24 cartons C01–C24` to **`15 cartons C01–C15`** (`-37.5%`) or **`only 8 cartons`** (`-66.7%`)—and save *(an optional 1-click **Simulate** shortcut is also available)*.
3. **Inspect & Sign (`~30 s`)**: Return to your `Done` issue (click **Refresh** if the tab stayed open, or **Sync linked Jira evidence** for instant pull) to watch `avi:jira:updated:issue` append `SCAN-RUN@2` (`Actor: [jira-trigger]`), compute your exact custom `%` drift, render the **Word-Level LCS Redline Diff**, flip `D6` & `D8` to `TO REVIEW` (`releaseGate: BLOCKED` while Jira stays `Done`), sign human dispositions, and export the **SHA-256 Audit Evidence Pack**. Jump to the [3-Step Evaluation Guide](#evaluation-guide).

---

## Why Still Supported Exists (Specialized Regulated Industries)

In regulated engineering and quality workflows—**Medical Devices (ISO 13485 CAPA)**, **Automotive & Aerospace (IATF 16949 / AS9100 8D)**, **Pharma Cold-Chain**, and **SOC 2 Change Governance**—a Jira work item is often closed (`Done`) on the strength of laboratory or field evidence `@1`. Weeks later, an amended laboratory report `@2` narrows the verified scope (for example, cold-storage telemetry confirms only `12` of `24` cartons underwent `-20 °C` conditioning).

Teams face a dangerous blind spot:
- **Jira status still reads `Done`**, masking that the evidence cited by `D6 Effectiveness`, `D8 Closure`, and historical customer acceptance has shifted underneath them.
- **Auto-reopening tickets or letting AI rewrite decisions breaks audit compliance**: regulated standards require preserving historical sign-offs verbatim, distinguishing editorial typo fixes (`0` numeric drift) from quantitative scope contractions (`-50%`), and requiring an attributed human reviewer to sign a new disposition on `@current`.

**Still Supported 2.0** solves this natively on Atlassian Forge.

---

## What's New in Still Supported 2.0.1 (Forge Production [3.0.0])

- **Works on ANY Jira Work Item**: No `still-supported-demo` label lock. Open any closed (`Done`) Jira issue assigned to you and start immediately, with 100% backward compatibility for existing stored cases.
- **Atlassian Design System (`ADS`) Light Custom UI Cockpit (`viewportSize: large` + `jira:issueContext` glance)**:
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

## Evaluation guide

[Install Still Supported in Jira](https://developer.atlassian.com/console/install/a02e8917-1f2e-4737-a4d5-5a858b729799?signature=AYABeALhwI1nlL2IRWKPvZfDO2EAAAADAAdhd3Mta21zAEthcm46YXdzOmttczp1cy13ZXN0LTI6NzA5NTg3ODM1MjQzOmtleS83MDVlZDY3MC1mNTdjLTQxYjUtOWY5Yi1lM2YyZGNjMTQ2ZTcAuAECAQB4CxqLTo9l4lqXuFjNim1xJM%2Bp%2F3TVP9xHS2BrU5DRRucBIXV1VYLU%2BVwT%2Fxgx0HgBzgAAAH4wfAYJKoZIhvcNAQcGoG8wbQIBADBoBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDCBCcnGrjaBQsu84pQIBEIA70mCIO4Apy3z5CJEsbBdfx5bNzR25K0vTTtGafPUGsTfhGdZt740QBvZy8M5Iv6mPTsjuQgB2Zm2crKoAB2F3cy1rbXMAS2Fybjphd3M6a21zOmV1LXdlc3QtMTo3MDk1ODc4MzUyNDM6a2V5LzQ2MzBjZTZiLTAwYzMtNGRlMi04NzdiLTYyN2UyMDYwZTVjYwC4AQICAHi9bVMAkme4qVQX1fQHo6ePw3H40A7cGfz7yrmSfBWMXgHFfNY2OEaYAMf7BAziA1VhAAAAfjB8BgkqhkiG9w0BBwagbzBtAgEAMGgGCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMm8Dvs7XO0%2FPpP55%2FAgEQgDuaW2r5Ty6I4sp3%2Fxkzd9Zz5VEEndaoQXxrbjun9TA7dYrpSwHQop9yCUINC5W9PKnq643jGN3IdGt9ygAHYXdzLWttcwBLYXJuOmF3czprbXM6dXMtZWFzdC0xOjcwOTU4NzgzNTI0MzprZXkvNmMxMjBiYTAtNGNkNS00OTg1LWI4MmUtNDBhMDQ5NTJjYzU3ALgBAgIAeDYASx0XCjkny4iLV6vz%2BKtEGSGT6kdt0QRpkn6D%2FlVEAd%2BFUlInKFZH2wW97XVDZ5YAAAB%2BMHwGCSqGSIb3DQEHBqBvMG0CAQAwaAYJKoZIhvcNAQcBMB4GCWCGSAFlAwQBLjARBAxyul518gRhyZD%2BWR4CARCAO0RVEvAjss98DkLzvfIWcYMXyOnHkOYFms4vJXx8hmrn3YdE9VPkih%2B0UAoJ%2BOWJXvXtdX35V%2BRaxdm%2FAgAAAAAMAAAQAAAAAAAAAAAAAAAAAJrcMXqWhXKVIObgop%2F8ldL%2F%2F%2F%2F%2FAAAAAQAAAAAAAAAAAAAAAQAAADKfHUuvoTSzds21CXR6mkN%2FJkGgV7TENsUqNW58kJWpDxvrRBzVcowvgOJydD7mtjRU6%2BjgNiNx2eNi0nCE%2B1V583k%3D&product=jira)

*(Installs Forge Production deployment `[3.0.0]` — app release `v2.0.1` on **Jira**. Cold-install verified on fresh Jira-only sites with **no Confluence linked** and **no Rovo required**.)*

### 3-Step Live Judge Evaluation (`< 90 seconds` — Free Jira Edit, Zero Hardcoded Path)

1. **Step 1 (`~20 s`) — Seed a live linked case on any `Done` Jira issue**
   - Open any Jira work item on your site. *(On a fresh `To Do` or unassigned ticket, Still Supported displays a 2-step checklist: assign the ticket to yourself, set its status to **Done**, and click **Refresh** in the panel header.)*
   - Click **Seed 1-Click Live Linked Demo (8D + Linked Lab Issue)**. Still Supported creates and links a real upstream Jira issue `[LAB-SC20]` in the same project (`SCAN-RUN@1`: `24 cartons` `C01–C24`, `72 hours` at `-20 °C`; `ALL DECISIONS SUPPORTED`, `releaseGate: CLEAR`). *(Prefer zero extra tickets? Click **Initialize Local 8D Case**.)*
2. **Step 2 (`~35 s`) — Open `[LAB-SC20]` in Jira and edit its Description yourself**
   - Click the newly created `[LAB-SC20]` ticket in Jira's native **Linked work items** list right above the panel.
   - Edit `[LAB-SC20]`'s **Description** with your own wording and numbers—for example, in paragraph 2 change `"completed on all 24 cartons C01–C24"` to **`"completed on 15 cartons C01–C15"`** (`-37.5%`), **`"completed on only 8 cartons"`** (`-66.7%`), or change `"72 hours"` to **`"48 hours"`** (`-33.3%`)—and click **Save** in Jira.
   - *(Optional shortcut: if you prefer a 1-click preset instead of manual editing, click **Simulate upstream lab amendment (`24 → 12 cartons`)** in Tab 1.)*
3. **Step 3 (`~30 s`) — Inspect live `avi:jira:updated:issue` drift, Redline Diff, Human Sign-Off & Audit Pack**
   - Return to your `Done` case issue *(if that browser tab stayed open, wait ~1–3 s for the background `avi:jira:updated:issue` event and click **Refresh** in the Still Supported top bar, or click **Sync linked Jira evidence** in Tab 1 for instant pull)*:
     - **Tab 1 (`Support Graph`)**: `SCAN-RUN@2` (`Actor: [jira-trigger]`) computes your exact custom `%` drift, flags `D6-effectiveness` & `D8` `TO REVIEW` (`releaseGate: BLOCKED`), and preserves `CUSTOMER CITES @1` while Jira status remains **Done**.
     - **Tab 2 (`Evidence & Redline Diff`)**: Inspect the word-level LCS redline of your exact edit, SHA-256 digests, and live Jira / Teamwork Graph links *(or bind any custom Jira ticket via **Bind & Sync into `SCAN-RUN`** using units like `cartons`, `vials`, `units`, `samples`, `batches`, `lots`, `devices`, `pallets`, `items`, `cycles`, `hours`, `days`, `ppm`, `mg`, `ml`, `kg`, `°C`, or serial spans like `N01–N60`)*.
     - **Tab 3 (`Examine & Sign`) & Tab 4 (`Audit Pack & Privacy`)**: Click **Assume Supplier Reviewer Role**, sign explicit human dispositions (`Withdraw support` / `Reopen closure review`), and export the canonical **SHA-256 Audit Evidence Pack** (`.json`, `.md`, `.html`) or test GDPR erasure (`[erased]` / `CASE_ERASED`).

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
  - `write:jira-work`: GET-only Rovo/MCP actions perform **0 AI writes**; `write:jira-work` is restricted **exclusively** to synthetic `still-supported-upstream-lab` demo tickets when an operator explicitly clicks *Seed 1-Click Live Linked Demo* or *Simulate upstream lab amendment* (enforced by server-side label verification before any `PUT`). Real Jira issues and statuses are never modified.
  - `storage:app`: stores versioned cases, SHA-256 digests, dispositions, and the GDPR account-reference register in Forge Custom Entity Store (`case-state`), isolated per tenant installation.
  - `read:chat:rovo`: powers the read-only `Still Supported Inspector` Rovo Agent.
- **Account Minimization & Self-Service GDPR Erasure**: Only opaque Atlassian account IDs are stored in structured attribution slots—never names, email addresses, or avatars. Automated trigger syncs use a non-personal marker (`[jira-trigger]`). Any user can redact their own account ID (`[erased]`) and the assigned custodian can permanently erase an entire case (`CASE_ERASED` tombstone) directly from Tab 4. Uninstallation follows [Atlassian's Forge hosted-storage lifecycle](https://developer.atlassian.com/platform/forge/storage-reference/hosted-storage-data-lifecycle/).

---

## Evaluation Terms

Effective 22 November 2026.

You may install and use Still Supported free of charge for evaluation and Codegeist judging with synthetic/non-confidential data. Still Supported is an epistemic decision-support and audit-trail visibility tool; it is not an automated certification engine, medical device, or substitute for qualified human engineering and quality sign-off. No warranty or SLA is implied.

Support & privacy inquiries: yann.abadie@gmail.com.
