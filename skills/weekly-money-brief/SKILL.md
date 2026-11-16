---
name: weekly-money-brief
description: Where the money stands this week, what comes in and goes out in the next weeks, and what is late, in a few lines for the owner.
---

# Weekly money brief

Write a short weekly money brief for my company.

1. Call `list_companies`, then `get_money_view` for the company: cash, what customers owe and what is overdue, what is owed to suppliers, VAT so far.
2. Call `get_upcoming` (the next 90 days) and note the lowest cash point and its date, and the largest payments due.
3. Call `get_deadlines` for anything due in the next 30 days.
4. Write at most eight lines: cash today; overdue invoices (how many, how much, the oldest customer); the next big payments; the lowest point ahead; deadlines. Amounts with their currency, dates as the person reads them.

Do not guess figures the tools did not give. If something needs the owner (a month to approve, a question waiting), end with one line saying what and where in Netsum.
