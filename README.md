# Awesome AgentOps

> A curated guide to operating AI agents in production: observability, evaluation, tracing, guardrails, deployment, security, governance, and incident response.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Links Checked](https://img.shields.io/badge/links-checked-brightgreen.svg)](#contents)
[![Focus: AgentOps](https://img.shields.io/badge/focus-AgentOps-blue.svg)](#scope)
[![Status: v0.1](https://img.shields.io/badge/status-v0.1-informational.svg)](#contributing)

AgentOps is the production operating layer for AI agents. It is broader than agent monitoring: it covers how teams ship, observe, evaluate, debug, secure, control, and improve autonomous or semi-autonomous AI systems after they leave a demo environment.

This list is intentionally focused on engineering resources for production agents. It favors tools, papers, patterns, and references that help teams answer operational questions:

- What did the agent do, and why?
- Did it complete the task correctly, safely, and within policy?
- Can we replay, debug, and evaluate failures?
- Can humans approve, interrupt, or override high-impact actions?
- Can we manage cost, latency, secrets, identity, and permissions?
- Can we respond to agent incidents with evidence instead of guesswork?

## Contents

- [Scope](#scope)
- [Conceptual Map](#conceptual-map)
- [AgentOps vs DevOps vs MLOps](#agentops-vs-devops-vs-mlops)
- [Observability and Tracing](#observability-and-tracing)
- [Evaluation and Testing](#evaluation-and-testing)
- [Replay and Debugging](#replay-and-debugging)
- [Guardrails and Runtime Controls](#guardrails-and-runtime-controls)
- [Security, Identity, and Access Control](#security-identity-and-access-control)
- [Human Approval and Workflow Control](#human-approval-and-workflow-control)
- [Deployment and Runtime Infrastructure](#deployment-and-runtime-infrastructure)
- [Cloud AgentOps Platforms](#cloud-agentops-platforms)
- [Cost, Latency, and Reliability](#cost-latency-and-reliability)
- [Incident Response and Governance](#incident-response-and-governance)
- [Multi-Agent Operations](#multi-agent-operations)
- [Standards and Protocols](#standards-and-protocols)
- [Research and References](#research-and-references)
- [Contributing](#contributing)

## Scope

Included:

- Production agent observability, tracing, evaluation, testing, and replay.
- Runtime guardrails, policy checks, approvals, and control planes.
- Agent security, identity, permissions, sandboxing, and secret handling.
- Deployment, reliability, cost, latency, and incident response practices.
- Multi-agent coordination and operational failure modes.

Not included by default:

- Generic LLM chat apps without an operational angle.
- Prompt collections with no evaluation or production discipline.
- Broad AI tool directories that do not focus on running agents.
- Vendor marketing pages without useful engineering substance.

## Conceptual Map

AgentOps spans the full lifecycle of an agent system:

1. **Design**: define tasks, tools, permissions, policies, and success criteria.
2. **Build**: instrument traces, model calls, tool calls, memory, and state transitions.
3. **Test**: run unit tests, scenario tests, adversarial tests, and regression evals.
4. **Deploy**: manage environments, secrets, rollout, rate limits, and fallbacks.
5. **Operate**: monitor correctness, safety, cost, latency, drift, and incidents.
6. **Improve**: replay failures, evaluate fixes, update policies, and govern change.

## AgentOps vs DevOps vs MLOps

AgentOps overlaps with DevOps and MLOps, but it is not the same discipline.

DevOps focuses on shipping and operating software systems: infrastructure, CI/CD, deployment, monitoring, reliability, and incident response.

MLOps focuses on the machine learning lifecycle: datasets, training pipelines, model registries, model deployment, drift, performance monitoring, and retraining.

AgentOps focuses on the operational behaviour of AI agents after they are given goals, tools, memory, context, permissions, workflows, and the ability to take actions.

| Discipline | Primary concern | Typical operational objects | Key questions |
|---|---|---|---|
| DevOps | Software delivery and infrastructure reliability | Services, containers, APIs, databases, networks, deployments | Is the system available, scalable, secure, and deployable? |
| MLOps | Model and data lifecycle management | Datasets, features, models, training jobs, model endpoints, drift metrics | Is the model trained, evaluated, deployed, monitored, and updated correctly? |
| AgentOps | Agent behaviour in production | Agent runs, tool calls, traces, memory, plans, policies, approvals, permissions, outcomes | Did the agent act correctly, safely, within policy, and with enough evidence to debug or govern it? |

AgentOps extends operational practice into areas that traditional DevOps and MLOps do not fully cover:

- agent trajectories and step-by-step execution traces
- tool-use monitoring and permission boundaries
- memory, context, and retrieval behaviour
- runtime policy checks and guardrails
- human approval for high-impact actions
- replay and debugging of agent failures
- evaluation of task completion, behaviour, and safety
- auditability of autonomous or semi-autonomous decisions

A useful shorthand:

```text
DevOps keeps the software running.
MLOps keeps the model lifecycle controlled.
AgentOps keeps agent behaviour observable, evaluable, constrained, and governable.
```

## Observability and Tracing

- [OpenTelemetry](https://opentelemetry.io/) - Vendor-neutral observability framework for traces, metrics, and logs.
- [OpenLLMetry](https://github.com/traceloop/openllmetry) - OpenTelemetry-based instrumentation for LLM applications.
- [Langfuse](https://github.com/langfuse/langfuse) - Open-source LLM engineering platform with tracing, prompt management, evals, and metrics.
- [Arize Phoenix](https://github.com/Arize-ai/phoenix) - Open-source observability and evaluation for LLM applications.
- [LangSmith](https://www.langchain.com/langsmith) - Platform for tracing, debugging, evaluating, and monitoring LangChain and agent applications.
- [Weights & Biases Weave](https://github.com/wandb/weave) - Tracking and evaluation for LLM applications.
- [Helicone](https://github.com/Helicone/helicone) - Open-source observability platform for LLM usage, cost, latency, and requests.
- [AgentOps](https://github.com/AgentOps-AI/agentops) - Session replay, analytics, and observability for AI agents.
- [ax](https://github.com/Necmttn/ax) - Local telemetry and recall graph for AI coding-agent sessions, including cost, tool, skill, routing, hook, and OTLP analytics.
- [agent-watch](https://github.com/soul-sol/agent-watch) - POSIX shell scripts that classify background coding-agent runs as RUNNING, DONE, FAILED, or STALL and preflight transport versus authentication failures.
- [Failproof](https://github.com/FailproofAI/failproofai) - Tracing and runtime policy enforcement for coding-agent harnesses such as Claude Code, Cursor, and GitHub Copilot.
- [Agent Observatory](https://github.com/abhishekash/agent-observatory) - Local dashboard for inspecting coding-agent sessions, tool activity, MCP calls, traces, and host processes.
- [LiteLLM Lens](https://docs.litellm.ai/docs/proxy/lens) - Agent trace analysis for LiteLLM Proxy that investigates failures across runs, groups recurring problems, and links findings to the original OpenTelemetry traces.
- [MLflow Tracing](https://mlflow.org/docs/latest/genai/tracing/) - Open-source tracing for LLM and agent applications with OpenTelemetry ingestion, LLM-judge evaluation, and links to MLflow experiment lineage.
- [OpenInference](https://github.com/Arize-ai/openinference) - OpenTelemetry instrumentation and span conventions for tracing LLM calls, tools, and agent frameworks.
- [Pydantic Logfire](https://github.com/pydantic/logfire) - OpenTelemetry-based observability SDK and platform that renders GenAI, OpenInference, and OpenLLMetry agent spans alongside application telemetry.
- [Datadog LLM Observability](https://docs.datadoghq.com/llm_observability/) - Tracing, evaluation, and cost monitoring for LLM and agent applications within Datadog, including OpenTelemetry GenAI span ingestion.
- [Flowcept](https://github.com/ORNL/flowcept) - Provenance capture for scientific and agentic workflows that records prompts, model calls, and tool use as W3C PROV lineage via the PROV-AGENT model.
- [Claude Agent SDK Observability](https://code.claude.com/docs/en/agent-sdk/observability) - OpenTelemetry export of traces, metrics, and events for Claude Agent SDK runs, including tool calls, hooks, and nested subagent spans.
- [Flowlines](https://flowlines.ai/) - Hosted analytics for MCP servers and agent sessions that links tool adoption, reported outcomes, and recurring failures to the source sessions.



## Evaluation and Testing

- [OpenAI Evals](https://github.com/openai/evals) - Framework and registry for evaluating language model behaviour.
- [DeepEval](https://github.com/confident-ai/deepeval) - Evaluation framework for LLM applications with regression testing support.
- [Ragas](https://github.com/explodinggradients/ragas) - Evaluation framework for retrieval-augmented generation and LLM pipelines.
- [promptfoo](https://github.com/promptfoo/promptfoo) - CLI and framework for testing prompts, models, and LLM applications.
- [Giskard](https://github.com/Giskard-AI/giskard) - Testing and risk scanning for AI systems.
- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) - Framework for large language model evaluations.
- [Braintrust](https://www.braintrust.dev/) - Evaluation, logging, and prompt iteration platform for AI products.
- [AgentCompass](https://arxiv.org/abs/2607.13705) - Evaluation infrastructure for agent benchmarks, harnesses, environments, asynchronous execution, and trajectory-level failure analysis.
- [LLMs Get Lost in Evolving User Intent](https://github.com/microsoft/evolving-intent) - Benchmark framework for testing whether agents track incrementally revealed, revised, and redirected user intent across multi-turn tasks.
- [YYLO Benchmark](https://github.com/yylo-dev/yylo-benchmark) - Longitudinal evaluation and immutable evidence for agent runs: fresh-repository attempt isolation, deterministic and LLM-judge evaluation profiles, and hash-linked receipts, manifests, and provenance.
- [ClawBench](https://github.com/TIGER-AI-Lab/ClawBench) - Benchmark for browser agents on everyday tasks across live websites, with isolated runs and multi-layer execution traces.
- [Holistic Agent Leaderboard (HAL)](https://github.com/princeton-pli/hal-harness) - Harness for running agent benchmarks in parallel across local and cloud environments with cost tracking and log inspection.
- [PerspectiveGap](https://github.com/WhymustIhaveaname/PerspectiveGap) - Benchmark for multi-agent orchestration prompts that tests whether a model gives each sub-agent the context it needs without omissions or cross-role leakage.


## Replay and Debugging

- [LangSmith Tracing](https://docs.langchain.com/langsmith/home) - Trace inspection, dataset creation, and regression workflows for agent runs.
- [Langfuse Tracing](https://langfuse.com/docs/observability/overview) - Traces for LLM calls, tool calls, chains, and agent sessions.
- [Phoenix Tracing](https://docs.arize.com/phoenix/tracing) - OpenTelemetry-based tracing for LLM application debugging.
- [Weave Tracing](https://docs.wandb.ai/weave) - Tracing and interactive debugging for model and agent workflows.
- [agenttrace](https://github.com/luoyuctl/agenttrace) - Local-first TUI and report generator for auditing AI coding-agent session logs, cost, tokens, latency, tool failures, health, and regression checks.
- [Transect](https://github.com/AI-Safety-Institute/transect) - Transcript analysis for long-horizon agent evaluations that places events, token use, sub-agent activity, and LLM-judge behaviour labels on a turn-based timeline, with judge-disagreement flags and links back to the source transcript.

## Guardrails and Runtime Controls

- [Guardrails AI](https://github.com/guardrails-ai/guardrails) - Validation and guardrail framework for LLM inputs and outputs.
- [NVIDIA NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) - Toolkit for programmable guardrails around LLM applications.
- [Llama Guard](https://www.llama.com/docs/model-cards-and-prompt-formats/llama-guard-3/) - Meta's safety classification model family for policy enforcement.
- [Rebuff](https://github.com/protectai/rebuff) - Prompt injection detection and mitigation framework.
- [Lakera Guard](https://www.lakera.ai/lakera-guard) - Runtime protection for LLM applications against prompt injection and unsafe content.
- [OpenAI Moderation](https://developers.openai.com/api/docs/guides/moderation) - Content safety models and moderation patterns.
- [Speakeasy](https://www.speakeasy.com/product/ai-control-plane) - Control plane for policy enforcement, access control, and audit trails across AI agents, MCP servers, and tool calls.
- [Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit) - Middleware that evaluates agent tool calls, resource access, and inter-agent messages against YAML, Rego, or Cedar policies before execution.

## Security, Identity, and Access Control

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - Security risks for LLM and agent systems.
- [OWASP Agentic Security Initiative](https://genai.owasp.org/initiatives/agentic-security-initiative/) - Security work focused on agentic AI systems.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - Risk management framework for AI systems.
- [PyRIT](https://github.com/Azure/PyRIT) - Microsoft framework for red teaming generative AI systems.
- [garak](https://github.com/NVIDIA/garak) - LLM vulnerability scanner and red-teaming tool.
- [Invariant](https://github.com/invariantlabs-ai/invariant) - Testing and guardrails for agent behaviour and tool use.
- [AffixIO](https://www.npmjs.com/package/affixio) - Agentic Pay Kit (`npm i affixio`) with host-side signed ACTION attestation / KYA for agent pay flows (x402BeforePay; not person KYC). ([GitHub](https://github.com/AffixIO/SDK)) ([docs](https://www.affix-io.com/agent-trust/))
- [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) - Taxonomy of ten security risks specific to agentic systems, from goal hijack and tool misuse to memory poisoning and rogue agents.
- [NCCoE Software and AI Agent Identity and Authorization](https://www.nccoe.nist.gov/projects/software-and-ai-agent-identity-and-authorization) - NIST project and concept paper on applying OAuth, OpenID Connect, and SPIFFE to AI agent identity, delegation, and authorisation.
- [Aident Loadout](https://docs.aident.ai/loadout/overview) - Remote MCP server and CLI that brokers agent access to connected apps from a credential vault and records each action in an audit log.


Operational topics to cover in production reviews:

- Tool permission boundaries and least privilege.
- Secret isolation and credential rotation.
- User, agent, service, and tool identity.
- Sandboxing for code execution, browser use, and filesystem access.
- Audit logs for privileged or irreversible actions.

## Human Approval and Workflow Control

- [Temporal](https://temporal.io/) - Durable execution platform for long-running workflows, retries, and human-in-the-loop steps.
- [Inngest](https://www.inngest.com/) - Durable functions and event-driven workflows for reliable background execution.
- [Hatchet](https://github.com/hatchet-dev/hatchet) - Distributed task queue and workflow engine.
- [HumanLayer](https://github.com/humanlayer/humanlayer) - Human approval workflows for AI agents and tool calls.
- [Tenet](https://www.trytenet.com/) - Approval gates, cost caps, credential mediation, and audit logs for AI agent tool calls.
- [LedgerGuard](https://github.com/Val1-IT/Arvanta-Ledgerguard) - Policy checks and human approval bound to a plan version for agent-proposed Postgres writes, with execution keys that stop a retried write from running twice.

Useful approval patterns:

- Require approval for external side effects such as sending email, spending money, merging code, or changing infrastructure.
- Store the proposed action, context, risk level, approver, and final decision.
- Make approvals replayable and auditable, not transient chat messages.

## Deployment and Runtime Infrastructure

- [LiteLLM](https://github.com/BerriAI/litellm) - LLM gateway for model routing, budgets, retries, keys, and provider abstraction.
- [Portkey](https://github.com/Portkey-AI/gateway) - AI gateway for observability, caching, routing, guardrails, and reliability.
- [Bifrost](https://github.com/maximhq/bifrost) - OpenAI-compatible gateway for provider routing, failover, guardrails, usage controls, MCP, and production observability.
- [Ray Serve](https://docs.ray.io/en/latest/serve/index.html) - Scalable model and application serving for Python workloads.
- [BentoML](https://github.com/bentoml/BentoML) - Framework for building and deploying AI applications.
- [Modal](https://modal.com/) - Serverless infrastructure for AI and data workloads.
- [Fly.io](https://fly.io/) - Application runtime useful for globally deployed agent services.
- [SandBase Harness](https://github.com/sandbaseai/sandbase-harness) - Self-hosted agent runtime with persistent sessions, MCP tools, sandbox providers, approvals, credentials, audit logs, and replay.
- [Reef](https://github.com/Human-Agent-Society/reef) - Self-hosted agent serving runtime that records each request behind an OpenAI- and Anthropic-compatible endpoint, returns a receipt for attaching scores or feedback later, and publishes model or harness updates as versioned, rollback-capable artifacts without a restart.

## Cloud AgentOps Platforms

Major cloud platforms are beginning to expose AgentOps capabilities through managed agent runtimes, observability tools, tracing, evaluations, guardrails, identity controls, and governance features.

This section tracks cloud-native services that help teams build, deploy, monitor, evaluate, secure, and govern AI agents in production.

### Microsoft Azure and Microsoft Foundry

- [Microsoft Foundry Agent Service](https://learn.microsoft.com/en-us/azure/foundry/agents/overview) - Managed platform for building, deploying, and scaling AI agents across prompt agents, workflow agents, and hosted agents.
- [Microsoft Foundry Control Plane](https://learn.microsoft.com/en-us/azure/foundry/control-plane/how-to-manage-agents) - Centralised management and observability for agent inventory, agent health, and lifecycle operations.
- [Microsoft Foundry Playgrounds](https://learn.microsoft.com/en-us/azure/foundry/concepts/concept-playgrounds) - Agent development environment with tracing and evaluation data for agent responses.
- [Azure AI Agent Design Patterns](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns) - Architecture guidance for multi-agent orchestration patterns.
- [Azure AI Agent Adoption Process](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/build-secure-process) - Organisational guidance for building agents consistently and securely.
- [Microsoft Entra Agent ID](https://learn.microsoft.com/entra/agent-id/) - Identity platform for registering AI agents, issuing agent identities from blueprints, and applying access policies to them.

Operational capabilities to track:

- agent inventory and lifecycle management
- managed agent hosting
- tracing and evaluation
- multi-agent orchestration patterns
- security and governance controls
- organisational adoption processes

### Google Cloud and Gemini Enterprise Agent Platform

- [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/overview) - Unified platform for building, deploying, governing, and optimising enterprise-grade AI agents.
- [Scale your agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale) - Production guidance for deploying, managing, tracing, logging, monitoring, and scaling agents.
- [Agent Platform Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime) - Managed runtime services for deploying, managing, and scaling AI agents in production.
- [Agent Development Kit](https://google.github.io/adk-docs/) - Open-source framework for building and orchestrating agents.
- [Agent identity and IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale) - Identity and access management patterns for deployed agents.

Operational capabilities to track:

- managed serverless agent runtime
- tracing, logging, monitoring, and alerts
- IAM-based agent identity
- session and memory management
- secure connectivity through Agent Gateway
- production scaling controls

### AWS, Amazon Bedrock and Amazon Bedrock AgentCore

- [Amazon Bedrock AgentCore](https://docs.aws.amazon.com/bedrock-agentcore/) - Managed service for deploying and operating AI agents securely at scale across frameworks and models.
- [Amazon Bedrock AgentCore Observability](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/observability.html) - Production observability for tracing, debugging, monitoring, and investigating agent performance.
- [Amazon Bedrock AgentCore Identity](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/identity.html) - Identity and credential management for agent applications and automated workloads.
- [Amazon Bedrock AgentCore Memory](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/memory.html) - Managed memory for agent applications that need session context, user preferences, and longer-running continuity.
- [Amazon Bedrock Agents](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html) - Managed agent capability for orchestrating foundation models, knowledge bases, APIs, and user interactions.
- [Amazon Bedrock Agent Traces](https://docs.aws.amazon.com/bedrock/latest/userguide/trace-events.html) - Step-by-step traces for understanding agent orchestration and behaviour.
- [Amazon Bedrock Observability](https://docs.aws.amazon.com/bedrock/latest/userguide/observability.html) - Observability guidance for tracking performance, resources, and operational behaviour.
- [Monitor Amazon Bedrock Agents with CloudWatch](https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-agents-cw-metrics.html) - Runtime metrics for monitoring agent invocations and performance.
- [Amazon Bedrock Guardrails](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html) - Configurable safeguards for generative AI applications and agent workflows.
- [Amazon Bedrock Security, Guardrails, and Observability](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html) - Security and compliance guidance for Bedrock-based systems.

Operational capabilities to track:

- agent orchestration and API action execution
- traces for agent reasoning and tool use
- CloudWatch metrics and logs
- CloudTrail auditability
- guardrails and policy enforcement
- knowledge base and runtime monitoring

### What to compare across cloud platforms

When evaluating cloud AgentOps capabilities, compare:

| Capability | What to inspect |
|---|---|
| Managed runtime | Can agents be hosted, scaled, isolated, and versioned in production? |
| Tracing | Can teams inspect agent steps, tool calls, retrieval, memory, and reasoning paths? |
| Evaluation | Can outputs, trajectories, and task outcomes be evaluated continuously? |
| Identity | Can agents have distinct identities, permissions, and credential boundaries? |
| Guardrails | Can runtime policy, safety, and action constraints be enforced? |
| Monitoring | Can cost, latency, errors, usage, token consumption, and reliability be tracked? |
| Governance | Can teams audit lifecycle, approvals, access, incidents, and compliance evidence? |
| Portability | Can agents use external frameworks, APIs, tools, and model providers without deep lock-in? |

## Cost, Latency, and Reliability

- [OpenCost](https://www.opencost.io/) - Open-source cost monitoring for Kubernetes infrastructure.
- [Grafana](https://grafana.com/) - Dashboards and alerting for metrics, logs, and traces.
- [Prometheus](https://prometheus.io/) - Metrics and alerting toolkit.
- [Sentry](https://sentry.io/) - Application error monitoring and performance tracing.
- [Vercel AI Gateway](https://vercel.com/ai-gateway) - Gateway for model routing, observability, and usage controls.
- [AgentOps for senior engineers](https://aiarch.dev/agentops-for-senior-engineers) - Guide mapping SRE and DevOps practices (tracing, cost control, least privilege, evals) onto production agents, with two as-built production bugs.

Agent-specific signals worth tracking:

- Task success rate and policy violation rate.
- Tool call count, tool error rate, and tool latency.
- Model fallback rate and retry rate.
- Cost per task, cost per successful task, and cost per user.
- Human escalation rate and approval rejection rate.
- Context length, memory growth, and retrieval quality.

## Incident Response and Governance

- [PagerDuty Incident Response](https://www.pagerduty.com/resources/learn/incident-response/) - Practical incident response concepts and lifecycle.
- [Google SRE Book](https://sre.google/sre-book/table-of-contents/) - Foundational reliability practices.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) - Practical guide for applying the NIST AI Risk Management Framework.
- [Partnership on AI: AI Incident Database](https://incidentdatabase.ai/) - Database of AI-related incidents and harms.
- [Orca AI Incident Archive](https://github.com/Continuum-AI-Corp/Orca-AI-Incident-Archive) - Open database of real-world AI agent security incidents, each linked to primary sources and flagged for whether a victim was confirmed.
- [IMDA Model AI Governance Framework for Agentic AI](https://www.imda.gov.sg/resources/press-releases-factsheets-and-speeches/factsheets/2026/updated-model-ai-governance-framework-for-agentic-ai) - Singapore's voluntary framework for bounding agent risk, human accountability, lifecycle technical controls, and agent audit trails.
- [Agentic AI Risk-Management Standards Profile](https://cltc.berkeley.edu/agentic-ai-risk-management-standards-profile) - Berkeley CLTC profile extending the NIST AI RMF with risks and controls specific to autonomous and multi-agent systems.
- [ISO/IEC 42001](https://www.iso.org/standard/81230.html) - International standard for establishing, auditing, and certifying an AI management system.
- [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) - Official text of the EU regulation setting risk-tiered obligations for AI systems, including human oversight, robustness, and transparency requirements.

Agent incident checklist:

- Preserve traces, prompts, tool inputs, tool outputs, retrieved context, and approval records.
- Identify whether the failure came from model behaviour, retrieval, tool execution, policy, permissions, or orchestration.
- Reproduce the run with the same inputs where possible.
- Add regression evals before changing prompts, tools, or policies.
- Record user impact, safety impact, cost impact, and data exposure.

## Multi-Agent Operations

- [AutoGen](https://github.com/microsoft/autogen) - Framework for building multi-agent AI applications.
- [CrewAI](https://github.com/crewAIInc/crewAI) - Framework for orchestrating role-based AI agents.
- [LangGraph](https://github.com/langchain-ai/langgraph) - Framework for stateful, controllable agent workflows.
- [Semantic Kernel](https://github.com/microsoft/semantic-kernel) - SDK for building agents and AI orchestration into applications.
- [OpenAI Swarm](https://github.com/openai/swarm) - Educational framework for lightweight multi-agent orchestration.
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) - Framework for multi-agent workflows with handoffs, built-in tracing, and input, output, and tool guardrails.
- [Pydantic AI](https://github.com/pydantic/pydantic-ai) - Typed Python agent framework with OpenTelemetry GenAI tracing of runs, model calls, and tools, plus a companion evaluation library.
- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) - Python and .NET framework for agents and multi-agent workflows, successor to AutoGen and Semantic Kernel, with built-in OpenTelemetry GenAI telemetry.

Operational concerns for multi-agent systems:

- Shared state ownership and conflict resolution.
- Message visibility, routing, and provenance.
- Tool access per agent role.
- Runaway loops, deadlocks, and duplicated work.
- Evaluation at both individual-agent and system levels.

## Standards and Protocols

- [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) - Protocol for connecting AI applications to tools and data sources.
- [OpenAPI](https://www.openapis.org/) - Standard for describing HTTP APIs exposed to agents.
- [AsyncAPI](https://www.asyncapi.com/) - Standard for event-driven API definitions.
- [CloudEvents](https://cloudevents.io/) - Specification for event data interoperability.
- [OpenTelemetry Semantic Conventions](https://opentelemetry.io/docs/specs/semconv/) - Shared conventions for telemetry data.
- [OpenTelemetry GenAI Semantic Conventions](https://github.com/open-telemetry/semantic-conventions-genai) - Span and attribute conventions for agent invocations, model calls, tool execution, and MCP requests.
- [Agent2Agent (A2A) Protocol](https://a2a-protocol.org/) - Open protocol for agent discovery, task exchange, and communication between agents, with optionally signed Agent Cards.
- [NIST AI Agent Standards Initiative](https://www.nist.gov/caisi/ai-agent-standards-initiative) - NIST CAISI programme coordinating standards, open protocols, and research on AI agent security, identity, and interoperability.

## Research and References

- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) - Introduced reasoning plus acting patterns used by many agents.
- [Toolformer](https://arxiv.org/abs/2302.04761) - Research on language models learning to use external tools.
- [Voyager](https://arxiv.org/abs/2305.16291) - Example of lifelong learning and skill acquisition in an embodied agent setting.
- [SWE-bench](https://www.swebench.com/) - Benchmark for evaluating agents on real software engineering issues.
- [AgentBench](https://arxiv.org/abs/2308.03688) - Benchmark for evaluating LLMs as agents across environments.
- [AI Incident Database](https://incidentdatabase.ai/) - Public incident database useful for governance and risk analysis.
- [Where Facts Go Missing: A Layerwise Taxonomy and Per-Layer Attribution of Information Omission in Air-Gapped LLM Agent Pipelines](https://arxiv.org/abs/2607.22448) - Presents a layerwise taxonomy and per-layer attribution method for locating information omissions in air-gapped LLM agent pipelines, helping operators evaluate and debug where facts are lost across pipeline stages.
- [MemTrapBench](https://arxiv.org/abs/2608.20202) - Benchmark for cognitive traps in LLM memory use, showing that accurately retrieved memories can still induce reasoning fixation and belief distortion that degrade task performance, paired with AdaptiveMem, an inference-time method that checks whether retrieved memories apply before use.
- [Identical Runs, Different Results](https://arxiv.org/abs/2609.33812) - Repeated-run study of coding agents on open-weight models showing that run-to-run variance can exceed differences between agent-model pairings, with guidance on run counts, compliance reporting, and cost comparison.
- [MCP Error Messages Written for Developers Hurt the Most Capable Agents Most](https://arxiv.org/abs/2609.35381) - Survey of 3,001 error messages from 150 MCP servers and controlled experiments on how error text affects agent recovery from tool failures, with server-side and agent-side mitigations.
- [ARIA: Runtime Inspection and Amendment for Multi-Agent Systems](https://arxiv.org/abs/2610.20780) - Trains a compact model on execution-verified repairs from multi-agent trajectories to detect when a running multi-agent system needs intervention and amend its continuation, with released code and framework hooks.
- [AgentOps: Enabling Observability of LLM Agents](https://arxiv.org/abs/2411.05285) - Taxonomy of the artefacts and data to trace across the lifecycle of LLM agents to support observability and AI safety.
- [Which Agent Causes Task Failures and When? (Who&When)](https://arxiv.org/abs/2505.00212) - Benchmark and study of automatically attributing multi-agent system failures to a responsible agent and step.
- [AgenTracer](https://arxiv.org/abs/2509.03312) - Counterfactual-replay pipeline and lightweight trained model for attributing failures in multi-agent trajectories, with diagnoses usable as feedback for system improvement.
- [BabelJudge](https://arxiv.org/abs/2606.22329) - Label-free reliability audit for LLM judges that applies controlled perturbations to responses and agent trajectories to measure bias and blind spots.
- [Why Do Multi-Agent LLM Systems Fail?](https://arxiv.org/abs/2503.13657) - Taxonomy of multi-agent system failure modes (MAST) derived from annotated execution traces across popular frameworks.
- [Seeing the Whole Elephant](https://arxiv.org/abs/2604.22708) - Benchmark with full execution traces and reproducible environments showing that output-only logs substantially limit multi-agent failure attribution.
- [trajectory-judge](https://arxiv.org/abs/2609.00038) - Fault-injection testbed and study showing outcome-only LLM judges miss silent trajectory faults, with a paired-discrimination protocol for validating step-level judges.
- [FAMAS](https://arxiv.org/abs/2509.13782) - Spectrum-based method that replays failed multi-agent tasks and ranks the agent actions most likely responsible for the failure.
- [Who&When Pro](https://arxiv.org/abs/2607.09996) - Benchmark of 12,326 failure-injected agent trajectories across frameworks and modalities for evaluating automated root-cause attribution.
- [LongRCA Bench](https://arxiv.org/abs/2608.15242) - Benchmark of human-annotated long-horizon agent failures for evaluating responsible-role and earliest root-cause step attribution.
- [Reliability without Validity](https://arxiv.org/abs/2606.19544) - Large-scale evaluation of LLM-as-a-judge models showing that high test-retest consistency can coexist with position bias, with a minimum validation protocol.
- [MobileJudgeBench](https://arxiv.org/abs/2608.11434) - Benchmark of human-annotated mobile-agent trajectories for comparing LLM-judge methods and backbones used to evaluate GUI agents.
- [Catching One in Five](https://arxiv.org/abs/2606.10315) - Production case study showing an LLM judge missed most human-confirmed multi-turn failures in a deployed transaction agent, with a taxonomy of what judges catch and miss.
- [Harness-Bench](https://arxiv.org/abs/2605.27922) - Benchmark that varies agent harnesses across model backends on fixed tasks to measure how much the scaffold changes agent results.
- [Reasoning Provenance for Autonomous AI Agents](https://arxiv.org/abs/2603.21692) - Proposes the Agent Execution Record for capturing per-step intent, evidence, plan revisions, and delegation chains at execution time for audit and cross-run analysis.
- [From Agent Traces to Trust](https://arxiv.org/abs/2606.04990) - Survey of execution provenance and evidence tracing for LLM agents, covering trace sources, provenance relations, tool-use provenance, and trace-based failure diagnosis.
- [NovaFabric](https://arxiv.org/abs/2609.12582) - Signed, timestamped, Merkle-logged capsules for agent runs that support tamper detection, redaction attestation, and replay for third-party audit.
- [A Trace-Based Assurance Framework for Agentic AI Orchestration](https://arxiv.org/abs/2603.18096) - Contracts over agent message-action traces that localise the first violating step, combined with perturbation-based stress testing and runtime capability enforcement.
- [Runtime Governance for AI Agents: Policies on Paths](https://arxiv.org/abs/2603.16586) - Formal framework for runtime policies that score the probability of violation from an agent's identity, execution path so far, and proposed next action.
- [Governance Gaps in Agent Interoperability Protocols](https://arxiv.org/abs/2606.31498) - Gap analysis of MCP, A2A, ACP, and other agent protocols against governance requirements such as human escalation, dissent preservation, and audit replay.
- [Your Agent May Misevolve](https://arxiv.org/abs/2509.26354) - Study of safety degradation in self-evolving agents across model, memory, tool, and workflow pathways, with deployment recommendations for auditing, validating, and rolling back self-modifications.
- [Safety in Self-Evolving Agents: A Survey](https://arxiv.org/abs/2610.00093) - Survey and SAVER framework for how self-modified memory, skills, tools, and workflows create safety failures, with containment, repair, and descendant-aware rollback responses.
- [Back Up Before You Regret](https://arxiv.org/abs/2610.28934) - Introduces RegretBench, showing that coding agents rarely back up state before changing it, and BackUpper, a harness plug-in that cheaply saves affected state beforehand.
- [SciΠvot](https://arxiv.org/abs/2610.21082) - Benchmark of 248 judgment calls taken from senior researchers' real corrections of LLM research agents on 26 projects, showing that frontier models lean toward the agent's original plan and that four of five score below chance at deciding when to change course.

## Contributing

<p align="center">
  <img src="assets/We love Contributors — section title banner.png" alt="We love Contributors" width="480">
</p>

<p align="center">
Thrilled to have you here.<br>
Whether it's a quick typo fix, a fresh resource,<br> a doc polish, or a sweeping overhaul — every contribution helps this list grow.<br>
Jump in and join the community — PRs of every size are welcome.
</p>

<p align="center">
📝 <a href="CONTRIBUTING.md">Read the contributing guide</a>  ·  🐛 <a href="https://github.com/natnew/awesome-agentops/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22">good first issues</a>
</p>

## License

MIT. See [LICENSE](LICENSE).
