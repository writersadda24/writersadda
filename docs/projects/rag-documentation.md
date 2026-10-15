# RAG Developer Documentation — Portfolio Sample

**Status:** Work in progress · **Type:** Self-directed demonstration project

## Goal

Explain a document question-answering application using Python, embeddings, vector retrieval, and a locally hosted language model.

## Conceptual architecture

```text
PDF documents
    ↓
Text extraction → Chunking → Embeddings → Vector store
                                            ↓
User question → Query embedding → Retrieval → Context + prompt
                                            ↓
                                        Local LLM
                                            ↓
                                      Grounded answer
```

## Planned sections

1. Prerequisites and installation
2. Document ingestion
3. Chunking and embedding configuration
4. Vector-store creation and persistence
5. Retrieval and prompt construction
6. Local model integration with Ollama
7. Running and testing the application
8. Limitations, evaluation, and troubleshooting

## Next steps

Link to a tested reference implementation, provide executable commands, and verify responses and retrieval behavior.
