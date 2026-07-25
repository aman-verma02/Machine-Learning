
## Batch Learning

The model is trained on the **entire dataset at once**, then deployed. It doesn't learn incrementally from new data as it arrives.

**How it works:**
- Collect all training data
- Train the model in one go (or a few passes/epochs over the full dataset)
- Deploy the trained model
- To incorporate new data, you retrain from scratch (or from a checkpoint) on the full updated dataset

**Characteristics:**
- Also called "offline learning"
- Needs significant compute/time/resources per training run
- Once deployed, the model is static until the next retrain
- Works well when data doesn't change fast and you have the resources to periodically retrain

**Example:** Training a fraud detection model once a week on all transactions from the past month, then deploying that fixed model until next week's retrain.

## Online Learning

The model is trained **incrementally**, learning from data as it arrives — one instance or small mini-batch at a time.

**How it works:**
- Feed data sequentially (a stream)
- Model updates its parameters after each instance/mini-batch
- No need to store the whole dataset — you can discard data after learning from it
- The model keeps adapting continuously

**Characteristics:**
- Cheap, fast updates — good when data arrives continuously (streaming)
- Great for **concept drift** — when the underlying data patterns change over time (e.g., stock prices, user behavior)
- Risk: bad or noisy data can degrade the model quickly since it updates live — you often need to monitor performance and have a rollback plan
- Learning rate matters a lot — how much weight new data gets vs. old learned patterns

**Example:** A recommendation system that updates as users click, adapting to trending preferences in real time.

## Key Tradeoff Table

| | Batch | Online |
|---|---|---|
| Data availability | Need full dataset upfront | Can start with a stream |
| Compute pattern | Heavy, periodic | Light, continuous |
| Adaptability | Slow (only updates on retrain) | Fast (updates continuously) |
| Risk of drift | Model can go stale between retrains | Can adapt to drift automatically |
| Risk of corruption | Lower (controlled retrain env) | Higher (bad data can hurt immediately) |
| Typical use case | Stable environments, resource-rich | Streaming data, resource-constrained, fast-changing environments |

A useful mental model: batch learning is like studying for an exam by cramming with all your notes at once; online learning is like learning on the job, updating your understanding a little every day as new info comes in.

Want me to go deeper into how online learning is implemented (e.g., SGD-based incremental updates, learning rate schedules) or how this maps to something like your anomaly detection project — that could actually benefit from online learning if you're dealing with streaming logs?