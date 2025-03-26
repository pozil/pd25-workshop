# Agentforce Workshop Instructions for Polish Dreamin '25

> [!NOTE]  
> These instructions are derived from the full day 📖 [Agentforce workshop](https://developer.salesforce.com/agentforce-workshop) with some extra exercises based on TDX content.

## Agenda

1. [Get Started with Agentforce](https://developer.salesforce.com/agentforce-workshop/agents/1-get-started) 📖
1. Build custom agent actions
    1. [Flow action](https://developer.salesforce.com/agentforce-workshop/agents/2-flow-actions-credit) 📖
    1. [Apex action](https://developer.salesforce.com/agentforce-workshop/agents/4-apex-actions) 📖
    1. [Prompt template action](https://developer.salesforce.com/agentforce-workshop/agents/5-prompt-template-actions) 📖
    1. [External Service action](#external-service-action) (TDX bonus)
1. Work with Service Agents
    1. [Create a Service Agent](https://developer.salesforce.com/agentforce-workshop/service-agents/1-create-a-service-agent) 📖
    1. [Configure a Service Deployment](https://developer.salesforce.com/agentforce-workshop/service-agents/2-configure-a-service-deployment) 📖
    1. [Use the Agent API](#use-the-agent-api) (TDX bonus)


## External Service action

### Create a Named Credentials

1. From Salesforce Setup go, to **Named Credentials**.
1. Click the 🔽 down caret next to the **New** button and click **New Legacy**.
1. Fill the form with these details:

    | Field | Value |
    |:---|:---|
    | Label | `Air Travel Service` |
    | Name | `Air_Travel_Service` |
    | URL | `https://a3092717-9181-473a-a6f2-fd80c745960c.mock.pstmn.io` |

1. Uncheck **Generate Authorization Header**.
1. Click **Save**.

### Create an External Service

1. From Salesforce Setup go, to **External Services**
1. Click **Add an External Services**.
1. Select **From API Specification** and click **Next**.
1. Fill the form with these details:

    | Field | Value |
    |:---|:---|
    | External Service Name | `AirTravelService` |
    | Service Schema | Absolute URL |
    | Select a Named Credential | Air_Travel_Service |
    | URL | `https://raw.githubusercontent.com/pozil/pd25-workshop/refs/heads/main/res/air-travel-api.json` |

1. Click **Save & Next**.

### Create an API Action

### Add the action to an agent

## Use the Agent API

> [!IMPORTANT]  
> This steps assume that you have a working Service Agent.


