---
name: azure-bot-service
description: "Azure Bot Service API skill. Use when working with Azure Bot Service for subscriptions, providers. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Bot Service
API version: 2018-07-12

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.BotService/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName}/listChannelWithKeys -- create first listChannelWithKeys

## Endpoints

27 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName} | Creates a Bot Service. Bot Service is a resource group wide resource type. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName} | Updates a Bot Service |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName} | Deletes a Bot Service from the resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName} | Returns a BotService specified by the parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices | Returns all the resources of a particular type belonging to a resource group |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.BotService/botServices | Returns all the resources of a particular type belonging to a subscription. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName} | Creates a Channel registration for a Bot Service |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName} | Updates a Channel registration for a Bot Service |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName} | Deletes a Channel registration from a Bot Service |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName} | Returns a BotService Channel registration specified by the parameters. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName}/listChannelWithKeys | Lists a Channel registration for a Bot Service including secrets |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels | Returns all the Channel registrations of a particular BotService resource |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.BotService/listAuthServiceProviders | Lists the available Service Providers for creating Connection Settings |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName}/listWithSecrets | Get a Connection Setting registration for a Bot Service |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName} | Register a new Auth Connection for a Bot Service |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName} | Updates a Connection Setting registration for a Bot Service |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName} | Get a Connection Setting registration for a Bot Service |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName} | Deletes a Connection Setting registration for a Bot Service |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/connections | Returns all the Connection Settings registered to a particular BotService resource |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels | Returns all the resources of a particular type belonging to a resource group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels/{resourceName} | Creates an Enterprise Channel. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels/{resourceName} | Updates an Enterprise Channel. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels/{resourceName} | Deletes an Enterprise Channel from the resource group |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels/{resourceName} | Returns an Enterprise Channel specified by the parameters. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| POST | /providers/Microsoft.BotService/checkNameAvailability | Check whether a bot name is available. |
| GET | /providers/Microsoft.BotService/operations | Lists all the available BotService operations. |
| POST | /providers/Microsoft.BotService/checkEnterpriseChannelNameAvailability | Check whether an Enterprise Channel name is available. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new bot service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}
- "How do I update an existing bot's settings?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}
- "How do I delete a bot service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}
- "How do I get details about a specific bot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}
- "How do I list all bots in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices
- "How do I list all bots in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.BotService/botServices
- "How do I check if a bot name is available?" -> POST /providers/Microsoft.BotService/checkNameAvailability
- "How do I connect a channel (Teams, Slack, etc.) to my bot?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName}
- "How do I remove a channel from my bot?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName}
- "How do I get a channel's keys and secrets?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels/{channelName}/listChannelWithKeys
- "How do I list all channels configured on a bot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/channels
- "How do I create a connection setting (OAuth link) for my bot?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName}
- "How do I retrieve secrets for a connection setting?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/botServices/{resourceName}/Connections/{connectionName}/listWithSecrets
- "What auth service providers are available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.BotService/listAuthServiceProviders
- "How do I set up an enterprise channel?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.BotService/enterpriseChannels/{resourceName}

## Response Tips

- **Bot CRUD (200/201):** 200 means updated in place, 201 means newly created; both return the full bot resource object with `properties.endpoint`, `properties.msaAppId`, and `sku` nested inside.
- **Delete operations (200/204):** 200 confirms deletion with a body, 204 means already deleted or no content; treat both as success.
- **List operations (200):** Returns a `value` array with `nextLink` for pagination; keep following `nextLink` until it is absent or null.
- **Name availability check (200):** Returns `{ valid: bool, message: string }`; check `valid` before attempting resource creation.
- **Channel with keys (200):** Returns the channel resource with embedded secrets in `properties`; secrets are only exposed via this POST, never via GET.
- **Connections (200):** Connection settings contain `clientId` and `clientSecret` in `properties.parameters`; the listWithSecrets variant populates `clientSecret` while the GET variant omits it.

## Anomaly Flags

- **409 Conflict on PUT:** Bot name already taken by another subscription; surface immediately and suggest running checkNameAvailability first.
- **404 on channel operations:** The bot resource or channel does not exist; verify the bot was created before configuring channels.
- **api-version mismatch:** If responses include `error.code: "NoRegisteredProviderFound"`, the api-version query parameter may be wrong; flag and suggest `2018-07-12`.
- **201 on PATCH:** Unexpected -- PATCH should return 200 for updates; if 201 is returned, flag that the resource was created rather than updated (possible race condition).
- **Empty `value` array on list:** Could indicate the subscription lacks the Microsoft.BotService resource provider registration; surface a suggestion to register it via `az provider register --namespace Microsoft.BotService`.
- **Throttling (429):** Azure ARM enforces rate limits per subscription; surface `Retry-After` header value and queue remaining calls accordingly.
- **Enterprise channel deprecation:** Enterprise channels are a legacy feature; flag when users create new ones and suggest standard channels instead.

## Playbook

### 1. Create a Bot and Connect a Channel

1. Call POST `/providers/Microsoft.BotService/checkNameAvailability` with `{ name, type: "Bot" }` to verify the desired bot name is free.
2. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.BotService/botServices/{name}` with location, SKU, and properties (msaAppId, endpoint) to create the bot.
3. Confirm 201 response and note the returned resource `id`.
4. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.BotService/botServices/{name}/channels/{channelName}` (e.g., `MsTeamsChannel`) with channel-specific properties.
5. Call POST `.../channels/{channelName}/listChannelWithKeys` to retrieve the channel keys for integration.

### 2. Configure OAuth Connection Settings

1. Call POST `/subscriptions/{sub}/providers/Microsoft.BotService/listAuthServiceProviders` to discover available providers (AAD, Google, etc.) and their required parameters.
2. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.BotService/botServices/{name}/Connections/{connectionName}` with the chosen provider's `serviceProviderId`, `clientId`, `clientSecret`, and `scopes`.
3. Verify with GET on the same connection path (note: `clientSecret` will be redacted).
4. To rotate secrets, PATCH the connection with updated `clientSecret`, then POST `.../listWithSecrets` to confirm the new value is stored.

### 3. Audit All Bots and Channels Across a Subscription

1. Call GET `/subscriptions/{sub}/providers/Microsoft.BotService/botServices` to list all bots subscription-wide.
2. Follow `nextLink` pagination until all bots are collected.
3. For each bot, call GET `.../botServices/{name}/channels` to enumerate configured channels.
4. For each bot, call GET `.../botServices/{name}/connections` to enumerate OAuth connection settings.
5. Compile results into an inventory, flagging bots with no channels (unused) or deprecated enterprise channels.

### 4. Safely Delete a Bot and Its Dependencies

1. Call GET `.../botServices/{name}/channels` to list all channels on the bot.
2. For each channel, call DELETE `.../channels/{channelName}` and confirm 200 or 204.
3. Call GET `.../botServices/{name}/connections` to list all connection settings.
4. For each connection, call DELETE `.../Connections/{connectionName}` and confirm 200 or 204.
5. Call DELETE `.../botServices/{name}` to remove the bot itself.
6. Verify with GET on the same bot path; expect 404 to confirm deletion.

### 5. Set Up an Enterprise Channel

1. Call POST `/providers/Microsoft.BotService/checkEnterpriseChannelNameAvailability` with `{ name }` to verify the name is free.
2. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.BotService/enterpriseChannels/{name}` with node locations and SKU.
3. Poll GET on the same path until `properties.provisioningState` is `Succeeded`.
4. Call GET `.../enterpriseChannels` at the resource group level to confirm it appears in the listing.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
