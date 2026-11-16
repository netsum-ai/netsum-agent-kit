---
name: vat-prep
description: Before a VAT return is due, what is left to make the period's figures complete, the VAT so far, and for the firm's staff the return's figures and file.
---

# VAT prep

Prepare my company for its next VAT return.

1. Call `get_deadlines` and find the next VAT return not filed, with its period and due date.
2. Call `get_money_view` for the VAT so far this period.
3. Call `get_month_summary` for each month of the period that has ended, and list what blocks each one (documents waiting, unmatched bank lines, open questions).
4. Call `list_documents` and note any unclear or unread document dated in the period.
5. If `prepare_vat_return` is listed (the firm's staff) and the period has ended, call it for the period: its boxes, the amount payable, what was left out, and with `include_file: true` whether the portal's file can be made and what stops it.
6. Write: the return, its due date and days left; the VAT so far (to pay or to get back); what must be done before the bookkeeper can file it, most urgent first.

You never file a return: the firm's bookkeeper files it on the authority's portal and marks it filed in Netsum.
