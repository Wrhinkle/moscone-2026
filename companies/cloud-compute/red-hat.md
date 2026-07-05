# Red Hat

> The enterprise Linux/Kubernetes company (an IBM subsidiary) now positioning OpenShift + vLLM as the open-source stack for deploying and serving models and agents at scale.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** silver
- **Website:** https://www.redhat.com/en/products/ai · https://github.com/vllm-project · https://github.com/llm-d/llm-d

## What they do

Red Hat's AI stack layers on top of its existing enterprise infrastructure business (RHEL, OpenShift): **Red Hat AI Inference Server** packages vLLM (Red Hat is one of the largest commercial contributors) as a supported, hardware-agnostic serving layer; **Red Hat OpenShift AI** adds a model/agent lifecycle platform (AI Hub, GenAI Studio) on Kubernetes; and **llm-d**, co-founded with CoreWeave, Google Cloud, IBM Research and NVIDIA, is a Kubernetes-native distributed-inference project targeting long-running, multi-step, agentic and RAG workloads across GPU fleets. RHEL AI bundles the open Granite models with InstructLab tuning tools. The pitch to engineers: run and scale open-weight models and agent workloads on your own infrastructure without hand-rolling an inference stack (Verified — Red Hat product pages, press release).

## Founders & origins

Founded 1993, Raleigh NC, by **Bob Young** and **Marc Ewing**; acquired by **IBM** in 2019 for **$34B**, now an independent subsidiary (Verified — Wikipedia, CNBC, multiple press).

## Evidence of real-world use

Major commercial vLLM contributor; llm-d built with CoreWeave/Google Cloud/IBM/NVIDIA as founding partners (Verified — Red Hat press release). Broad existing OpenShift/RHEL enterprise install base is the primary distribution channel.

## Relevance to agentic AI engineering

Infrastructure layer for agent serving/scaling: inference-server choice and Kubernetes-native routing matter directly to cost and latency in production agent systems.

## Sources

- https://www.redhat.com/en/products/ai
- https://www.redhat.com/en/events/red-hat-ai-engineer-worlds-fair-2026
- https://www.redhat.com/en/about/press-releases/red-hat-launches-llm-d-community-powering-distributed-gen-ai-inference-scale
- https://en.wikipedia.org/wiki/Red_Hat
- https://www.cnbc.com/2018/11/01/before-sale-to-ibm-for-billions-red-hat-started-in-cofounders-closet.html

*Profile written 2026-07-02.*
