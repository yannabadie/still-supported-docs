# Fictional rehearsal inputs

These inputs belong to the configurable carton-label example in Still Supported. They were used for the received Jira workflow. They are operator choices for a synthetic demonstration, not conclusions inferred by the software.

Start with **Adapt the carton-label example**. The case has three source records, historical supplier decisions, separate historical customer acceptance and stock hold H20. Initial receipt exposes version 1. The prepared correction is SCAN-RUN@3; no version 2 is supplied.

## Explicit decisions after SCAN-RUN@3

Select both D6 and D8 examinations and inspect the references shown by the app.

**D6 effectiveness — Withdraw support**

SCAN-RUN@3 supports cold-storage readability for C01–C12 only. C13–C24 were observed at room temperature. Withdraw support for the original 24-carton cold-storage claim; no new label failure is established. LABEL-WORK@1 remains implementation evidence and H20 remains.

**D8 supplier closure — Reopen closure review**

CL20 was closed on the original D6 effectiveness claim for all 24 cartons after cold storage. That scope lacks evidence for C13–C24 after the correction. Reopen the supplier closure review while preserving the earlier closure and customer response. Jira status and H20 are unchanged.

Record once, then receive the confirmation and exact references before continuing.

## Later evidence, after preparing a handover

Open **Open a new evidence receipt** and fill the named fields:

| Field | Value |
|---|---|
| Record receiving a new version | SCAN-RUN |
| New evidence version | 4 |
| New evidence title | Additional fictional cold-storage follow-up |
| Declared changes in this notice | Cold-storage observations for the previously missing C13–C24 are now supplied. |
| Question raised by this new evidence | Does the completed cold-storage follow-up support the original 24-carton scope? Any D6/D8 disposition remains explicit. |

**New evidence text**

Additional fictional comparison continuation. The coordinator supplies readable label observations for C13–C24 after cold storage. Combined with the preserved cold-storage observations for C01–C12, this covers the agreed 24-carton scope. No broader reliability or certification claim is made. H20 remains in place. No later supplier decision, customer acceptance or release is supplied.

**Unchanged facts declared in this notice** — one statement per line:

```text
Original C01–C12 observations and implementation are preserved.
H20 remains; no later customer decision or release is supplied.
```

Choose **Record this evidence receipt** once. The earlier handover must remain visible and become stale. Refreshing the case does not rebuild it; use **Rebuild draft** explicitly. The rebuilt draft is still **DRAFT — NOT SENT**. Stop before any later supplier disposition, customer acceptance or stock release.

[Return to the installation and evaluation guide](README.md#evaluation-guide).
