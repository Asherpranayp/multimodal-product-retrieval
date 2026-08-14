# Toward Evaluable Multimodal Retrieval for Conversational Product Agents

**Asher Pranay Palle**
PhD Candidate, Artificial Intelligence — Southwest Baptist University | AI Data Engineer, Cardinality AI

## Abstract

Conversational commerce agents increasingly need to reason over both text and product imagery — matching a user's described intent ("something like this, but more casual") to a catalog of visually and semantically diverse items. Most production retrieval-augmented generation (RAG) systems are text-first: they retrieve well over documents and structured data, but treat product images as metadata rather than a first-class retrieval signal. This proposal outlines a research direction for building and evaluating a multimodal retrieval layer for conversational product agents, with a focus on evaluation methodology — measuring retrieval precision, ranking quality, and hallucination rate where "relevance" is partly visual and partly semantic.

## 1. Motivation

In production agent systems (multi-agent orchestration, MCP-based tool-calling, RAG pipelines), text-based retrieval evaluation — accuracy, latency, drift — is well understood. Two gaps stand out: (1) text-only retrieval underserves visually-driven domains like styling and product search, and (2) evaluation methodology for multimodal retrieval is less mature than for text RAG — there's no strong consensus on how to jointly measure visual correctness and grounded reasoning.

## 2. Problem Statement

Given a query combining text (style, occasion, budget) and/or image (inspiration photo, wardrobe photo), retrieve and rank catalog products that are visually consistent and contextually appropriate, and generate a grounded explanation — without hallucinating attributes the retrieved products don't have.

## 3. Proposed Approach

- **Representation:** CLIP-style joint image-text embeddings (e.g., OpenCLIP) over product images + metadata, using a small open dataset (e.g., DeepFashion) for initial experiments.
- **Retrieval + ranking:** FAISS nearest-neighbor retrieval, then a re-ranker blending embedding similarity with structured constraints (price, styling rules) — heuristic first, learned-to-rank as a stretch goal.
- **Agent integration:** expose retrieval as an MCP-style tool an LLM agent can invoke selectively.
- **Evaluation (core contribution):** Precision@k/Recall@k/NDCG for retrieval; a groundedness/hallucination-rate metric extending text-RAG hallucination detection into multimodal outputs; latency under load; a failure-mode taxonomy (visually right but contextually wrong, vice versa, hallucinated attributes).

## 4. Expected Contributions

1. Small open reference implementation of multimodal retrieval for a conversational product agent.
2. An evaluation framework/taxonomy extending text-RAG evaluation practice into multimodal settings.
3. Empirical findings on where CLIP-style retrieval succeeds/fails for styling-specific queries.

## 5. Timeline

| Phase | Duration | Output |
|---|---|---|
| Baseline retrieval (CLIP + FAISS) | 2 weeks | Working retrieval over a small product image set |
| Ranking layer + agent integration | 2 weeks | Agent that calls retrieval as an MCP-style tool |
| Evaluation harness | 1–2 weeks | Precision@k/NDCG/hallucination-rate pipeline |
| Write-up and open release | 1 week | Public repo + short technical report |

## 6. Status

Proposed research direction, early implementation. This document will be updated as the reference implementation and evaluation results are produced.

---

*Contact: [add email/LinkedIn]*
