# Atlassian Marketplace Submission Package — Still Supported `2.0.1`

Ready-to-paste fields for the Atlassian Marketplace Partner Portal submission (*Codegeist 2026 Bonus Track: Marketplace-Ready App*).

---

## 1. Core Listing Identity

- **App Name**: `Still Supported`
- **App ID (Forge ARI)**: `ari:cloud:ecosystem::app/a02e8917-1f2e-4737-a4d5-5a858b729799`
- **Version**: `2.0.1`
- **Tagline (`76` chars <= 80)**:
  `Audit-grade decision support & redline drift tracking for closed Jira issues`
- **Primary Product**: `Jira` (Jira Cloud, Rovo, Atlassian Teamwork Graph)
- **Categories**:
  1. `Quality Assurance & Testing`
  2. `Compliance & Risk Management`
  3. `Workflow & Process Automation`
  4. `AI & Rovo Agents`
- **Target Specialized Industries**:
  - Medical Devices & Diagnostics (`ISO 13485` CAPA & Design History Files)
  - Automotive, Aerospace & Defense (`IATF 16949` / `AS9100` 8D Corrective Actions & MRB)
  - Pharmaceuticals & Cold-Chain Logistics (`GxP` Deviation & Lot Quarantine Review)
  - Regulated Cloud & Financial Operations (`SOC 2 CC7.3 / CC8.1` Post-Incident Evidence Audits)

---

## 2. Short Summary (Marketplace Search Card)

Still Supported tracks whether signed quality and engineering decisions on closed Jira issues remain supported when upstream laboratory, test, or field evidence changes—featuring a visual Epistemic Support DAG, word-level redline diffs, quantitative drift detection, SHA-256 audit packs, and read-only Rovo + MCP inspection.

---

## 3. Highlights (3 Marketplace Feature Callouts)

1. **Interactive Epistemic Support DAG & Quantitative Drift Detector**
   Visualize how versioned evidence records and live linked Jira lab issues support `D6` effectiveness, `D8` closure, and historical customer acceptances—distinguishing typo fixes (`0` numeric shifts) from scope contractions (`24 → 12 cartons, -50%`).
2. **Word-Level Redline Diff, Live Jira Watcher & Teamwork Graph**
   Bind upstream Jira issues and Teamwork Graph objects (`Confluence` SOPs, `Atlassian Goals`). Edits to upstream issues automatically append `@v+1` via `avi:jira:updated:issue`, flagging dependent decisions `TO REVIEW` and handovers `STALE` without altering Jira status.
3. **Read-Only Rovo Inspector, Forge MCP Server & SHA-256 Audit Packs**
   Inspect broken evidence links from Rovo Chat, Claude Code, or Cursor via `still-supported-mcp` (`GET`-only: AI never signs for humans), export canonical SHA-256 ISO 13485 / IATF 16949 / SOC 2 audit packs, and exercise built-in GDPR erasure (`[erased]` & `CASE_ERASED`).

---

## 4. Detailed Marketplace Description

### The Post-Closure Evidence Problem in Regulated Industries
When a regulated engineering or quality issue closes (`Done`) in Jira, its approvals (`D6 Effectiveness`, `D8 Supplier Closure`, customer acceptance) rest on specific versions of laboratory, test, or field records (`@1`). When an amended report (`@2`) arrives weeks later narrowing the verified scope, teams face two bad choices: silently ignore the change because Jira still shows `Done`, or overwrite historical records and lose audit traceability.

### How Still Supported Solves It
- **Version-Bound Epistemic Graph**: Every decision cites immutable `RECORD@VERSION` snapshots with UTF-8 SHA-256 digests stored in Forge Custom Entity Store (`@forge/kvs`) using conditional compare-and-swap transactions.
- **Zero Silent Status Rewrites**: Closed Jira issues remain `Done` while affected supplier decisions flip to `TO REVIEW`, customer acceptances show `CITES EARLIER VERSION`, and outdated handover drafts show `STALE`.
- **Separation of Duties ("AI Inspects, Humans Sign")**: `Still Supported Inspector` (`rovo:agent`) and `Still Supported MCP` (`rovo:mcp`) expose strictly read-only `GET` tools. Only an explicitly assigned human reviewer can sign a new disposition (`Reaffirm`, `Withdraw support`, `Reopen closure review`) sealing `@current` citations.
- **100% Runs on Atlassian**: Zero external egress (`permissions.external` absent), full light/dark Atlassian Design System (`ADS`) Custom UI, and native self-service GDPR erasure controls.

---

## 5. Trust, Security & Scope Justification (Marketplace Review Notes)

- **Runs on Atlassian Eligibility**: **Yes** — 100% Forge-hosted compute (`nodejs24.x`) and Forge KVS storage (`storage:app`). Zero external domains in `manifest.yml`.
- **Scopes Justification Table**:

| Scope | Minimum-Privilege Justification |
| :--- | :--- |
| `read:jira-work` | Verify user read access to the current Jira issue and read linked upstream Jira evidence issues. |
| `write:jira-work` | GET-only Rovo/MCP actions (0 AI writes); `write:jira-work` is restricted **exclusively** to synthetic `still-supported-upstream-lab` demo tickets on explicit user click (enforced by server-side label verification). Never modifies non-synthetic Jira issues or statuses. |
| `storage:app` | Persist versioned evidence records, dispositions, watcher indices, and GDPR account register in Forge KVS (`case-state`). |
| `read:chat:rovo` | Required by Forge `rovo:agent` (`Still Supported Inspector`) for read-only conversational inspection. |
| `read:graph:issue:jira` | Discover linked Jira work items via `api.asUser().requestTeamworkGraph`. |
| `read:graph:page:confluence` | Surface linked Confluence SOP/specification pages via Teamwork Graph. |
| `read:graph:goal:atlassian` | Surface linked quality/compliance Atlassian Goals via Teamwork Graph. |

---

## 6. Legal, Support & Vendor URLs

- **Vendor / Publisher**: Yann Abadie
- **Support Email**: `yann.abadie@gmail.com`
- **Documentation URL**: `https://github.com/yannabadie/still-supported-docs#readme`
- **Privacy Policy URL**: `https://github.com/yannabadie/still-supported-docs#privacy-notice`
- **Terms of Use URL**: `https://github.com/yannabadie/still-supported-docs#evaluation-terms`
- **MCP Agent Skill URL**: `https://github.com/yannabadie/still-supported-docs/blob/main/skills/still-supported-mcp/SKILL.md`
- **Pricing Model**: Free / Included with Atlassian Cloud evaluation
