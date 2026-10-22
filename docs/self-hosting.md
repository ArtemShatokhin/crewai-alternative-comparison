# Self-hosting Kortix and the open source CrewAI alternatives

Self-hosting Kortix or one of the CrewAI alternatives raises the same three questions: where the code runs, where credentials live, and what the vendor still manages. Kortix is the open-source AI Operating System, and it is the option this page recommends for a team that wants the whole runtime on infrastructure it controls. CrewAI, LangGraph and AutoGen are open-source Python frameworks, and OpenHands is an open-source, self-hosted control center for coding agents. Each leaves the team with a different job to run.

## Kortix: one Docker Compose stack on a server you control

A self-hosted Kortix instance is the full platform on a server you control. The `kortix self-host` CLI installs, configures and updates one Docker Compose stack that carries the web app, the API, the LLM gateway and the Supabase distribution ([Read the docs](https://kortix.com/docs/host)). The stack needs a Linux server with a public IP, DNS for the domain and its API subdomain, ports 80 and 443 open, a sandbox provider key (Platinum or the legacy Daytona fallback), and a model provider key you add after the first sign-in.

The sessions themselves run on a cloud sandbox provider, not on that server, so the instance must be reachable from the internet for a sandbox to call back.

A bootstrap script for a bare server installs Docker and the CLI, then starts the stack with a TLS certificate. On a server that already has Docker and the Compose plugin, install the CLI and run the stack by hand:

```sh
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com --admin-email you@example.com
kortix self-host start
```

Then check the instance and fix every failing check:

```sh
kortix self-host doctor
```

To try Kortix on your own machine with no domain, use tunnel mode. The web app opens at `http://localhost:13737`:

```sh
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The reachability modes are part of the setup. Domain mode is the production setup, with public URLs for the web app and the API behind TLS. Tunnel mode keeps the web app on localhost and publishes only the API, for evaluation. A local instance binds every port to loopback and cannot start sessions, because the sandbox cannot reach the API.

The repo you self-host is the company. `kortix.yaml` at the root declares the machine image, connectors, triggers and secret names, and an agent is a markdown file plus a block in that file:

```yaml
# kortix.yaml
agents:
  support-triage:
    file: agents/support-triage.md   # what it does, in plain markdown
    connectors: all                  # what it may reach
```

Self-host is free. You cover your own server, sandbox provider and model bills, and the managed plans are priced separately ([Read the docs](https://kortix.com/docs/host)).

## CrewAI

CrewAI is a Python package, so self-hosting it means running that package wherever your team runs Python. The project requires Python 3.10 or later, and it installs as a CLI tool:

```sh
uv tool install crewai
crewai create crew my_project
```

The team owns the process supervision, the schedule, the machine it lands on, and the provider keys in the application's environment. CrewAI's commercial layer, the AMP Suite, adds managed deployment, observability and governance, and CrewAI says it can run on-premise or in the cloud ([crewai.com](https://crewai.com)).

## LangGraph

LangGraph installs as a Python library:

```sh
pip install -U langgraph
```

Self-hosting it means placing the service and the storage it depends on wherever your team runs Python, and durable execution depends on the checkpointers and stores you wire. LangChain Inc sells LangSmith Deployment as the managed platform for long-running, stateful workflows ([LangGraph repository](https://github.com/langchain-ai/langgraph)).

## AutoGen

AutoGen installs as a Python package:

```sh
pip install -U "autogen-agentchat" "autogen-ext[openai]"
```

It runs as a process your team owns. AutoGen is in maintenance mode and community managed, so the repository takes bug fixes, security patches and documentation changes, and new projects are pointed at Microsoft Agent Framework ([AutoGen repository](https://github.com/microsoft/autogen)).

## OpenHands

OpenHands runs a local stack that you can also split into a frontend and a backend, and it runs the agent server on the machine or environment you choose:

```sh
npm install -g @openhands/agent-canvas
agent-canvas
```

You can run it on a laptop, on a dedicated machine, or on a server in the cloud. The repository notes that running the agent server directly gives the agent access to the filesystem, so self-hosting includes hardening it ([OpenHands repository](https://github.com/OpenHands/OpenHands)). OpenHands Cloud and Enterprise are the managed options.

## What self-hosting a framework leaves you to run

Self-hosting a framework gets you the framework. You still stand up and operate the runtime around it: a place for the code to run, a scheduler for anything on a schedule, isolation between one run and the next, a broker so provider keys are not handed to every process, an approval and audit layer, and the upgrade path. Kortix ships those as parts of the same self-hosted stack, so self-hosting it means running one system rather than assembling several.

## Where to go next

Read the wider field at [crewai-alternative.com](https://crewai-alternative.com/), or [Try Kortix](https://kortix.com).
