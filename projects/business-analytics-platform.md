[← Back to profile](../README.md)

# Business analytics platform

**Next.js · TypeScript · Tailwind and shadcn/ui · PostgreSQL · materialised views · Netlify**

An internal web application for a pharmacy group. Where the reporting pipeline pushes reports out, this is where people go to look things up, correct data and see the whole business, with each role seeing only what it should.

## Modules

Sales and revenue, inventory, purchasing, finance, insurance and claims, remittances, staff performance, an executive overview, upload links for staff, and a help section.

## What I built

- **Seven roles, six modules:** access is editable at runtime, per page, tab, column and export, by role and by individual account. A CEO role and an owner-only area sit on top.
- **Claims tracking:** a filterable claims table with a document checklist per claim (invoice, claim form, prescription, pre-authorisation, report).
- **Remittance handling:** insurer payment files are hashed so the same file cannot be loaded twice, and a confirmed-payment key blocks duplicates. A real delete reverses confirmed amounts.
- **Data corrections:** a per-claim insurer override for admin and operations staff. Corrections use strict dropdowns of known values instead of free text, with an "Other" fallback.
- **CEO reporting pack:** a template-driven Excel export, with month-range export and dynamic formula ranges.
- **Document capture:** a self-hosted document-corner-detection model, run as a service, replaced an older OpenCV heuristic for photographing paperwork.
- **Performance:** a "no page loads" problem traced to unbounded queries. Fixed with lazy pagination, indexes, six materialised views and a scheduled refresh.
- **Sign-in:** magic links through a real mailbox, self-service forgot-password and set-password, a redesigned login, and a cross-domain sign-in bug fixed in middleware.
- **Platform plumbing:** git-triggered deploys, a custom domain, and a read-only diagnostic API (with a narrow, audited ability to replace computed views) for investigating production data safely.
- **Database as a product:** the computed layer was rebuilt as a Postgres view hierarchy so the platform no longer depended on the automation tool's data tables.

## Engineering notes

- Schema changes go through a documented migration path, because the app's database roles cannot run DDL.
- A new enum value needs its database constraints updated too, not just the TypeScript types.
- I packaged the deploy and database know-how into project skills so the process is repeatable.

## Status

Live and in daily use by the team.
