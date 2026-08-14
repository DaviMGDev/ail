---
type: reference
title: "Worked Example of an Agent Instruction Text"
description: "One complete example text for an order-processing agent, with annotation sentences that explain the structure"
tags: [sae]
created: "2026-08-08"
updated: "2026-08-14"
---

# Worked Example

## Example text

```text
Facts:
- A queue has an order.
- A warehouse has a stock.
- Every order has a customer, an address, some items, and a status.

Rules:
- If the address of an order is valid, the order is accepted.
- If the address of an order is not valid, the order is rejected.

1. Process the order.
2. Report the status of the order.
3. If the order is accepted:
   the agent marks the order as handled.

Failure behavior:
- If the agent cannot read the address of the order, the agent reports "unreadable address" and stops.

To process an order:

1. The agent reads the address of the order.
2. If the address of the order is valid:
   the order is accepted.
3. If the address of the order is not valid:
   the order is rejected.
4. If the order is rejected:
   stop.
5. For each item of the order:
   the agent reserves the item.
6. While an item of the order is unprocessed:
   the agent processes the item.

To reserve an item:

1. The agent finds the item in the stock.
2. If the stock has the item:
   the item becomes reserved.
3. If the stock does not have the item:
   the agent reports "missing item" and continues with the next item.
```

## Annotation

The Facts-lines and the Rules-lines are knowledge.
The knowledge has no order.
The numbered lines 1 to 3 are the main flow of the text.
The failure rule is top-level knowledge.
The failure rule applies to every step of the text.
The two To-blocks are procedures.
The procedure "To process an order" has the parameter slot "an order".
Step 1 of the main flow invokes the procedure "To process an order".
The invocation binds by ordinary-English understanding.
The condition of step 2 of the procedure is open-world.
The agent knows the address of the order, so the condition is known-true or known-false.
A For-each loop fixes its collection at the entry of the loop.
Step 5 of the procedure visits every item of the order that exists at the entry of the loop.
Step 6 of the procedure is live.
The author of step 6 guarantees that the body of the loop processes the item.
A step that fails stops the flow and reports the failure.
The side effects of the steps before a failing step persist.
