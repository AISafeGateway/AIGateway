# AI Firewall

A security gateway for applications that use large language models (LLMs).

> **Status: under development.** Final project (TFG) of the Higher Vocational Diploma in Multiplatform Application Development (DAM). There is no stable release yet.

## What is it?

AI Firewall is a Python gateway that sits between an application and the language model it uses. It analyzes every request and every response, allows, masks or blocks them according to a set of policies, and logs each event for auditing.

It exposes an OpenAI-compatible API, so an existing application can be protected by changing only its target address (`base_url`).

## What problem does it solve?

Companies are adopting AI assistants, and with them come the risks listed in the [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/):

- Prompt injection (direct and indirect).
- Leakage of personal or confidential data.
- Extraction of the model's internal instructions.
- Agents performing unauthorized actions.
- Lack of traceability.

## What it will include

- **Gateway** with layered detection: rules, sensitive data, AI classifier and output filter.
- **RAG assistant** that enforces role-based permissions.
- **Red teaming**: automated attacks with and without the firewall, with detection and false-positive metrics.
- **Web application**: security dashboard and demo chat with a Firewall ON/OFF switch.
- **AWS deployment** with Terraform and CI/CD, plus a local Docker alternative.

## Roadmap

| Version | Content | Status |
|---|---|---|
| v0.1 (MVP) | Gateway, rules, sensitive data, event logging, minimal chat and attack script | Pending |
| v0.2 | Output filter and risk score | Pending |
| v0.3 | RAG with role-based permissions | Pending |
| v0.4 | AI classifier for prompt injection | Pending |
| v0.5 | Web dashboard and role-based login | Pending |
| v0.6 | AWS deployment | Pending |

## Repository structure

```
ai-firewall/
├── gateway/        # API and detection layers
├── rag/            # Assistant and permissions
├── redteam/        # Attacks and metrics
├── web/            # Chat and dashboard
├── infra/          # Terraform
└── docs/           # Project documentation
```

## Documentation

All project documentation is in [`docs/`](docs/):

- [`docs/project-proposal/`](docs/project-proposal/): the submitted project proposal.
- [`docs/presentations/`](docs/presentations/): team presentations.
- [`docs/meeting-notes/`](docs/meeting-notes/): meeting notes.
- [`docs/decisions/`](docs/decisions/): technical decisions.

To contribute (branches, commits and Pull Requests), read [`CONTRIBUTING.md`](CONTRIBUTING.md).

## How to run it

Coming soon. The first version will start with `docker compose up`.

## Team

| Member | Role |
|---|---|
| Lucía Anguita Luna | Team Lead |
| Liam Bezanilla Alonso | Technical architecture, AI and security |
| Alexandru Ilie Gabriel | Data, testing and deployment |

## Responsible use

This project is educational. All test attacks target only the project's own system, and only fictional data is used.

## License

Licensed under the [Apache License, Version 2.0](LICENSE). See the [NOTICE](NOTICE) file for copyright information.
