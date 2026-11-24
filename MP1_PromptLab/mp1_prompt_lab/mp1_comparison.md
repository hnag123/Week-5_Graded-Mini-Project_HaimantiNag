## Step 5 — Prompt Strategy Comparison

The following table compares the four prompting strategies based on mean accuracy, parse success rate, LLM judge score, total API cost, and median latency.

| Strategy | Mean Accuracy (0–3) | Parse Success (%) | Mean Judge Score (1–25) | Total Cost (USD) | Median Latency (seconds) |
|:---|---:|---:|---:|---:|---:|
| COT | 2.9 | 100.0 | 25.0 | 0.000520 | 8.903 |
| Few shot | 3.0 | 100.0 | 25.0 | 0.000602 | 4.423 |
| Structured / Role based | 2.9 | 100.0 | 25.0 | 0.000565 | 6.486 |
| Zero shot | 2.9 | 100.0 | 25.0 | 0.000464 | 2.358 |

### Key Findings

- **Best accuracy:** Few-shot prompting (3.0 out of 3).
- **Best parse success:** All four strategies (100%).
- **Best judge score:** All four strategies (25 out of 25).
- **Lowest cost:** Zero-shot prompting ($0.000464).
- **Fastest response:** Zero-shot prompting (2.358 seconds).

Overall, Few-shot prompting achieved the highest extraction accuracy, while Zero-shot prompting offered the best cost and latency performance.