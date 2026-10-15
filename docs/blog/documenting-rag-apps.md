# What to document in a RAG application

A retrieval-augmented generation feature can look deceptively simple in a product demo: ask a question, receive an answer with citations. Users and support teams need more context to understand why an answer appeared, when to trust it, and what to do when the source material is missing or out of date.

Documentation should cover the full information path, from source content to the answer the user sees.

## Explain what the feature can and cannot answer

Describe the kinds of documents the system can search, how recently those sources are refreshed, and which users can access them. Explain that generated answers can be incomplete or incorrect, even when they include source references. Make clear what users should do when the answer conflicts with an authoritative source.

Use examples that show both a successful answer and a case where the system should say it cannot find enough evidence. Avoid claiming that retrieval eliminates hallucinations or guarantees correctness.

## Show where answers come from

Explain how a user can open the cited source and interpret its title, section, or date. Document what a citation means in the product. If a citation identifies a retrieved passage but does not prove every sentence in the answer, state that distinction.

Also document the expected behavior when sources are unavailable, access has changed, or content has been replaced. This is especially important when an answer may persist after a user's permissions change.

## Document the source lifecycle

For administrators, describe supported file types, ingestion limits, update frequency, deletion behavior, and any processing delay. Clarify how failed imports are surfaced and how users can tell whether a document is searchable.

Teams should explain the consequences of removing a source: whether its extracted text, index entry, caches, or prior conversation history are also removed, and on what timeline. These behaviors depend on the implementation and must be confirmed with product and security owners.

## Cover privacy and access control

State which data is processed, where administrators can configure sources, who can see indexed content, and what happens to prompts and answers. Link to the product's privacy and security documentation where applicable.

Document the access model accurately. Filtering results in the interface after retrieval does not prevent restricted source text from being sent to a model. The system must enforce authorization before restricted content reaches the generation step.

## Give support teams diagnostic clues

Useful troubleshooting information includes what to check when a source is missing, a citation points to an unexpected passage, an answer is stale, or the system returns no results. Separate user actions from administrator actions, and identify when to contact support with a request ID or other safe diagnostic detail.

## Review checklist

- Are source formats, limits, and update timing explained?
- Can users inspect cited sources and understand the citations?
- Are uncertainty and unsupported-answer behavior described?
- Are access control, deletion, retention, and data processing confirmed with owners?
- Are troubleshooting steps available for missing, stale, or irrelevant results?
- Are claims about accuracy backed by evaluation evidence?

RAG documentation is strongest when product behavior, security controls, and limitations are described together. Readers can then understand not only what the feature does, but also where its boundaries are.

[Read the WritersAdda RAG guide sample](../projects/rag-documentation.md) · [Discuss AI documentation](../contact.md)
