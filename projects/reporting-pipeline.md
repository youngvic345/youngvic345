[← Back to profile](../README.md)

# Self-healing reporting pipeline

**n8n · Python · Playwright · PostgreSQL · SQL views · Excel (generated) · WhatsApp · SMTP/IMAP · Docker**

Managers of a multi-branch pharmacy group used to wait for someone to export spreadsheets from the ERP. I built a pipeline that extracts the data, computes daily, weekly and monthly analysis, and delivers finished Excel reports to the right people on WhatsApp and email, without anyone touching it.

## How it works

```
ERP web UI ──► Playwright extraction ──► database tables ──► SQL computed views
                                                                  │
   WhatsApp + email  ◄── Excel report builder  ◄── n8n workflows ◄┘
```

- **Extraction:** the ERP had no usable API, so I drive its real web interface with Playwright and export data through the built-in configuration packages. Every domain supports arbitrary start and end dates, so any period can be re-pulled.
- **Analysis:** SQL views roll raw rows up into daily, weekly and monthly time series. Cadence is deliberate: reports always cover the last completed period.
- **Reports:** a Python and JavaScript builder generates formatted Excel files, with charts, notes and a raw-data sheet. It covers 23 report shapes, including trendlines, a profit waterfall and 100%-stacked bars. The same data feeds sales, inventory and purchase reports, and combined executive packs.
- **Delivery:** WhatsApp through a self-hosted gateway, and email with attachments. Sent mail is mirrored into the Sent folder over IMAP.
- **Scale:** about a hundred workflows in production, across sales, inventory, purchasing, finance and executive communications.

## The self-healing layer

- A failed workflow wakes an AI agent that diagnoses the cause and applies a fix, within written guardrails.
- A heartbeat checks that n8n itself is responsive, a dead-man's switch catches silent failure, and a resource monitor tracks memory and CPU.
- A host-wide watchdog kills stuck browser processes left behind by extraction or the WhatsApp gateway.
- A schedule manager gives the WhatsApp session a daily uptime window instead of blind restarts.
- Server backups run on a schedule.
- A growing playbook of failure signatures: symptom, root cause, confirmed fix.

## Hard problems I solved

- **Silent zero reports:** a missing `alwaysOutputData` setting caused workflows to send empty reports with no error. Found, fixed, and swept across every active workflow.
- **Cron races:** analysis jobs fired before extraction finished. Retimed and backfilled.
- **Stale published code:** many workflows were silently running old published versions. Fixed with a forced version bump and a verification sweep.
- **A frozen WhatsApp session** that still reported "ready" and blocked every send for most of a day. Diagnosed from process and log evidence, with a recovery playbook.
- **Out-of-memory crash** from a heavy loop inside a workflow node. Moved heavy compute into a standalone script.
- **Corrupt Excel files:** a charting gap left some real reports unopenable. I now render and inspect the actual delivered file, not a mock.
- **Historical rebuild:** reconstructed months of inventory snapshots (hundreds of thousands of rows) without gaps.

## Principles I took from it

Verify the live artifact, not just the source. Audit the leaf action, not the wrapper's "success". Check live evidence before trusting a stated cause.
