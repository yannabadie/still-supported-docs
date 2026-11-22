# Rehearsal & Synthetic Counterexamples — Still Supported `2.0.1` (`Forge Production [3.0.0]`)

All records, issue summaries, lot identifiers, environmental parameters, approvals, and amendments below are synthetic demonstration inputs for evaluating **Still Supported `2.0.1`** (deployed as **Forge Production `[3.0.0]`**). Still Supported never infers quality dispositions or modifies Jira workflow statuses; AI inspection tools (**Rovo `Still Supported Inspector`** and **`still-supported-mcp`**) are strictly read-only (`GET`-only, `0` AI writes), and all post-closure dispositions are signed explicitly by an attributed human reviewer.

---

## 1. 1-Click Live Linked Rehearsal on Any `Done` Jira Issue (`CQ-20` — Quantitative Scope Contraction)

1. **Open any closed (`Done`) Jira work item assigned to your account**
   - No custom Jira label or workflow scheme is required. Open the **Still Supported** issue panel (`viewportSize: large`).
2. **Seed the baseline case and linked laboratory ticket (`@1`)**
   - Click **Seed 1-Click Live Linked Demo (8D + Linked Lab Issue)**.
   - Still Supported creates and links a synthetic upstream Jira issue (`[LAB-SC20] Cold-storage barcode scan report — 24 cartons`) carrying the safety label `still-supported-upstream-lab`, binds it to evidence record `SCAN-RUN@1` (`24 cartons` `C01–C24` conditioned at `-20 °C` for `72 hours`, active stock hold `H20`), and initializes `CQ20-LIVE`:
     - Supplier decisions (`D6-implementation`, `D6-effectiveness`, `D8`) are `SUPPORTED` (`@cited === @current`).
     - Historical customer acceptance (`customer-CL20`) is `CURRENT`.
     - `releaseGate` is `CLEAR` (`ALL DECISIONS SUPPORTED`).
     - *(Optional)* Open **Tab 4 (`Handover, Audit Pack & Data Privacy`)** and click **Build Handover Draft** to snapshot a baseline handover at the current revision.
3. **Trigger the post-closure laboratory amendment (`SCAN-RUN@1 → @2`, `-50%`)**
   - In **Tab 1 (`Support Graph`)**, click **Simulate upstream lab amendment on `<ISSUE-KEY>` (24 → 12 cartons)** *(or open `[LAB-SC20]` directly in Jira and edit its description/summary so the `avi:jira:updated:issue` trigger fires automatically)*.
   - `[LAB-SC20]` updates to `[LAB-SC20] Amended cold-storage barcode scan report — 12 cartons`, appending **`SCAN-RUN@2`** (`12 cartons` `C01–C12` verified at `-20 °C`; `12 cartons` `C13–C24` remained at room temperature — **`-50%` quantitative drift**).
   - **Immediate deterministic state transition (Jira status remains `Done`)**:
     - `D6-effectiveness` and `D8` flip to `TO REVIEW` (`status: "DECISIONS_REQUIRE_REVIEW"`, `2 DECISIONS TO REVIEW`); `D6-implementation` remains `SUPPORTED` (`LABEL-WORK@1` is unchanged).
     - `customer-CL20` displays `CITES @1` (`CITES EARLIER VERSION`), preserving historical customer acceptance verbatim.
     - Any previously built handover snapshot is flagged `STALE` until explicitly regenerated via **Rebuild Handover Draft**.
     - `releaseGate` flips to `BLOCKED`.
4. **Inspect read-only via Redline Diff, Teamwork Graph, Rovo & Atlassian MCP (`0` AI Writes)**
   - **Tab 2 (`Evidence & Redline Diff`)**: Inspect the word-level LCS redline (`#FFD5D2` removals / `#BAF3DB` additions), the **Quantitative Drift Detector** (`24 cartons → 12 cartons (-50%)`), UTF-8 SHA-256 version digests, and live **Atlassian Teamwork Graph** context (`stillsupported_workItemContext`, Jira `issuelinks`, Confluence `/remotelink` SOP pages, and Atlassian Goals).
   - **Rovo Agent (`Still Supported Inspector`)**: Click **Ask Rovo Inspector** in the cockpit header (or open Rovo Chat) and run any 1-click zero-input conversation starter.
   - **Atlassian Remote MCP (`still-supported-mcp`)**: From Claude Code, Cursor, or Rovo Studio, invoke the read-only `GET` tools `inspect-decision-support`, `diff-evidence-versions`, and `discover-teamwork-context` (see [`skills/still-supported-mcp/SKILL.md`](skills/still-supported-mcp/SKILL.md)).
5. **Sign explicit human dispositions (`Tab 3 — Examine & Sign`)**
   - Click **Assume Supplier Reviewer Role** to satisfy separation-of-duties enforcement.
   - Select both decisions under review and record explicit dispositions on `@current` (`SCAN-RUN@2`):
     - **`D6-effectiveness`** → **`Withdraw support (scope no longer established)`** (`withdraw-support`)
       - *Sample rationale*: `SCAN-RUN@2 establishes -20 °C cold-storage readability for 12 cartons (C01–C12) only; C13–C24 stayed at room temperature (-50% verified cold-chain coverage). Withdraw support for the 24-carton cold-storage effectiveness claim while keeping LABEL-WORK@1 and hold H20 in place.`
     - **`D8`** → **`Reopen closure review (prerequisite or scope broken)`** (`reopen-review`) *(enforced prerequisite rule: `D8` cannot maintain closure while `D6-effectiveness` support is withdrawn)*
       - *Sample rationale*: `Closure CL20 depended on 24-carton D6 effectiveness under cold storage. Reopen supplier closure review pending re-conditioning of C13–C24; Jira Done history, customer-CL20 (@1), and stock hold H20 remain untouched.`
   - Click **Sign & Record Explicit Dispositions**.
   - **Resulting state**: Top bar displays `SUPPORT WITHDRAWN · CLOSURE REOPENED`, and `inspect-decision-support` returns `status: "SUPPORT_WITHDRAWN_OR_REOPENED"` with `releaseGate: "BLOCKED"` (`supplierToReviewCount: 0`, `supplierWithdrawnOrReopenedCount: 2`).
6. **Export the SHA-256 Audit Evidence Pack & verify GDPR controls (`Tab 4`)**
   - Click **Generate / Verify Audit Pack** to preview or download the canonical **SHA-256 Audit Evidence Pack** (`.json`, `.md`, printable `.html`) mapped to ISO 13485, IATF 16949 8D, and SOC 2.
   - Exercise self-service privacy controls:
     - **Erase my account ID (`[erased]`)**: replaces your Atlassian `accountId` with `[erased]` across stored case events while keeping the technical audit evidence intact.
     - **Erase this stored case (`CASE_ERASED`)**: purges all case data from Forge KVS and leaves an empty cryptographic tombstone rejecting stale browser tabs.

---

## 2. Synthetic Counterexamples (`CQ-18`, `CQ-19`, `CQ-20`)

Still Supported ships three complementary synthetic cases illustrating how the epistemic engine separates supported baselines, harmless editorial corrections, and material scope or measurement invalidations:

| Case | How to Load on a `Done` Issue | Evidence Shift | Quantitative Drift | Expected Epistemic & Release-Gate Outcome |
|---|---|---|---|---|
| **`CQ-18`** *(Supported Baseline & Instrument Check)* | Add Jira label `cq18` → **Initialize Labelled Fixture (`CQ18`)** | At `@1`: `E-BASE@1`, `E-WORK@1`, `E-VERIFY@1`, `R-DECISIONS@1` all match signed citations *(optional staged `@2`: `PG-7` position gauge → `DG-2` diameter-only gauge)* | `@1`: none (`@cited === @current`) | **At `@1` (Supported Baseline)**: `ALL DECISIONS SUPPORTED`, `releaseGate: CLEAR`. *(If staged `E-VERIFY@2` is received: `D3`–`D7` stay `SUPPORTED` while `D6-effectiveness` & `D8` move to `TO REVIEW`, `releaseGate: BLOCKED`.)* |
| **`CQ-19`** *(Editorial / Typo Amendment)* | Add Jira label `cq19` → **Initialize Labelled Fixture (`CQ19`)** → **Receive post-closure evidence amendment** | `E-MEASURE19@1 → @2`: report title typo `"Follow-up verificaton"` → `"Follow-up verification"` (`12` units `N01–N12`, lot `N9`, method `MP9` unchanged) | **`0` numeric shifts** (`hasQuantitativeDrift: false`) | Word-level LCS redline isolates the title typo with **`0 NUMERIC SHIFTS`** (zero false quantitative alarm); **Examine & Sign** pre-selects **Reaffirm / Maintain within scope on `@current`** (`maintain-within-scope` / `maintain`), restoring `ALL DECISIONS SUPPORTED` and `releaseGate: CLEAR`. |
| **`CQ-20`** *(Material Scope Contraction)* | **Seed 1-Click Live Linked Demo** + **Simulate upstream lab amendment** *(or **Initialize Local 8D Case (No Extra Ticket)** for offline KVS mode)* | `SCAN-RUN@1 → @2` (`[LAB-SC20]`): `-20 °C` verified cold-storage coverage drops from `24 cartons` (`C01–C24`) to `12 cartons` (`C01–C12`) under hold `H20` | **`-50%`** (`24 cartons → 12 cartons`) | Breaks `SCAN-RUN@2 → D6-effectiveness → D8` (`DECISIONS_REQUIRE_REVIEW`, `releaseGate: BLOCKED`); after human sign-off (`D6: Withdraw support`, `D8: Reopen closure review`), transitions to `SUPPORT_WITHDRAWN_OR_REOPENED` while keeping `releaseGate: BLOCKED`. |

*(Note: **Initialize Local 8D Case (No Extra Ticket)** seeds the standalone offline `CQ20` definition directly in Forge KVS without creating a second Jira ticket, using a pre-staged local amendment record for zero-ticket rehearsals.)*

[Return to the installation and evaluation guide](README.md#evaluation-guide).
