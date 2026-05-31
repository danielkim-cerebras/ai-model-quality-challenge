# AI Engineer — Model Quality & Performance Challenge

Welcome, and thanks for taking the time. This challenge has two independent tasks.

Read each task's spec in full before starting. Each lists hard requirements and a
set of **forbidden trivial baselines** that will not pass the rubric.

---

## What's in this repo

| Path | What it is |
|---|---|
| `Task1_Performance.md` | Task 1 spec — performance UI for customer + internal audiences |
| `Task2_Model_Quality.md` | Task 2 spec — benchmark/eval pruning inside `evalscope` |
| `perf_data.zip` | Task 1 data — perf projections, Models A–K × 7 traffic profiles (`.xlsx`) |
| `Evals/` | Task 2 data — model outputs (`predictions/`) + per-sample scores (`reviews/`) for LiveCodeBench, AA-LCR, MMMU |

> **Git LFS:** the files under `Evals/` are stored via [Git LFS](https://git-lfs.github.com/).
> Install it (`git lfs install`) before cloning, or the `.jsonl` files will appear as
> small pointer stubs instead of the real data.

---

## The two tasks

### Task 1 — Performance UI for Customer and Product
Turn an internal `.xlsx` perf projection sheet into something two audiences can act on:
a customer/PM who needs a **go/no-go** signal, and an internal engineer who needs to
**sanity-check** a projection. See [`Task1_Performance.md`](./Task1_Performance.md).

Run contract: document your own install and launch steps in your README — a reviewer
will clone and follow them. Your choice of framework and packaging. **Also deploy it:**
ship a publicly reachable URL (a free host is fine — Vercel, Netlify, Cloudflare Pages,
GitHub Pages, …) so a reviewer can click through without cloning, and let them **upload
the `.xlsx` files to render the views live** (we'll test it with a new model). See
[`Task1_Performance.md`](./Task1_Performance.md#deploying-for-free).

### Task 2 — Benchmark Compression for a Real Customer
Prune coding (LiveCodeBench), long-context (AA-LCR), and (forward-looking) multimodal
(MMMU) benchmarks to the smallest sample set that still gives a useful good-or-not
signal. Your pruner **must live inside [`evalscope`](https://github.com/modelscope/evalscope)**
as an upstream-quality extension. See [`Task2_Model_Quality.md`](./Task2_Model_Quality.md).

Run contract:
```bash
evalscope eval --model <model> --datasets live_code_bench --output ./results_full/
evalscope eval --model <model> --datasets live_code_bench_pruned \
    --dataset-args '{"pruning_strategy": "your_strategy", "prune_ratio": 0.1}' \
    --output ./results_pruned/
python -m evalscope_ext.tools.compare_runs --full ./results_full/ --pruned ./results_pruned/
```

Each task's spec defines exactly what to submit (code, written handouts, and/or video).

---

## How to submit

**Submit via this form:** https://docs.google.com/forms/d/e/1FAIpQLSdwLrRJkKUgTd2sisyJO10VSf1-1vJ3NIywV5HtMlUSc7ijMw/viewform?usp=publish-editor

Your submission **must** include:

1. **A private GitHub repo** with your code.
   - Keep it **private**, and grant access to the reviewers listed in the form.
   - Make it runnable from the instructions above — a reviewer will clone and run it.
   - For Task 2, pin the `evalscope` commit SHA you developed against in your fork's README.

2. **A live URL for the Task 1 UI** — **required**.
   - A publicly reachable link to your deployed frontend, running the shipped data.
   - Put it at the top of your README **and paste it into the submission form above**.
   - A free host is expected — see
     [`Task1_Performance.md`](./Task1_Performance.md#deploying-for-free) for options.
   - The repo stays private; only the deployed UI is public (the perf data is synthetic).

3. **Video walkthrough(s)** explaining your work — **required**.
   - Task 1: a ≤5-minute video covering the questions in `Task1_Performance.md`
     (what you cut and why, framework chosen vs ruled out, your assumptions, and your
     read on the model sizes / profile use-cases).
   - Task 2: walk through your pruning approach and the trade-offs in your handouts.
   - Link the video(s) in the form (Loom, Drive, YouTube-unlisted, etc.). Make sure
     reviewers can actually open the link.

A submission without a private repo, a live Task 1 URL, **and** video(s) is incomplete.
