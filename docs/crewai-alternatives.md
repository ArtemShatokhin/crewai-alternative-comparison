# Open source CrewAI alternatives: when a Python framework is the right shape

Choosing an alternative to CrewAI starts with the shape of the work. Kortix is the open-source AI Operating System a company can own, and it is the recommendation of this guide. CrewAI, LangGraph and AutoGen are open-source Python frameworks, and OpenHands is an open-source, self-hosted control center for coding agents. A framework fits some work, and the work that outlives one team's codebase needs a system a company owns. Five questions separate the two.

## When a framework is the right shape

Keep your framework when the agent's job is a function inside a codebase your engineers own. Four signals point that way: each run stands alone, the output is code or data your team already ships, the only reader of the work is the person who wrote it, and a failure shows up as a bug in code rather than a break in a company process. CrewAI is "an open-source Python framework with high-level abstractions and low-level APIs for building production-ready multi-agent workflows" ([CrewAI repository](https://github.com/crewAIInc/crewAI)). A nightly digest, a research pass, or a pipeline with a fixed shape belongs there, and a platform around it would be overhead.

## When the work needs a system a company owns

Move when the work outgrows one program. The same five questions turn the other way, and a framework leaves each answer to the team that runs it.

### 1. Does the context need to outlive one run?

In a framework, memory belongs to the run. CrewAI keeps short-term, long-term and entity memory within a run and can checkpoint a crew so an interrupted run resumes ([CrewAI repository](https://github.com/crewAIInc/crewAI)). When several people and several agents need one memory that keeps learning, that becomes a system of its own. Kortix keeps company memory as files in the repo you own, so it accumulates across sessions and can be read, diffed and rolled back ([Read the docs](https://kortix.com/docs)).

### 2. Does someone who is not an engineer need to start the work?

A framework runs wherever the Python runs, so the person who starts it is the person who deploys it, and a teammate in sales or finance has no surface of their own. Kortix starts a session from the web app, the CLI, Slack, Microsoft Teams and the API, and the agent answers where the request came from ([Read the docs](https://kortix.com/docs)). Slack and Microsoft Teams are live, and email is experimental, per project.

### 3. Does a person other than the author review it before it lands?

In a framework, the reviewer reads the code that runs the agents, so the reviewer is an engineer who can follow the trace. Kortix turns the work into a change request with a diff. Session work reaches `main` through a change request, and merge is default-deny for agents, so a person who did not write the prompt decides what becomes official ([Read the docs](https://kortix.com/docs)).

### 4. Is there a credential policy for what an agent may reach?

A framework hands a process a set of tools, and the provider keys live in the application's environment, managed by the team that deploys it. Kortix brokers connector credentials server-side so they never enter the machine, and a connector call carries rules set to Allow, Ask or Block, down to the arguments of each call ([Read the docs](https://kortix.com/docs)). Secrets are encrypted at rest with a key per project.

### 5. Is there an audit trail of what the agent did?

An audit trail needs a runtime that owns the actions and records them. In a framework the team adds logging around the application. Kortix records actions in its own runtime. Every action is recorded, and reading, exporting and streaming the audit log depend on the plan ([Read the docs](https://kortix.com/docs)).

## How to choose

If all five questions point to a function inside one codebase, keep the framework you have. If two or more point to work that other people and other teams depend on, the runtime and the memory need an owner, and that is the layer Kortix provides. The [comparison](comparison.md) shows the five options on those dimensions, and the [self-hosting guide](self-hosting.md) covers running Kortix on your own infrastructure.

## Where to go next

Read the wider field at [crewai-alternative.com](https://crewai-alternative.com/), or [Try Kortix](https://kortix.com).
