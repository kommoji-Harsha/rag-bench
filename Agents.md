# AGENTS.md: RAG Bench

## Project
Benchmark of retrieval strategies (BM25, vector, hybrid RRF, hybrid +
cross-encoder rerank) for RAG. Measures recall@k, MRR, nDCG,
faithfulness, citation accuracy, latency and cost.

## Corpus
<FILL IN: e.g. Indian government scheme PDFs and pages>. Raw files go in
data/raw/. Do not commit large files; document how to download them.

## Stack
Python 3.11, FastAPI, pytest, ruff, sentence-transformers,
rank_bm25 (or Tantivy), pgvector or Qdrant, Streamlit (dashboard).

## Layout
src/ragbench/{ingest,index,retrieve,rerank,generate,eval,api}
tests/, data/, results/, docs/

## Commands (always run before finishing a task)
- make install
- make lint      (ruff)
- make test      (pytest)

## Working rules
1. Do one task per session and stay in scope. Do not refactor unrelated code.
2. Use the common interfaces (Chunker, Retriever, Reranker, Generator).
   New strategies implement the interface; they don't bypass it.
3. Tests must not call real LLM or embedding APIs. Use mocks or tiny
   local fixtures.
4. Never invent numbers. Any metric shown in docs must come from
   results/results.json produced by the eval CLI.
5. Never commit secrets or datasets over 5 MB. Use environment variables.
6. Do not edit data/qa/handwritten.jsonl. It is human-written gold data.
   Synthetic questions go in data/qa/synthetic.jsonl.
7. Type hints and docstrings on all public functions.

## Definition of done
`make lint` and `make test` pass, the task's stated acceptance
criteria are met, and the PR description explains what changed, how to
run it, and any assumptions.
