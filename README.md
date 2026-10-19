# Decision / Receipt

**A live, miniature data + ML audition for Burq.**

> Every dispatch gets a receipt. Predictions are cheap. Accountable decisions are the product.

**Created:** October 19, 2026  
**Author / project direction:** Jimmy Kahn, with an AI coding assistant.  
**Status:** Independent speculative application prototype. Not affiliated with Burq. All operations and data are synthetic.

## Try it

Open `index.html` in any modern browser. No installation, API keys, Python, backend, account, network access, or customer data required. The app is intentionally small enough to inspect fully.

1. Choose **Normal**, **Lunch rush**, or **Rainstorm**.
2. Adjust the lateness penalty and courier reliability floor.
3. Select **Run the dispatch**. Inspect an order's **decision receipt**, including model ETA, inferred lateness risk, the courier selected, counterfactual nearest option, and constraints.
4. Select **Replay actual outcomes** to generate fictional deliveries, inspect prediction errors, and update model parameters.
5. Select **Run the challenge** to force a rainy high-trust scenario. The system should decline to fill assignments it cannot justify.

## What is real, and what is not?

| Component | Implementation | Limitation |
| --- | --- | --- |
| ETA prediction | Actual ridge-regularized linear regression fitted in the browser on 1,200 generated trips | The history is synthetic, not representative of real Burq deliveries |
| Offline validation | Actual mean absolute error on 300 held-out synthetic trips | Not a deployed performance estimate |
| Assignment | Exact exhaustive small-batch search across courier options with hard reliability constraints | Five-by-five toy problem, not production routing or optimization |
| Comparison | Nearest-available baseline vs cost/risk-aware optimized assignments | A stylized counterfactual, not an A/B test |
| Probabilities | Explicit sigmoid transform of ETA distance to the delivery promise | **Not calibrated** to real late-delivery rates |
| Learning loop | Simulated actuals feed bounded online coefficient updates | Feedback is generated, not collected from customers |
| Decision receipts | Auditable display of input, chosen courier, forecast, constraint check and observed synthetic result | No persistent event store or identity/authentication |
| AI agents | **Not included** | Honest omission: no fake chat UI or false production agent claim |

## Why this product concept?

The important design choice is to make the model **accountable to a decision**. The UI prioritizes a clear decision receipt and a fail-closed reliability constraint. When an order cannot be assigned under the selected rule, it remains unassigned rather than being falsely represented as safely dispatched.

A real version would need location/time routing, event-driven ingestion, dispatch constraints, calibrated uncertainty, production MLOps, identity/permissions, data governance, a human override and real customer outcomes. AI agents should only be introduced after reliable tools, boundaries, evaluation and audit trails are in place.

## How to evaluate quickly

Try Normal / 80% first and inspect individual receipts. Then try Rainstorm / 95% and verify that orders are refused without eligible capacity. Replay a fulfillment round and observe that the weight update runs in-browser. Review `app.js` to verify no hardcoded prediction outputs or network model call exist.

## Files

- `index.html` - semantic UI
- `styles.css` - responsive visual system
- `app.js` - seeded synthetic generator, actual model training, assignment optimizer, decision receipt, and update loop
- `tests.cjs` - small Playwright integration test (requires Playwright installed)

## Privacy & security

Zero tracking, zero dependencies, no API keys, no cookies/local storage, zero network requests. The HTML can run offline. All demo names and datasets are fictional.

## Honest attribution

The project was commissioned and directed by Jimmy Kahn specifically as a short AI-assisted coding demonstration for his Burq application. Code was produced collaboratively with an AI assistant. This is a recent, self-contained proof of approach and product judgment, **not** a claim that Jimmy individually hand-authored every line or has previously operated Burq's production infrastructure.
