---
type: reference
title: "Worked Example of an Agent Instruction Text"
description: "One complete example text for an order-processing agent, with annotation sentences that explain the structure"
tags: [ail]
created: "2026-08-08"
updated: "2026-08-08"
---

# Worked Example

## Example text

```
A queue has an order.
A warehouse has a stock.
Every order has a customer, an address, some items, and a status.
If the address of an order is valid then the order is accepted. Otherwise the order is rejected.

First process-order(the order)!
Then report the status of the order!
Is the order accepted?

Procedure process-order(Order O):
  If the address of the order O is valid then accept the order O! Otherwise reject the order O!
  If the order O is rejected then Stop!
  For every item of the order O: reserve-item(the item)!
  While an item of the order O is unprocessed: process-item(the item)!

Procedure reserve-item(Item I):
  Reserve the item I!
  The item I is reserved.

Procedure process-item(Item I):
  If the warehouse has the item I then ship the item I! Otherwise store the item I!
```

## Annotation

An example text has a knowledge-section, a main-sequence, a query, and three procedures.
The first sentence of the example text introduces a queue and an order.
The total-case rule of the example text accepts an order with a valid address and rejects an order with an invalid address.
The main-sequence of the example text has two commands.
The query of the example text is valid at the top level.
The procedure process-order uses the command "Stop!" as a guard.
The for-every loop of the procedure process-order snapshots its collection at the entry of the loop.
The while-loop of the procedure process-order re-evaluates its condition before every pass.
The last line of the body of the procedure reserve-item is an assertion.
