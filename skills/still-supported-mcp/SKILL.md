---
name: still-supported-mcp
description: Inspect epistemic decision support, compute word-level evidence redline diffs with quantitative drift detection, and discover linked Atlassian Teamwork Graph context on regulated Jira issues via the Forge-native `still-supported-mcp` (`rovo:mcp`) server. Use from Claude Code, Cursor, Rovo Studio, or any MCP-compatible client whenever reviewing ISO 13485 CAPA, IATF 16949 8D, aerospace MRB, clinical, or SOC 2 change/closure records in Jira.
---

# Still Supported MCP Skill (`still-supported-mcp`)

Still Supported exposes a native Atlassian Forge MCP server (`rovo:mcp` module key: `still-supported-mcp`) running 100% inside Atlassian Cloud (`Runs on Atlassian`, zero external egress).

## Core Epistemic Safety Invariant ("AI Inspects, Humans Sign")

All three MCP tools are **strictly read-only (`actionVerb: GET`)** and execute under the signed-in user's Jira and Teamwork Graph permissions:
1. **Zero silent Jira writes**: MCP tools never transition Jira status, overwrite descriptions, or post unapproved comments.
2. **Zero AI sign-offs**: MCP tools never record or renew supplier quality dispositions (`D6-effectiveness`, `D8`) or customer acceptances. Only an authenticated human reviewer inside Jira can sign a disposition on `@current` evidence.
3. **Deterministic cryptographic verification**: Every evidence version and audit summary includes deterministic UTF-8 SHA-256 digests and exact `@version` citations.

---

## Connecting from Claude Code, Cursor, or Rovo Studio

### 1. Rovo Studio / Atlassian Cloud
When Still Supported `2.0.0` is installed on your Jira Cloud site, both **`Still Supported Inspector`** (`rovo:agent`) and **`Still Supported MCP`** (`rovo:mcp`) are automatically registered in your Atlassian site's Rovo catalog.

### 2. Claude Code / Cursor (via Atlassian Remote MCP)
Connect your MCP client to your Atlassian Cloud MCP endpoint with OAuth 2.1 user consent, enabling the `still-supported-mcp` toolset:

```json
{
  "mcpServers": {
    "atlassian-still-supported": {
      "url": "https://mcp.atlassian.com/v1/sse",
      "description": "Atlassian Remote MCP including Still Supported epistemic audit tools"
    }
  }
}
```

---

## Available MCP Tools (3 `GET` Tools)

### 1. `inspect-decision-support`
Returns the complete epistemic support projection for a Jira work item.
- **Input**:
  - `issueKey` (`string`, required): Jira issue key, e.g. `"KAN-3"`.
- **Returns**:
  - `status`: `"ALL_DECISIONS_SUPPORTED"` | `"DECISIONS_REQUIRE_REVIEW"` | `"UNINITIALIZED"` | `"CASE_ERASED"`
  - `decisions[]`: each supplier and customer decision with `review` (`"CURRENT"`, `"TO REVIEW"`, or `"CITES EARLIER VERSION"`), `basisComparison` (`citedVersion` vs `currentVersion`), `brokenPrerequisites` (e.g. `D6-effectiveness` breaking `D8`), and `currentDisposition`.
  - `changedEvidence[]`: multi-version records with SHA-256 digests and `quantitativeDrift` (`24 cartons -> 12 cartons (-50%)`).
  - `handover`: `{ status: "CURRENT" | "STALE", snapshotRevision, currentRevision }`.
  - `auditDigestSha256`: canonical SHA-256 digest of the ISO 13485 / IATF 16949 / SOC 2 Audit Pack.

### 2. `diff-evidence-versions`
Computes a deterministic word-level Longest Common Subsequence (LCS) redline diff and quantitative scope shift between the cited version and current version of an evidence record.
- **Inputs**:
  - `issueKey` (`string`, required): Jira issue key, e.g. `"KAN-3"`.
  - `recordId` (`string`, required): Evidence record ID, e.g. `"SCAN-RUN"`.
- **Returns**:
  - `fromVersion`, `toVersion`, `before` & `after` bodies + `sha256` digests.
  - `inlineRedline`: compact inline redline (`[-removed-]{+added+}`) optimized for LLM token efficiency.
  - `quantitativeDrift`: `{ hasQuantitativeDrift, shiftCount, headline, shifts: [{ metric, before, after, delta, pctChange }] }` — cleanly separating editorial typo fixes (`0` numeric shifts) from quantitative scope contractions (`24 -> 12`, `-50%`).

### 3. `discover-teamwork-context`
Queries Jira `issuelinks` and Atlassian Teamwork Graph (`api.asUser().requestTeamworkGraph`) around the work item.
- **Input**:
  - `issueKey` (`string`, required): Jira issue key, e.g. `"KAN-3"`.
- **Returns**:
  - `teamworkGraph`: `{ status: "connected" | "fallback-jira-rest", queriedAri, graphObjectCount, jiraIssueLinkCount }`
  - `jiraIssues[]` (indicating `boundRecordId` when already tracked as versioned evidence), `confluencePages[]`, and `atlassianGoals[]`.

---

## Recommended Agent Workflow

When a user asks *"Is KAN-3 still safe to ship / close?"* or *"What changed after closure on KAN-3?"*:

1. Call **`inspect-decision-support`** with `{ "issueKey": "KAN-3" }`.
2. If `supplierToReviewCount > 0` or `changedEvidence.length > 0`, call **`diff-evidence-versions`** for each changed `recordId` (e.g. `"SCAN-RUN"`).
3. Call **`discover-teamwork-context`** with `{ "issueKey": "KAN-3" }` to check linked laboratory Jira tickets, SOP Confluence pages, and quality Goals.
4. Report clearly:
   - Which supplier decisions are `CURRENT` vs `TO REVIEW` (and whether `D8` is blocked by a broken `D6-effectiveness` prerequisite).
   - Whether historical customer acceptance (`CITES EARLIER VERSION`) predates the latest evidence.
   - Exact quantitative shifts (`24 cartons -> 12 cartons (-50%)`) vs editorial-only revisions (`0` numeric shifts) and SHA-256 digests.
   - Remind the human reviewer to open the **Still Supported** cockpit in Jira (`Examine & Sign` tab) to record their signed disposition.
