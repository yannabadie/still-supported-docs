# Rehearsal & Synthetic Counterexamples — Still Supported `2.0.1` (`Forge Production [3.0.0]`)

All records, issue summaries, lot identifiers, environmental parameters, approvals, and amendments below are synthetic demonstration inputs for evaluating **Still Supported `2.0.1`** (deployed as **Forge Production `[3.0.0]`**). Still Supported never infers quality dispositions or modifies Jira workflow statuses; AI inspection tools (**Rovo `Still Supported Inspector`** and **`still-supported-mcp`**) are strictly read-only (`GET`-only, `0` AI writes), and all post-closure dispositions are signed explicitly by an attributed human reviewer.

---

## 1. Live Linked Rehearsal on Any `Done` Jira Issue (`CQ-20` — Free Jira Edit + Optional 1-Click Shortcut)

1. **Open any closed (`Done`) Jira work item assigned to your account**
   - Works out of the box on a brand-new **Jira-only** project with **no Confluence linked** (`discoverTeamworkContext` cleanly falls back to Jira REST `issuelinks`) and **no Rovo required** (`rovo.isEnabled()` hides the Rovo header button cleanly when Rovo is inactive on a site).
   - No custom Jira label or workflow scheme is required. If you open a fresh unassigned or `To Do` ticket first, Still Supported displays a 2-item readiness checklist (**1. Assigned Custodian** + **2. Closed Work Item (`Done`)**); assign the issue to yourself, transition it to **Done**, and click **Refresh** in the Still Supported top bar.
2. **Seed the baseline case and linked laboratory ticket (`@1`)**
   - Click **Seed 1-Click Live Linked Demo (8D + Linked Lab Issue)**.
   - Still Supported creates and links a synthetic upstream Jira issue (`[LAB-SC20] Cold-storage barcode scan report — 24 cartons`) in the same project carrying the safety label `still-supported-upstream-lab`, binds it to evidence record `SCAN-RUN@1` (`24 cartons` `C01–C24` conditioned at `-20 °C` for `72 hours`, active stock hold `H20`), and initializes `CQ20-LIVE`:
     - Supplier decisions (`D6-implementation`, `D6-effectiveness`, `D8`) are `SUPPORTED` (`@cited === @current`).
     - Historical customer acceptance (`customer-CL20`) is `CURRENT`.
     - `releaseGate` is `CLEAR` (`ALL DECISIONS SUPPORTED`).
     - *(Optional)* Open **Tab 4 (`Handover, Audit Pack & Data Privacy`)** and click **Build Handover Draft** to snapshot a baseline handover at the current revision.
3. **Trigger a post-closure laboratory amendment (`SCAN-RUN@1 → @2`)**
   - **Option A — Recommended Judge Verification: Free Manual Edit in Jira (`avi:jira:updated:issue`)**
     1. Click the newly created `[LAB-SC20]` ticket (`<PROJECT>-<N>`) in Jira's native **Linked work items** list right above the Still Supported panel.
     2. Edit `[LAB-SC20]`'s **Description** with your own wording and numbers—for example, in paragraph 2 change `"completed on all 24 cartons C01–C24"` to **`"completed on 15 cartons C01–C15"`** (`-37.5%`), **`"completed on only 8 cartons"`** (`-66.7%`), or change `"72 hours"` to **`"48 hours"`** (`-33.3%`)—and click **Save** in Jira.
     3. Return to your closed (`Done`) case issue. If that tab remained open in your browser, wait ~1–3 seconds for the background `avi:jira:updated:issue` event to write `SCAN-RUN@2` (`Actor: [jira-trigger]`) and click **Refresh** in the Still Supported top bar *(or click **Sync linked Jira evidence** in Tab 1 for immediate pull without waiting)*.
   - **Option B — Optional 1-Click Shortcut**
     - In **Tab 1 (`Support Graph`)**, click **Simulate upstream lab amendment on `<ISSUE-KEY>` (24 → 12 cartons)** to apply the preset `-50%` contraction (`12 cartons` `C01–C12` verified at `-20 °C`; `12 cartons` `C13–C24` at room temperature).
   - **Immediate deterministic state transition (Jira status remains `Done`)**:
     - `D6-effectiveness` and `D8` flip to `TO REVIEW` (`status: "DECISIONS_REQUIRE_REVIEW"`, `2 DECISIONS TO REVIEW`); `D6-implementation` remains `SUPPORTED` (`LABEL-WORK@1` is unchanged).
     - `customer-CL20` displays `CITES @1` (`CITES EARLIER VERSION`), preserving historical customer acceptance verbatim.
     - Any previously built handover snapshot is flagged `STALE` until explicitly regenerated via **Rebuild Handover Draft**.
     - `releaseGate` flips to `BLOCKED`.
4. **Inspect read-only via Redline Diff, Teamwork Graph, Rovo & Atlassian MCP (`0` AI Writes)**
   - **Tab 2 (`Evidence & Redline Diff`)**: Inspect the word-level LCS redline (`#FFD5D2` removals / `#BAF3DB` additions) highlighting your exact Jira text edit, the **Quantitative Drift Detector** (e.g. `24 cartons → 15 cartons (-37.5%)`, `24 cartons → 8 cartons (-66.7%)`, or `24 cartons → 12 cartons (-50%)`), UTF-8 SHA-256 version digests, `Actor: [jira-trigger]`, and live **Jira + Atlassian Teamwork Graph** context (`stillsupported_workItemContext`, Jira `issuelinks`, Confluence `/remotelink` SOP pages, and Atlassian Goals).
   - **Rovo Agent (`Still Supported Inspector`, when Rovo is enabled on your site)**: Click **Ask Rovo Inspector** in the cockpit header (or open Rovo Chat) and run any 1-click zero-input conversation starter.
   - **Atlassian Remote MCP (`still-supported-mcp`)**: From Claude Code, Cursor, or Rovo Studio, invoke the read-only `GET` tools `inspect-decision-support`, `diff-evidence-versions`, and `discover-teamwork-context` (see [`skills/still-supported-mcp/SKILL.md`](skills/still-supported-mcp/SKILL.md)).
5. **Sign explicit human dispositions (`Tab 3 — Examine & Sign`)**
   - Click **Assume Supplier Reviewer Role** to satisfy separation-of-duties enforcement.
   - Select both decisions under review and record explicit dispositions on `@current` (`SCAN-RUN@2`):
     - **`D6-effectiveness`** → **`Withdraw support (scope no longer established)`** (`withdraw-support`)
       - *Sample rationale*: `SCAN-RUN@2 narrows verified -20 °C cold-storage coverage below the 24-carton baseline cited at closure. Withdraw support for the 24-carton cold-storage effectiveness claim while keeping LABEL-WORK@1 and hold H20 in place.`
     - **`D8`** → **`Reopen closure review (prerequisite or scope broken)`** (`reopen-review`) *(enforced prerequisite rule: `D8` cannot maintain closure while `D6-effectiveness` support is withdrawn)*
       - *Sample rationale*: `Closure CL20 depended on 24-carton D6 effectiveness under cold storage. Reopen supplier closure review pending re-conditioning of remaining cartons; Jira Done history, customer-CL20 (@1), and stock hold H20 remain untouched.`
   - Click **Sign & Record Explicit Dispositions**.
   - **Resulting state**: Top bar displays `SUPPORT WITHDRAWN · CLOSURE REOPENED`, and `inspect-decision-support` returns `status: "SUPPORT_WITHDRAWN_OR_REOPENED"` with `releaseGate: "BLOCKED"` (`supplierToReviewCount: 0`, `supplierWithdrawnOrReopenedCount: 2`).
6. **Export the SHA-256 Audit Evidence Pack & verify GDPR controls (`Tab 4`)**
   - Click **Generate / Verify Audit Pack** to preview or download the canonical **SHA-256 Audit Evidence Pack** (`.json`, `.md`, printable `.html`) mapped to ISO 13485, IATF 16949 8D, and SOC 2.
   - Exercise self-service privacy controls:
     - **Erase my account ID (`[erased]`)**: replaces your Atlassian `accountId` with `[erased]` across stored case events while keeping the technical audit evidence intact.
     - **Erase this stored case (`CASE_ERASED`)**: purges all case data from Forge KVS and leaves an empty cryptographic tombstone rejecting stale browser tabs.

### Deterministic Quantitative Drift Extractor — Free-Edit Rules & Supported Units

Still Supported's numeric drift detector is 100% deterministic (zero LLM guesswork) and compares the **Description** text of `@cited` (`@1`) against `@current`, matching the **first occurrence** of each canonical unit or serial span present in **both** versions:
- **Editing the seeded `[LAB-SC20]` issue (`SCAN-RUN@1`)**: Baseline `@1` contains **`24 cartons`** (first occurrence in `"completed on all 24 cartons C01–C24"`), **`72 hours`**, **`-20 °C`**, and serial span **`C01–C24`**. Changing that first `24 cartons` (e.g. to `15 cartons` or `8 cartons`), `72 hours` (e.g. to `48 hours`), or `C01–C24` (e.g. to `C01–C15`) in `[LAB-SC20]`'s **Description**—or replacing the entire Description with a sentence containing `<N> cartons`—computes the exact `%` shift on the first try.
- **Binding your own custom Jira issue (`Tab 2 → Bind & Sync into SCAN-RUN`) or manual `@1 → @2` versions**: Recognizes **18 engineering/quality units** (singular or plural, case-insensitive, integer or decimal: `cartons`, `units`, `samples`, `labels`, `batches`, `lots`, `vials`, `devices`, `pallets`, `items`, `cycles`, `hours`, `days`, `ppm`, `mg`, `ml`, `kg`, `°C`) plus **alphanumeric serial ranges** (`[A-Z]{1,4}\d{1,4}[–-]\d{1,4}`, e.g. `50 vials → 30 vials (-40%)`, `100 units (N01–N100) → 60 units (N01–N60) (-40%)`).
- **Editorial-only edits (`0 NUMERIC SHIFTS`)**: Editing text or adding a Jira comment without changing a shared baseline unit still records `@v+1`, highlights the word-level LCS redline, and flags dependent decisions `TO REVIEW`, while reporting `0 NUMERIC SHIFTS` (`hasQuantitativeDrift: false`).

---

## 2. Synthetic Counterexamples (`CQ-18`, `CQ-19`, `CQ-20`)

Still Supported ships three complementary synthetic cases illustrating how the epistemic engine separates supported baselines, harmless editorial corrections, and material scope or measurement invalidations:

| Case | How to Load on a `Done` Issue | Evidence Shift | Quantitative Drift | Expected Epistemic & Release-Gate Outcome |
|---|---|---|---|---|
| **`CQ-18`** *(Supported Baseline & Instrument Check)* | Add Jira label `cq18` → **Initialize Labelled Fixture (`CQ18`)** | At `@1`: `E-BASE@1`, `E-WORK@1`, `E-VERIFY@1`, `R-DECISIONS@1` all match signed citations *(optional staged `@2`: `PG-7` position gauge → `DG-2` diameter-only gauge)* | `@1`: none (`@cited === @current`) | **At `@1` (Supported Baseline)**: `ALL DECISIONS SUPPORTED`, `releaseGate: CLEAR`. *(If staged `E-VERIFY@2` is received: `D3`–`D7` stay `SUPPORTED` while `D6-effectiveness` & `D8` move to `TO REVIEW`, `releaseGate: BLOCKED`.)* |
| **`CQ-19`** *(Editorial / Typo Amendment)* | Add Jira label `cq19` → **Initialize Labelled Fixture (`CQ19`)** → **Receive post-closure evidence amendment** | `E-MEASURE19@1 → @2`: report title typo `"Follow-up verificaton"` → `"Follow-up verification"` (`12` units `N01–N12`, lot `N9`, method `MP9` unchanged) | **`0` numeric shifts** (`hasQuantitativeDrift: false`) | Word-level LCS redline isolates the title typo with **`0 NUMERIC SHIFTS`** (zero false quantitative alarm); **Examine & Sign** pre-selects **Reaffirm / Maintain within scope on `@current`** (`maintain-within-scope` / `maintain`), restoring `ALL DECISIONS SUPPORTED` and `releaseGate: CLEAR`. |
| **`CQ-20`** *(Material Scope Contraction)* | **Seed 1-Click Live Linked Demo** + **free manual edit of `[LAB-SC20]` in Jira** *(or optional **Simulate upstream lab amendment** shortcut; **Initialize Local 8D Case** for zero-ticket offline mode)* | `SCAN-RUN@1 → @2` (`[LAB-SC20]`): `-20 °C` verified cold-storage coverage drops below `24 cartons` (`C01–C24`) under hold `H20` (e.g. free edit to `15 cartons` / `8 cartons`, or `-50%` `12 cartons` shortcut) | Custom `%` (e.g. **`-37.5%`** on `24 → 15 cartons`, **`-66.7%`** on `24 → 8 cartons`, or **`-50%`** on `24 → 12 cartons`) | Breaks `SCAN-RUN@2 → D6-effectiveness → D8` (`DECISIONS_REQUIRE_REVIEW`, `releaseGate: BLOCKED`); after human sign-off (`D6: Withdraw support`, `D8: Reopen closure review`), transitions to `SUPPORT_WITHDRAWN_OR_REOPENED` while keeping `releaseGate: BLOCKED`. |

*(Note: **Initialize Local 8D Case (No Extra Ticket)** seeds the standalone offline `CQ20` definition directly in Forge KVS without creating a second Jira ticket, using a pre-staged local amendment record for zero-ticket rehearsals.)*

[Return to the installation and evaluation guide](README.md#evaluation-guide).
