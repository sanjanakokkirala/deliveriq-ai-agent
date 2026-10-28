# 🚚 DeliverIQ

AI root-cause agent for a Flipkart-style e-commerce network: capacity looks adequate, yet deliveries are late. Where does the delay really come from? (Synthetic illustrative data.)

## Levers: improve the whole network

Close staffing gap: **0**%

Localize inventory (cut transfers): **0**%

Optimize dispatch & routes: **0**%

Late-order estimates scale with the remaining excess delay hours; they are model estimates, not guarantees.

## Fulfilment nodes – ranked by late orders (click a row)

Inventory allocationPick & packDispatch waitLast mile

## Detail

## Agent

Ask the agent. It reasons over the live numbers above.

## What drives late orders? (correlation across nodes)

## Algorithm used by the agent

1. **Ingest** per fulfilment node: orders/day, capacity, pickers staffed vs needed, share of orders needing inter-warehouse transfer, pick-pack hours, dispatch wait, last-mile hours, km per delivery, late-order % and complaints.
2. **Decompose** end-to-end delay into four stages and compute excess over target: `allocation = 0.18 h × transfer %`, `pick-pack = hours − 4`, `dispatch = wait − 2`, `last mile = hours − 8`.
3. **Capacity paradox test**: network utilization = orders ÷ capacity, plus the spread across nodes. Adequate average with high spread means imbalance, not shortage.
4. **Attribute** the root cause per node as the stage with the largest excess; confirm network-wide with Pearson correlation of each stage’s excess against the late-order rate.
5. **Staffing check**: `fill = staffed ÷ needed`; below 90% explains slow pick-pack.
6. **Rank** nodes by late orders = `orders × late %`.
7. **Recommend** per cause: staffing → shift or hire pickers; inventory → re-slot and allocate from nearest stock; dispatch/last mile → wave planning, route re-optimization, more riders; spare-capacity nodes absorb overflow.
8. **Simulate** levers: new late % = old × (remaining excess ÷ old excess), re-aggregated across the network.