# Azure Token Capital Agent Accelerator

A reference accelerator for building governed, cost-aware enterprise AI agents on Azure.

This project demonstrates how to operationalize **Token Capital**: treating AI consumption as a managed enterprise resource where tokens, model choices, agent performance, governance, and business value are measured together.

## Goals

- Build agents with Microsoft Agent Framework
- Run agent workloads on Azure Kubernetes Service
- Use Microsoft Foundry for model access, evaluation, and optimization
- Apply AI Agent Identity for secure agent-to-resource access
- Register and govern agents with Agent 365
- Track token usage, cost, latency, quality, and business value
- Support model routing and tiering for cost/performance optimization

## Architecture

Core components:

- **Microsoft Foundry**: model catalog, evaluations, tracing, and optimization
- **Microsoft Agent Framework**: agent orchestration and tool execution
- **Azure Kubernetes Service**: scalable runtime for agent services
- **AI Agent Identity**: workload identity and least-privilege access
- **Agent 365**: agent registry, governance, and lifecycle visibility
- **Azure Monitor / Application Insights**: telemetry and observability
- **Cost + Token Ledger**: token attribution by agent, user, task, model, and business unit

## Repository structure

```text
/
├── infra/                 # Bicep or Terraform Azure deployment
├── src/
│   ├── agents/            # Agent Framework implementations
│   ├── tools/             # Agent tools and connectors
│   ├── api/               # Agent runtime APIs
│   └── telemetry/         # Token, cost, latency, and quality tracking
├── k8s/                   # Kubernetes manifests and Helm charts
├── evaluations/           # Foundry evaluation configs and test datasets
├── governance/            # Agent 365 registration and policy templates
├── docs/                  # Architecture and operating model guidance
└── README.md
```

## Key scenarios

1. **Model routing**
   - Route simple tasks to lower-cost models
   - Escalate complex reasoning to advanced models
   - Compare cost, latency, and quality

2. **Agent identity**
   - Assign managed identity per agent
   - Enforce least-privilege access
   - Audit agent actions

3. **Token capital dashboard**
   - Track token spend by agent, workflow, and business owner
   - Attribute cost to business outcomes
   - Identify optimization opportunities

4. **Governed deployment**
   - Package agents as Kubernetes services
   - Register agents in Agent 365
   - Apply governance metadata, owners, and lifecycle controls

## Getting started

### Prerequisites

- Azure subscription
- Azure CLI
- kubectl
- Microsoft Foundry project
- AKS cluster or permission to create one
- Agent 365 access
- Microsoft Agent Framework SDK

### Deploy infrastructure

```bash
az login
az deployment sub create \
  --location eastus \
  --template-file infra/main.bicep
```

### Deploy agent runtime

```bash
kubectl apply -f k8s/
```

### Run locally

```bash
cd src/api
npm install
npm run dev
```

## Configuration

Create a `.env` file:

```env
AZURE_CLIENT_ID=
AZURE_TENANT_ID=
FOUNDRY_PROJECT_ENDPOINT=
AGENT365_REGISTRY_ENDPOINT=
APPLICATIONINSIGHTS_CONNECTION_STRING=
TOKEN_LEDGER_STORAGE_ACCOUNT=
```

## Telemetry model

Each agent request should emit:

- Agent ID
- User or workload identity
- Task type
- Model selected
- Prompt tokens
- Completion tokens
- Total cost estimate
- Latency
- Evaluation score
- Business outcome tag

## Roadmap

- Foundry Model Router integration
- Agent 365 registration automation
- Token cost dashboard
- Evaluation-driven prompt and model optimization
- Policy-as-code for agent governance
- Multi-agent workflow examples

## License

MIT
