# Still Supported — evaluation guide and notices

**30-second setup: 1. Add label `still-supported-demo` · 2. Assign the work item to yourself · 3. Set status to Done · 4. Open Still Supported from app actions.**

Still Supported is a Jira Forge app for reviewing a decision when one of its supporting records changes. It keeps the earlier evidence, the recorded decision and the new evidence side by side. A well-maintained evidence table can find the same facts; this app adds version-bound decisions, server-checked case ownership and stale-draft detection inside Jira.

This repository contains public evaluation documentation, not conversation history or private project records.

## Evaluation guide

Current release: application **0.8.1** (2 scopes: `read:jira-work` and `storage:app`), with guided setup readiness, unfolded evidence version comparison, and stored-data erasure controls verified natively in Jira.

[Install Still Supported in Jira](https://developer.atlassian.com/console/install/a02e8917-1f2e-4737-a4d5-5a858b729799?signature=AYABeJTZWerkMRhm5PczaHBwKcoAAAADAAdhd3Mta21zAEthcm46YXdzOmttczp1cy13ZXN0LTI6NzA5NTg3ODM1MjQzOmtleS83MDVlZDY3MC1mNTdjLTQxYjUtOWY5Yi1lM2YyZGNjMTQ2ZTcAuAECAQB4CxqLTo9l4lqXuFjNim1xJM%2Bp%2F3TVP9xHS2BrU5DRRucBemLYfBVOTT4z9noIJHgIdgAAAH4wfAYJKoZIhvcNAQcGoG8wbQIBADBoBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDAQf%2FM2cE7ANsfLowQIBEIA7EyM8qV2rip5NRO0Q0ZvFBtzXw99T7TMezShSnYJRnvUhLjqi5uZVP9jagKmN6dgYnetrB%2BBsHv0sHkMAB2F3cy1rbXMAS2Fybjphd3M6a21zOmV1LXdlc3QtMTo3MDk1ODc4MzUyNDM6a2V5LzQ2MzBjZTZiLTAwYzMtNGRlMi04NzdiLTYyN2UyMDYwZTVjYwC4AQICAHi9bVMAkme4qVQX1fQHo6ePw3H40A7cGfz7yrmSfBWMXgGGviZ33UZi0BqmZy4iH76kAAAAfjB8BgkqhkiG9w0BBwagbzBtAgEAMGgGCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMbGPGvz8qnH8rU5f%2BAgEQgDuXbWkXFRt9GrlLF4rYjDIgf%2FIPMmRb2hiqZgHoWyiocb9MoxN%2Bj6u4YpLO5EjPm9AwwzEUMa%2FE%2Ft4ZuQAHYXdzLWttcwBLYXJuOmF3czprbXM6dXMtZWFzdC0xOjcwOTU4NzgzNTI0MzprZXkvNmMxMjBiYTAtNGNkNS00OTg1LWI4MmUtNDBhMDQ5NTJjYzU3ALgBAgIAeDYASx0XCjkny4iLV6vz%2BKtEGSGT6kdt0QRpkn6D%2FlVEAREzFCxCGb6JIK%2B99pkhNzYAAAB%2BMHwGCSqGSIb3DQEHBqBvMG0CAQAwaAYJKoZIhvcNAQcBMB4GCWCGSAFlAwQBLjARBAy%2FlIfoNba19Kv3UO8CARCAO1A7EEOAj6SzBUrYEzu7LElQrZE0JLaYC5aT8RnJxcWncnLspLa1ljYOIPWB8dSex%2F%2FqGVjb8U7F33cZAgAAAAAMAAAQAAAAAAAAAAAAAAAAACU9%2BwB3fJH%2FSBkeiaNeL4r%2F%2F%2F%2F%2FAAAAAQAAAAAAAAAAAAAAAQAAADIP1aLkv2hDEHxo7%2F0FzXNXRj3Yl%2BCf95Z0Z0mjMjqD9D%2BArL2CGx%2BVjNn7YhyJTcUbluZwf8KJTjDOiM2T6jvVj%2BY%3D&product=jira). A Jira site administrator can use this external distribution link to install the app on a test Jira Cloud site (external distribution link, not a Marketplace listing).

1. Use a test Jira issue with fictional content. Assign the issue to yourself and put it in a status whose Jira category is Done. Add the label `still-supported-demo`.
2. Open **Still Supported** from the issue's app actions.
3. Configure a case with the guided editor, or use the provided fictional carton-label example. Validate and initialize it once.
4. Receive the prepared correction. Read the original and changed source text. The old decision and Jira status remain unchanged.
5. Assign yourself the explicit **fictional supplier reviewer** role. Open an examination, select decisions and record a reason for each. The application checks the current issue assignee and role on the server.
6. Prepare a handover draft. A later evidence receipt makes that draft stale. Refreshing the case preserves the old draft; **Rebuild draft** explicitly creates a new snapshot.
7. Reload the issue to receive the stored case again. An initialized case must not be initialized a second time.

[Exact fictional inputs, review reasons and later evidence](REHEARSAL.md) are available for reproducing the demonstration.

This is a synthetic evaluation. Do not enter professional, supplier, customer, confidential, medical, financial or other personal case data. The app does not certify evidence, decide automatically, modify Jira status, release stock or send customer messages.

## Privacy notice

Effective 16 November 2026. Developer: Yann Abadie, personal Codegeist project, not an employer product. Contact: yann.abadie@gmail.com.

The app reads the current Jira issue's summary, status, labels and assignee reference using the signed-in user's Jira access. It keeps case definitions, supplied fictional source texts and versions, explicit decisions, reasons, timestamps and event history in Atlassian Forge Custom Entity Store, isolated to the app installation. The initial issue reference and status are retained with the case.

Opaque Atlassian account IDs are retained to attribute actions and check the fictional reviewer role. They are not anonymous identifiers. The app does not copy profile names, email addresses, avatars, locations or job titles into its stored case, and does not maintain a user-profile cache. Account references are used with fictional evaluation records only.

There is no external AI call, advertising, payment, external database or external analytics service in the app. Forge and Jira provide the hosting and identity services. Application diagnostic logs contain operation, result/error code, fictional case ID and revision; the app does not deliberately log evidence bodies, reasons or account IDs.

Data persists between sessions to preserve the evaluation history. In version 0.8.1 (`read:jira-work` and `storage:app` only), stored-data controls provide explicit self-service removal of your stored account references (replaced by `[erased]`) and custodian-confirmed erasure of a synthetic case, both verified natively in Jira. There is no periodic account reporting or external AI call. For a request concerning stored evaluation data, provide only the site, issue key and necessary reference, never credentials or confidential content. The developer does not have direct administrative access to another site's app storage. Uninstallation and hosted-storage retention are subject to [Atlassian's Forge storage lifecycle](https://developer.atlassian.com/platform/forge/storage-reference/hosted-storage-data-lifecycle/).

GitHub hosts these public documents under its own privacy policy. Do not put private account information or case data in a public GitHub issue.

## Evaluation terms

Effective 16 November 2026.

You may install and use this version to evaluate Still Supported with fictional cases, including Codegeist judging. The developer charges no fee for this evaluation and requests no payment details. Your separate Jira or Atlassian subscription remains your responsibility; this invitation does not purchase or upgrade it.

You must have permission to install the app on the selected Jira site and to use the test issue. Use synthetic data only. Preserve the distinction between a supplied source, an operator's fictional decision and a real business authorization.

This experimental app is not a quality certification system, a production approval service or a substitute for professional review. A result describes the recorded evidence and explicit dispositions; it does not establish safety, conformity, customer acceptance or authorization to ship. No service-level or outcome guarantee is offered. Nothing here removes rights that applicable law does not allow to be excluded.

The app may be updated or its evaluation availability may end. Retain any evaluation material you need through authorized means. Do not rely on this version as your only record of an actual business process.

Questions and private support: yann.abadie@gmail.com.
