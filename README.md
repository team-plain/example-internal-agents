# Plain custom agent examples

**These examples now live in one repository each.** Use the repositories below; the directories
here are kept only so existing links keep working, and they are no longer maintained.

| Repository | Agent built with | Reach for it when |
| --- | --- | --- |
| [`example-eve-assistant-agent`](https://github.com/team-plain/example-eve-assistant-agent) | [Vercel eve](https://github.com/vercel/eve) | you want durable sessions and a working harness. |
| [`example-aisdk-assistant-agent`](https://github.com/team-plain/example-aisdk-assistant-agent) | [Vercel AI SDK](https://ai-sdk.dev) | you want to own the model loop and build your own harness. |

Each repository keeps the full history of its example and stands alone: its own lockfile, its own
CI, and a README covering setup and the five tools it implements. The package name in each one
changed to match its repository.

## What the agents do

Both are discussion agents built on Plain's API, with the same five tools:

- `list_thread_queue` and `search_threads` find a thread the discussion was not opened on
- `read_customer_thread` reads a customer thread
- `search_knowledge` searches your knowledge sources in Plain
- `reply_to_customer` replies to a customer thread, gated behind human approval

To use one, start an "Ask Sidekick" conversation in Plain and pick your custom agent.

## Docs

The protocol is documented under
[custom internal agents](https://www.plain.com/docs/agents/internal-agent). If you want a support
agent that answers customers instead, see
[support agents](https://www.plain.com/docs/agents/support-agent).
