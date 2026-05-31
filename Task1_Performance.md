# Task 1 — Performance UI for Customer and Product

## The scenario

Cerebras is known for being fast. Customers care about throughput and gen speed — they want to know, before they commit, whether a model running on us will keep up with their workload.

Today, that answer lives in an `.xlsx` perf projection sheet that only Cerebras perf engineers can read. A customer-facing PM has to open the sheet, decode the column names, and translate the numbers into something the customer can act on. The customer never sees the file directly.

Build the layer that turns those projections into an answer two different audiences can act on:

- **Customer / customer-facing PM** — needs a go/no-go signal: is the model fast enough for the workload they described? What does "fast" look like in numbers they recognize (tok/s, TTFT, context, cost implications)?
- **Internal product / deployment engineer** — needs to sanity-check a projection, see how it shifts with config, and spot anomalies before they reach a customer.

You decide how to serve both audiences. One UI with two views, two separate UIs, or a defended argument for which audience to build for first — all defensible, none obvious.


## The challenge

Build a UI that lets the two audiences above answer their questions from the shipped data. You decide what data to provide and what UI to use

## Hard requirements

- **Documented launch**. Bringing up the UI should be straightforward from a clean clone. Document your install and launch steps in your README — a reviewer will follow them.
- **Live deployed frontend**. In addition to the source, ship a **publicly reachable URL** where the UI is already running, so a reviewer can click through it without cloning or installing anything. A free host is expected — see [Deploying for free](#deploying-for-free). The deployed build must serve the same data as the repo; don't ship a stripped-down demo.
- **Upload to render**. The deployed UI must let a reviewer **upload the `.xlsx` files** — one model's set or all of them at once — and see the views render **live, with no rebuild and no code changes**. Parsing happens in the app (client- or server-side); the `Model_<X>_profile_<N>/...xlsx` naming is the only contract you can rely on. Loading the shipped data by default is fine, but upload must be a first-class path, not a dev-only script.
- **Defensible for a twelfth model**. We will exercise the upload above with a brand-new `Model L` (`Model_L_profile_<N>/Model L profile <N>.xlsx`) and expect it to appear and render correctly with **zero code edits**. Hard-coded model lists or hand-tuned views that only work for the shipped letters will be marked down.


## Forbidden trivial baselines

These will not pass the rubric. We will check.

- Static HTML dump of the `.xlsx` or a single big table with no audience differentiation.
- A UI that shows every column to every audience and calls it "configurable."
- Hard-coded views or copy that only work for the specific models in `perf_data.zip`.
- "Upload" that really means re-running a build script or editing a config to bake the data in — the deployed UI must ingest uploaded `.xlsx` and render without a rebuild.

## What to submit

Three things.

### 1. Code

A link to (or zip of) your project. Document your install and launch steps in your
README — a reviewer will clone and follow them. Your choice of framework and packaging.

### 2. Live URL

A **publicly reachable link** to the deployed UI, running the shipped data. Put it at the
top of your README **and paste it into the submission form** (link in the root README). A
reviewer should be able to open it and use it without cloning or installing anything.
Hosting on a free tier is fine and expected.

#### Deploying for free

You don't need to pay for hosting. Any of these have a no-cost tier that comfortably
covers this project — pick whichever fits your stack:

- **[Vercel](https://vercel.com)** — best for React/Next/Vite SPAs; connect the repo and it builds and deploys on push. *(Recommended starting point.)*
- **[Netlify](https://netlify.com)** — same idea, framework-agnostic; drag-and-drop a build folder or connect the repo.
- **[Cloudflare Pages](https://pages.cloudflare.com)** — generous free static hosting with a global edge.
- **[GitHub Pages](https://pages.github.com)** — zero extra accounts if your repo is already on GitHub; good for a static build.
- **[Render](https://render.com)** or **[Fly.io](https://fly.io)** — if your UI needs a small backend/server rather than a static bundle.
- **[Streamlit Community Cloud](https://streamlit.io/cloud)** or **[Hugging Face Spaces](https://huggingface.co/spaces)** — if you build a Python/Streamlit/Gradio app instead of a JS frontend.

Keep the deployment in sync with the repo, and make sure the link stays live through the
review window.

### 3. Video Explanation (5 min max)
Create a video where you explain
- What problem did you understand yourself to be solving for each audience? What did you cut and why?
- What framework did you pick and what did you rule out?
- What assumptions did you make about the data, the audience, and the deployment context?
- What would change if you had (a) more data, (b) production measurements alongside the projections, (c) more time?
- Based on the performance numbers what size do you think each model A-K represent
- Based on the traffic profile, what do you think are the use case of profile 1-7
