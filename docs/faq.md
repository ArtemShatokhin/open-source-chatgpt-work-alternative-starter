# FAQ: running the open source Kortix starter

Kortix is the open-source AI Management System. These answers cover the questions that come up after setup and self-hosting.

## What does the licence let me do with the code?

Kortix ships under the Elastic License 2.0, so you can self-host it, read the source and modify it for your company. That is the whole point of a repo you own: the agents, skills, memory and connector config are files you can audit, change and version like any other code.

## Where does company memory live, and can I move it?

Company memory lives in the `memory/` folder of the project repo, as plain Markdown. It moves with the repo: clone the project on another machine and the agent reads the same files. Keep entries short and factual, and update an entry in place when a fact changes so the folder stays current.

## Can an agent start work without a person asking?

Yes. A trigger starts a session on a cron schedule or a signed webhook with nobody present. The agent still lands its result as a change request, so a person reviews the diff before it reaches the default branch. Add triggers to `kortix.yaml` when the project needs them.

## Can I add my own connectors to an agent?

Kortix reaches 3,000+ apps, plus any MCP, OpenAPI, Postman, GraphQL or raw HTTP API. Connector credentials are brokered server-side and never enter the session machine. Add a connector to `kortix.yaml`, then scope it to the agent that needs it, with allow, ask or block on each tool call.

For questions that go beyond this starter, the companion site keeps a wider [Kortix FAQ](https://chatgptworkalternative.com/faq.html).
