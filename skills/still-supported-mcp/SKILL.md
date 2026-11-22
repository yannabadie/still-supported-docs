---
name: still-supported-mcp
description: Inspect epistemic decision support, compute word-level evidence redline diffs with quantitative drift detection, and discover linked Atlassian Teamwork Graph context on regulated Jira issues via the Forge-native `still-supported-mcp` (`rovo:mcp`) server. Use from Claude Code, Cursor, Rovo Studio, or any MCP-compatible client whenever reviewing ISO 13485 CAPA, IATF 16949 8D, aerospace MRB, clinical, or SOC 2 change/closure records in Jira.
---

# Still Supported MCP Skill (`still-supported-mcp`)

Still Supported exposes a native Atlassian Forge MCP server (`rovo:mcp` module key: `still-supported-mcp`, app ID: `a02e8917-1f2e-4737-a4d5-5a858b729799`) running 100% inside Atlassian Cloud (`Runs on Atlassian`, zero external egress).

## Core Epistemic Safety Invariant ("AI Inspects, Humans Sign")

All three MCP tools are **strictly read-only (`actionVerb: GET`, 0 AI writes)** and execute under the signed-in user's Jira and Teamwork Graph permissions:
1. **Zero silent Jira writes**: MCP tools never transition Jira status, overwrite descriptions, or post unapproved comments.
2. **Zero AI sign-offs**: MCP tools never record or renew supplier quality dispositions (`D6-effectiveness`, `D8`) or customer acceptances. Only an authenticated human reviewer inside Jira can sign a disposition on `@current` evidence.
3. **Deterministic cryptographic verification**: Every evidence version and audit summary includes deterministic UTF-8 SHA-256 digests, explicit `releaseGate` (`CLEAR` vs `BLOCKED`), and exact `@version` citations.

---

## Connecting from Claude Code, Cursor, or Rovo Studio

### 1. Rovo Studio / Atlassian Cloud (Zero-Config)
When Still Supported `2.0.1` (Forge Production deployment `[3.0.0]`) is installed on your Jira Cloud site, both **`Still Supported Inspector`** (`rovo:agent`) and **`Still Supported MCP`** (`rovo:mcp`) are automatically registered in your Atlassian site's Rovo catalog.

### 2. Claude Code / Cursor (Streamable HTTP Forge MCP Endpoint)
**Prerequisite**: Install Still Supported on **Jira** (single site installation so Rovo and MCP read the Jira KVS partition) and enable external MCP exposure in **Atlassian Administration** (`Site settings -> Connected apps -> Still Supported -> Enable tools`). On first invocation, your MCP client completes standard Atlassian OAuth 2.1 PKCE consent (`resource: https://mcp.atlassian.com/forge/a02e8917-1f2e-4737-a4d5-5a858b729799`).

#### Claude Code CLI (1-liner)
```bash
claude mcp add --transport http still-supported https://mcp.atlassian.com/forge/a02e8917-1f2e-4737-a4d5-5a858b729799
```

#### Standard `.mcp.json` / Cursor MCP Configuration
```json
{
  "mcpServers": {
    "still-supported": {
      "type": "http",
      "url": "https://mcp.atlassian.com/forge/a02e8917-1f2e-4737-a4d5-5a858b729799"
    }
  }
}
```

*(Optional)* To pair Still Supported's epistemic audit tools with Atlassian's first-party Jira/Confluence Rovo MCP tools in the same workspace, add `"atlassian-rovo": { "type": "http", "url": "https://mcp.atlassian.com/v2/mcp" }` alongside `"still-supported"`.

---

## Available MCP Tools (3 Read-Only `GET` Tools)

### 1. `inspect-decision-support`
Returns the complete epistemic support and release-gate projection for a Jira work item.
- **Input**:
  - `issueKey` (`string`, optional in Rovo Jira issue context; pass explicitly in external MCP clients, e.g. `"KAN-3"`).
- **Returns**:
  - `status`: `"ALL_DECISIONS_SUPPORTED"` | `"DECISIONS_REQUIRE_REVIEW"` | `"SUPPORT_WITHDRAWN_OR_REOPENED"` | `"UNINITIALIZED"` | `"CASE_ERASED"`
  - `releaseGate`: `"CLEAR"` | `"BLOCKED"` (remains `"BLOCKED"` with explicit `blockingReasons[]` both when evidence advances past signed citations AND when a reviewer signs `withdraw-support` or `reopen-review`).
  - `supplierToReviewCount` & `supplierWithdrawnOrReopenedCount`.
  - `decisions[]`: each supplier and customer decision with `review` (`"CURRENT"`, `"TO REVIEW"`, or `"CITES EARLIER VERSION"`), `basisComparison` (`citedVersion` vs `currentVersion`), `brokenPrerequisites` (e.g. `D6-effectiveness` breaking `D8`), and `currentDisposition`.
  - `changedEvidence[]`: multi-version records with SHA-256 digests and `quantitativeDrift` (`24 cartons -> 12 cartons (-50%)`).
  - `handover`: `{ status: "CURRENT" | "STALE" | "NOT_GENERATED", stale, snapshotRevision, currentRevision }`.
  - `auditDigestSha256`: canonical SHA-256 digest of the ISO 13485 / IATF 16949 / SOC 2 Audit Pack.

### 2. `diff-evidence-versions`
Computes a deterministic word-level Longest Common Subsequence (LCS) redline diff and quantitative scope shift between the cited version and current version of an evidence record.
- **Inputs**:
  - `issueKey` (`string`, e.g. `"KAN-3"`).
  - `recordId` (`string`, optional — defaults to the latest amended record such as `"SCAN-RUN"`).
- **Returns**:
  - `fromVersion`, `toVersion`, `before` & `after` bodies + `sha256` digests.
  - `inlineRedline`: compact inline redline (`[-removed-]{+added+}`) optimized for LLM token efficiency.
  - `quantitativeDrift`: `{ hasQuantitativeDrift, shiftCount, headline, shifts: [{ metric, before, after, delta, pctChange }] }` — cleanly separating editorial typo fixes (`0` numeric shifts) from quantitative scope contractions (`24 -> 12`, `-50%`).

### 3. `discover-teamwork-context`
Queries Jira `issuelinks`, Jira `remotelink` Confluence SOP pages, and Atlassian Teamwork Graph (`api.asUser().requestTeamworkGraph` curated query `stillsupported_workItemContext`) around the work item.
- **Input**:
  - `issueKey` (`string`, e.g. `"KAN-3"`).
- **Returns**:
  - `teamworkGraph`: `{ status: "connected" | "connected-empty-fallback-rest" | "fallback-jira-rest", queriedAri, graphObjectCount, jiraIssueLinkCount, confluenceRemoteLinkCount }`
  - `jiraIssues[]` (indicating `boundRecordId` when already tracked as versioned evidence), `confluencePages[]`, and `atlassianGoals[]`.

---

## Recommended Agent Workflow

When a user asks *"Is KAN-3 still safe to ship / close?"* or *"What changed after closure on KAN-3?"*:

1. Call **`inspect-decision-support`** with `{ "issueKey": "KAN-3" }`.
2. Check `releaseGate` (`"CLEAR"` vs `"BLOCKED"`), `status` (`"DECISIONS_REQUIRE_REVIEW"` vs `"SUPPORT_WITHDRAWN_OR_REOPENED"` vs `"ALL_DECISIONS_SUPPORTED"`), and `blockingReasons`.
3. If `changedEvidence.length > 0`, call **`diff-evidence-versions`** for each changed `recordId` (e.g. `"SCAN-RUN"`).
4. Call **`discover-teamwork-context`** with `{ "issueKey": "KAN-3" }` to check linked laboratory Jira tickets, SOP Confluence pages, and quality Goals.
5. Report clearly:
   - Whether `releaseGate` is `CLEAR` or `BLOCKED` (distinguishing unreviewed `TO REVIEW` decisions from explicitly signed `WITHDRAWN / REOPENED` dispositions).
   - Whether historical customer acceptance (`CITES EARLIER VERSION`) predates the latest evidence.
   - Exact quantitative shifts (`24 cartons -> 12 cartons (-50%)`) vs editorial-only revisions (`0` numeric shifts) and SHA-256 digests.
   - Remind the human reviewer to open the **Still Supported** cockpit in Jira (`Examine & Sign` tab) when a human disposition is needed.
