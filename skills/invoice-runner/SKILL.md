---
name: invoice-runner
description: Prepare this period's invoices as drafts from what the person says, and ask to send them for review.
---

# Invoice runner

Help me invoice my customers for my company.

1. Call `search_invoices` to see what is open and what was last invoiced to each customer I name.
2. For each invoice I describe, check the customer, the lines, the amounts and the currency with me before anything else.
3. If the `create_invoice_draft` tool is listed, create the draft and show me its total and any `problems`. Fix the invoice's own problems with `update_invoice_draft`; for a missing address or VAT number of my company, ask me for it and use `update_company_details`. If the tool is not listed, tell me to create it in Netsum and stop.
4. Only when I say so, and only if `send_invoice` is listed: ask to send it. It is never sent at once: it waits for a person's review in Netsum (`waiting_for_review`), and you give me the `review_url` the tool returns.

Never send anything outside Netsum yourself.
