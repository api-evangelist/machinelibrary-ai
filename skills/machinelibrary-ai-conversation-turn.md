---
name: machinelibrary-ai-conversation-turn
description: Perform a retrieval-augmented conversation with the Machine Library agent, allowing iterative refinement of queries and responses based on retrieved documents and supporting streaming, editing, and deletion of conversations.
api: openapi/machinelibrary-ai-openapi.yml
operations: [createConversationTurn, streamConversationTurn, getConversation, editConversationStep, deleteConversation]
generated: '2026-09-19'
method: generated
---

# Run and revise a retrieval-augmented conversation

Base URL `https://api.machinelibrary.ai`; authenticate with `X-Api-Key` or a Bearer token. Conversation turns cost $0.05 + $0.015 per requested result (`/v1/pricing`), so choose `limit` deliberately.

## Steps

1. **Ask** — `createConversationTurn`: `POST /v2/conversations/` with a `ConversationRequest`: `query` and `llm_config` are required; optional `conversation_id` continues an existing thread, `document_ids[]` pins exact documents into retrieval, `limit` bounds retrieved results, `max_model_documents` caps what reaches the model. Returns a `ConversationResponse`.
2. **Or stream** — `streamConversationTurn`: `POST /v2/conversations/stream` with the same body returns `text/event-stream` newline-delimited progress and result events.
3. **Read back** — `getConversation`: `GET /v2/conversations/{slug}` returns the `FullConversation` with every recorded request/response step; `listConversations` (`GET /v2/conversations/`) enumerates the caller's conversations.
4. **Revise** — `editConversationStep`: `PUT /v2/conversations/{conversation_id_or_slug}/edit-step/{step_id}` with an `EditStepRequest` replaces one request step and recomputes the conversation from that point (there is a `/stream` variant). This is a write that recomputes downstream steps; there is no documented undo.
5. **Clean up** — `deleteConversation`: `DELETE /v2/conversations/{slug}`. Deletion is not reversible and no restore operation is published (see `reversibility` in `../conventions/machinelibrary-ai-conventions.yml`).

## Errors

`400` invalid request or replacement query; `401` credential; `402` insufficient balance; `404` conversation or step not found. All bodies use the `{detail, status: "error"}` envelope.
