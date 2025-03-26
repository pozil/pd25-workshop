# Agentforce Workshop Instructions for Polish Dreamin '25

> [!NOTE]  
> These instructions are derived from the full day 📖 [Agentforce workshop](https://developer.salesforce.com/agentforce-workshop) with some extra exercises based on TDX content.

## Agenda

1. [Get Started with Agentforce](https://developer.salesforce.com/agentforce-workshop/agents/1-get-started) 📖
1. Build custom agent actions
    1. [Flow action](https://developer.salesforce.com/agentforce-workshop/agents/2-flow-actions-credit) 📖
    1. [Apex action](https://developer.salesforce.com/agentforce-workshop/agents/4-apex-actions) 📖
    1. [Prompt template action](https://developer.salesforce.com/agentforce-workshop/agents/5-prompt-template-actions) 📖
    1. [External Service action](#es-external-service-action) (TDX bonus)
1. Work with Service Agents
    1. [Create a Service Agent](https://developer.salesforce.com/agentforce-workshop/service-agents/1-create-a-service-agent) 📖
    1. [Configure a Service Deployment](https://developer.salesforce.com/agentforce-workshop/service-agents/2-configure-a-service-deployment) 📖
    1. [Use the Agent API](#aa-agent-api) (TDX bonus)


## ES. External Service action

- ES.1. [Create a Named Credential](#es1-create-a-named-credential)
- ES.2. [Create an External Service](#es2-create-an-external-service)
- ES.3. [Create an External Service Action](#es3-create-an-external-service-action)
- ES.4. [Prepare a topic with the action](#es4-prepare-a-topic-with-the-action)
- ES.5. [Test the action](#es5-test-the-action)

### ES.1. Create a Named Credential

1. From Setup, go to **Named Credentials**.
1. Click the 🔽 dropdown arrow next to the **New** button and click **New Legacy**.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | Label | `Air Travel Service Credentials` |
    | Name | `Air_Travel_Service_Credentials` |
    | URL | `https://a3092717-9181-473a-a6f2-fd80c745960c.mock.pstmn.io` |

1. Uncheck **Generate Authorization Header**.
1. Click **Save**.

### ES.2. Create an External Service

1. From Setup, go to **External Services**
1. Click **Add an External Services**.
1. Select **From API Specification** and click **Next**.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | External Service Name | `AirTravelService` |
    | Service Schema | Complete Schema |
    | Select a Named Credential | Air_Travel_Service_Credentials |
    | Schema | Copy the content of [this JSON file](https://raw.githubusercontent.com/pozil/pd25-workshop/refs/heads/main/res/air-travel-api.json) |

1. Click **Save & Next**.
1. Check all four operations and click **Next**.
1. Click **Finish**.

### ES.3. Create an External Service action

1. From Setup, go to **Agent Actions**.
1. Click **New Agent Action**.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | Reference Action Type | API |
    | Reference Action Category | External Services |
    | Reference Action | Get Bookings For User |

1. Click **Next**.
1. For the **Loading Text**, enter `Fetching your bookings`.
1. For the **200** output parameter, check **Show in conversation**.
1. Click **Finish**.

### ES.4. Prepare a topic with the action

1. From Setup, go to **Agents**.
1. Click the 🔽 dropdown arrow next on the default agent row and click **Open in Buildery**.
1. Click **New** and select **New Topic**
1. For the topic description, enter `Help users with air travel related enquiries.` and click **Next**.
1. Leave the default values and click **Next**.
1. Check **Get Bookings For User**.
1. Click **Finish**.

### ES.5. Test the action

1. In the Conversation Preview panel of Agent Builder, send the following prompt: `My user ID is 12345. Show me my flight bookings.`.
2. Watch the planner (center panel) as the API is being called. Notice the API input parameters and the External Service Apex-generated reponses.

## AA. Agent API

> [!IMPORTANT]  
> These steps assume that you have a working Service Agent. The Agent API is **not available** on the default employee agent.

- AA.1. [Create a Connected App](#aa1-create-a-connected-app)
- AA.2. [Add the Connected App to the agent](#aa2-add-the-connected-app-to-the-agent)
- AA.3. [Obtain the Connected App credentials](#aa3-obtain-the-connected-app-credentials)
- AA.4. [Call the Agent API](#aa4-call-the-agent-api-with-postman)

### AA.1. Create a Connected App

1. From Setup, go to **App Manager**.
1. Click **New Connected App**, select **Create a Connected App** and click **Continue**.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | Connected App Name | `Agent API Integration` |
    | Contact Email | Your admin email address |

1. Check **Enable OAuth Settings**.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | Callback URL | `https://login.salesforce.com` |
    | Selected OAuth Scopes | Access chatbot services (chatbot_api)<br>Access the Salesforce API Platform (sfap_api)<br>Manage user data via APIs (api)<br>Perform requests at any time (refresh_token, offline_access) |

1. Uncheck the following:
    - Require Proof Key for Code Exchange (PKCE) Extension for Support Authorization Flows
    - Require Secret for Web Server Flow
    - Require Secret for Refresh Token Flow

1. Check the following:
    - Enable Client Credentials Flow
    - Issue JSON Web Token (JWT)-based access tokens for named users

1. Review this screenshot to verify that you selected the correct settings:

    ![Connected app configuration](https://a.sfdcstatic.com/developer-website/sfdocs/genai/media/agent-api-connected-app.png)

1. Click **Save**.
1. Click **Manage**.
1. Click **Edit Policies**.
1. In the **OAuth Policies** section, set the **Permitted Users** dropdown to Admin approved users are pre-authorized.
1. In the **Client Credentials Flow** section, set **Run As** to your user.
1. Check **Issue JSON Web Token (JWT)-based access tokens**.
1. Click **Save**.

### AA.2. Add the Connected App to the agent

1. From Setup, go to **Agents**.
1. Click on **Coral Cloud Agent**.
1. Select the **Connections** tab, and click **Add** from the Connections section.
1. Fill the form with these values:

    | Field | Value |
    |:---|:---|
    | Connection | API |
    | Integration Name | `Agent API Integration` |
    | Connected App | Agent API Integration |

1. Click **Save**.

### AA.3. Obtain the Connected App credentials

1. From Setup, go to **App Manager**.
1. Find the **Agent API Integration** connected app, click the 🔽 dropdown arrow on the right, and then click **View**.
1. Click **Manage Consumer Details**.
1. Copy **Consumer Key** and **Consumer Secret**.

### AA.4. Call the Agent API with Postman

1. [Sign up](https://identity.getpostman.com/signup) for a Postman account
1. [Fork](https://app.getpostman.com/run-collection/12721794-8612c754-9efc-4ea1-b876-e8f9af0fe09d?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D12721794-8612c754-9efc-4ea1-b876-e8f9af0fe09d%26entityType%3Dcollection%26workspaceId%3D34382471-0c97-40e5-a206-f947271665c4) the Agent API collection.
1. Select the root of **Agent API** collection and open the **Variables** tab.
1. Paste the **Consumer Key** and **Consumer Secret** respectively in the `clientId` and `clientSecret` collection variables.
1. From Setup, go to **My Domain**, and then copy the value of **Current My Domain URL** into the `sfOrgDomain` collection variable.
1. From Setup, go to **Agents**, select the agent that you want to interact with and and then copy value of the agent ID (a value starting with `0Xx.....`) from the browser URL into the `agentId` collection variable.
1. Save your collection variables (press `Cmd + S` or `Ctrl + S`).
1. Open the **Authorization** tab of the Postman collection and click **Get New Access Token** at the bottom of the screen.
1. Click **Use Token**.
1. Select the **Start Session** request and click **Send** to open a session.
1. Send a prompt: select the **Send Message - Streaming** request, modify the body with your prompt and click **Send**.
