# example-aisdk-agent

A Plain agent built on the [Vercel AI SDK](https://ai-sdk.dev), with no framework in between.

The protocol is documented [here](https://www.plain.com/docs/agents/internal-agent).

## Setting it up

1. [Create an agent machine user](https://www.plain.com/docs/agents) and give it an API key.

   Permissions: `threadDiscussion:read`, `threadDiscussion:edit`,
   `threadDiscussionMessage:create`, `threadDiscussionMessage:edit`, `thread:read` and
   `thread:reply`.

2. Copy `.env.example` to `.env` in this directory and fill in `PLAIN_API_KEY`,
   `PLAIN_WEBHOOK_SECRET` from
   [Settings → Request Signing](https://app.plain.com/~/settings/request-signing/), and
   `AI_GATEWAY_API_KEY`.

3. Get a public https URL that reaches this process. By default it runs on port `8082`. Locally, `ngrok http 8082`.

4. Create the webhook under
   [Settings → Webhooks → Add webhook target](https://app.plain.com/~/settings/webhooks/add/),
   pointed at `$PUBLIC_URL/plain/webhook` on version `2026-09-06`, subscribed to
   `discussion.message_created` and `discussion.tool_call_approval_resolved`.

   `bun run check` prints the exact event list, so create the target after running it rather than
   guessing.

## Running it

```
bun install
bun run help      # the commands and what .env is still missing
bun run check     # identity, events, model, and whether anything is indexed to search
bun run serve
```

Then open a thread in Plain, click Ask Sidekick, pick your agent, and ask it to help with customer requests.

## The tools

**`list_thread_queue`** and **`search_threads`** find a thread the discussion was not opened on.
Plain does not always attach one, and without these a threadless Sidekick session has nothing to
work with. Every id they return becomes reachable for the rest of the turn.

**`read_customer_thread`** paginates `timelineEntries` and concatenates `llmText`, which is Plain's
own rendering of a timeline entry for a language model. 

**`search_knowledge`** calls `searchKnowledgeSources`, so Plain does the retrieval and you don't have to deal with vectorising your knowledge sources.

**`reply_to_customer`** is the call a customer sees, and the only one gated behind human approval. It reports
the call, asks for approval, waits, and on approval calls `replyToThread` on the parent thread.
