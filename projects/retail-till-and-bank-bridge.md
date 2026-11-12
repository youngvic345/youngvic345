[← Back to profile](../README.md)

# Retail till & bank bridge

**Python · FastAPI · Odoo (POS and Accounting) · Windows WebView2 · Chrome extension · Docker**

A retail business takes most of its money through M-Pesa and bank transfers, but its till and its books did not talk to each other. Cashiers had to trust a customer's phone screen, and the accountant matched thousands of bank lines by hand. I built the system that closes that gap: a locked-down till program, and a bridge that connects the bank to the ERP.

## What I built

**1. The bank bridge (server)**
- Receives every transaction from a Kenyan bank's open-banking API and creates exactly one bank-statement line in Odoo for it, checking for duplicates locally and in Odoo.
- Reconciles automatically in three steps: a document number in the bank narrative links straight away; otherwise saved, human-approved rules apply (bank charges, rent, utilities and so on); otherwise the line goes to a review queue with suggestions of the same amount.
- Handles part-payments, payments spread over several documents, and overpayments held as customer credit.
- Sales orders: a payment on a quotation is held as credit, the order confirms once a deposit percentage is reached, a down-payment invoice is created, and the final invoice deducts deposits.
- A worker retries failed posts, fills gaps by pulling from the bank, and purges bank content within the retention period the bank requires.
- An end-of-day check compares the bank balance with the ERP's bank journal and lists every unexplained line and every unpaid order.

**2. The till program ("Counter")**
- A Windows kiosk application that wraps the Odoo POS in WebView2, so the cashier sees a normal POS but cannot leave it.
- Shows incoming M-Pesa payments live, lets the cashier claim one payment for one sale (one use only, with a 30-minute undo), and guards the Validate button so a sale cannot complete without a verified payment.
- A PIN override with a recorded reason for exceptions.
- Closing the register is blocked when payments are missing, and a session-close step pairs each sale with its receipt.
- Self-updating, with signed releases, an installer with a setup wizard, and a watchdog.
- White-label by design: one brand file, one server and one signing key per business, so a second business can be set up from a walkthrough.
- An earlier Chrome extension version of the same idea, and an installable web app for phones and tablets.

**3. The accountant's workspace inside Odoo**
- A "Bank Bridge" area in Accounting with Home, Work (queue, payouts), Controls (end of day, POS sessions) and Setup (rules, payees, people and access, settings).
- The bridge polls Odoo for requests and writes answers back, so it needs no inbound connections. Only accounting managers approve rules, and only approved rules ever run on live data.

**4. Speed and operations**
- Odoo webhooks replaced slow polling: a payment request went from about 28 seconds to about 3 seconds.
- A redesigned operations console, with a widget per page and a phone layout.
- Card payments through a payment gateway: an arithmetic matcher that works out fees and payouts, rehearsed in shadow mode alongside the real process before being trusted.

## Engineering habits worth noting

- Every script that touches Odoo is idempotent and refuses to run against the live database unless told to.
- Rehearsed on an isolated copy first: realistic scenarios ran end to end with all checks passing before anything touched live data.
- Backlog clean-ups run in three modes: a read-only preflight that writes a plan with checksums, an apply step that re-checks each line just before writing, and an independent verify step. A rerun writes nothing.
- Tested on real Windows machines with real clicks, and I recorded what was not tested.

## Status

Live in production at the client, with the till and bridge in daily use.
