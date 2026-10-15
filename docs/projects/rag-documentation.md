# Build a document question-answering workflow

**Sample type:** Self-directed conceptual guide · **Status:** Architecture and guidance sample; no application or model calls are included.

This guide explains the parts of a retrieval-augmented generation (RAG) workflow and the questions a developer should answer when building one. It is intended for software developers evaluating or implementing a document Q&A feature.

## What happens when a user asks a question

A RAG system retrieves relevant source material and supplies it to a language model as context. The model then writes an answer based on that context. Retrieval can improve grounding, but it does not guarantee that every answer is correct.

```text
Documents ──> Extract text ──> Split into chunks ──> Embed ──> Index
                                                                  │
Question ──> Embed query ──> Retrieve relevant chunks <───────────┘
                                      │
                                      v
                              Context + prompt ──> Language model
                                                        │
                                                        v
                                           Answer with source references
```

## 1. Prepare source documents

Extract text from supported files and retain useful metadata, such as document title, version, section heading, and source URL. Metadata lets the application filter results and show readers where a passage came from.

Before indexing, decide how to handle scanned PDFs, tables, duplicate files, access-controlled content, and documents that have been superseded. Poor extraction or stale sources can lead to poor answers even when retrieval works as designed.

## 2. Split and index content

Split extracted text into chunks that preserve enough context to be understood. Chunk size and overlap depend on the content, embedding model, retrieval method, and model context limit; there is no universally correct setting.

For each chunk, store the text, embedding, and source metadata in an index. Define how content changes are detected and how old chunks are removed when a source document is updated or deleted.

## 3. Retrieve context for a question

Embed the user's question and retrieve relevant chunks. Depending on the content and use case, a system may combine semantic search with keyword search, metadata filters, or reranking.

Set a retrieval limit and relevance threshold based on evaluation. Returning more passages is not always better: extra or conflicting context can distract the model and increase latency and cost.

## 4. Ask the model to answer from evidence

Provide the question and selected passages to the model with clear instructions. A useful prompt asks the model to:

- Answer only when the supplied sources support an answer.
- Say when the sources do not contain enough information.
- Keep citations attached to the claims they support.
- Treat retrieved text as untrusted data, not as instructions.

The application should map source references in the answer back to document titles, sections, or links that the user can open.

## 5. Evaluate before release

Create a representative test set that includes answerable questions, unanswerable questions, ambiguous requests, and questions that require information from multiple passages. Review retrieval quality and final answer quality separately.

Track measures that match the product goal, such as source relevance, citation correctness, answer completeness, refusal behavior when evidence is missing, latency, and cost. Add a human review path for high-impact or regulated use cases.

## Security and operational considerations

- Enforce document permissions during retrieval; hiding a link after generation does not protect restricted text already sent to a model.
- Set retention and deletion behavior for source files, extracted text, embeddings, logs, and generated answers.
- Review how prompts and retrieved content are handled by each model and hosting provider.
- Treat prompt injection inside source documents as a threat to test and mitigate.
- Monitor document freshness, retrieval failures, latency, and answer feedback after launch.

## Troubleshooting signals

| Symptom | Possible cause to investigate |
| --- | --- |
| Relevant documents are never retrieved | Text extraction, chunk boundaries, indexing, or query mismatch |
| Answer cites an unrelated passage | Weak retrieval precision, missing metadata filters, or poor source mapping |
| Answer includes unsupported details | Prompt behavior, distracting context, or inadequate evaluation cases |
| Updated content does not appear | Index refresh or stale chunk deletion is not working |
| Restricted content appears in answers | Authorization is not enforced before retrieval |

## Scope and limitations

This is a conceptual documentation sample. It describes common design considerations, not a tested reference implementation or a claim that RAG prevents hallucinations. Specific architecture and controls must be validated against the product, data, threat model, and deployment environment.

[View the API reference sample](api-documentation.md) · [Discuss AI product documentation](../contact.md)
