# Roboflow

> Developer platform for building, training, and deploying computer vision models — labeling, datasets, and inference in one pipeline.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** supporting
- **Founded:** 2019, Des Moines, Iowa (Verified — Wikipedia, Crunchbase)
- **Website / GitHub:** https://roboflow.com/ · https://github.com/roboflow

## What they do
Roboflow is an end-to-end computer vision stack: image/video annotation tooling, dataset management (Roboflow Universe hosts thousands of public datasets), model training (custom and fine-tuned foundation models), and a deployment layer (Inference, an open-source HTTP microservice for serving CV models to edge or cloud). Its open-source library `supervision` (38,000+ GitHub stars, 1M+ monthly PyPI downloads per its own site) provides a unified "Detections" API that normalizes outputs across YOLO, Detectron2, SAM, Hugging Face, and VLM-based detectors — making it a common glue layer engineers reach for regardless of which vision model they trained.

**Founders & funding:** Founded by Joseph Nelson and Brad Dwyer, who previously built an AR Sudoku-solving app together (Verified). Raised ~$63.6M total: $2.1M seed (2021), $20M Series A (2021, Craft Ventures), $40M Series B (2024, led by GV/Google Ventures) (Verified — Crunchbase, company blog).

**Evidence of real-world use:** Company claims over half the Fortune 100 builds with Roboflow; published case studies name BNSF Railway (train/yard inspection), USG (manufacturing), Ulteig (solar/energy monitoring), and others — real named-customer evidence, not just logos.

**Relevance to agentic AI engineering:** Vision is a frequent tool call in multimodal agent stacks (object detection/tracking as an agent "eye"); `supervision` and Inference are the kind of composable, self-hostable primitives an agent-tooling layer would call into.

## Sources
- https://roboflow.com/about
- https://blog.roboflow.com/series-b/
- https://en.wikipedia.org/wiki/Roboflow
- https://roboflow.com/customer-stories
- https://github.com/roboflow/supervision
- https://blog.roboflow.com/open-source-inference-server/
