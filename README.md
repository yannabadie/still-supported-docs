# Still Supported — evaluation guide and notices

Still Supported is a Jira Forge app for reviewing a decision when one of its supporting records changes. It keeps the earlier evidence, the recorded decision and the new evidence side by side. A well-maintained evidence table can find the same facts; this app adds version-bound decisions, server-checked case ownership and stale-draft detection inside Jira.

This repository contains public evaluation documentation, not conversation history or private project records.

## Evaluation guide

Version received in Jira: application 0.7.2, Forge production 2.0.0, 16 November 2026.

A Jira site administrator can install the app through its Forge distribution link. The link will be added here after it has been received and opened. This is not a Marketplace listing.

1. Use a test Jira issue with fictional content. Assign the issue to yourself. Add the label `still-supported-demo`.
2. Open **Still Supported** from the issue's app actions.
3. Configure a case with the guided editor, or use the provided fictional carton-label example. Validate and initialize it once.
4. Receive the prepared correction. Read the original and changed source text. The old decision and Jira status remain unchanged.
5. Assign yourself the explicit **fictional supplier reviewer** role. Open an examination, select decisions and record a reason for each. The application checks the current issue assignee and role on the server.
6. Prepare a handover draft. A later evidence receipt makes that draft stale. Refreshing the case preserves the old draft; **Rebuild draft** explicitly creates a new snapshot.
7. Reload the issue to receive the stored case again. An initialized case must not be initialized a second time.

This is a synthetic evaluation. Do not enter professional, supplier, customer, confidential, medical, financial or other personal case data. The app does not certify evidence, decide automatically, modify Jira status, release stock or send customer messages.

## Privacy notice

Effective 16 November 2026. Developer: Yann Abadie, personal Codegeist project, not an employer product. Contact: yann.abadie.exakis@gmail.com.

The app reads the current Jira issue's summary, status, labels and assignee reference using the signed-in user's Jira access. It keeps case definitions, supplied fictional source texts and versions, explicit decisions, reasons, timestamps and event history in Atlassian Forge Custom Entity Store, isolated to the app installation. The initial issue reference and status are retained with the case.

Opaque Atlassian account IDs are retained to attribute actions and check the fictional reviewer role. They are not anonymous identifiers. The app does not copy profile names, email addresses, avatars, locations or job titles into its stored case, and does not maintain a user-profile cache. Account references are used with fictional evaluation records only.

There is no external AI call, advertising, payment, external database or external analytics service in the app. Forge and Jira provide the hosting and identity services. Application diagnostic logs contain operation, result/error code, fictional case ID and revision; the app does not deliberately log evidence bodies, reasons or account IDs.

Data persists between sessions to preserve the evaluation history. This version has no in-panel erasure button. Contact the developer for a request concerning a stored evaluation case or account reference; provide only the site, issue key and necessary reference, never credentials or confidential content. Access or removal must be handled through verified, authorized administration. Uninstallation and hosted-storage retention are subject to [Atlassian's Forge storage lifecycle](https://developer.atlassian.com/platform/forge/hosted-storage-data-lifecycle/).

GitHub hosts these public documents under its own privacy policy. Do not put private account information or case data in a public GitHub issue.

## Evaluation terms

Effective 16 November 2026.

You may install and use this version to evaluate Still Supported with fictional cases, including Codegeist judging. The developer charges no fee for this evaluation and requests no payment details. Your separate Jira or Atlassian subscription remains your responsibility; this invitation does not purchase or upgrade it.

You must have permission to install the app on the selected Jira site and to use the test issue. Use synthetic data only. Preserve the distinction between a supplied source, an operator's fictional decision and a real business authorization.

This experimental app is not a quality certification system, a production approval service or a substitute for professional review. A result describes the recorded evidence and explicit dispositions; it does not establish safety, conformity, customer acceptance or authorization to ship. No service-level or outcome guarantee is offered. Nothing here removes rights that applicable law does not allow to be excluded.

The app may be updated or its evaluation availability may end. Retain any evaluation material you need through authorized means. Do not rely on this version as your only record of an actual business process.

Questions and private support: yann.abadie.exakis@gmail.com.
