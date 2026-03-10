---
name: cloudflare-api
description: "Cloudflare API skill. Use when working with Cloudflare for accounts, certificates, internal. Covers 2603 endpoints."
version: 1.0.0
generator: lapsh
---

# Cloudflare API
API version: 4.0.0

## Auth
ApiKey X-Auth-Email in header | ApiKey X-Auth-Key in header | Bearer bearer | ApiKey X-Auth-User-Service-Key in header

## Base URL
https://api.cloudflare.com/client/v4

## Setup
1. Set Authorization header with your Bearer token
2. GET /accounts -- verify access
3. POST /accounts -- create first accounts

## Endpoints

2603 endpoints across 15 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List Accounts |
| POST | /accounts | Create an account |
| POST | /accounts/move | Batch move accounts |
| GET | /accounts/{accountId}/resource-library/applications | Get  applications |
| POST | /accounts/{accountId}/resource-library/applications | Create application |
| GET | /accounts/{accountId}/resource-library/applications/{id} | Get application By Id |
| PATCH | /accounts/{accountId}/resource-library/applications/{id} | Update application version |
| GET | /accounts/{accountId}/resource-library/categories | Get all application categories |
| GET | /accounts/{accountId}/resource-library/categories/{id} | Show application category by ID |
| GET | /accounts/{account_identifier}/custom_pages | List custom pages |
| GET | /accounts/{account_identifier}/custom_pages/{identifier} | Get a custom page |
| PUT | /accounts/{account_identifier}/custom_pages/{identifier} | Update a custom page |
| DELETE | /accounts/{account_id} | Delete a specific account |
| GET | /accounts/{account_id} | Account Details |
| PUT | /accounts/{account_id} | Update Account |
| GET | /accounts/{account_id}/abuse-reports | List abuse reports |
| GET | /accounts/{account_id}/abuse-reports/{report_id}/emails | List abuse report emails |
| GET | /accounts/{account_id}/abuse-reports/{report_id}/mitigations | List abuse report mitigations |
| POST | /accounts/{account_id}/abuse-reports/{report_id}/mitigations/appeal | Request review on mitigations |
| GET | /accounts/{account_id}/abuse-reports/{report_param} | Abuse Report Details |
| POST | /accounts/{account_id}/abuse-reports/{report_param} | Submit an abuse report |
| GET | /accounts/{account_id}/access/ai-controls/mcp/portals | List MCP Portals |
| POST | /accounts/{account_id}/access/ai-controls/mcp/portals | Create a new MCP Portal |
| DELETE | /accounts/{account_id}/access/ai-controls/mcp/portals/{id} | Delete a MCP Portal |
| GET | /accounts/{account_id}/access/ai-controls/mcp/portals/{id} | Read details of an MCP Portal |
| PUT | /accounts/{account_id}/access/ai-controls/mcp/portals/{id} | Update a MCP Portal |
| GET | /accounts/{account_id}/access/ai-controls/mcp/servers | List MCP Servers |
| POST | /accounts/{account_id}/access/ai-controls/mcp/servers | Create a new MCP Server |
| DELETE | /accounts/{account_id}/access/ai-controls/mcp/servers/{id} | Delete a MCP Server |
| GET | /accounts/{account_id}/access/ai-controls/mcp/servers/{id} | Read the details of a MCP Server |
| PUT | /accounts/{account_id}/access/ai-controls/mcp/servers/{id} | Update a MCP Server |
| POST | /accounts/{account_id}/access/ai-controls/mcp/servers/{id}/sync | Sync MCP Server Capabilities |
| GET | /accounts/{account_id}/access/apps | List Access applications |
| POST | /accounts/{account_id}/access/apps | Add an Access application |
| GET | /accounts/{account_id}/access/apps/ca | List short-lived certificate CAs |
| DELETE | /accounts/{account_id}/access/apps/{app_id} | Delete an Access application |
| GET | /accounts/{account_id}/access/apps/{app_id} | Get an Access application |
| PUT | /accounts/{account_id}/access/apps/{app_id} | Update an Access application |
| DELETE | /accounts/{account_id}/access/apps/{app_id}/ca | Delete a short-lived certificate CA |
| GET | /accounts/{account_id}/access/apps/{app_id}/ca | Get a short-lived certificate CA |
| POST | /accounts/{account_id}/access/apps/{app_id}/ca | Create a short-lived certificate CA |
| GET | /accounts/{account_id}/access/apps/{app_id}/policies | List Access application policies |
| POST | /accounts/{account_id}/access/apps/{app_id}/policies | Create an Access application policy |
| DELETE | /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id} | Delete an Access application policy |
| GET | /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id} | Get an Access application policy |
| PUT | /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id} | Update an Access application policy |
| PUT | /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id}/make_reusable | Convert an Access application policy to a reusable policy |
| POST | /accounts/{account_id}/access/apps/{app_id}/revoke_tokens | Revoke application tokens |
| PATCH | /accounts/{account_id}/access/apps/{app_id}/settings | Update Access application settings |
| PUT | /accounts/{account_id}/access/apps/{app_id}/settings | Update Access application settings |
| GET | /accounts/{account_id}/access/apps/{app_id}/user_policy_checks | Test Access policies |
| GET | /accounts/{account_id}/access/bookmarks | List Bookmark applications |
| DELETE | /accounts/{account_id}/access/bookmarks/{bookmark_id} | Delete a Bookmark application |
| GET | /accounts/{account_id}/access/bookmarks/{bookmark_id} | Get a Bookmark application |
| POST | /accounts/{account_id}/access/bookmarks/{bookmark_id} | Create a Bookmark application |
| PUT | /accounts/{account_id}/access/bookmarks/{bookmark_id} | Update a Bookmark application |
| GET | /accounts/{account_id}/access/certificates | List mTLS certificates |
| POST | /accounts/{account_id}/access/certificates | Add an mTLS certificate |
| GET | /accounts/{account_id}/access/certificates/settings | List all mTLS hostname settings |
| PUT | /accounts/{account_id}/access/certificates/settings | Update an mTLS certificate's hostname settings |
| DELETE | /accounts/{account_id}/access/certificates/{certificate_id} | Delete an mTLS certificate |
| GET | /accounts/{account_id}/access/certificates/{certificate_id} | Get an mTLS certificate |
| PUT | /accounts/{account_id}/access/certificates/{certificate_id} | Update an mTLS certificate |
| GET | /accounts/{account_id}/access/custom_pages | List custom pages |
| POST | /accounts/{account_id}/access/custom_pages | Create a custom page |
| DELETE | /accounts/{account_id}/access/custom_pages/{custom_page_id} | Delete a custom page |
| GET | /accounts/{account_id}/access/custom_pages/{custom_page_id} | Get a custom page |
| PUT | /accounts/{account_id}/access/custom_pages/{custom_page_id} | Update a custom page |
| GET | /accounts/{account_id}/access/gateway_ca | List SSH Certificate Authorities (CA) |
| POST | /accounts/{account_id}/access/gateway_ca | Add a new SSH Certificate Authority (CA) |
| DELETE | /accounts/{account_id}/access/gateway_ca/{certificate_id} | Delete an SSH Certificate Authority (CA) |
| GET | /accounts/{account_id}/access/groups | List Access groups |
| POST | /accounts/{account_id}/access/groups | Create an Access group |
| DELETE | /accounts/{account_id}/access/groups/{group_id} | Delete an Access group |
| GET | /accounts/{account_id}/access/groups/{group_id} | Get an Access group |
| PUT | /accounts/{account_id}/access/groups/{group_id} | Update an Access group |
| GET | /accounts/{account_id}/access/identity_providers | List Access identity providers |
| POST | /accounts/{account_id}/access/identity_providers | Add an Access identity provider |
| DELETE | /accounts/{account_id}/access/identity_providers/{identity_provider_id} | Delete an Access identity provider |
| GET | /accounts/{account_id}/access/identity_providers/{identity_provider_id} | Get an Access identity provider |
| PUT | /accounts/{account_id}/access/identity_providers/{identity_provider_id} | Update an Access identity provider |
| GET | /accounts/{account_id}/access/identity_providers/{identity_provider_id}/scim/groups | List SCIM Group resources |
| GET | /accounts/{account_id}/access/identity_providers/{identity_provider_id}/scim/users | List SCIM User resources |
| GET | /accounts/{account_id}/access/keys | Get the Access key configuration |
| PUT | /accounts/{account_id}/access/keys | Update the Access key configuration |
| POST | /accounts/{account_id}/access/keys/rotate | Rotate Access keys |
| GET | /accounts/{account_id}/access/logs/access_requests | Get Access authentication logs |
| GET | /accounts/{account_id}/access/logs/scim/updates | List Access SCIM update logs |
| GET | /accounts/{account_id}/access/organizations | Get your Zero Trust organization |
| POST | /accounts/{account_id}/access/organizations | Create your Zero Trust organization |
| PUT | /accounts/{account_id}/access/organizations | Update your Zero Trust organization |
| GET | /accounts/{account_id}/access/organizations/doh | Get your Zero Trust organization DoH settings |
| PUT | /accounts/{account_id}/access/organizations/doh | Update your Zero Trust organization DoH settings |
| POST | /accounts/{account_id}/access/organizations/revoke_user | Revoke all Access tokens for a user |
| GET | /accounts/{account_id}/access/policies | List Access reusable policies |
| POST | /accounts/{account_id}/access/policies | Create an Access reusable policy |
| DELETE | /accounts/{account_id}/access/policies/{policy_id} | Delete an Access reusable policy |
| GET | /accounts/{account_id}/access/policies/{policy_id} | Get an Access reusable policy |
| PUT | /accounts/{account_id}/access/policies/{policy_id} | Update an Access reusable policy |
| POST | /accounts/{account_id}/access/policy-tests | Start Access policy test |
| GET | /accounts/{account_id}/access/policy-tests/{policy_test_id} | Get the current status of a given Access policy test |
| GET | /accounts/{account_id}/access/policy-tests/{policy_test_id}/users | Get an Access policy test users page |
| PATCH | /accounts/{account_id}/access/seats | Update a user seat |
| GET | /accounts/{account_id}/access/service_tokens | List service tokens |
| POST | /accounts/{account_id}/access/service_tokens | Create a service token |
| DELETE | /accounts/{account_id}/access/service_tokens/{service_token_id} | Delete a service token |
| GET | /accounts/{account_id}/access/service_tokens/{service_token_id} | Get a service token |
| PUT | /accounts/{account_id}/access/service_tokens/{service_token_id} | Update a service token |
| POST | /accounts/{account_id}/access/service_tokens/{service_token_id}/refresh | Refresh a service token |
| POST | /accounts/{account_id}/access/service_tokens/{service_token_id}/rotate | Rotate a service token |
| GET | /accounts/{account_id}/access/tags | List tags |
| POST | /accounts/{account_id}/access/tags | Create a tag |
| DELETE | /accounts/{account_id}/access/tags/{tag_name} | Delete a tag |
| GET | /accounts/{account_id}/access/tags/{tag_name} | Get a tag |
| PUT | /accounts/{account_id}/access/tags/{tag_name} | Update a tag |
| GET | /accounts/{account_id}/access/users | Get users |
| POST | /accounts/{account_id}/access/users | Create a user |
| DELETE | /accounts/{account_id}/access/users/{user_id} | Delete a user |
| GET | /accounts/{account_id}/access/users/{user_id} | Get a user |
| PUT | /accounts/{account_id}/access/users/{user_id} | Update a user |
| GET | /accounts/{account_id}/access/users/{user_id}/active_sessions | Get active sessions |
| GET | /accounts/{account_id}/access/users/{user_id}/active_sessions/{nonce} | Get single active session |
| GET | /accounts/{account_id}/access/users/{user_id}/failed_logins | Get failed logins |
| GET | /accounts/{account_id}/access/users/{user_id}/last_seen_identity | Get last seen identity |
| DELETE | /accounts/{account_id}/access/users/{user_id}/mfa_authenticators/{authenticator_id} | Delete a user's MFA device |
| GET | /accounts/{account_id}/addressing/address_maps | List Address Maps |
| POST | /accounts/{account_id}/addressing/address_maps | Create Address Map |
| DELETE | /accounts/{account_id}/addressing/address_maps/{address_map_id} | Delete Address Map |
| GET | /accounts/{account_id}/addressing/address_maps/{address_map_id} | Address Map Details |
| PATCH | /accounts/{account_id}/addressing/address_maps/{address_map_id} | Update Address Map |
| DELETE | /accounts/{account_id}/addressing/address_maps/{address_map_id}/accounts/{account_id} | Remove an account membership from an Address Map |
| PUT | /accounts/{account_id}/addressing/address_maps/{address_map_id}/accounts/{account_id} | Add an account membership to an Address Map |
| DELETE | /accounts/{account_id}/addressing/address_maps/{address_map_id}/ips/{ip_address} | Remove an IP from an Address Map |
| PUT | /accounts/{account_id}/addressing/address_maps/{address_map_id}/ips/{ip_address} | Add an IP to an Address Map |
| DELETE | /accounts/{account_id}/addressing/address_maps/{address_map_id}/zones/{zone_id} | Remove a zone membership from an Address Map |
| PUT | /accounts/{account_id}/addressing/address_maps/{address_map_id}/zones/{zone_id} | Add a zone membership to an Address Map |
| GET | /accounts/{account_id}/addressing/leases | List Leases |
| POST | /accounts/{account_id}/addressing/loa_documents | Upload LOA Document |
| GET | /accounts/{account_id}/addressing/loa_documents/{loa_document_id}/download | Download LOA Document |
| GET | /accounts/{account_id}/addressing/prefixes | List Prefixes |
| POST | /accounts/{account_id}/addressing/prefixes | Add Prefix |
| DELETE | /accounts/{account_id}/addressing/prefixes/{prefix_id} | Delete Prefix |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id} | Prefix Details |
| PATCH | /accounts/{account_id}/addressing/prefixes/{prefix_id} | Update Prefix Description |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes | List BGP Prefixes |
| POST | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes | Create BGP Prefix |
| DELETE | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id} | Delete BGP Prefix |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id} | Fetch BGP Prefix |
| PATCH | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id} | Update BGP Prefix |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/status | Get Advertisement Status |
| PATCH | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/status | Update Prefix Dynamic Advertisement Status |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings | List Service Bindings |
| POST | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings | Create Service Binding |
| DELETE | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings/{binding_id} | Delete Service Binding |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings/{binding_id} | Get Service Binding |
| GET | /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations | List Prefix Delegations |
| POST | /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations | Create Prefix Delegation |
| DELETE | /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations/{delegation_id} | Delete Prefix Delegation |
| POST | /accounts/{account_id}/addressing/prefixes/{prefix_id}/validate | Validate Prefix |
| GET | /accounts/{account_id}/addressing/regional_hostnames/regions | List Regions |
| GET | /accounts/{account_id}/addressing/services | List Services |
| GET | /accounts/{account_id}/ai-gateway/evaluation-types | List Evaluators |
| GET | /accounts/{account_id}/ai-gateway/gateways | List Gateways |
| POST | /accounts/{account_id}/ai-gateway/gateways | Create a new Gateway |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets | List Datasets |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets | Create a new Dataset |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id} | Delete a Dataset |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id} | Fetch a Dataset |
| PUT | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id} | Update a Dataset |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations | List Evaluations |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations | Create a new Evaluation |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations/{id} | Delete a Evaluation |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations/{id} | Fetch a Evaluation |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs | Delete Gateway Logs |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs | List Gateway Logs |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id} | Get Gateway Log Detail |
| PATCH | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id} | Patch Gateway Log |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}/request | Get Gateway Log Request |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}/response | Get Gateway Log Response |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs | List Provider Configs |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs | Create a new Provider Configs |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs/{id} | Delete a Provider Configs |
| PUT | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs/{id} | Update a Provider Configs |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes | List all AI Gateway Dynamic Routes. |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes | Create a new AI Gateway Dynamic Route. |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id} | Delete an AI Gateway Dynamic Route. |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id} | Get an AI Gateway Dynamic Route. |
| PATCH | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id} | Update an AI Gateway Dynamic Route. |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/deployments | List all AI Gateway Dynamic Route Deployments. |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/deployments | Create a new AI Gateway Dynamic Route Deployment. |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions | List all AI Gateway Dynamic Route Versions. |
| POST | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions | Create a new AI Gateway Dynamic Route Version. |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions/{version_id} | Get an AI Gateway Dynamic Route Version. |
| GET | /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/url/{provider} | Get Gateway URL |
| DELETE | /accounts/{account_id}/ai-gateway/gateways/{id} | Delete a Gateway |
| GET | /accounts/{account_id}/ai-gateway/gateways/{id} | Fetch a Gateway |
| PUT | /accounts/{account_id}/ai-gateway/gateways/{id} | Update a Gateway |
| GET | /accounts/{account_id}/ai-search/instances | List instances. |
| POST | /accounts/{account_id}/ai-search/instances | Create new instances. |
| DELETE | /accounts/{account_id}/ai-search/instances/{id} | Delete instances. |
| GET | /accounts/{account_id}/ai-search/instances/{id} | Read instances. |
| PUT | /accounts/{account_id}/ai-search/instances/{id} | Update instances. |
| POST | /accounts/{account_id}/ai-search/instances/{id}/chat/completions | Chat Completions |
| GET | /accounts/{account_id}/ai-search/instances/{id}/items | Items List. |
| PUT | /accounts/{account_id}/ai-search/instances/{id}/items | Create or Update Item. |
| GET | /accounts/{account_id}/ai-search/instances/{id}/items/{item_id} | Get Item. |
| PATCH | /accounts/{account_id}/ai-search/instances/{id}/items/{item_id} | Sync Item. |
| GET | /accounts/{account_id}/ai-search/instances/{id}/jobs | List Jobs |
| POST | /accounts/{account_id}/ai-search/instances/{id}/jobs | Create new job |
| GET | /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id} | Get a Job Details |
| PATCH | /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id} | Change Job Status |
| GET | /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id}/logs | List Job Logs |
| POST | /accounts/{account_id}/ai-search/instances/{id}/search | Search |
| GET | /accounts/{account_id}/ai-search/instances/{id}/stats | Stats |
| GET | /accounts/{account_id}/ai-search/tokens | List tokens. |
| POST | /accounts/{account_id}/ai-search/tokens | Create new tokens. |
| DELETE | /accounts/{account_id}/ai-search/tokens/{id} | Delete tokens. |
| GET | /accounts/{account_id}/ai-search/tokens/{id} | Read tokens. |
| PUT | /accounts/{account_id}/ai-search/tokens/{id} | Update tokens. |
| GET | /accounts/{account_id}/ai/authors/search | Author Search |
| GET | /accounts/{account_id}/ai/finetunes | List Finetunes |
| POST | /accounts/{account_id}/ai/finetunes | Create a new Finetune |
| GET | /accounts/{account_id}/ai/finetunes/public | List Public Finetunes |
| POST | /accounts/{account_id}/ai/finetunes/{finetune_id}/finetune-assets | Upload a Finetune Asset |
| GET | /accounts/{account_id}/ai/models/schema | Get Model Schema |
| GET | /accounts/{account_id}/ai/models/search | Model Search |
| POST | /accounts/{account_id}/ai/run/@cf/ai4bharat/indictrans2-en-indic-1B | Execute @cf/ai4bharat/indictrans2-en-indic-1B model. |
| POST | /accounts/{account_id}/ai/run/@cf/ai4bharat/omni-indictrans2-en-indic-1b | Execute @cf/ai4bharat/omni-indictrans2-en-indic-1b model. |
| POST | /accounts/{account_id}/ai/run/@cf/aisingapore/gemma-sea-lion-v4-27b-it | Execute @cf/aisingapore/gemma-sea-lion-v4-27b-it model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/bge-base-en-v1.5 | Execute @cf/baai/bge-base-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/bge-large-en-v1.5 | Execute @cf/baai/bge-large-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/bge-m3 | Execute @cf/baai/bge-m3 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/bge-reranker-base | Execute @cf/baai/bge-reranker-base model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/bge-small-en-v1.5 | Execute @cf/baai/bge-small-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/omni-bge-base-en-v1.5 | Execute @cf/baai/omni-bge-base-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/omni-bge-large-en-v1.5 | Execute @cf/baai/omni-bge-large-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/omni-bge-m3 | Execute @cf/baai/omni-bge-m3 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/omni-bge-small-en-v1.5 | Execute @cf/baai/omni-bge-small-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/baai/ray-bge-large-en-v1.5 | Execute @cf/baai/ray-bge-large-en-v1.5 model. |
| POST | /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-1-schnell | Execute @cf/black-forest-labs/flux-1-schnell model. |
| POST | /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-dev | Execute @cf/black-forest-labs/flux-2-dev model. |
| POST | /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-klein-4b | Execute @cf/black-forest-labs/flux-2-klein-4b model. |
| POST | /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-klein-9b | Execute @cf/black-forest-labs/flux-2-klein-9b model. |
| POST | /accounts/{account_id}/ai/run/@cf/bytedance/stable-diffusion-xl-lightning | Execute @cf/bytedance/stable-diffusion-xl-lightning model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura | Open Websocket connection with @cf/deepgram/aura model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura-1 | Open Websocket connection with @cf/deepgram/aura-1 model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepgram/aura-1 | Execute @cf/deepgram/aura-1 model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura-1-internal | Open Websocket connection with @cf/deepgram/aura-1-internal model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura-2 | Open Websocket connection with @cf/deepgram/aura-2 model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-en | Open Websocket connection with @cf/deepgram/aura-2-en model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-en | Execute @cf/deepgram/aura-2-en model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-es | Open Websocket connection with @cf/deepgram/aura-2-es model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-es | Execute @cf/deepgram/aura-2-es model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/flux | Open Websocket connection with @cf/deepgram/flux model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepgram/flux | Execute @cf/deepgram/flux model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/nova-3 | Open Websocket connection with @cf/deepgram/nova-3 model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepgram/nova-3 | Execute @cf/deepgram/nova-3 model. |
| GET | /accounts/{account_id}/ai/run/@cf/deepgram/nova-3-internal | Open Websocket connection with @cf/deepgram/nova-3-internal model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepseek-ai/deepseek-math-7b-instruct | Execute @cf/deepseek-ai/deepseek-math-7b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/deepseek-ai/deepseek-r1-distill-qwen-32b | Execute @cf/deepseek-ai/deepseek-r1-distill-qwen-32b model. |
| POST | /accounts/{account_id}/ai/run/@cf/defog/sqlcoder-7b-2 | Execute @cf/defog/sqlcoder-7b-2 model. |
| POST | /accounts/{account_id}/ai/run/@cf/facebook/bart-large-cnn | Execute @cf/facebook/bart-large-cnn model. |
| POST | /accounts/{account_id}/ai/run/@cf/facebook/omni-bart-large-cnn | Execute @cf/facebook/omni-bart-large-cnn model. |
| POST | /accounts/{account_id}/ai/run/@cf/facebook/omni-detr-resnet-50 | Execute @cf/facebook/omni-detr-resnet-50 model. |
| POST | /accounts/{account_id}/ai/run/@cf/fblgit/una-cybertron-7b-v2-bf16 | Execute @cf/fblgit/una-cybertron-7b-v2-bf16 model. |
| POST | /accounts/{account_id}/ai/run/@cf/google/embeddinggemma-300m | Execute @cf/google/embeddinggemma-300m model. |
| POST | /accounts/{account_id}/ai/run/@cf/google/gemma-2b-it-lora | Execute @cf/google/gemma-2b-it-lora model. |
| POST | /accounts/{account_id}/ai/run/@cf/google/gemma-3-12b-it | Execute @cf/google/gemma-3-12b-it model. |
| POST | /accounts/{account_id}/ai/run/@cf/google/gemma-7b-it-lora | Execute @cf/google/gemma-7b-it-lora model. |
| POST | /accounts/{account_id}/ai/run/@cf/google/omni-embeddinggemma-300m | Execute @cf/google/omni-embeddinggemma-300m model. |
| POST | /accounts/{account_id}/ai/run/@cf/huggingface/distilbert-sst-2-int8 | Execute @cf/huggingface/distilbert-sst-2-int8 model. |
| POST | /accounts/{account_id}/ai/run/@cf/huggingface/omni-distilbert-sst-2-int8 | Execute @cf/huggingface/omni-distilbert-sst-2-int8 model. |
| POST | /accounts/{account_id}/ai/run/@cf/ibm-granite/granite-4.0-h-micro | Execute @cf/ibm-granite/granite-4.0-h-micro model. |
| POST | /accounts/{account_id}/ai/run/@cf/leonardo/lucid-origin | Execute @cf/leonardo/lucid-origin model. |
| POST | /accounts/{account_id}/ai/run/@cf/leonardo/phoenix-1.0 | Execute @cf/leonardo/phoenix-1.0 model. |
| POST | /accounts/{account_id}/ai/run/@cf/lykon/dreamshaper-8-lcm | Execute @cf/lykon/dreamshaper-8-lcm model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta-llama/llama-2-7b-chat-hf-lora | Execute @cf/meta-llama/llama-2-7b-chat-hf-lora model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-2-7b-chat-fp16 | Execute @cf/meta/llama-2-7b-chat-fp16 model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-2-7b-chat-int8 | Execute @cf/meta/llama-2-7b-chat-int8 model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3-8b-instruct | Execute @cf/meta/llama-3-8b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3-8b-instruct-awq | Execute @cf/meta/llama-3-8b-instruct-awq model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-70b-instruct-fp8-fast | Execute @cf/meta/llama-3.1-70b-instruct-fp8-fast model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-awq | Execute @cf/meta/llama-3.1-8b-instruct-awq model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-fp8 | Execute @cf/meta/llama-3.1-8b-instruct-fp8 model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-fp8-fast | Execute @cf/meta/llama-3.1-8b-instruct-fp8-fast model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-11b-vision-instruct | Execute @cf/meta/llama-3.2-11b-vision-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-1b-instruct | Execute @cf/meta/llama-3.2-1b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-3b-instruct | Execute @cf/meta/llama-3.2-3b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-3.3-70b-instruct-fp8-fast | Execute @cf/meta/llama-3.3-70b-instruct-fp8-fast model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-4-scout-17b-16e-instruct | Execute @cf/meta/llama-4-scout-17b-16e-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/llama-guard-3-8b | Execute @cf/meta/llama-guard-3-8b model. |
| POST | /accounts/{account_id}/ai/run/@cf/meta/m2m100-1.2b | Execute @cf/meta/m2m100-1.2b model. |
| POST | /accounts/{account_id}/ai/run/@cf/microsoft/phi-2 | Execute @cf/microsoft/phi-2 model. |
| POST | /accounts/{account_id}/ai/run/@cf/microsoft/resnet-50 | Execute @cf/microsoft/resnet-50 model. |
| POST | /accounts/{account_id}/ai/run/@cf/mistral/mistral-7b-instruct-v0.1 | Execute @cf/mistral/mistral-7b-instruct-v0.1 model. |
| POST | /accounts/{account_id}/ai/run/@cf/mistral/mistral-7b-instruct-v0.2-lora | Execute @cf/mistral/mistral-7b-instruct-v0.2-lora model. |
| POST | /accounts/{account_id}/ai/run/@cf/mistralai/mistral-small-3.1-24b-instruct | Execute @cf/mistralai/mistral-small-3.1-24b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/myshell-ai/melotts | Execute @cf/myshell-ai/melotts model. |
| POST | /accounts/{account_id}/ai/run/@cf/openai/gpt-oss-120b | Execute @cf/openai/gpt-oss-120b model. |
| POST | /accounts/{account_id}/ai/run/@cf/openai/gpt-oss-20b | Execute @cf/openai/gpt-oss-20b model. |
| POST | /accounts/{account_id}/ai/run/@cf/openai/whisper | Execute @cf/openai/whisper model. |
| POST | /accounts/{account_id}/ai/run/@cf/openai/whisper-large-v3-turbo | Execute @cf/openai/whisper-large-v3-turbo model. |
| POST | /accounts/{account_id}/ai/run/@cf/openai/whisper-tiny-en | Execute @cf/openai/whisper-tiny-en model. |
| POST | /accounts/{account_id}/ai/run/@cf/openchat/openchat-3.5-0106 | Execute @cf/openchat/openchat-3.5-0106 model. |
| POST | /accounts/{account_id}/ai/run/@cf/pfnet/plamo-embedding-1b | Execute @cf/pfnet/plamo-embedding-1b model. |
| GET | /accounts/{account_id}/ai/run/@cf/pipecat-ai/smart-turn-v2 | Open Websocket connection with @cf/pipecat-ai/smart-turn-v2 model. |
| GET | /accounts/{account_id}/ai/run/@cf/pipecat-ai/smart-turn-v3 | Open Websocket connection with @cf/pipecat-ai/smart-turn-v3 model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-0.5b-chat | Execute @cf/qwen/qwen1.5-0.5b-chat model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-1.8b-chat | Execute @cf/qwen/qwen1.5-1.8b-chat model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-14b-chat-awq | Execute @cf/qwen/qwen1.5-14b-chat-awq model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-7b-chat-awq | Execute @cf/qwen/qwen1.5-7b-chat-awq model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen2.5-coder-32b-instruct | Execute @cf/qwen/qwen2.5-coder-32b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen3-30b-a3b-fp8 | Execute @cf/qwen/qwen3-30b-a3b-fp8 model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwen3-embedding-0.6b | Execute @cf/qwen/qwen3-embedding-0.6b model. |
| POST | /accounts/{account_id}/ai/run/@cf/qwen/qwq-32b | Execute @cf/qwen/qwq-32b model. |
| POST | /accounts/{account_id}/ai/run/@cf/runwayml/stable-diffusion-v1-5-img2img | Execute @cf/runwayml/stable-diffusion-v1-5-img2img model. |
| POST | /accounts/{account_id}/ai/run/@cf/runwayml/stable-diffusion-v1-5-inpainting | Execute @cf/runwayml/stable-diffusion-v1-5-inpainting model. |
| POST | /accounts/{account_id}/ai/run/@cf/stabilityai/stable-diffusion-xl-base-1.0 | Execute @cf/stabilityai/stable-diffusion-xl-base-1.0 model. |
| GET | /accounts/{account_id}/ai/run/@cf/sven/test-pipe-http | Open Websocket connection with @cf/sven/test-pipe-http model. |
| GET | /accounts/{account_id}/ai/run/@cf/test/hello-world-cog | Open Websocket connection with @cf/test/hello-world-cog model. |
| POST | /accounts/{account_id}/ai/run/@cf/thebloke/discolm-german-7b-v1-awq | Execute @cf/thebloke/discolm-german-7b-v1-awq model. |
| POST | /accounts/{account_id}/ai/run/@cf/tiiuae/falcon-7b-instruct | Execute @cf/tiiuae/falcon-7b-instruct model. |
| POST | /accounts/{account_id}/ai/run/@cf/tinyllama/tinyllama-1.1b-chat-v1.0 | Execute @cf/tinyllama/tinyllama-1.1b-chat-v1.0 model. |
| POST | /accounts/{account_id}/ai/run/@cf/zai-org/glm-4.7-flash | Execute @cf/zai-org/glm-4.7-flash model. |
| POST | /accounts/{account_id}/ai/run/@hf/google/gemma-7b-it | Execute @hf/google/gemma-7b-it model. |
| POST | /accounts/{account_id}/ai/run/@hf/mistral/mistral-7b-instruct-v0.2 | Execute @hf/mistral/mistral-7b-instruct-v0.2 model. |
| POST | /accounts/{account_id}/ai/run/@hf/nexusflow/starling-lm-7b-beta | Execute @hf/nexusflow/starling-lm-7b-beta model. |
| POST | /accounts/{account_id}/ai/run/@hf/nousresearch/hermes-2-pro-mistral-7b | Execute @hf/nousresearch/hermes-2-pro-mistral-7b model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/deepseek-coder-6.7b-base-awq | Execute @hf/thebloke/deepseek-coder-6.7b-base-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/deepseek-coder-6.7b-instruct-awq | Execute @hf/thebloke/deepseek-coder-6.7b-instruct-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/llama-2-13b-chat-awq | Execute @hf/thebloke/llama-2-13b-chat-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/mistral-7b-instruct-v0.1-awq | Execute @hf/thebloke/mistral-7b-instruct-v0.1-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/neural-chat-7b-v3-1-awq | Execute @hf/thebloke/neural-chat-7b-v3-1-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/openhermes-2.5-mistral-7b-awq | Execute @hf/thebloke/openhermes-2.5-mistral-7b-awq model. |
| POST | /accounts/{account_id}/ai/run/@hf/thebloke/zephyr-7b-beta-awq | Execute @hf/thebloke/zephyr-7b-beta-awq model. |
| POST | /accounts/{account_id}/ai/run/{model_name} | Execute AI model |
| GET | /accounts/{account_id}/ai/tasks/search | Task Search |
| POST | /accounts/{account_id}/ai/tomarkdown | Convert Files into Markdown |
| GET | /accounts/{account_id}/ai/tomarkdown/supported | Get all converted formats supported |
| GET | /accounts/{account_id}/alerting/v3/available_alerts | Get Alert Types |
| GET | /accounts/{account_id}/alerting/v3/destinations/eligible | Get delivery mechanism eligibility |
| DELETE | /accounts/{account_id}/alerting/v3/destinations/pagerduty | Delete PagerDuty Services |
| GET | /accounts/{account_id}/alerting/v3/destinations/pagerduty | List PagerDuty services |
| POST | /accounts/{account_id}/alerting/v3/destinations/pagerduty/connect | Create PagerDuty integration token |
| GET | /accounts/{account_id}/alerting/v3/destinations/pagerduty/connect/{token_id} | Connect PagerDuty |
| GET | /accounts/{account_id}/alerting/v3/destinations/webhooks | List webhooks |
| POST | /accounts/{account_id}/alerting/v3/destinations/webhooks | Create a webhook |
| DELETE | /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id} | Delete a webhook |
| GET | /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id} | Get a webhook |
| PUT | /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id} | Update a webhook |
| GET | /accounts/{account_id}/alerting/v3/history | List History |
| GET | /accounts/{account_id}/alerting/v3/policies | List Notification policies |
| POST | /accounts/{account_id}/alerting/v3/policies | Create a Notification policy |
| DELETE | /accounts/{account_id}/alerting/v3/policies/{policy_id} | Delete a Notification policy |
| GET | /accounts/{account_id}/alerting/v3/policies/{policy_id} | Get a Notification policy |
| PUT | /accounts/{account_id}/alerting/v3/policies/{policy_id} | Update a Notification policy |
| GET | /accounts/{account_id}/alerting/v3/silences | List Silences |
| POST | /accounts/{account_id}/alerting/v3/silences | Create Silences |
| PUT | /accounts/{account_id}/alerting/v3/silences | Update Silences |
| DELETE | /accounts/{account_id}/alerting/v3/silences/{silence_id} | Delete Silence |
| GET | /accounts/{account_id}/alerting/v3/silences/{silence_id} | Get Silence |
| GET | /accounts/{account_id}/audit_logs | Get account audit logs |
| POST | /accounts/{account_id}/autorag/rags/{id}/ai-search | AI Search |
| GET | /accounts/{account_id}/autorag/rags/{id}/files | Files |
| GET | /accounts/{account_id}/autorag/rags/{id}/jobs | List Jobs |
| GET | /accounts/{account_id}/autorag/rags/{id}/jobs/{job_id} | Get a Job Details |
| GET | /accounts/{account_id}/autorag/rags/{id}/jobs/{job_id}/logs | List Job Logs |
| POST | /accounts/{account_id}/autorag/rags/{id}/search | Search |
| PATCH | /accounts/{account_id}/autorag/rags/{id}/sync | Sync |
| GET | /accounts/{account_id}/billing/profile | Billing Profile Details |
| GET | /accounts/{account_id}/botnet_feed/asn/{asn_id}/day_report | Get daily report |
| GET | /accounts/{account_id}/botnet_feed/asn/{asn_id}/full_report | Get full report |
| GET | /accounts/{account_id}/botnet_feed/configs/asn | Get list of ASNs |
| DELETE | /accounts/{account_id}/botnet_feed/configs/asn/{asn_id} | Delete an ASN |
| GET | /accounts/{account_id}/brand-protection/alerts | Read all alerts on submitted domains |
| PATCH | /accounts/{account_id}/brand-protection/alerts | Update alerts on submitted domains by ID |
| PATCH | /accounts/{account_id}/brand-protection/alerts/clear | Update verification statuses of tracked URLs to awaiting by ID |
| PATCH | /accounts/{account_id}/brand-protection/alerts/refute | Update verification statuses of tracked URLs to disproven by ID |
| PATCH | /accounts/{account_id}/brand-protection/alerts/verify | Update verification statuses of tracked URLs to confirmed by ID |
| DELETE | /accounts/{account_id}/brand-protection/brands | Delete brands by ID |
| GET | /accounts/{account_id}/brand-protection/brands | Read all brands |
| POST | /accounts/{account_id}/brand-protection/brands | Create new brands |
| DELETE | /accounts/{account_id}/brand-protection/brands/patterns | Delete patterns for brands by ID |
| GET | /accounts/{account_id}/brand-protection/brands/patterns | Read patterns for brands by ID |
| POST | /accounts/{account_id}/brand-protection/brands/patterns | Create new patterns for brands by ID |
| PATCH | /accounts/{account_id}/brand-protection/clear | Update verification statuses of submitted URLs to awaiting by ID |
| GET | /accounts/{account_id}/brand-protection/domain-info | Read submitted domains by ID |
| GET | /accounts/{account_id}/brand-protection/logo-matches | Read matches for logo queries by ID |
| GET | /accounts/{account_id}/brand-protection/logo-matches/download | Download matches for logo queries by ID |
| GET | /accounts/{account_id}/brand-protection/logos | Read all saved logo queries |
| POST | /accounts/{account_id}/brand-protection/logos | Create new saved logo queries from image files |
| DELETE | /accounts/{account_id}/brand-protection/logos/{logo_id} | Delete saved logo queries by ID |
| GET | /accounts/{account_id}/brand-protection/logos/{logo_id} | Read saved logo queries by ID |
| GET | /accounts/{account_id}/brand-protection/matches | Read matches for string queries by ID |
| GET | /accounts/{account_id}/brand-protection/matches/download | Download matches for string queries by ID |
| DELETE | /accounts/{account_id}/brand-protection/queries | Delete saved string queries by ID |
| GET | /accounts/{account_id}/brand-protection/queries | Read string queries by ID |
| PATCH | /accounts/{account_id}/brand-protection/queries | Update saved string queries by ID |
| POST | /accounts/{account_id}/brand-protection/queries | Create new saved string queries |
| POST | /accounts/{account_id}/brand-protection/queries/bulk | Create new saved string queries in bulk |
| GET | /accounts/{account_id}/brand-protection/recent-submissions | Read recent URL submissions |
| PATCH | /accounts/{account_id}/brand-protection/refute | Update verification statuses of submitted URLs to disproven by ID |
| POST | /accounts/{account_id}/brand-protection/scan-logo | Create new logo queries from image files |
| POST | /accounts/{account_id}/brand-protection/scan-page | Create new logo queries from URLs |
| POST | /accounts/{account_id}/brand-protection/search | Create new string queries |
| GET | /accounts/{account_id}/brand-protection/submission-info | Read URL submissions by ID |
| POST | /accounts/{account_id}/brand-protection/submit | Create new URL submissions |
| GET | /accounts/{account_id}/brand-protection/total-queries | Read the total number of saved string queries |
| GET | /accounts/{account_id}/brand-protection/tracked-domains | Read submitted domains by pattern |
| GET | /accounts/{account_id}/brand-protection/url-info | Read submitted URLs by ID |
| PATCH | /accounts/{account_id}/brand-protection/verify | Update verification statuses of submitted URLs to confirmed by ID |
| POST | /accounts/{account_id}/browser-rendering/content | Get HTML content. |
| POST | /accounts/{account_id}/browser-rendering/json | Get json. |
| POST | /accounts/{account_id}/browser-rendering/links | Get Links. |
| POST | /accounts/{account_id}/browser-rendering/markdown | Get markdown. |
| POST | /accounts/{account_id}/browser-rendering/pdf | Get PDF. |
| POST | /accounts/{account_id}/browser-rendering/scrape | Scrape elements. |
| POST | /accounts/{account_id}/browser-rendering/screenshot | Get screenshot. |
| POST | /accounts/{account_id}/browser-rendering/snapshot | Get HTML content and screenshot. |
| GET | /accounts/{account_id}/builds/account/limits | Get account limits |
| GET | /accounts/{account_id}/builds/builds | Get builds by version IDs |
| GET | /accounts/{account_id}/builds/builds/latest | Get latest builds by script IDs |
| GET | /accounts/{account_id}/builds/builds/{build_uuid} | Get build by UUID |
| PUT | /accounts/{account_id}/builds/builds/{build_uuid}/cancel | Cancel build |
| GET | /accounts/{account_id}/builds/builds/{build_uuid}/logs | Get build logs |
| PUT | /accounts/{account_id}/builds/repos/connections | Create or update repository connection |
| DELETE | /accounts/{account_id}/builds/repos/connections/{repo_connection_uuid} | Delete repository connection |
| GET | /accounts/{account_id}/builds/repos/{provider_type}/{provider_account_id}/{repo_id}/config_autofill | Get repository configuration autofill |
| GET | /accounts/{account_id}/builds/tokens | List build tokens |
| POST | /accounts/{account_id}/builds/tokens | Create build token |
| DELETE | /accounts/{account_id}/builds/tokens/{build_token_uuid} | Delete build token |
| POST | /accounts/{account_id}/builds/triggers | Create trigger |
| DELETE | /accounts/{account_id}/builds/triggers/{trigger_uuid} | Delete trigger |
| PATCH | /accounts/{account_id}/builds/triggers/{trigger_uuid} | Update trigger |
| POST | /accounts/{account_id}/builds/triggers/{trigger_uuid}/builds | Create manual build |
| GET | /accounts/{account_id}/builds/triggers/{trigger_uuid}/environment_variables | List environment variables |
| PATCH | /accounts/{account_id}/builds/triggers/{trigger_uuid}/environment_variables | Upsert environment variables |
| DELETE | /accounts/{account_id}/builds/triggers/{trigger_uuid}/environment_variables/{environment_variable_key} | Delete environment variable |
| POST | /accounts/{account_id}/builds/triggers/{trigger_uuid}/purge_build_cache | Purge build cache |
| GET | /accounts/{account_id}/builds/workers/{external_script_id}/builds | List builds by script |
| GET | /accounts/{account_id}/builds/workers/{external_script_id}/triggers | List triggers by script |
| GET | /accounts/{account_id}/calls/apps | List apps |
| POST | /accounts/{account_id}/calls/apps | Create a new app |
| DELETE | /accounts/{account_id}/calls/apps/{app_id} | Delete app |
| GET | /accounts/{account_id}/calls/apps/{app_id} | Retrieve app details |
| PUT | /accounts/{account_id}/calls/apps/{app_id} | Edit app details |
| GET | /accounts/{account_id}/calls/turn_keys | List TURN Keys |
| POST | /accounts/{account_id}/calls/turn_keys | Create a new TURN key |
| DELETE | /accounts/{account_id}/calls/turn_keys/{key_id} | Delete TURN key |
| GET | /accounts/{account_id}/calls/turn_keys/{key_id} | Retrieve TURN key details |
| PUT | /accounts/{account_id}/calls/turn_keys/{key_id} | Edit TURN key details |
| GET | /accounts/{account_id}/cfd_tunnel | List Cloudflare Tunnels |
| POST | /accounts/{account_id}/cfd_tunnel | Create a Cloudflare Tunnel |
| DELETE | /accounts/{account_id}/cfd_tunnel/{tunnel_id} | Delete a Cloudflare Tunnel |
| GET | /accounts/{account_id}/cfd_tunnel/{tunnel_id} | Get a Cloudflare Tunnel |
| PATCH | /accounts/{account_id}/cfd_tunnel/{tunnel_id} | Update a Cloudflare Tunnel |
| GET | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/configurations | Get configuration |
| PUT | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/configurations | Put configuration |
| DELETE | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/connections | Clean up Cloudflare Tunnel connections |
| GET | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/connections | List Cloudflare Tunnel connections |
| GET | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/connectors/{connector_id} | Get Cloudflare Tunnel connector |
| POST | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/management | Get a Cloudflare Tunnel management token |
| GET | /accounts/{account_id}/cfd_tunnel/{tunnel_id}/token | Get a Cloudflare Tunnel token |
| GET | /accounts/{account_id}/challenges/widgets | List Turnstile Widgets |
| POST | /accounts/{account_id}/challenges/widgets | Create a Turnstile Widget |
| DELETE | /accounts/{account_id}/challenges/widgets/{sitekey} | Delete a Turnstile Widget |
| GET | /accounts/{account_id}/challenges/widgets/{sitekey} | Turnstile Widget Details |
| PUT | /accounts/{account_id}/challenges/widgets/{sitekey} | Update a Turnstile Widget |
| POST | /accounts/{account_id}/challenges/widgets/{sitekey}/rotate_secret | Rotate Secret for a Turnstile Widget |
| POST | /accounts/{account_id}/cloudforce-one/binary | Posts a file to Binary Storage |
| GET | /accounts/{account_id}/cloudforce-one/binary/{hash} | Retrieves a file from Binary Storage |
| GET | /accounts/{account_id}/cloudforce-one/events | Filter and list events |
| GET | /accounts/{account_id}/cloudforce-one/events/aggregate | Aggregate events by single or multiple columns with optional date filtering |
| GET | /accounts/{account_id}/cloudforce-one/events/attackers | Lists attackers across multiple datasets |
| GET | /accounts/{account_id}/cloudforce-one/events/categories | Lists categories across multiple datasets |
| GET | /accounts/{account_id}/cloudforce-one/events/categories/catalog | Lists categories |
| POST | /accounts/{account_id}/cloudforce-one/events/categories/create | Creates a new category |
| DELETE | /accounts/{account_id}/cloudforce-one/events/categories/{category_id} | Deletes a category |
| GET | /accounts/{account_id}/cloudforce-one/events/categories/{category_id} | Reads a category |
| PATCH | /accounts/{account_id}/cloudforce-one/events/categories/{category_id} | Updates a category |
| POST | /accounts/{account_id}/cloudforce-one/events/categories/{category_id} | Updates a category |
| GET | /accounts/{account_id}/cloudforce-one/events/countries | Retrieves countries information for all countries |
| POST | /accounts/{account_id}/cloudforce-one/events/create | Creates a new event |
| POST | /accounts/{account_id}/cloudforce-one/events/create/bulk | Creates bulk events |
| POST | /accounts/{account_id}/cloudforce-one/events/create/bulk/relationships | Creates bulk DOS event with relationships and indicators |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset | Lists all datasets in an account |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/create | Creates a dataset |
| DELETE | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id} | Delete a dataset |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id} | Reads a dataset |
| PATCH | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id} | Updates an existing dataset |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id} | Updates an existing dataset |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/events/{event_id} | Reads an event |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicatorTypes/create | Create a new indicator type |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators | Lists indicators |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/bulk | Creates multiple indicators in bulk |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/create | Creates a new indicator |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/tags | List mirrored tags for an indicator dataset |
| DELETE | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id} | Deletes an indicator |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id} | Reads an indicator |
| PATCH | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id} | Updates an indicator |
| POST | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/move | Moves specified events from one dataset to another dataset |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/tags/{tag_uuid}/indicators | List indicators related to a tag |
| GET | /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/targetIndustries | Lists all target industries for a specific dataset |
| POST | /accounts/{account_id}/cloudforce-one/events/datasets/populate | Populate dataset-specific lookup tables from existing Events data with batch processing |
| DELETE | /accounts/{account_id}/cloudforce-one/events/event_tag/{event_id} | Removes a tag from an event |
| POST | /accounts/{account_id}/cloudforce-one/events/event_tag/{event_id}/create | Adds a tag to an event |
| GET | /accounts/{account_id}/cloudforce-one/events/indicator-types | Lists indicator types across multiple datasets |
| GET | /accounts/{account_id}/cloudforce-one/events/indicatorTypes | Lists all indicator types |
| GET | /accounts/{account_id}/cloudforce-one/events/indicators | Lists indicators across multiple datasets |
| GET | /accounts/{account_id}/cloudforce-one/events/queries | List all saved event queries |
| GET | /accounts/{account_id}/cloudforce-one/events/queries/alerts | List all event query alerts |
| POST | /accounts/{account_id}/cloudforce-one/events/queries/alerts/create | Create an event query alert |
| DELETE | /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id} | Delete an event query alert |
| GET | /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id} | Read an event query alert |
| PATCH | /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id} | Update an event query alert |
| POST | /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id} | Update an event query alert |
| POST | /accounts/{account_id}/cloudforce-one/events/queries/create | Create a saved event query |
| DELETE | /accounts/{account_id}/cloudforce-one/events/queries/{query_id} | Delete a saved event query |
| GET | /accounts/{account_id}/cloudforce-one/events/queries/{query_id} | Read a saved event query |
| PATCH | /accounts/{account_id}/cloudforce-one/events/queries/{query_id} | Update a saved event query |
| POST | /accounts/{account_id}/cloudforce-one/events/queries/{query_id} | Update a saved event query |
| GET | /accounts/{account_id}/cloudforce-one/events/raw/{dataset_id}/{event_id} | Reads data for a raw event |
| DELETE | /accounts/{account_id}/cloudforce-one/events/relate/{event_id} | Removes an event reference |
| POST | /accounts/{account_id}/cloudforce-one/events/relate/{event_id}/create | Creates event references for a event |
| POST | /accounts/{account_id}/cloudforce-one/events/relationships/create | Create a relationship between two events |
| GET | /accounts/{account_id}/cloudforce-one/events/tags | Lists all tags (SoT) |
| GET | /accounts/{account_id}/cloudforce-one/events/tags/categories | Lists all tag categories (SoT) |
| POST | /accounts/{account_id}/cloudforce-one/events/tags/categories/create | Creates a new tag category (SoT) |
| DELETE | /accounts/{account_id}/cloudforce-one/events/tags/categories/{category_uuid} | Deletes a tag category (SoT) |
| PATCH | /accounts/{account_id}/cloudforce-one/events/tags/categories/{category_uuid} | Updates a tag category (SoT) |
| POST | /accounts/{account_id}/cloudforce-one/events/tags/create | Creates a new tag |
| DELETE | /accounts/{account_id}/cloudforce-one/events/tags/{tag_uuid} | Deletes a tag (SoT) |
| PATCH | /accounts/{account_id}/cloudforce-one/events/tags/{tag_uuid} | Updates a tag (SoT) |
| GET | /accounts/{account_id}/cloudforce-one/events/targetIndustries | Lists target industries across multiple datasets |
| GET | /accounts/{account_id}/cloudforce-one/events/targetIndustries/catalog | Lists all target industries from industry map catalog |
| DELETE | /accounts/{account_id}/cloudforce-one/events/{dataset_id}/delete | Deletes one or more events |
| POST | /accounts/{account_id}/cloudforce-one/events/{dataset_id}/revert-do | Revert an Events Durable Object to a point in time |
| GET | /accounts/{account_id}/cloudforce-one/events/{event_id} | Reads an event |
| PATCH | /accounts/{account_id}/cloudforce-one/events/{event_id} | Updates an event |
| POST | /accounts/{account_id}/cloudforce-one/events/{event_id} | Updates an event |
| GET | /accounts/{account_id}/cloudforce-one/events/{event_id}/raw/{raw_id} | Reads data for a raw event |
| PATCH | /accounts/{account_id}/cloudforce-one/events/{event_id}/raw/{raw_id} | Updates a raw event |
| POST | /accounts/{account_id}/cloudforce-one/events/{event_id}/raw/{raw_id} | Updates a raw event |
| GET | /accounts/{account_id}/cloudforce-one/events/{event_id}/relationships | Filter and list events related to specific event |
| POST | /accounts/{account_id}/cloudforce-one/requests | List Requests |
| GET | /accounts/{account_id}/cloudforce-one/requests/constants | Get Request Priority, Status, and TLP constants |
| POST | /accounts/{account_id}/cloudforce-one/requests/new | Create a New Request. |
| POST | /accounts/{account_id}/cloudforce-one/requests/priority | List Priority Intelligence Requirements |
| POST | /accounts/{account_id}/cloudforce-one/requests/priority/new | Create a New Priority Intelligence Requirement |
| GET | /accounts/{account_id}/cloudforce-one/requests/priority/quota | Get Priority Intelligence Requirement Quota |
| DELETE | /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id} | Delete a Priority Intelligence Requirement |
| GET | /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id} | Get a Priority Intelligence Requirement |
| PUT | /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id} | Update a Priority Intelligence Requirement |
| GET | /accounts/{account_id}/cloudforce-one/requests/quota | Get Request Quota |
| GET | /accounts/{account_id}/cloudforce-one/requests/types | Get Request Types |
| DELETE | /accounts/{account_id}/cloudforce-one/requests/{request_id} | Delete a Request |
| GET | /accounts/{account_id}/cloudforce-one/requests/{request_id} | Get a Request |
| PUT | /accounts/{account_id}/cloudforce-one/requests/{request_id} | Update a Request |
| POST | /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset | List Request Assets |
| POST | /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/new | Create a New Request Asset |
| DELETE | /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id} | Delete a Request Asset |
| GET | /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id} | Get a Request Asset |
| PUT | /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id} | Update a Request Asset |
| POST | /accounts/{account_id}/cloudforce-one/requests/{request_id}/message | List Request Messages |
| POST | /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/new | Create a New Request Message |
| DELETE | /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/{message_id} | Delete a Request Message |
| PUT | /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/{message_id} | Update a Request Message |
| GET | /accounts/{account_id}/cloudforce-one/scans/config | List Scan Configs |
| POST | /accounts/{account_id}/cloudforce-one/scans/config | Create a new Scan Config |
| DELETE | /accounts/{account_id}/cloudforce-one/scans/config/{config_id} | Delete a Scan Config |
| PATCH | /accounts/{account_id}/cloudforce-one/scans/config/{config_id} | Update an existing Scan Config |
| GET | /accounts/{account_id}/cloudforce-one/scans/results/{config_id} | Get the Latest Scan Result |
| POST | /accounts/{account_id}/cloudforce-one/v2/events/graphql | GraphQL endpoint for event aggregation |
| GET | /accounts/{account_id}/cni/cnis | List existing CNI objects |
| POST | /accounts/{account_id}/cni/cnis | Create a new CNI object |
| DELETE | /accounts/{account_id}/cni/cnis/{cni} | Delete a specified CNI object |
| GET | /accounts/{account_id}/cni/cnis/{cni} | Get information about a CNI object |
| PUT | /accounts/{account_id}/cni/cnis/{cni} | Modify stored information about a CNI object |
| GET | /accounts/{account_id}/cni/interconnects | List existing interconnects |
| POST | /accounts/{account_id}/cni/interconnects | Create a new interconnect |
| DELETE | /accounts/{account_id}/cni/interconnects/{icon} | Delete an interconnect object |
| GET | /accounts/{account_id}/cni/interconnects/{icon} | Get information about an interconnect object |
| GET | /accounts/{account_id}/cni/interconnects/{icon}/loa | Generate the Letter of Authorization (LOA) for a given interconnect |
| GET | /accounts/{account_id}/cni/interconnects/{icon}/status | Get the current status of an interconnect object |
| GET | /accounts/{account_id}/cni/settings | Get the current settings for the active account |
| PUT | /accounts/{account_id}/cni/settings | Update the current settings for the active account |
| GET | /accounts/{account_id}/cni/slots | Retrieve a list of all slots matching the specified parameters |
| GET | /accounts/{account_id}/cni/slots/{slot} | Get information about the specified slot |
| GET | /accounts/{account_id}/connectivity/directory/services | List connectivity services |
| POST | /accounts/{account_id}/connectivity/directory/services | Create connectivity service |
| DELETE | /accounts/{account_id}/connectivity/directory/services/{service_id} | Delete connectivity service |
| GET | /accounts/{account_id}/connectivity/directory/services/{service_id} | Get connectivity service |
| PUT | /accounts/{account_id}/connectivity/directory/services/{service_id} | Update connectivity service |
| GET | /accounts/{account_id}/containers | List containers. |
| POST | /accounts/{account_id}/containers/registries/{domain}/credentials | Generate a JWT to interact with the specified image registry. |
| GET | /accounts/{account_id}/custom_ns | List Account Custom Nameservers |
| POST | /accounts/{account_id}/custom_ns | Add Account Custom Nameserver |
| DELETE | /accounts/{account_id}/custom_ns/{custom_ns_id} | Delete Account Custom Nameserver |
| GET | /accounts/{account_id}/d1/database | List D1 Databases |
| POST | /accounts/{account_id}/d1/database | Create D1 Database |
| DELETE | /accounts/{account_id}/d1/database/{database_id} | Delete D1 Database |
| GET | /accounts/{account_id}/d1/database/{database_id} | Get D1 Database |
| PATCH | /accounts/{account_id}/d1/database/{database_id} | Update D1 Database partially |
| PUT | /accounts/{account_id}/d1/database/{database_id} | Update D1 Database |
| POST | /accounts/{account_id}/d1/database/{database_id}/export | Export D1 Database as SQL |
| POST | /accounts/{account_id}/d1/database/{database_id}/import | Import SQL into your D1 Database |
| POST | /accounts/{account_id}/d1/database/{database_id}/query | Query D1 Database |
| POST | /accounts/{account_id}/d1/database/{database_id}/raw | Raw D1 Database query |
| GET | /accounts/{account_id}/d1/database/{database_id}/time_travel/bookmark | Get D1 database bookmark |
| POST | /accounts/{account_id}/d1/database/{database_id}/time_travel/restore | Restore D1 Database to a bookmark or point in time |
| GET | /accounts/{account_id}/devices | List devices (deprecated) |
| GET | /accounts/{account_id}/devices/ip-profiles | List IP profiles |
| POST | /accounts/{account_id}/devices/ip-profiles | Create IP profile |
| DELETE | /accounts/{account_id}/devices/ip-profiles/{profile_id} | Delete IP profile |
| GET | /accounts/{account_id}/devices/ip-profiles/{profile_id} | Get IP profile |
| PATCH | /accounts/{account_id}/devices/ip-profiles/{profile_id} | Update IP profile |
| GET | /accounts/{account_id}/devices/networks | List your device managed networks |
| POST | /accounts/{account_id}/devices/networks | Create a device managed network |
| DELETE | /accounts/{account_id}/devices/networks/{network_id} | Delete a device managed network |
| GET | /accounts/{account_id}/devices/networks/{network_id} | Get device managed network details |
| PUT | /accounts/{account_id}/devices/networks/{network_id} | Update a device managed network |
| GET | /accounts/{account_id}/devices/physical-devices | List devices |
| DELETE | /accounts/{account_id}/devices/physical-devices/{device_id} | Delete device |
| GET | /accounts/{account_id}/devices/physical-devices/{device_id} | Get device |
| POST | /accounts/{account_id}/devices/physical-devices/{device_id}/revoke | Revoke device registrations |
| GET | /accounts/{account_id}/devices/policies | List device settings profiles |
| GET | /accounts/{account_id}/devices/policy | Get the default device settings profile |
| PATCH | /accounts/{account_id}/devices/policy | Update the default device settings profile |
| POST | /accounts/{account_id}/devices/policy | Create a device settings profile |
| GET | /accounts/{account_id}/devices/policy/exclude | Get the Split Tunnel exclude list |
| PUT | /accounts/{account_id}/devices/policy/exclude | Set the Split Tunnel exclude list |
| GET | /accounts/{account_id}/devices/policy/fallback_domains | Get your Local Domain Fallback list |
| PUT | /accounts/{account_id}/devices/policy/fallback_domains | Set your Local Domain Fallback list |
| GET | /accounts/{account_id}/devices/policy/include | Get the Split Tunnel include list |
| PUT | /accounts/{account_id}/devices/policy/include | Set the Split Tunnel include list |
| DELETE | /accounts/{account_id}/devices/policy/{policy_id} | Delete a device settings profile |
| GET | /accounts/{account_id}/devices/policy/{policy_id} | Get device settings profile by ID |
| PATCH | /accounts/{account_id}/devices/policy/{policy_id} | Update a device settings profile |
| GET | /accounts/{account_id}/devices/policy/{policy_id}/exclude | Get the Split Tunnel exclude list for a device settings profile |
| PUT | /accounts/{account_id}/devices/policy/{policy_id}/exclude | Set the Split Tunnel exclude list for a device settings profile |
| GET | /accounts/{account_id}/devices/policy/{policy_id}/fallback_domains | Get the Local Domain Fallback list for a device settings profile |
| PUT | /accounts/{account_id}/devices/policy/{policy_id}/fallback_domains | Set the Local Domain Fallback list for a device settings profile |
| GET | /accounts/{account_id}/devices/policy/{policy_id}/include | Get the Split Tunnel include list for a device settings profile |
| PUT | /accounts/{account_id}/devices/policy/{policy_id}/include | Set the Split Tunnel include list for a device settings profile |
| GET | /accounts/{account_id}/devices/posture | List device posture rules |
| POST | /accounts/{account_id}/devices/posture | Create a device posture rule |
| GET | /accounts/{account_id}/devices/posture/integration | List your device posture integrations |
| POST | /accounts/{account_id}/devices/posture/integration | Create a device posture integration |
| DELETE | /accounts/{account_id}/devices/posture/integration/{integration_id} | Delete a device posture integration |
| GET | /accounts/{account_id}/devices/posture/integration/{integration_id} | Get device posture integration details |
| PATCH | /accounts/{account_id}/devices/posture/integration/{integration_id} | Update a device posture integration |
| DELETE | /accounts/{account_id}/devices/posture/{rule_id} | Delete a device posture rule |
| GET | /accounts/{account_id}/devices/posture/{rule_id} | Get device posture rule details |
| PUT | /accounts/{account_id}/devices/posture/{rule_id} | Update a device posture rule |
| DELETE | /accounts/{account_id}/devices/registrations | Delete registrations |
| GET | /accounts/{account_id}/devices/registrations | List registrations |
| POST | /accounts/{account_id}/devices/registrations/revoke | Revoke registrations |
| POST | /accounts/{account_id}/devices/registrations/unrevoke | Unrevoke registrations |
| DELETE | /accounts/{account_id}/devices/registrations/{registration_id} | Delete registration |
| GET | /accounts/{account_id}/devices/registrations/{registration_id} | Get registration |
| GET | /accounts/{account_id}/devices/registrations/{registration_id}/override_codes | Get override codes |
| GET | /accounts/{account_id}/devices/resilience/disconnect | Retrieve Global WARP override state |
| POST | /accounts/{account_id}/devices/resilience/disconnect | Set Global WARP override state |
| POST | /accounts/{account_id}/devices/revoke | Revoke devices (deprecated) |
| DELETE | /accounts/{account_id}/devices/settings | Reset device settings for a Zero Trust account with defaults. This turns off all proxying. |
| GET | /accounts/{account_id}/devices/settings | Get device settings for a Zero Trust account |
| PATCH | /accounts/{account_id}/devices/settings | Patch device settings for a Zero Trust account |
| PUT | /accounts/{account_id}/devices/settings | Update device settings for a Zero Trust account |
| POST | /accounts/{account_id}/devices/unrevoke | Unrevoke devices (deprecated) |
| GET | /accounts/{account_id}/devices/{device_id} | Get device (deprecated) |
| GET | /accounts/{account_id}/devices/{device_id}/override_codes | Get override codes (deprecated) |
| GET | /accounts/{account_id}/dex/colos | List Cloudflare colos |
| GET | /accounts/{account_id}/dex/commands | List account commands |
| POST | /accounts/{account_id}/dex/commands | Create account commands |
| GET | /accounts/{account_id}/dex/commands/devices | List devices eligible for remote captures |
| GET | /accounts/{account_id}/dex/commands/quota | Returns account commands usage, quota, and reset time |
| GET | /accounts/{account_id}/dex/commands/{command_id}/downloads/{filename} | Download command output file |
| GET | /accounts/{account_id}/dex/devices/dex_tests | List Device DEX tests |
| POST | /accounts/{account_id}/dex/devices/dex_tests | Create Device DEX test |
| DELETE | /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id} | Delete Device DEX test |
| GET | /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id} | Get Device DEX test |
| PUT | /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id} | Update Device DEX test |
| GET | /accounts/{account_id}/dex/devices/{device_id}/fleet-status/live | Get the live status of a latest device |
| GET | /accounts/{account_id}/dex/fleet-status/devices | List fleet status devices |
| GET | /accounts/{account_id}/dex/fleet-status/live | List fleet status details by dimension |
| GET | /accounts/{account_id}/dex/fleet-status/over-time | List fleet status aggregate details by dimension |
| GET | /accounts/{account_id}/dex/http-tests/{test_id} | Get details and aggregate metrics for an http test |
| GET | /accounts/{account_id}/dex/http-tests/{test_id}/percentiles | Get percentiles for an http test |
| GET | /accounts/{account_id}/dex/rules | List DEX Rules |
| POST | /accounts/{account_id}/dex/rules | Create a DEX Rule |
| DELETE | /accounts/{account_id}/dex/rules/{rule_id} | Delete a DEX Rule |
| GET | /accounts/{account_id}/dex/rules/{rule_id} | Get DEX Rule |
| PATCH | /accounts/{account_id}/dex/rules/{rule_id} | Update a DEX Rule |
| GET | /accounts/{account_id}/dex/tests/overview | List DEX test analytics |
| GET | /accounts/{account_id}/dex/tests/unique-devices | Get count of devices targeted |
| GET | /accounts/{account_id}/dex/traceroute-test-results/{test_result_id}/network-path | Get details for a specific traceroute test run |
| GET | /accounts/{account_id}/dex/traceroute-tests/{test_id} | Get details and aggregate metrics for a traceroute test |
| GET | /accounts/{account_id}/dex/traceroute-tests/{test_id}/network-path | Get network path breakdown for a traceroute test |
| GET | /accounts/{account_id}/dex/traceroute-tests/{test_id}/percentiles | Get percentiles for a traceroute test |
| GET | /accounts/{account_id}/dex/warp-change-events | List WARP change events. |
| GET | /accounts/{account_id}/diagnostics/endpoint-healthchecks | List Endpoint Health Checks |
| POST | /accounts/{account_id}/diagnostics/endpoint-healthchecks | Endpoint Health Check |
| DELETE | /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id} | Delete Endpoint Health Check |
| GET | /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id} | Get Endpoint Health Check |
| PUT | /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id} | Update Endpoint Health Check |
| POST | /accounts/{account_id}/diagnostics/traceroute | Traceroute |
| GET | /accounts/{account_id}/dlp/datasets | Fetch all datasets |
| POST | /accounts/{account_id}/dlp/datasets | Create a new dataset |
| DELETE | /accounts/{account_id}/dlp/datasets/{dataset_id} | Delete a dataset |
| GET | /accounts/{account_id}/dlp/datasets/{dataset_id} | Fetch a specific dataset |
| PUT | /accounts/{account_id}/dlp/datasets/{dataset_id} | Update details about a dataset |
| POST | /accounts/{account_id}/dlp/datasets/{dataset_id}/upload | Prepare to upload a new version of a dataset |
| POST | /accounts/{account_id}/dlp/datasets/{dataset_id}/upload/{version} | Upload a new version of a dataset |
| POST | /accounts/{account_id}/dlp/datasets/{dataset_id}/versions/{version} | Sets the column information for a multi-column upload |
| POST | /accounts/{account_id}/dlp/datasets/{dataset_id}/versions/{version}/entries/{entry_id} | Upload a new version of a multi-column dataset |
| GET | /accounts/{account_id}/dlp/document_fingerprints | Retrieve data about all document fingerprints. |
| POST | /accounts/{account_id}/dlp/document_fingerprints | Creates a new document fingerprint. |
| DELETE | /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id} | Delete a single document fingerprint. |
| GET | /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id} | Retrieve data about a specific document fingerprint. |
| POST | /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id} | Update the attributes of a single document fingerprint. |
| PUT | /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id} | Uploads a new version for a document fingerprint. |
| GET | /accounts/{account_id}/dlp/email/account_mapping | Get mapping |
| POST | /accounts/{account_id}/dlp/email/account_mapping | Create mapping |
| GET | /accounts/{account_id}/dlp/email/rules | List all email scanner rules |
| PATCH | /accounts/{account_id}/dlp/email/rules | Update email scanner rule priorities |
| POST | /accounts/{account_id}/dlp/email/rules | Create email scanner rule |
| DELETE | /accounts/{account_id}/dlp/email/rules/{rule_id} | Delete email scanner rule |
| GET | /accounts/{account_id}/dlp/email/rules/{rule_id} | Get an email scanner rule |
| PUT | /accounts/{account_id}/dlp/email/rules/{rule_id} | Update email scanner rule |
| GET | /accounts/{account_id}/dlp/entries | List all entries |
| POST | /accounts/{account_id}/dlp/entries | Create custom entry |
| PUT | /accounts/{account_id}/dlp/entries/custom/{entry_id} | Update custom entry |
| POST | /accounts/{account_id}/dlp/entries/integration | Create integration entry |
| DELETE | /accounts/{account_id}/dlp/entries/integration/{entry_id} | Delete integration entry |
| PUT | /accounts/{account_id}/dlp/entries/integration/{entry_id} | Update integration entry |
| POST | /accounts/{account_id}/dlp/entries/predefined | Create predefined entry |
| DELETE | /accounts/{account_id}/dlp/entries/predefined/{entry_id} | Delete predefined entry |
| PUT | /accounts/{account_id}/dlp/entries/predefined/{entry_id} | Update predefined entry |
| DELETE | /accounts/{account_id}/dlp/entries/{entry_id} | Delete custom entry |
| GET | /accounts/{account_id}/dlp/entries/{entry_id} | Get DLP Entry |
| PUT | /accounts/{account_id}/dlp/entries/{entry_id} | Update entry |
| GET | /accounts/{account_id}/dlp/limits | Fetch limits associated with DLP for account |
| POST | /accounts/{account_id}/dlp/patterns/validate | Validate a DLP regex pattern |
| GET | /accounts/{account_id}/dlp/payload_log | Get payload log settings |
| PUT | /accounts/{account_id}/dlp/payload_log | Set payload log settings |
| GET | /accounts/{account_id}/dlp/profiles | List all profiles |
| GET | /accounts/{account_id}/dlp/profiles/custom | List all custom profiles |
| POST | /accounts/{account_id}/dlp/profiles/custom | Create custom profile |
| DELETE | /accounts/{account_id}/dlp/profiles/custom/{profile_id} | Delete custom profile |
| GET | /accounts/{account_id}/dlp/profiles/custom/{profile_id} | Get custom profile |
| PUT | /accounts/{account_id}/dlp/profiles/custom/{profile_id} | Update custom profile |
| POST | /accounts/{account_id}/dlp/profiles/predefined | Create predefined profile |
| DELETE | /accounts/{account_id}/dlp/profiles/predefined/{profile_id} | Delete predefined profile |
| GET | /accounts/{account_id}/dlp/profiles/predefined/{profile_id} | Get predefined profile |
| PUT | /accounts/{account_id}/dlp/profiles/predefined/{profile_id} | Update predefined profile |
| GET | /accounts/{account_id}/dlp/profiles/predefined/{profile_id}/config | Get predefined profile config |
| POST | /accounts/{account_id}/dlp/profiles/predefined/{profile_id}/config | Create predefined profile |
| PUT | /accounts/{account_id}/dlp/profiles/predefined/{profile_id}/config | Update predefined profile config |
| GET | /accounts/{account_id}/dlp/profiles/{profile_id} | Get DLP Profile |
| GET | /accounts/{account_id}/dns_firewall | List DNS Firewall Clusters |
| POST | /accounts/{account_id}/dns_firewall | Create DNS Firewall Cluster |
| DELETE | /accounts/{account_id}/dns_firewall/{dns_firewall_id} | Delete DNS Firewall Cluster |
| GET | /accounts/{account_id}/dns_firewall/{dns_firewall_id} | DNS Firewall Cluster Details |
| PATCH | /accounts/{account_id}/dns_firewall/{dns_firewall_id} | Update DNS Firewall Cluster |
| GET | /accounts/{account_id}/dns_firewall/{dns_firewall_id}/dns_analytics/report | Table |
| GET | /accounts/{account_id}/dns_firewall/{dns_firewall_id}/dns_analytics/report/bytime | By Time |
| GET | /accounts/{account_id}/dns_firewall/{dns_firewall_id}/reverse_dns | Show DNS Firewall Cluster Reverse DNS |
| PATCH | /accounts/{account_id}/dns_firewall/{dns_firewall_id}/reverse_dns | Update DNS Firewall Cluster Reverse DNS |
| GET | /accounts/{account_id}/dns_records/usage | Get DNS Record Usage for Account |
| GET | /accounts/{account_id}/dns_settings | Show DNS Settings |
| PATCH | /accounts/{account_id}/dns_settings | Update DNS Settings |
| GET | /accounts/{account_id}/dns_settings/views | List Internal DNS Views |
| POST | /accounts/{account_id}/dns_settings/views | Create Internal DNS View |
| DELETE | /accounts/{account_id}/dns_settings/views/{view_id} | Delete Internal DNS View |
| GET | /accounts/{account_id}/dns_settings/views/{view_id} | DNS Internal View Details |
| PATCH | /accounts/{account_id}/dns_settings/views/{view_id} | Update Internal DNS View |
| GET | /accounts/{account_id}/email-security/investigate | Search email messages |
| POST | /accounts/{account_id}/email-security/investigate/move | Move multiple messages |
| POST | /accounts/{account_id}/email-security/investigate/preview | Preview for non-detection messages |
| POST | /accounts/{account_id}/email-security/investigate/release | Release messages from quarantine |
| GET | /accounts/{account_id}/email-security/investigate/{postfix_id} | Get message details |
| GET | /accounts/{account_id}/email-security/investigate/{postfix_id}/detections | Get message detection details |
| POST | /accounts/{account_id}/email-security/investigate/{postfix_id}/move | Move a message |
| GET | /accounts/{account_id}/email-security/investigate/{postfix_id}/preview | Get email preview |
| GET | /accounts/{account_id}/email-security/investigate/{postfix_id}/raw | Get raw email content |
| POST | /accounts/{account_id}/email-security/investigate/{postfix_id}/reclassify | Change email classfication |
| GET | /accounts/{account_id}/email-security/investigate/{postfix_id}/trace | Get email trace |
| GET | /accounts/{account_id}/email-security/phishguard/reports | Get `PhishGuard` reports |
| GET | /accounts/{account_id}/email-security/settings/allow_policies | List email allow policies |
| POST | /accounts/{account_id}/email-security/settings/allow_policies | Create an email allow policy |
| POST | /accounts/{account_id}/email-security/settings/allow_policies/batch | Batch Allow Policies |
| DELETE | /accounts/{account_id}/email-security/settings/allow_policies/{policy_id} | Delete an email allow policy |
| GET | /accounts/{account_id}/email-security/settings/allow_policies/{policy_id} | Get an email allow policy |
| PATCH | /accounts/{account_id}/email-security/settings/allow_policies/{policy_id} | Update an email allow policy |
| GET | /accounts/{account_id}/email-security/settings/block_senders | List blocked email senders |
| POST | /accounts/{account_id}/email-security/settings/block_senders | Create a blocked email sender |
| POST | /accounts/{account_id}/email-security/settings/block_senders/batch | Batch Block Senders |
| DELETE | /accounts/{account_id}/email-security/settings/block_senders/{pattern_id} | Delete a blocked email sender |
| GET | /accounts/{account_id}/email-security/settings/block_senders/{pattern_id} | Get a blocked email sender |
| PATCH | /accounts/{account_id}/email-security/settings/block_senders/{pattern_id} | Update a blocked email sender |
| DELETE | /accounts/{account_id}/email-security/settings/domains | Unprotect multiple email domains |
| GET | /accounts/{account_id}/email-security/settings/domains | List protected email domains |
| DELETE | /accounts/{account_id}/email-security/settings/domains/{domain_id} | Unprotect an email domain |
| GET | /accounts/{account_id}/email-security/settings/domains/{domain_id} | Get an email domain |
| PATCH | /accounts/{account_id}/email-security/settings/domains/{domain_id} | Update an email domain |
| GET | /accounts/{account_id}/email-security/settings/impersonation_registry | List entries in impersonation registry |
| POST | /accounts/{account_id}/email-security/settings/impersonation_registry | Create an entry in impersonation registry |
| DELETE | /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id} | Delete an entry from impersonation registry |
| GET | /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id} | Get an entry in impersonation registry |
| PATCH | /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id} | Update an entry in impersonation registry |
| POST | /accounts/{account_id}/email-security/settings/sending_domain_restrictions/batch | Batch Sending Domain Restrictions |
| GET | /accounts/{account_id}/email-security/settings/trusted_domains | List trusted email domains |
| POST | /accounts/{account_id}/email-security/settings/trusted_domains | Create a trusted email domain |
| POST | /accounts/{account_id}/email-security/settings/trusted_domains/batch | Batch Trusted Domains |
| DELETE | /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id} | Delete a trusted email domain |
| GET | /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id} | Get a trusted email domain |
| PATCH | /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id} | Update a trusted email domain |
| GET | /accounts/{account_id}/email-security/submissions | Get reclassify submissions |
| GET | /accounts/{account_id}/email/routing/addresses | List destination addresses |
| POST | /accounts/{account_id}/email/routing/addresses | Create a destination address |
| DELETE | /accounts/{account_id}/email/routing/addresses/{destination_address_identifier} | Delete destination address |
| GET | /accounts/{account_id}/email/routing/addresses/{destination_address_identifier} | Get a destination address |
| GET | /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration | List Event Notification Rules |
| DELETE | /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id} | Delete Event Notification Rules |
| GET | /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id} | Get Event Notification Rule |
| PUT | /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id} | Create Event Notification Rule |
| GET | /accounts/{account_id}/event_subscriptions/subscriptions | List Event Subscriptions |
| POST | /accounts/{account_id}/event_subscriptions/subscriptions | Create Event Subscription |
| DELETE | /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id} | Delete Event Subscription |
| GET | /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id} | Get Event Subscription |
| PATCH | /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id} | Update Event Subscription |
| GET | /accounts/{account_id}/firewall/access_rules/rules | List IP Access rules |
| POST | /accounts/{account_id}/firewall/access_rules/rules | Create an IP Access rule |
| DELETE | /accounts/{account_id}/firewall/access_rules/rules/{rule_id} | Delete an IP Access rule |
| GET | /accounts/{account_id}/firewall/access_rules/rules/{rule_id} | Get an IP Access rule |
| PATCH | /accounts/{account_id}/firewall/access_rules/rules/{rule_id} | Update an IP Access rule |
| GET | /accounts/{account_id}/gateway | Get Zero Trust account information |
| POST | /accounts/{account_id}/gateway | Create Zero Trust account |
| GET | /accounts/{account_id}/gateway/app_types | List application and application type mappings |
| GET | /accounts/{account_id}/gateway/apps/review_status | List applications review statuses |
| PUT | /accounts/{account_id}/gateway/apps/review_status | Update applications review statuses |
| GET | /accounts/{account_id}/gateway/audit_ssh_settings | Get Zero Trust SSH settings |
| PUT | /accounts/{account_id}/gateway/audit_ssh_settings | Update Zero Trust SSH settings |
| POST | /accounts/{account_id}/gateway/audit_ssh_settings/rotate_seed | Rotate Zero Trust SSH account seed |
| GET | /accounts/{account_id}/gateway/categories | List categories |
| GET | /accounts/{account_id}/gateway/certificates | List Zero Trust certificates |
| POST | /accounts/{account_id}/gateway/certificates | Create Zero Trust certificate |
| DELETE | /accounts/{account_id}/gateway/certificates/{certificate_id} | Delete Zero Trust certificate |
| GET | /accounts/{account_id}/gateway/certificates/{certificate_id} | Get Zero Trust certificate details |
| POST | /accounts/{account_id}/gateway/certificates/{certificate_id}/activate | Activate a Zero Trust certificate |
| POST | /accounts/{account_id}/gateway/certificates/{certificate_id}/deactivate | Deactivate a Zero Trust certificate |
| GET | /accounts/{account_id}/gateway/configuration | Get Zero Trust account configuration |
| PATCH | /accounts/{account_id}/gateway/configuration | Patch Zero Trust account configuration |
| PUT | /accounts/{account_id}/gateway/configuration | Update Zero Trust account configuration |
| GET | /accounts/{account_id}/gateway/configuration/custom_certificate | Get Zero Trust certificate configuration |
| GET | /accounts/{account_id}/gateway/lists | List Zero Trust lists |
| POST | /accounts/{account_id}/gateway/lists | Create Zero Trust list |
| DELETE | /accounts/{account_id}/gateway/lists/{list_id} | Delete Zero Trust list |
| GET | /accounts/{account_id}/gateway/lists/{list_id} | Get Zero Trust list details |
| PATCH | /accounts/{account_id}/gateway/lists/{list_id} | Patch Zero Trust list. |
| PUT | /accounts/{account_id}/gateway/lists/{list_id} | Update Zero Trust list |
| GET | /accounts/{account_id}/gateway/lists/{list_id}/items | Get Zero Trust list items |
| GET | /accounts/{account_id}/gateway/locations | List Zero Trust Gateway locations |
| POST | /accounts/{account_id}/gateway/locations | Create a Zero Trust Gateway location |
| DELETE | /accounts/{account_id}/gateway/locations/{location_id} | Delete a Zero Trust Gateway location |
| GET | /accounts/{account_id}/gateway/locations/{location_id} | Get Zero Trust Gateway location details |
| PUT | /accounts/{account_id}/gateway/locations/{location_id} | Update a Zero Trust Gateway location |
| GET | /accounts/{account_id}/gateway/logging | Get logging settings for the Zero Trust account |
| PUT | /accounts/{account_id}/gateway/logging | Update Zero Trust account logging settings |
| GET | /accounts/{account_id}/gateway/pacfiles | List PAC files |
| POST | /accounts/{account_id}/gateway/pacfiles | Create a PAC file |
| DELETE | /accounts/{account_id}/gateway/pacfiles/{pacfile_id} | Delete a PAC file |
| GET | /accounts/{account_id}/gateway/pacfiles/{pacfile_id} | Get a PAC file |
| PUT | /accounts/{account_id}/gateway/pacfiles/{pacfile_id} | Update a Zero Trust Gateway PAC file |
| GET | /accounts/{account_id}/gateway/proxy_endpoints | List proxy endpoints |
| POST | /accounts/{account_id}/gateway/proxy_endpoints | Create a proxy endpoint |
| DELETE | /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id} | Delete a proxy endpoint |
| GET | /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id} | Get a proxy endpoint |
| PATCH | /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id} | Update a proxy endpoint |
| GET | /accounts/{account_id}/gateway/rules | List Zero Trust Gateway rules |
| POST | /accounts/{account_id}/gateway/rules | Create a Zero Trust Gateway rule |
| GET | /accounts/{account_id}/gateway/rules/tenant | List Zero Trust Gateway rules inherited from the parent account |
| DELETE | /accounts/{account_id}/gateway/rules/{rule_id} | Delete a Zero Trust Gateway rule |
| GET | /accounts/{account_id}/gateway/rules/{rule_id} | Get Zero Trust Gateway rule details. |
| PUT | /accounts/{account_id}/gateway/rules/{rule_id} | Update a Zero Trust Gateway rule |
| POST | /accounts/{account_id}/gateway/rules/{rule_id}/reset_expiration | Reset the expiration of a Zero Trust Gateway Rule |
| GET | /accounts/{account_id}/hyperdrive/configs | List Hyperdrives |
| POST | /accounts/{account_id}/hyperdrive/configs | Create Hyperdrive |
| DELETE | /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id} | Delete Hyperdrive |
| GET | /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id} | Get Hyperdrive |
| PATCH | /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id} | Patch Hyperdrive |
| PUT | /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id} | Update Hyperdrive |
| GET | /accounts/{account_id}/iam/permission_groups | List Account Permission Groups |
| GET | /accounts/{account_id}/iam/permission_groups/{permission_group_id} | Permission Group Details |
| GET | /accounts/{account_id}/iam/resource_groups | List Resource Groups |
| POST | /accounts/{account_id}/iam/resource_groups | Create Resource Group |
| DELETE | /accounts/{account_id}/iam/resource_groups/{resource_group_id} | Remove Resource Group |
| GET | /accounts/{account_id}/iam/resource_groups/{resource_group_id} | Resource Group Details |
| PUT | /accounts/{account_id}/iam/resource_groups/{resource_group_id} | Update Resource Group |
| GET | /accounts/{account_id}/iam/user_groups | List User Groups |
| POST | /accounts/{account_id}/iam/user_groups | Create User Group |
| DELETE | /accounts/{account_id}/iam/user_groups/{user_group_id} | Remove User Group |
| GET | /accounts/{account_id}/iam/user_groups/{user_group_id} | User Group Details |
| PUT | /accounts/{account_id}/iam/user_groups/{user_group_id} | Update User Group |
| GET | /accounts/{account_id}/iam/user_groups/{user_group_id}/members | List User Group Members |
| POST | /accounts/{account_id}/iam/user_groups/{user_group_id}/members | Add User Group Members |
| PUT | /accounts/{account_id}/iam/user_groups/{user_group_id}/members | Update User Group Members |
| DELETE | /accounts/{account_id}/iam/user_groups/{user_group_id}/members/{member_id} | Remove User Group Member |
| GET | /accounts/{account_id}/images/v1 | List images |
| POST | /accounts/{account_id}/images/v1 | Upload an image |
| GET | /accounts/{account_id}/images/v1/keys | List Signing Keys |
| DELETE | /accounts/{account_id}/images/v1/keys/{signing_key_name} | Delete Signing Key |
| PUT | /accounts/{account_id}/images/v1/keys/{signing_key_name} | Create a new Signing Key |
| GET | /accounts/{account_id}/images/v1/stats | Images usage statistics |
| GET | /accounts/{account_id}/images/v1/variants | List variants |
| POST | /accounts/{account_id}/images/v1/variants | Create a variant |
| DELETE | /accounts/{account_id}/images/v1/variants/{variant_id} | Delete a variant |
| GET | /accounts/{account_id}/images/v1/variants/{variant_id} | Variant details |
| PATCH | /accounts/{account_id}/images/v1/variants/{variant_id} | Update a variant |
| DELETE | /accounts/{account_id}/images/v1/{image_id} | Delete image |
| GET | /accounts/{account_id}/images/v1/{image_id} | Image details |
| PATCH | /accounts/{account_id}/images/v1/{image_id} | Update image |
| GET | /accounts/{account_id}/images/v1/{image_id}/blob | Base image |
| GET | /accounts/{account_id}/images/v2 | List images V2 |
| POST | /accounts/{account_id}/images/v2/direct_upload | Create authenticated direct upload URL V2 |
| GET | /accounts/{account_id}/infrastructure/targets | List all targets |
| POST | /accounts/{account_id}/infrastructure/targets | Create new target |
| DELETE | /accounts/{account_id}/infrastructure/targets/batch | Delete targets (Deprecated) |
| PUT | /accounts/{account_id}/infrastructure/targets/batch | Create new targets |
| POST | /accounts/{account_id}/infrastructure/targets/batch_delete | Delete targets |
| DELETE | /accounts/{account_id}/infrastructure/targets/{target_id} | Delete target |
| GET | /accounts/{account_id}/infrastructure/targets/{target_id} | Get target |
| PUT | /accounts/{account_id}/infrastructure/targets/{target_id} | Update target |
| GET | /accounts/{account_id}/intel/asn/{asn} | Get ASN Overview. |
| GET | /accounts/{account_id}/intel/asn/{asn}/subnets | Get ASN Subnets |
| GET | /accounts/{account_id}/intel/attack-surface-report/issue-types | Retrieves Security Center Issues Types |
| GET | /accounts/{account_id}/intel/attack-surface-report/issues | Retrieves Security Center Issues |
| GET | /accounts/{account_id}/intel/attack-surface-report/issues/class | Retrieves Security Center Issue Counts by Class |
| GET | /accounts/{account_id}/intel/attack-surface-report/issues/severity | Retrieves Security Center Issue Counts by Severity |
| GET | /accounts/{account_id}/intel/attack-surface-report/issues/type | Retrieves Security Center Issue Counts by Type |
| PUT | /accounts/{account_id}/intel/attack-surface-report/{issue_id}/dismiss | Archives Security Center Insight |
| GET | /accounts/{account_id}/intel/dns | Get Passive DNS by IP |
| GET | /accounts/{account_id}/intel/domain | Get Domain Details |
| GET | /accounts/{account_id}/intel/domain-history | Get Domain History |
| GET | /accounts/{account_id}/intel/domain/bulk | Get Multiple Domain Details |
| GET | /accounts/{account_id}/intel/indicator-feeds | Get indicator feeds owned by this account |
| POST | /accounts/{account_id}/intel/indicator-feeds | Create new indicator feed |
| PUT | /accounts/{account_id}/intel/indicator-feeds/permissions/add | Grant permission to indicator feed |
| PUT | /accounts/{account_id}/intel/indicator-feeds/permissions/remove | Revoke permission to indicator feed |
| GET | /accounts/{account_id}/intel/indicator-feeds/permissions/view | List indicator feed permissions |
| GET | /accounts/{account_id}/intel/indicator-feeds/{feed_id} | Get indicator feed metadata |
| PUT | /accounts/{account_id}/intel/indicator-feeds/{feed_id} | Update indicator feed metadata |
| GET | /accounts/{account_id}/intel/indicator-feeds/{feed_id}/data | Get indicator feed data |
| GET | /accounts/{account_id}/intel/indicator-feeds/{feed_id}/download | Download indicator feed data |
| PUT | /accounts/{account_id}/intel/indicator-feeds/{feed_id}/snapshot | Update indicator feed data |
| GET | /accounts/{account_id}/intel/ip | Get IP Overview |
| GET | /accounts/{account_id}/intel/ip-lists | Get Available IP Lists |
| POST | /accounts/{account_id}/intel/miscategorization | Create Miscategorization |
| GET | /accounts/{account_id}/intel/sinkholes | List sinkholes owned by this account |
| GET | /accounts/{account_id}/intel/whois | Get WHOIS Record |
| GET | /accounts/{account_id}/load_balancers/monitor_groups | List Monitor Groups |
| POST | /accounts/{account_id}/load_balancers/monitor_groups | Create Monitor Group |
| DELETE | /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id} | Delete Monitor Group |
| GET | /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id} | Monitor Group Details |
| PATCH | /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id} | Patch Monitor Group |
| PUT | /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id} | Update Monitor Group |
| GET | /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}/references | List Monitor Group References |
| GET | /accounts/{account_id}/load_balancers/monitors | List Monitors |
| POST | /accounts/{account_id}/load_balancers/monitors | Create Monitor |
| DELETE | /accounts/{account_id}/load_balancers/monitors/{monitor_id} | Delete Monitor |
| GET | /accounts/{account_id}/load_balancers/monitors/{monitor_id} | Monitor Details |
| PATCH | /accounts/{account_id}/load_balancers/monitors/{monitor_id} | Patch Monitor |
| PUT | /accounts/{account_id}/load_balancers/monitors/{monitor_id} | Update Monitor |
| POST | /accounts/{account_id}/load_balancers/monitors/{monitor_id}/preview | Preview Monitor |
| GET | /accounts/{account_id}/load_balancers/monitors/{monitor_id}/references | List Monitor References |
| GET | /accounts/{account_id}/load_balancers/pools | List Pools |
| PATCH | /accounts/{account_id}/load_balancers/pools | Patch Pools |
| POST | /accounts/{account_id}/load_balancers/pools | Create Pool |
| DELETE | /accounts/{account_id}/load_balancers/pools/{pool_id} | Delete Pool |
| GET | /accounts/{account_id}/load_balancers/pools/{pool_id} | Pool Details |
| PATCH | /accounts/{account_id}/load_balancers/pools/{pool_id} | Patch Pool |
| PUT | /accounts/{account_id}/load_balancers/pools/{pool_id} | Update Pool |
| GET | /accounts/{account_id}/load_balancers/pools/{pool_id}/health | Pool Health Details |
| POST | /accounts/{account_id}/load_balancers/pools/{pool_id}/preview | Preview Pool |
| GET | /accounts/{account_id}/load_balancers/pools/{pool_id}/references | List Pool References |
| GET | /accounts/{account_id}/load_balancers/preview/{preview_id} | Preview Result |
| GET | /accounts/{account_id}/load_balancers/regions | List Regions |
| GET | /accounts/{account_id}/load_balancers/regions/{region_id} | Get Region |
| GET | /accounts/{account_id}/load_balancers/search | Search Resources |
| GET | /accounts/{account_id}/logpush/datasets/{dataset_id}/fields | List fields |
| GET | /accounts/{account_id}/logpush/datasets/{dataset_id}/jobs | List Logpush jobs for a dataset |
| GET | /accounts/{account_id}/logpush/jobs | List Logpush jobs |
| POST | /accounts/{account_id}/logpush/jobs | Create Logpush job |
| DELETE | /accounts/{account_id}/logpush/jobs/{job_id} | Delete Logpush job |
| GET | /accounts/{account_id}/logpush/jobs/{job_id} | Get Logpush job details |
| PUT | /accounts/{account_id}/logpush/jobs/{job_id} | Update Logpush job |
| POST | /accounts/{account_id}/logpush/ownership | Get ownership challenge |
| POST | /accounts/{account_id}/logpush/ownership/validate | Validate ownership challenge |
| POST | /accounts/{account_id}/logpush/validate/destination | Validate destination |
| POST | /accounts/{account_id}/logpush/validate/destination/exists | Check destination exists |
| POST | /accounts/{account_id}/logpush/validate/origin | Validate origin |
| GET | /accounts/{account_id}/logs/audit | Get account audit logs (Version 2, Beta release) |
| DELETE | /accounts/{account_id}/logs/control/cmb/config | Delete CMB config |
| GET | /accounts/{account_id}/logs/control/cmb/config | Get CMB config |
| POST | /accounts/{account_id}/logs/control/cmb/config | Update CMB config |
| DELETE | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules | Delete all DNS Protection rules. |
| GET | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules | List all DNS Protection rules. |
| POST | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules | Create DNS Protection rule. |
| DELETE | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id} | Delete DNS Protection rule. |
| GET | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id} | Get DNS Protection rule. |
| PATCH | /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id} | Update DNS Protection rule. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist | Delete all allowlist prefixes. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist | List all allowlist prefixes. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist | Create allowlist prefix. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id} | Delete allowlist prefix. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id} | Get allowlist prefix. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id} | Update allowlist prefix. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes | Delete all prefixes. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes | List all prefixes. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes | Create prefix. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/bulk | Create multiple prefixes. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id} | Delete prefix. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id} | Get prefix. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id} | Update prefix. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters | Delete all SYN Protection filters. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters | List all SYN Protection filters. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters | Create a SYN Protection filter. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id} | Delete SYN Protection filter. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id} | Get SYN Protection filter. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id} | Update SYN Protection filter. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules | Delete all SYN Protection rules. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules | List all SYN Protection rules. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules | Create SYN Protection rule. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id} | Delete SYN Protection rule. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id} | Get SYN Protection rule. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id} | Update SYN Protection rule. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters | Delete all TCP Flow Protection filters. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters | List all TCP Flow Protection filters. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters | Create a TCP Flow Protection filter. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id} | Delete TCP Flow Protection filter. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id} | Get TCP Flow Protection filter. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id} | Update TCP Flow Protection filter. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules | Delete all TCP Flow Protection rules. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules | List all TCP Flow Protection rules. |
| POST | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules | Create TCP Flow Protection rule. |
| DELETE | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id} | Delete TCP Flow Protection rule. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id} | Get TCP Flow Protection rule. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id} | Update TCP Flow Protection rule. |
| GET | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_protection_status | Get protection status. |
| PATCH | /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_protection_status | Update protection status. |
| GET | /accounts/{account_id}/magic/apps | List Apps |
| POST | /accounts/{account_id}/magic/apps | Create a new App |
| DELETE | /accounts/{account_id}/magic/apps/{account_app_id} | Delete Account App |
| PATCH | /accounts/{account_id}/magic/apps/{account_app_id} | Update an App |
| PUT | /accounts/{account_id}/magic/apps/{account_app_id} | Update an App |
| GET | /accounts/{account_id}/magic/cf_interconnects | List interconnects |
| PUT | /accounts/{account_id}/magic/cf_interconnects | Update multiple interconnects |
| GET | /accounts/{account_id}/magic/cf_interconnects/{cf_interconnect_id} | List interconnect Details |
| PUT | /accounts/{account_id}/magic/cf_interconnects/{cf_interconnect_id} | Update interconnect |
| GET | /accounts/{account_id}/magic/cloud/catalog-syncs | List Catalog Syncs |
| POST | /accounts/{account_id}/magic/cloud/catalog-syncs | Create Catalog Sync |
| GET | /accounts/{account_id}/magic/cloud/catalog-syncs/prebuilt-policies | List Prebuilt Policies |
| DELETE | /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id} | Delete Catalog Sync |
| GET | /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id} | Read Catalog Sync |
| PATCH | /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id} | Patch Catalog Sync |
| PUT | /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id} | Update Catalog Sync |
| POST | /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}/refresh | Run Catalog Sync |
| GET | /accounts/{account_id}/magic/cloud/onramps | List On-ramps |
| POST | /accounts/{account_id}/magic/cloud/onramps | Create On-ramp |
| GET | /accounts/{account_id}/magic/cloud/onramps/magic_wan_address_space | Read Magic WAN Address Space |
| PATCH | /accounts/{account_id}/magic/cloud/onramps/magic_wan_address_space | Patch Magic WAN Address Space |
| PUT | /accounts/{account_id}/magic/cloud/onramps/magic_wan_address_space | Update Magic WAN Address Space |
| DELETE | /accounts/{account_id}/magic/cloud/onramps/{onramp_id} | Delete On-ramp |
| GET | /accounts/{account_id}/magic/cloud/onramps/{onramp_id} | Read On-ramp |
| PATCH | /accounts/{account_id}/magic/cloud/onramps/{onramp_id} | Patch On-ramp |
| PUT | /accounts/{account_id}/magic/cloud/onramps/{onramp_id} | Update On-ramp |
| POST | /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/apply | Apply On-ramp |
| POST | /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/export | Export as Terraform |
| POST | /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/plan | Plan On-ramp |
| GET | /accounts/{account_id}/magic/cloud/providers | List Cloud Integrations |
| POST | /accounts/{account_id}/magic/cloud/providers | Create Cloud Integration |
| POST | /accounts/{account_id}/magic/cloud/providers/discover | Run Discovery for All Integrations |
| DELETE | /accounts/{account_id}/magic/cloud/providers/{provider_id} | Delete Cloud Integration |
| GET | /accounts/{account_id}/magic/cloud/providers/{provider_id} | Read Cloud Integration |
| PATCH | /accounts/{account_id}/magic/cloud/providers/{provider_id} | Patch Cloud Integration |
| PUT | /accounts/{account_id}/magic/cloud/providers/{provider_id} | Update Cloud Integration |
| POST | /accounts/{account_id}/magic/cloud/providers/{provider_id}/discover | Run Discovery |
| GET | /accounts/{account_id}/magic/cloud/providers/{provider_id}/initial_setup | Get Cloud Integration Setup Config |
| GET | /accounts/{account_id}/magic/cloud/resources | List Resources |
| GET | /accounts/{account_id}/magic/cloud/resources/export | Export Resources |
| POST | /accounts/{account_id}/magic/cloud/resources/policy-preview | Preview Rego Query |
| GET | /accounts/{account_id}/magic/cloud/resources/{resource_id} | Read Resource |
| GET | /accounts/{account_id}/magic/connectors | List Connectors |
| POST | /accounts/{account_id}/magic/connectors | Add a connector to your account |
| DELETE | /accounts/{account_id}/magic/connectors/{connector_id} | Remove a connector from your account |
| GET | /accounts/{account_id}/magic/connectors/{connector_id} | Fetch Connector |
| PATCH | /accounts/{account_id}/magic/connectors/{connector_id} | Edit Connector to update specific properties or Re-provision License Key |
| PUT | /accounts/{account_id}/magic/connectors/{connector_id} | Replace Connector or Re-provision License Key |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events | List Events |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events/latest | Get latest Events |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events/{event_t}.{event_n} | Get Event |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots | List Snapshots |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots/latest | Get latest Snapshots |
| GET | /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots/{snapshot_t} | Get Snapshot |
| GET | /accounts/{account_id}/magic/gre_tunnels | List GRE tunnels |
| POST | /accounts/{account_id}/magic/gre_tunnels | Create a GRE tunnel |
| PUT | /accounts/{account_id}/magic/gre_tunnels | Update multiple GRE tunnels |
| DELETE | /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id} | Delete GRE Tunnel |
| GET | /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id} | List GRE Tunnel Details |
| PUT | /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id} | Update GRE Tunnel |
| GET | /accounts/{account_id}/magic/ipsec_tunnels | List IPsec tunnels |
| POST | /accounts/{account_id}/magic/ipsec_tunnels | Create an IPsec tunnel |
| PUT | /accounts/{account_id}/magic/ipsec_tunnels | Update multiple IPsec tunnels |
| DELETE | /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id} | Delete IPsec Tunnel |
| GET | /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id} | List IPsec tunnel details |
| PUT | /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id} | Update IPsec Tunnel |
| POST | /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id}/psk_generate | Generate Pre Shared Key (PSK) for IPsec tunnels |
| DELETE | /accounts/{account_id}/magic/routes | Delete Many Routes |
| GET | /accounts/{account_id}/magic/routes | List Routes |
| POST | /accounts/{account_id}/magic/routes | Create a Route |
| PUT | /accounts/{account_id}/magic/routes | Update Many Routes |
| DELETE | /accounts/{account_id}/magic/routes/{route_id} | Delete Route |
| GET | /accounts/{account_id}/magic/routes/{route_id} | Route Details |
| PUT | /accounts/{account_id}/magic/routes/{route_id} | Update Route |
| GET | /accounts/{account_id}/magic/sites | List Sites |
| POST | /accounts/{account_id}/magic/sites | Create a new Site |
| DELETE | /accounts/{account_id}/magic/sites/{site_id} | Delete Site |
| GET | /accounts/{account_id}/magic/sites/{site_id} | Site Details |
| PATCH | /accounts/{account_id}/magic/sites/{site_id} | Patch Site |
| PUT | /accounts/{account_id}/magic/sites/{site_id} | Update Site |
| GET | /accounts/{account_id}/magic/sites/{site_id}/acls | List Site ACLs |
| POST | /accounts/{account_id}/magic/sites/{site_id}/acls | Create a new Site ACL |
| DELETE | /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id} | Delete Site ACL |
| GET | /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id} | Site ACL Details |
| PATCH | /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id} | Patch Site ACL |
| PUT | /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id} | Update Site ACL |
| GET | /accounts/{account_id}/magic/sites/{site_id}/app_configs | List App Configs |
| POST | /accounts/{account_id}/magic/sites/{site_id}/app_configs | Create a new App Config |
| DELETE | /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id} | Delete App Config |
| PATCH | /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id} | Update an App Config |
| PUT | /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id} | Update an App Config |
| GET | /accounts/{account_id}/magic/sites/{site_id}/lans | List Site LANs |
| POST | /accounts/{account_id}/magic/sites/{site_id}/lans | Create a new Site LAN |
| DELETE | /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id} | Delete Site LAN |
| GET | /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id} | Site LAN Details |
| PATCH | /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id} | Patch Site LAN |
| PUT | /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id} | Update Site LAN |
| DELETE | /accounts/{account_id}/magic/sites/{site_id}/netflow_config | Delete NetFlow Configuration |
| GET | /accounts/{account_id}/magic/sites/{site_id}/netflow_config | NetFlow Configuration Details |
| PATCH | /accounts/{account_id}/magic/sites/{site_id}/netflow_config | Update NetFlow Configuration |
| POST | /accounts/{account_id}/magic/sites/{site_id}/netflow_config | Create NetFlow Configuration |
| PUT | /accounts/{account_id}/magic/sites/{site_id}/netflow_config | Update NetFlow Configuration |
| GET | /accounts/{account_id}/magic/sites/{site_id}/wans | List Site WANs |
| POST | /accounts/{account_id}/magic/sites/{site_id}/wans | Create a new Site WAN |
| DELETE | /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id} | Delete Site WAN |
| GET | /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id} | Site WAN Details |
| PATCH | /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id} | Patch Site WAN |
| PUT | /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id} | Update Site WAN |
| GET | /accounts/{account_id}/members | List Members |
| POST | /accounts/{account_id}/members | Add Member |
| DELETE | /accounts/{account_id}/members/{member_id} | Remove Member |
| GET | /accounts/{account_id}/members/{member_id} | Member Details |
| PUT | /accounts/{account_id}/members/{member_id} | Update Member |
| DELETE | /accounts/{account_id}/mnm/config | Delete account configuration |
| GET | /accounts/{account_id}/mnm/config | List account configuration |
| PATCH | /accounts/{account_id}/mnm/config | Update account configuration fields |
| POST | /accounts/{account_id}/mnm/config | Create account configuration |
| PUT | /accounts/{account_id}/mnm/config | Update an entire account configuration |
| GET | /accounts/{account_id}/mnm/config/full | List rules and account configuration |
| GET | /accounts/{account_id}/mnm/rules | List rules |
| POST | /accounts/{account_id}/mnm/rules | Create rules |
| PUT | /accounts/{account_id}/mnm/rules | Update rules |
| DELETE | /accounts/{account_id}/mnm/rules/{rule_id} | Delete rule |
| GET | /accounts/{account_id}/mnm/rules/{rule_id} | Get rule |
| PATCH | /accounts/{account_id}/mnm/rules/{rule_id} | Update rule |
| PATCH | /accounts/{account_id}/mnm/rules/{rule_id}/advertisement | Update advertisement for rule |
| POST | /accounts/{account_id}/mnm/vpc-flows/token | Generate authentication token for VPC flow logs export. |
| POST | /accounts/{account_id}/move | Move account |
| GET | /accounts/{account_id}/mtls_certificates | List mTLS certificates |
| POST | /accounts/{account_id}/mtls_certificates | Upload mTLS certificate |
| DELETE | /accounts/{account_id}/mtls_certificates/{mtls_certificate_id} | Delete mTLS certificate |
| GET | /accounts/{account_id}/mtls_certificates/{mtls_certificate_id} | Get mTLS certificate |
| GET | /accounts/{account_id}/mtls_certificates/{mtls_certificate_id}/associations | List mTLS certificate associations |
| GET | /accounts/{account_id}/organizations | List account organizations |
| GET | /accounts/{account_id}/pages/projects | Get projects |
| POST | /accounts/{account_id}/pages/projects | Create project |
| DELETE | /accounts/{account_id}/pages/projects/{project_name} | Delete project |
| GET | /accounts/{account_id}/pages/projects/{project_name} | Get project |
| PATCH | /accounts/{account_id}/pages/projects/{project_name} | Update project |
| GET | /accounts/{account_id}/pages/projects/{project_name}/deployments | Get deployments |
| POST | /accounts/{account_id}/pages/projects/{project_name}/deployments | Create deployment |
| DELETE | /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id} | Delete deployment |
| GET | /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id} | Get deployment info |
| GET | /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/history/logs | Get deployment logs |
| POST | /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/retry | Retry deployment |
| POST | /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/rollback | Rollback deployment |
| GET | /accounts/{account_id}/pages/projects/{project_name}/domains | Get domains |
| POST | /accounts/{account_id}/pages/projects/{project_name}/domains | Add domain |
| DELETE | /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name} | Delete domain |
| GET | /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name} | Get domain |
| PATCH | /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name} | Patch domain |
| POST | /accounts/{account_id}/pages/projects/{project_name}/purge_build_cache | Purge build cache |
| DELETE | /accounts/{account_id}/pay-per-crawl/crawler/stripe | Deletes the stripe config for a crawler |
| GET | /accounts/{account_id}/pay-per-crawl/crawler/stripe | Gets the stripe config for a crawler |
| POST | /accounts/{account_id}/pay-per-crawl/crawler/stripe | Creates the stripe config for a crawler |
| DELETE | /accounts/{account_id}/pay-per-crawl/publisher/stripe | Deletes the stripe config for a publisher |
| GET | /accounts/{account_id}/pay-per-crawl/publisher/stripe | Gets the stripe config for a publisher |
| POST | /accounts/{account_id}/pay-per-crawl/publisher/stripe | Creates the stripe config for a publisher |
| PATCH | /accounts/{account_id}/pay-per-crawl/zones_can_be_enabled | Set can_be_enabled setting on zones |
| POST | /accounts/{account_id}/pay-per-crawl/zones_can_be_enabled/query | Gets the can_be_enabled zone setting |
| GET | /accounts/{account_id}/pcaps | List packet capture requests |
| POST | /accounts/{account_id}/pcaps | Create PCAP request |
| GET | /accounts/{account_id}/pcaps/ownership | List PCAPs Bucket Ownership |
| POST | /accounts/{account_id}/pcaps/ownership | Add buckets for full packet captures |
| POST | /accounts/{account_id}/pcaps/ownership/validate | Validate buckets for full packet captures |
| DELETE | /accounts/{account_id}/pcaps/ownership/{ownership_id} | Delete buckets for full packet captures |
| GET | /accounts/{account_id}/pcaps/{pcap_id} | Get PCAP request |
| GET | /accounts/{account_id}/pcaps/{pcap_id}/download | Download Simple PCAP |
| PUT | /accounts/{account_id}/pcaps/{pcap_id}/stop | Stop full PCAP |
| GET | /accounts/{account_id}/pipelines | [DEPRECATED] List Pipelines |
| POST | /accounts/{account_id}/pipelines | [DEPRECATED] Create Pipeline |
| GET | /accounts/{account_id}/pipelines/v1/pipelines | List Pipelines |
| POST | /accounts/{account_id}/pipelines/v1/pipelines | Create Pipeline |
| DELETE | /accounts/{account_id}/pipelines/v1/pipelines/{pipeline_id} | Delete Pipelines |
| GET | /accounts/{account_id}/pipelines/v1/pipelines/{pipeline_id} | Get Pipeline Details |
| GET | /accounts/{account_id}/pipelines/v1/sinks | List Sinks |
| POST | /accounts/{account_id}/pipelines/v1/sinks | Create Sink |
| DELETE | /accounts/{account_id}/pipelines/v1/sinks/{sink_id} | Delete Sink |
| GET | /accounts/{account_id}/pipelines/v1/sinks/{sink_id} | Get Sink Details |
| GET | /accounts/{account_id}/pipelines/v1/streams | List Streams |
| POST | /accounts/{account_id}/pipelines/v1/streams | Create Stream |
| DELETE | /accounts/{account_id}/pipelines/v1/streams/{stream_id} | Delete Stream |
| GET | /accounts/{account_id}/pipelines/v1/streams/{stream_id} | Get Stream Details |
| PATCH | /accounts/{account_id}/pipelines/v1/streams/{stream_id} | Update Stream |
| POST | /accounts/{account_id}/pipelines/v1/validate_sql | Validate SQL |
| DELETE | /accounts/{account_id}/pipelines/{pipeline_name} | [DEPRECATED] Delete Pipeline |
| GET | /accounts/{account_id}/pipelines/{pipeline_name} | [DEPRECATED] Get Pipeline |
| PUT | /accounts/{account_id}/pipelines/{pipeline_name} | [DEPRECATED] Update Pipeline |
| GET | /accounts/{account_id}/profile | Get account profile |
| PUT | /accounts/{account_id}/profile | Modify account profile |
| GET | /accounts/{account_id}/queues | List Queues |
| POST | /accounts/{account_id}/queues | Create Queue |
| DELETE | /accounts/{account_id}/queues/{queue_id} | Delete Queue |
| GET | /accounts/{account_id}/queues/{queue_id} | Get Queue |
| PATCH | /accounts/{account_id}/queues/{queue_id} | Update Queue |
| PUT | /accounts/{account_id}/queues/{queue_id} | Update Queue |
| GET | /accounts/{account_id}/queues/{queue_id}/consumers | List Queue Consumers |
| POST | /accounts/{account_id}/queues/{queue_id}/consumers | Create a Queue Consumer |
| DELETE | /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id} | Delete Queue Consumer |
| GET | /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id} | Get Queue Consumer |
| PUT | /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id} | Update Queue Consumer |
| POST | /accounts/{account_id}/queues/{queue_id}/messages | Push Message |
| POST | /accounts/{account_id}/queues/{queue_id}/messages/ack | Acknowledge + Retry Queue Messages |
| POST | /accounts/{account_id}/queues/{queue_id}/messages/batch | Push Message Batch |
| POST | /accounts/{account_id}/queues/{queue_id}/messages/pull | Pull Queue Messages |
| GET | /accounts/{account_id}/queues/{queue_id}/purge | Get Queue Purge Status |
| POST | /accounts/{account_id}/queues/{queue_id}/purge | Purge Queue |
| GET | /accounts/{account_id}/r2-catalog | List R2 catalogs |
| GET | /accounts/{account_id}/r2-catalog/{bucket_name} | Get R2 catalog details |
| POST | /accounts/{account_id}/r2-catalog/{bucket_name}/credential | Store catalog credentials |
| POST | /accounts/{account_id}/r2-catalog/{bucket_name}/disable | Disable R2 catalog |
| POST | /accounts/{account_id}/r2-catalog/{bucket_name}/enable | Enable R2 bucket as a catalog |
| GET | /accounts/{account_id}/r2-catalog/{bucket_name}/maintenance-configs | Get catalog maintenance configuration |
| POST | /accounts/{account_id}/r2-catalog/{bucket_name}/maintenance-configs | Update catalog maintenance configuration |
| GET | /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces | List namespaces in catalog |
| GET | /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables | List tables in namespace |
| GET | /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables/{table_name}/maintenance-configs | Get table maintenance configuration |
| POST | /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables/{table_name}/maintenance-configs | Update table maintenance configuration |
| GET | /accounts/{account_id}/r2/buckets | List Buckets |
| POST | /accounts/{account_id}/r2/buckets | Create Bucket |
| DELETE | /accounts/{account_id}/r2/buckets/{bucket_name} | Delete Bucket |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name} | Get Bucket |
| PATCH | /accounts/{account_id}/r2/buckets/{bucket_name} | Patch Bucket |
| DELETE | /accounts/{account_id}/r2/buckets/{bucket_name}/cors | Delete Bucket CORS Policy |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/cors | Get Bucket CORS Policy |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/cors | Put Bucket CORS Policy |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom | List Custom Domains of Bucket |
| POST | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom | Attach Custom Domain To Bucket |
| DELETE | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain} | Remove Custom Domain From Bucket |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain} | Get Custom Domain Settings |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain} | Configure Custom Domain Settings |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/managed | Get r2.dev Domain of Bucket |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/domains/managed | Update r2.dev Domain of Bucket |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/lifecycle | Get Object Lifecycle Rules |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/lifecycle | Put Object Lifecycle Rules |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/local-uploads | Get Local Uploads Configuration |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/local-uploads | Put Local Uploads Configuration |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/lock | Get Bucket Lock Rules |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/lock | Put Bucket Lock Rules |
| DELETE | /accounts/{account_id}/r2/buckets/{bucket_name}/sippy | Disable Sippy |
| GET | /accounts/{account_id}/r2/buckets/{bucket_name}/sippy | Get Sippy Configuration |
| PUT | /accounts/{account_id}/r2/buckets/{bucket_name}/sippy | Enable Sippy |
| GET | /accounts/{account_id}/r2/metrics | Get Account-Level Metrics |
| POST | /accounts/{account_id}/r2/temp-access-credentials | Create Temporary Access Credentials |
| GET | /accounts/{account_id}/realtime/kit/apps | Fetch all apps |
| POST | /accounts/{account_id}/realtime/kit/apps | Create App |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/analytics/daywise | Fetch day-wise session and recording analytics data for an App |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/analytics/livestreams/overall | Fetch complete analytics data for your livestreams |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/livestreams | Fetch all livestreams |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/livestreams | Create an independent livestream |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/livestreams/sessions/{livestream-session-id} | Fetch livestream session details using livestream session ID |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/livestreams/{livestream_id} | Fetch livestream details using livestream ID |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/livestreams/{livestream_id}/active-livestream-session | Fetch active livestream session details |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings | Fetch all meetings for an App |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings | Create a meeting |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id} | Fetch a meeting for an App |
| PATCH | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id} | Update a meeting |
| PUT | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id} | Replace a meeting |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-livestream | Fetch active livestreams for a meeting |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-livestream/stop | Stop livestreaming a meeting |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session | Fetch details of an active session |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/kick | Kick participants from an active session |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/kick-all | Kick all participants |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/mute | Mute participants of an active session |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/mute-all | Mute all participants |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/poll | Create a poll |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/livestream | Fetch livestream session details for a meeting |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/livestreams | Start livestreaming a meeting |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants | Fetch all participants of a meeting |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants | Add a participant |
| DELETE | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id} | Delete a participant |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id} | Fetch a participant's detail |
| PATCH | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id} | Edit a participant's detail |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id}/token | Refresh participant's authentication token |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/presets | Fetch all presets |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/presets | Create a preset |
| DELETE | /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id} | Delete a preset |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id} | Fetch details of a preset |
| PATCH | /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id} | Update a preset |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/recordings | Fetch all recordings for an App |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/recordings | Start recording a meeting |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/recordings/active-recording/{meeting_id} | Fetch active recording |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/recordings/track | Start recording audio and video tracks |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/recordings/{recording_id} | Fetch details of a recording |
| PUT | /accounts/{account_id}/realtime/kit/{app_id}/recordings/{recording_id} | Pause/Resume/Stop recording |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions | Fetch all sessions of an App |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/peer-report/{peer_id} | Fetch details of peer |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id} | Fetch details of a session |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/chat | Fetch all chat messages of a session |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/livestream-sessions | Fetch livestream session details using a session ID |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/participants | Fetch participants list of a session |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/participants/{participant_id} | Fetch details of a participant |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/summary | Fetch summary of transcripts for a session |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/summary | Generate summary of Transcripts for the session |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/transcript | Fetch the complete transcript for a session |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/webhooks | Fetch all webhooks details |
| POST | /accounts/{account_id}/realtime/kit/{app_id}/webhooks | Add a webhook |
| DELETE | /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id} | Delete a webhook |
| GET | /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id} | Fetch details of a webhook |
| PATCH | /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id} | Edit a webhook |
| PUT | /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id} | Replace a webhook |
| GET | /accounts/{account_id}/registrar/domains | List domains |
| GET | /accounts/{account_id}/registrar/domains/{domain_name} | Get domain |
| PUT | /accounts/{account_id}/registrar/domains/{domain_name} | Update domain |
| POST | /accounts/{account_id}/request-tracer/trace | Request Trace |
| GET | /accounts/{account_id}/roles | List Roles |
| GET | /accounts/{account_id}/roles/{role_id} | Role Details |
| GET | /accounts/{account_id}/rules/lists | Get lists |
| POST | /accounts/{account_id}/rules/lists | Create a list |
| GET | /accounts/{account_id}/rules/lists/bulk_operations/{operation_id} | Get bulk operation status |
| DELETE | /accounts/{account_id}/rules/lists/{list_id} | Delete a list |
| GET | /accounts/{account_id}/rules/lists/{list_id} | Get a list |
| PUT | /accounts/{account_id}/rules/lists/{list_id} | Update a list |
| DELETE | /accounts/{account_id}/rules/lists/{list_id}/items | Delete list items |
| GET | /accounts/{account_id}/rules/lists/{list_id}/items | Get list items |
| POST | /accounts/{account_id}/rules/lists/{list_id}/items | Create list items |
| PUT | /accounts/{account_id}/rules/lists/{list_id}/items | Update all list items |
| GET | /accounts/{account_id}/rules/lists/{list_id}/items/{item_id} | Get a list item |
| GET | /accounts/{account_id}/rulesets | List account rulesets |
| POST | /accounts/{account_id}/rulesets | Create an account ruleset |
| GET | /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint | Get an account entry point ruleset |
| PUT | /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint | Update an account entry point ruleset |
| GET | /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions | List an account entry point ruleset's versions |
| GET | /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions/{ruleset_version} | Get an account entry point ruleset version |
| DELETE | /accounts/{account_id}/rulesets/{ruleset_id} | Delete an account ruleset |
| GET | /accounts/{account_id}/rulesets/{ruleset_id} | Get an account ruleset |
| PUT | /accounts/{account_id}/rulesets/{ruleset_id} | Update an account ruleset |
| POST | /accounts/{account_id}/rulesets/{ruleset_id}/rules | Create an account ruleset rule |
| DELETE | /accounts/{account_id}/rulesets/{ruleset_id}/rules/{rule_id} | Delete an account ruleset rule |
| PATCH | /accounts/{account_id}/rulesets/{ruleset_id}/rules/{rule_id} | Update an account ruleset rule |
| GET | /accounts/{account_id}/rulesets/{ruleset_id}/versions | List an account ruleset's versions |
| DELETE | /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version} | Delete an account ruleset version |
| GET | /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version} | Get an account ruleset version |
| GET | /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version}/by_tag/{rule_tag} | List an account ruleset version's rules by tag |
| POST | /accounts/{account_id}/rum/site_info | Create a Web Analytics site |
| GET | /accounts/{account_id}/rum/site_info/list | List Web Analytics sites |
| DELETE | /accounts/{account_id}/rum/site_info/{site_id} | Delete a Web Analytics site |
| GET | /accounts/{account_id}/rum/site_info/{site_id} | Get a Web Analytics site |
| PUT | /accounts/{account_id}/rum/site_info/{site_id} | Update a Web Analytics site |
| POST | /accounts/{account_id}/rum/v2/{ruleset_id}/rule | Create a Web Analytics rule |
| DELETE | /accounts/{account_id}/rum/v2/{ruleset_id}/rule/{rule_id} | Delete a Web Analytics rule |
| PUT | /accounts/{account_id}/rum/v2/{ruleset_id}/rule/{rule_id} | Update a Web Analytics rule |
| GET | /accounts/{account_id}/rum/v2/{ruleset_id}/rules | List rules in Web Analytics ruleset |
| POST | /accounts/{account_id}/rum/v2/{ruleset_id}/rules | Update Web Analytics rules |
| GET | /accounts/{account_id}/secondary_dns/acls | List ACLs |
| POST | /accounts/{account_id}/secondary_dns/acls | Create ACL |
| DELETE | /accounts/{account_id}/secondary_dns/acls/{acl_id} | Delete ACL |
| GET | /accounts/{account_id}/secondary_dns/acls/{acl_id} | ACL Details |
| PUT | /accounts/{account_id}/secondary_dns/acls/{acl_id} | Update ACL |
| GET | /accounts/{account_id}/secondary_dns/peers | List Peers |
| POST | /accounts/{account_id}/secondary_dns/peers | Create Peer |
| DELETE | /accounts/{account_id}/secondary_dns/peers/{peer_id} | Delete Peer |
| GET | /accounts/{account_id}/secondary_dns/peers/{peer_id} | Peer Details |
| PUT | /accounts/{account_id}/secondary_dns/peers/{peer_id} | Update Peer |
| GET | /accounts/{account_id}/secondary_dns/tsigs | List TSIGs |
| POST | /accounts/{account_id}/secondary_dns/tsigs | Create TSIG |
| DELETE | /accounts/{account_id}/secondary_dns/tsigs/{tsig_id} | Delete TSIG |
| GET | /accounts/{account_id}/secondary_dns/tsigs/{tsig_id} | TSIG Details |
| PUT | /accounts/{account_id}/secondary_dns/tsigs/{tsig_id} | Update TSIG |
| GET | /accounts/{account_id}/secrets_store/quota | View secret usage |
| GET | /accounts/{account_id}/secrets_store/stores | List account stores |
| POST | /accounts/{account_id}/secrets_store/stores | Create a store |
| DELETE | /accounts/{account_id}/secrets_store/stores/{store_id} | Delete a store |
| DELETE | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets | Delete secrets |
| GET | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets | List store secrets |
| POST | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets | Create a secret |
| DELETE | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id} | Delete a secret |
| GET | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id} | Get a secret by ID |
| PATCH | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id} | Patch a secret |
| POST | /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id}/duplicate | Duplicate Secret |
| GET | /accounts/{account_id}/security-center/insights | Retrieves Security Center Insights |
| GET | /accounts/{account_id}/security-center/insights/class | Retrieves Security Center Insight Counts by Class |
| GET | /accounts/{account_id}/security-center/insights/severity | Retrieves Security Center Insight Counts by Severity |
| GET | /accounts/{account_id}/security-center/insights/type | Retrieves Security Center Insight Counts by Type |
| PUT | /accounts/{account_id}/security-center/insights/{issue_id}/dismiss | Archives Security Center Insight |
| GET | /accounts/{account_id}/shares | List account shares |
| POST | /accounts/{account_id}/shares | Create a new share |
| DELETE | /accounts/{account_id}/shares/{share_id} | Delete a share |
| GET | /accounts/{account_id}/shares/{share_id} | Get account share by ID |
| PUT | /accounts/{account_id}/shares/{share_id} | Update a share |
| GET | /accounts/{account_id}/shares/{share_id}/recipients | List share recipients by share ID |
| POST | /accounts/{account_id}/shares/{share_id}/recipients | Create a new share recipient |
| PUT | /accounts/{account_id}/shares/{share_id}/recipients | Update a share's recipients |
| DELETE | /accounts/{account_id}/shares/{share_id}/recipients/{recipient_id} | Delete a share recipient |
| GET | /accounts/{account_id}/shares/{share_id}/recipients/{recipient_id} | Get share recipient by ID |
| GET | /accounts/{account_id}/shares/{share_id}/resources | List share resources by share ID |
| POST | /accounts/{account_id}/shares/{share_id}/resources | Create a new share resource |
| DELETE | /accounts/{account_id}/shares/{share_id}/resources/{resource_id} | Delete a share resource |
| GET | /accounts/{account_id}/shares/{share_id}/resources/{resource_id} | Get share resource by ID |
| PUT | /accounts/{account_id}/shares/{share_id}/resources/{resource_id} | Update a share resource |
| GET | /accounts/{account_id}/slurper/jobs | List jobs |
| POST | /accounts/{account_id}/slurper/jobs | Create a job |
| PUT | /accounts/{account_id}/slurper/jobs/abortAll | Abort all jobs |
| GET | /accounts/{account_id}/slurper/jobs/{job_id} | Get job details |
| PUT | /accounts/{account_id}/slurper/jobs/{job_id}/abort | Abort a job |
| GET | /accounts/{account_id}/slurper/jobs/{job_id}/logs | Get job logs |
| PUT | /accounts/{account_id}/slurper/jobs/{job_id}/pause | Pause a job |
| GET | /accounts/{account_id}/slurper/jobs/{job_id}/progress | Get job progress |
| PUT | /accounts/{account_id}/slurper/jobs/{job_id}/resume | Resume a job |
| PUT | /accounts/{account_id}/slurper/source/connectivity-precheck | Check source connectivity |
| PUT | /accounts/{account_id}/slurper/target/connectivity-precheck | Check target connectivity |
| GET | /accounts/{account_id}/sso_connectors | Get all SSO connectors |
| POST | /accounts/{account_id}/sso_connectors | Initialize new SSO connector |
| DELETE | /accounts/{account_id}/sso_connectors/{sso_connector_id} | Delete SSO connector |
| GET | /accounts/{account_id}/sso_connectors/{sso_connector_id} | Get single SSO connector |
| PATCH | /accounts/{account_id}/sso_connectors/{sso_connector_id} | Update SSO connector state |
| POST | /accounts/{account_id}/sso_connectors/{sso_connector_id}/begin_verification | Begin SSO connector verification |
| GET | /accounts/{account_id}/storage/kv/namespaces | List Namespaces |
| POST | /accounts/{account_id}/storage/kv/namespaces | Create a Namespace |
| DELETE | /accounts/{account_id}/storage/kv/namespaces/{namespace_id} | Remove a Namespace |
| GET | /accounts/{account_id}/storage/kv/namespaces/{namespace_id} | Get a Namespace |
| PUT | /accounts/{account_id}/storage/kv/namespaces/{namespace_id} | Rename a Namespace |
| DELETE | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk | Delete multiple key-value pairs |
| PUT | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk | Write multiple key-value pairs |
| POST | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk/delete | Delete multiple key-value pairs |
| POST | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk/get | Get multiple key-value pairs |
| GET | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/keys | List a Namespace's Keys |
| GET | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/metadata/{key_name} | Read the metadata for a key |
| DELETE | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name} | Delete key-value pair |
| GET | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name} | Read key-value pair |
| PUT | /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name} | Write key-value pair with optional metadata |
| GET | /accounts/{account_id}/stream | List videos |
| POST | /accounts/{account_id}/stream | Initiate video uploads using TUS |
| POST | /accounts/{account_id}/stream/clip | Clip videos given a start and end time |
| POST | /accounts/{account_id}/stream/copy | Upload videos from a URL |
| POST | /accounts/{account_id}/stream/direct_upload | Upload videos via direct upload URLs |
| GET | /accounts/{account_id}/stream/keys | List signing keys |
| POST | /accounts/{account_id}/stream/keys | Create signing keys |
| DELETE | /accounts/{account_id}/stream/keys/{identifier} | Delete signing keys |
| GET | /accounts/{account_id}/stream/live_inputs | List live inputs |
| POST | /accounts/{account_id}/stream/live_inputs | Create a live input |
| DELETE | /accounts/{account_id}/stream/live_inputs/{live_input_identifier} | Delete a live input |
| GET | /accounts/{account_id}/stream/live_inputs/{live_input_identifier} | Retrieve a live input |
| PUT | /accounts/{account_id}/stream/live_inputs/{live_input_identifier} | Update a live input |
| POST | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/disable | Disable a live input |
| POST | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/enable | Enable a live input |
| GET | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs | List all outputs associated with a specified live input |
| POST | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs | Create a new output, connected to a live input |
| DELETE | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs/{output_identifier} | Delete an output |
| PUT | /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs/{output_identifier} | Update an output |
| GET | /accounts/{account_id}/stream/storage-usage | Storage use |
| GET | /accounts/{account_id}/stream/watermarks | List watermark profiles |
| POST | /accounts/{account_id}/stream/watermarks | Create watermark profiles via basic upload |
| DELETE | /accounts/{account_id}/stream/watermarks/{identifier} | Delete watermark profiles |
| GET | /accounts/{account_id}/stream/watermarks/{identifier} | Watermark profile details |
| DELETE | /accounts/{account_id}/stream/webhook | Delete webhooks |
| GET | /accounts/{account_id}/stream/webhook | View webhooks |
| PUT | /accounts/{account_id}/stream/webhook | Create webhooks |
| DELETE | /accounts/{account_id}/stream/{identifier} | Delete video |
| GET | /accounts/{account_id}/stream/{identifier} | Retrieve video details |
| POST | /accounts/{account_id}/stream/{identifier} | Edit video details |
| GET | /accounts/{account_id}/stream/{identifier}/audio | List additional audio tracks on a video |
| POST | /accounts/{account_id}/stream/{identifier}/audio/copy | Add audio tracks to a video |
| DELETE | /accounts/{account_id}/stream/{identifier}/audio/{audio_identifier} | Delete additional audio tracks on a video |
| PATCH | /accounts/{account_id}/stream/{identifier}/audio/{audio_identifier} | Edit additional audio tracks on a video |
| GET | /accounts/{account_id}/stream/{identifier}/captions | List captions or subtitles |
| DELETE | /accounts/{account_id}/stream/{identifier}/captions/{language} | Delete captions or subtitles |
| GET | /accounts/{account_id}/stream/{identifier}/captions/{language} | List captions or subtitles for a provided language |
| PUT | /accounts/{account_id}/stream/{identifier}/captions/{language} | Upload captions or subtitles |
| POST | /accounts/{account_id}/stream/{identifier}/captions/{language}/generate | Generate captions or subtitles for a provided language via AI |
| GET | /accounts/{account_id}/stream/{identifier}/captions/{language}/vtt | Return WebVTT captions for a provided language |
| DELETE | /accounts/{account_id}/stream/{identifier}/downloads | Delete downloads |
| GET | /accounts/{account_id}/stream/{identifier}/downloads | List downloads |
| POST | /accounts/{account_id}/stream/{identifier}/downloads | Create downloads |
| DELETE | /accounts/{account_id}/stream/{identifier}/downloads/{download_type} | Delete download |
| POST | /accounts/{account_id}/stream/{identifier}/downloads/{download_type} | Create download |
| GET | /accounts/{account_id}/stream/{identifier}/embed | Retrieve embed Code HTML |
| POST | /accounts/{account_id}/stream/{identifier}/token | Create signed URL tokens for videos |
| GET | /accounts/{account_id}/subscriptions | List Subscriptions |
| POST | /accounts/{account_id}/subscriptions | Create Subscription |
| DELETE | /accounts/{account_id}/subscriptions/{subscription_identifier} | Delete Subscription |
| PUT | /accounts/{account_id}/subscriptions/{subscription_identifier} | Update Subscription |
| GET | /accounts/{account_id}/teamnet/routes | List tunnel routes |
| POST | /accounts/{account_id}/teamnet/routes | Create a tunnel route |
| GET | /accounts/{account_id}/teamnet/routes/ip/{ip} | Get tunnel route by IP |
| DELETE | /accounts/{account_id}/teamnet/routes/network/{ip_network_encoded} | Delete a tunnel route (CIDR Endpoint) |
| PATCH | /accounts/{account_id}/teamnet/routes/network/{ip_network_encoded} | Update a tunnel route (CIDR Endpoint) |
| POST | /accounts/{account_id}/teamnet/routes/network/{ip_network_encoded} | Create a tunnel route (CIDR Endpoint) |
| DELETE | /accounts/{account_id}/teamnet/routes/{route_id} | Delete a tunnel route |
| GET | /accounts/{account_id}/teamnet/routes/{route_id} | Get tunnel route |
| PATCH | /accounts/{account_id}/teamnet/routes/{route_id} | Update a tunnel route |
| GET | /accounts/{account_id}/teamnet/virtual_networks | List virtual networks |
| POST | /accounts/{account_id}/teamnet/virtual_networks | Create a virtual network |
| DELETE | /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id} | Delete a virtual network |
| GET | /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id} | Get a virtual network |
| PATCH | /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id} | Update a virtual network |
| GET | /accounts/{account_id}/tokens | List Tokens |
| POST | /accounts/{account_id}/tokens | Create Token |
| GET | /accounts/{account_id}/tokens/permission_groups | List Permission Groups |
| GET | /accounts/{account_id}/tokens/verify | Verify Token |
| DELETE | /accounts/{account_id}/tokens/{token_id} | Delete Token |
| GET | /accounts/{account_id}/tokens/{token_id} | Token Details |
| PUT | /accounts/{account_id}/tokens/{token_id} | Update Token |
| PUT | /accounts/{account_id}/tokens/{token_id}/value | Roll Token |
| GET | /accounts/{account_id}/tunnels | List All Tunnels |
| GET | /accounts/{account_id}/urlscanner/response/{response_id} | Get raw response |
| GET | /accounts/{account_id}/urlscanner/scan | Search URL scans |
| POST | /accounts/{account_id}/urlscanner/scan | Create URL Scan |
| GET | /accounts/{account_id}/urlscanner/scan/{scan_id} | Get URL scan |
| GET | /accounts/{account_id}/urlscanner/scan/{scan_id}/har | Get URL scan's HAR |
| GET | /accounts/{account_id}/urlscanner/scan/{scan_id}/screenshot | Get screenshot |
| POST | /accounts/{account_id}/urlscanner/v2/bulk | Bulk create URL Scans |
| GET | /accounts/{account_id}/urlscanner/v2/dom/{scan_id} | Get URL scan's DOM |
| GET | /accounts/{account_id}/urlscanner/v2/har/{scan_id} | Get URL scan's HAR |
| GET | /accounts/{account_id}/urlscanner/v2/responses/{response_id} | Get raw response |
| GET | /accounts/{account_id}/urlscanner/v2/result/{scan_id} | Get URL scan |
| POST | /accounts/{account_id}/urlscanner/v2/scan | Create URL Scan |
| GET | /accounts/{account_id}/urlscanner/v2/screenshots/{scan_id}.png | Get screenshot |
| GET | /accounts/{account_id}/urlscanner/v2/search | Search URL scans |
| GET | /accounts/{account_id}/vectorize/indexes | List Vectorize Indexes (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes | Create Vectorize Index (Deprecated) |
| DELETE | /accounts/{account_id}/vectorize/indexes/{index_name} | Delete Vectorize Index (Deprecated) |
| GET | /accounts/{account_id}/vectorize/indexes/{index_name} | Get Vectorize Index (Deprecated) |
| PUT | /accounts/{account_id}/vectorize/indexes/{index_name} | Update Vectorize Index (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes/{index_name}/delete-by-ids | Delete Vectors By Identifier (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes/{index_name}/get-by-ids | Get Vectors By Identifier (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes/{index_name}/insert | Insert Vectors (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes/{index_name}/query | Query Vectors (Deprecated) |
| POST | /accounts/{account_id}/vectorize/indexes/{index_name}/upsert | Upsert Vectors (Deprecated) |
| GET | /accounts/{account_id}/vectorize/v2/indexes | List Vectorize Indexes |
| POST | /accounts/{account_id}/vectorize/v2/indexes | Create Vectorize Index |
| DELETE | /accounts/{account_id}/vectorize/v2/indexes/{index_name} | Delete Vectorize Index |
| GET | /accounts/{account_id}/vectorize/v2/indexes/{index_name} | Get Vectorize Index |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/delete_by_ids | Delete Vectors By Identifier |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/get_by_ids | Get Vectors By Identifier |
| GET | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/info | Get Vectorize Index Info |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/insert | Insert Vectors |
| GET | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/list | List Vectors |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/create | Create Metadata Index |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/delete | Delete Metadata Index |
| GET | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/list | List Metadata Indexes |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/query | Query Vectors |
| POST | /accounts/{account_id}/vectorize/v2/indexes/{index_name}/upsert | Upsert Vectors |
| GET | /accounts/{account_id}/waiting_rooms | List waiting rooms for account |
| GET | /accounts/{account_id}/warp_connector | List Warp Connector Tunnels |
| POST | /accounts/{account_id}/warp_connector | Create a Warp Connector Tunnel |
| DELETE | /accounts/{account_id}/warp_connector/{tunnel_id} | Delete a Warp Connector Tunnel |
| GET | /accounts/{account_id}/warp_connector/{tunnel_id} | Get a Warp Connector Tunnel |
| PATCH | /accounts/{account_id}/warp_connector/{tunnel_id} | Update a Warp Connector Tunnel |
| GET | /accounts/{account_id}/warp_connector/{tunnel_id}/token | Get a Warp Connector Tunnel token |
| GET | /accounts/{account_id}/workers/account-settings | Fetch Worker Account Settings |
| PUT | /accounts/{account_id}/workers/account-settings | Create Worker Account Settings |
| POST | /accounts/{account_id}/workers/assets/upload | Upload Assets |
| GET | /accounts/{account_id}/workers/dispatch/namespaces | List dispatch namespaces |
| POST | /accounts/{account_id}/workers/dispatch/namespaces | Create dispatch namespace |
| DELETE | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace} | Delete dispatch namespace |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace} | Get dispatch namespace |
| PATCH | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace} | Patch dispatch namespace |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace} | Update dispatch namespace |
| DELETE | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts | Delete Scripts in Namespace |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts | List Scripts in Namespace |
| DELETE | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name} | Delete Worker |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name} | Worker Details |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name} | Upload Worker Module |
| POST | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/assets-upload-session | Create Assets Upload Session |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/bindings | Get Script Bindings |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/content | Get Script Content |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/content | Put Script Content |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets | List Script Secrets |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets | Add script secret |
| DELETE | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets/{secret_name} | Delete script secret |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets/{secret_name} | Get secret binding |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/settings | Get Script Settings |
| PATCH | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/settings | Patch Script Settings |
| GET | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags | Get Script Tags |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags | Put Script Tags |
| DELETE | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags/{tag} | Delete Script Tag |
| PUT | /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags/{tag} | Put Script Tag |
| GET | /accounts/{account_id}/workers/domains | List Domains |
| PUT | /accounts/{account_id}/workers/domains | Attach to Domain |
| DELETE | /accounts/{account_id}/workers/domains/{domain_id} | Detach from Domain |
| GET | /accounts/{account_id}/workers/domains/{domain_id} | Get a Domain |
| GET | /accounts/{account_id}/workers/durable_objects/namespaces | List Namespaces |
| GET | /accounts/{account_id}/workers/durable_objects/namespaces/{id}/objects | List Objects |
| GET | /accounts/{account_id}/workers/observability/destinations | Get Destinations |
| POST | /accounts/{account_id}/workers/observability/destinations | Create Destination |
| DELETE | /accounts/{account_id}/workers/observability/destinations/{slug} | Delete Destination |
| PATCH | /accounts/{account_id}/workers/observability/destinations/{slug} | Update Destination |
| POST | /accounts/{account_id}/workers/observability/telemetry/keys | List keys |
| POST | /accounts/{account_id}/workers/observability/telemetry/query | Run a query |
| POST | /accounts/{account_id}/workers/observability/telemetry/values | List values |
| GET | /accounts/{account_id}/workers/placement/regions | List Placement Regions |
| GET | /accounts/{account_id}/workers/scripts | List Workers |
| GET | /accounts/{account_id}/workers/scripts-search | Search Workers |
| DELETE | /accounts/{account_id}/workers/scripts/{script_name} | Delete Worker |
| GET | /accounts/{account_id}/workers/scripts/{script_name} | Download Worker |
| PUT | /accounts/{account_id}/workers/scripts/{script_name} | Upload Worker Module |
| POST | /accounts/{account_id}/workers/scripts/{script_name}/assets-upload-session | Create Assets Upload Session |
| PUT | /accounts/{account_id}/workers/scripts/{script_name}/content | Put script content |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/content/v2 | Get script content |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/deployments | List Deployments |
| POST | /accounts/{account_id}/workers/scripts/{script_name}/deployments | Create Deployment |
| DELETE | /accounts/{account_id}/workers/scripts/{script_name}/deployments/{deployment_id} | Delete Deployment |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/deployments/{deployment_id} | Get Deployment |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/schedules | Get Cron Triggers |
| PUT | /accounts/{account_id}/workers/scripts/{script_name}/schedules | Update Cron Triggers |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/script-settings | Get Script Settings |
| PATCH | /accounts/{account_id}/workers/scripts/{script_name}/script-settings | Patch Script Settings |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/secrets | List script secrets |
| PUT | /accounts/{account_id}/workers/scripts/{script_name}/secrets | Add script secret |
| DELETE | /accounts/{account_id}/workers/scripts/{script_name}/secrets/{secret_name} | Delete script secret |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/secrets/{secret_name} | Get secret binding |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/settings | Get Settings |
| PATCH | /accounts/{account_id}/workers/scripts/{script_name}/settings | Patch Settings |
| DELETE | /accounts/{account_id}/workers/scripts/{script_name}/subdomain | Delete Worker subdomain |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/subdomain | Get Worker subdomain |
| POST | /accounts/{account_id}/workers/scripts/{script_name}/subdomain | Post Worker subdomain |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/tails | List Tails |
| POST | /accounts/{account_id}/workers/scripts/{script_name}/tails | Start Tail |
| DELETE | /accounts/{account_id}/workers/scripts/{script_name}/tails/{id} | Delete Tail |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/usage-model | Fetch Usage Model |
| PUT | /accounts/{account_id}/workers/scripts/{script_name}/usage-model | Update Usage Model |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/versions | List Versions |
| POST | /accounts/{account_id}/workers/scripts/{script_name}/versions | Upload Version |
| GET | /accounts/{account_id}/workers/scripts/{script_name}/versions/{version_id} | Get Version Detail |
| GET | /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/content | Get script content |
| PUT | /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/content | Put script content |
| GET | /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/settings | Get Script Settings |
| PATCH | /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/settings | Patch Script Settings |
| DELETE | /accounts/{account_id}/workers/subdomain | Delete Subdomain |
| GET | /accounts/{account_id}/workers/subdomain | Get Subdomain |
| PUT | /accounts/{account_id}/workers/subdomain | Create Subdomain |
| GET | /accounts/{account_id}/workers/workers | List Workers |
| POST | /accounts/{account_id}/workers/workers | Create Worker |
| DELETE | /accounts/{account_id}/workers/workers/{worker_id} | Delete Worker |
| GET | /accounts/{account_id}/workers/workers/{worker_id} | Get Worker |
| PATCH | /accounts/{account_id}/workers/workers/{worker_id} | Edit Worker |
| PUT | /accounts/{account_id}/workers/workers/{worker_id} | Update Worker |
| GET | /accounts/{account_id}/workers/workers/{worker_id}/versions | List Versions |
| POST | /accounts/{account_id}/workers/workers/{worker_id}/versions | Create Version |
| DELETE | /accounts/{account_id}/workers/workers/{worker_id}/versions/{version_id} | Delete Version |
| GET | /accounts/{account_id}/workers/workers/{worker_id}/versions/{version_id} | Get Version |
| GET | /accounts/{account_id}/workflows | List all Workflows |
| DELETE | /accounts/{account_id}/workflows/{workflow_name} | Deletes a Workflow |
| GET | /accounts/{account_id}/workflows/{workflow_name} | Get Workflow details |
| PUT | /accounts/{account_id}/workflows/{workflow_name} | Create/modify Workflow |
| GET | /accounts/{account_id}/workflows/{workflow_name}/instances | List of workflow instances |
| POST | /accounts/{account_id}/workflows/{workflow_name}/instances | Create a new workflow instance |
| POST | /accounts/{account_id}/workflows/{workflow_name}/instances/batch | Batch create new Workflow instances |
| POST | /accounts/{account_id}/workflows/{workflow_name}/instances/batch/terminate | Batch terminate instances of a workflow |
| GET | /accounts/{account_id}/workflows/{workflow_name}/instances/terminate | Get status of the job responsible for terminate all instances of a workflow |
| GET | /accounts/{account_id}/workflows/{workflow_name}/instances/{instance_id} | Get logs and status from instance |
| POST | /accounts/{account_id}/workflows/{workflow_name}/instances/{instance_id}/events/{event_type} | Send event to instance |
| PATCH | /accounts/{account_id}/workflows/{workflow_name}/instances/{instance_id}/status | Change status of instance |
| GET | /accounts/{account_id}/workflows/{workflow_name}/versions | List deployed Workflow versions |
| GET | /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id} | Get Workflow version details |
| GET | /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id}/dag | Get Workflow version dag |
| GET | /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id}/graph | Get Workflow version graph |
| GET | /accounts/{account_id}/zerotrust/connectivity_settings | Get Zero Trust Connectivity Settings |
| PATCH | /accounts/{account_id}/zerotrust/connectivity_settings | Updates the Zero Trust Connectivity Settings |
| GET | /accounts/{account_id}/zerotrust/routes/hostname | List hostname routes |
| POST | /accounts/{account_id}/zerotrust/routes/hostname | Create hostname route |
| DELETE | /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id} | Delete hostname route |
| GET | /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id} | Get hostname route |
| PATCH | /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id} | Update hostname route |
| GET | /accounts/{account_id}/zerotrust/subnets | List Subnets |
| PATCH | /accounts/{account_id}/zerotrust/subnets/cloudflare_source/{address_family} | Update Cloudflare Source Subnet |
| POST | /accounts/{account_id}/zerotrust/subnets/warp | Create WARP IP subnet |
| DELETE | /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id} | Delete WARP IP subnet |
| GET | /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id} | Get WARP IP subnet |
| PATCH | /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id} | Update WARP IP subnet |
| GET | /accounts/{account_id}/zt_risk_scoring/behaviors | Get all behaviors and associated configuration |
| PUT | /accounts/{account_id}/zt_risk_scoring/behaviors | Update configuration for risk behaviors |
| GET | /accounts/{account_id}/zt_risk_scoring/integrations | List all risk score integrations for the account. |
| POST | /accounts/{account_id}/zt_risk_scoring/integrations | Create new risk score integration. |
| GET | /accounts/{account_id}/zt_risk_scoring/integrations/reference_id/{reference_id} | Get risk score integration by reference id. |
| DELETE | /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id} | Delete a risk score integration. |
| GET | /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id} | Get risk score integration by id. |
| PUT | /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id} | Update a risk score integration. |
| GET | /accounts/{account_id}/zt_risk_scoring/summary | Get risk score info for all users in the account |
| GET | /accounts/{account_id}/zt_risk_scoring/{user_id} | Get risk event/score information for a specific user |
| POST | /accounts/{account_id}/zt_risk_scoring/{user_id}/reset | Clear the risk score for a particular user |

### certificates
| Method | Path | Description |
|--------|------|-------------|
| GET | /certificates | List Certificates |
| POST | /certificates | Create Certificate |
| DELETE | /certificates/{certificate_id} | Revoke Certificate |
| GET | /certificates/{certificate_id} | Get Certificate |

### internal
| Method | Path | Description |
|--------|------|-------------|
| POST | /internal/submit | Internal route for testing URL submissions |

### ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /ips | Cloudflare/JD Cloud IP Details |

### live
| Method | Path | Description |
|--------|------|-------------|
| GET | /live | Run liveness checks |

### memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /memberships | List Memberships |
| DELETE | /memberships/{membership_id} | Delete Membership |
| GET | /memberships/{membership_id} | Membership Details |
| PUT | /memberships/{membership_id} | Update Membership |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations | List organizations the user has access to |
| POST | /organizations | Create organization |
| DELETE | /organizations/{organization_id} | Delete organization. |
| GET | /organizations/{organization_id} | Get organization |
| PUT | /organizations/{organization_id} | Modify organization. |
| GET | /organizations/{organization_id}/accounts | Get organization accounts |
| GET | /organizations/{organization_id}/members | List organization members |
| POST | /organizations/{organization_id}/members | Create organization member |
| DELETE | /organizations/{organization_id}/members/{member_id} | Delete organization member |
| GET | /organizations/{organization_id}/members/{member_id} | Get organization member |
| POST | /organizations/{organization_id}/members:batchCreate | Batch create organization members |
| GET | /organizations/{organization_id}/profile | Get organization profile |
| PUT | /organizations/{organization_id}/profile | Modify organization profile. |
| GET | /organizations/{organization_id}/shares | List organization shares |

### radar
| Method | Path | Description |
|--------|------|-------------|
| GET | /radar/ai/bots/summary/user_agent | Get AI user agents summary |
| GET | /radar/ai/bots/summary/{dimension} | Get AI bots HTTP requests distribution by dimension |
| GET | /radar/ai/bots/timeseries | Get AI bots HTTP requests time series |
| GET | /radar/ai/bots/timeseries_groups/user_agent | Get AI user agents time series |
| GET | /radar/ai/bots/timeseries_groups/{dimension} | Get time series distribution of AI bots HTTP requests by dimension. |
| GET | /radar/ai/inference/summary/model | Get Workers AI models summary |
| GET | /radar/ai/inference/summary/task | Get Workers AI tasks summary |
| GET | /radar/ai/inference/summary/{dimension} | Get Workers AI inference distribution by dimension |
| GET | /radar/ai/inference/timeseries_groups/model | Get Workers AI models time series |
| GET | /radar/ai/inference/timeseries_groups/task | Get Workers AI tasks time series |
| GET | /radar/ai/inference/timeseries_groups/{dimension} | Get time series distribution of Workers AI inference by dimension. |
| GET | /radar/annotations | Get latest annotations |
| GET | /radar/annotations/outages | Get latest Internet outages and anomalies |
| GET | /radar/annotations/outages/locations | Get the number of outages by location |
| GET | /radar/as112/summary/dnssec | Get AS112 DNS queries by DNSSEC summary |
| GET | /radar/as112/summary/edns | Get AS112 DNS queries by EDNS summary |
| GET | /radar/as112/summary/ip_version | Get AS112 DNS queries by IP version summary |
| GET | /radar/as112/summary/protocol | Get AS112 DNS queries by DNS protocol summary |
| GET | /radar/as112/summary/query_type | Get AS112 DNS queries by type summary |
| GET | /radar/as112/summary/response_codes | Get AS112 DNS queries by response code summary |
| GET | /radar/as112/summary/{dimension} | Get AS112 summary by dimension |
| GET | /radar/as112/timeseries | Get AS112 DNS queries time series |
| GET | /radar/as112/timeseries_groups/dnssec | Get AS112 DNS queries by DNSSEC support time series |
| GET | /radar/as112/timeseries_groups/edns | Get AS112 DNS queries by EDNS support summary |
| GET | /radar/as112/timeseries_groups/ip_version | Get AS112 DNS queries by IP version time series |
| GET | /radar/as112/timeseries_groups/protocol | Get AS112 DNS queries by DNS protocol time series |
| GET | /radar/as112/timeseries_groups/query_type | Get AS112 DNS queries by type time series |
| GET | /radar/as112/timeseries_groups/response_codes | Get AS112 DNS queries by response code time series |
| GET | /radar/as112/timeseries_groups/{dimension} | Get AS112 time series grouped by dimension |
| GET | /radar/as112/top/locations | Get top locations by AS112 DNS queries |
| GET | /radar/as112/top/locations/dnssec/{dnssec} | Get top locations by AS112 DNS queries with DNSSEC support |
| GET | /radar/as112/top/locations/edns/{edns} | Get top locations by AS112 DNS queries with EDNS support |
| GET | /radar/as112/top/locations/ip_version/{ip_version} | Get top locations by AS112 DNS queries for an IP version |
| GET | /radar/attacks/layer3/summary/bitrate | Get layer 3 attacks by bitrate summary |
| GET | /radar/attacks/layer3/summary/duration | Get layer 3 attacks by duration summary |
| GET | /radar/attacks/layer3/summary/industry | Get layer 3 attacks by targeted industry summary |
| GET | /radar/attacks/layer3/summary/ip_version | Get layer 3 attacks by IP version summary |
| GET | /radar/attacks/layer3/summary/protocol | Get layer 3 attacks by protocol summary |
| GET | /radar/attacks/layer3/summary/vector | Get layer 3 attacks by vector summary |
| GET | /radar/attacks/layer3/summary/vertical | Get layer 3 attacks by targeted vertical summary |
| GET | /radar/attacks/layer3/summary/{dimension} | Get layer 3 attacks summary by dimension |
| GET | /radar/attacks/layer3/timeseries | Get layer 3 attacks by bytes time series |
| GET | /radar/attacks/layer3/timeseries_groups/bitrate | Get layer 3 attacks by bitrate time series |
| GET | /radar/attacks/layer3/timeseries_groups/duration | Get layer 3 attacks by duration time series |
| GET | /radar/attacks/layer3/timeseries_groups/industry | Get layer 3 attacks by target industries time series |
| GET | /radar/attacks/layer3/timeseries_groups/ip_version | Get layer 3 attacks by IP version time series |
| GET | /radar/attacks/layer3/timeseries_groups/protocol | Get layer 3 attacks by protocol time series |
| GET | /radar/attacks/layer3/timeseries_groups/vector | Get layer 3 attacks by vector time series |
| GET | /radar/attacks/layer3/timeseries_groups/vertical | Get layer 3 attacks by vertical time series |
| GET | /radar/attacks/layer3/timeseries_groups/{dimension} | Get layer 3 attacks time series grouped by dimension |
| GET | /radar/attacks/layer3/top/attacks | Get top layer 3 attack pairs (origin and target locations) |
| GET | /radar/attacks/layer3/top/industry | Get top industries targeted by layer 3 attacks |
| GET | /radar/attacks/layer3/top/locations/origin | Get top origin locations of layer 3 attacks |
| GET | /radar/attacks/layer3/top/locations/target | Get top target locations of layer 3 attacks |
| GET | /radar/attacks/layer3/top/vertical | Get top verticals targeted by layer 3 attacks |
| GET | /radar/attacks/layer7/summary/http_method | Get layer 7 attacks by HTTP method summary |
| GET | /radar/attacks/layer7/summary/http_version | Get layer 7 attacks by HTTP version summary |
| GET | /radar/attacks/layer7/summary/industry | Get layer 7 attacks by targeted industry summary |
| GET | /radar/attacks/layer7/summary/ip_version | Get layer 7 attacks by IP version summary |
| GET | /radar/attacks/layer7/summary/managed_rules | Get layer 7 attacks by managed rules summary |
| GET | /radar/attacks/layer7/summary/mitigation_product | Get layer 7 attacks by mitigation product summary |
| GET | /radar/attacks/layer7/summary/vertical | Get layer 7 attacks by targeted vertical summary |
| GET | /radar/attacks/layer7/summary/{dimension} | Get layer 7 attacks summary by dimension |
| GET | /radar/attacks/layer7/timeseries | Get layer 7 attacks time series |
| GET | /radar/attacks/layer7/timeseries_groups/http_method | Get layer 7 attacks by HTTP method time series |
| GET | /radar/attacks/layer7/timeseries_groups/http_version | Get layer 7 attacks by HTTP version time series |
| GET | /radar/attacks/layer7/timeseries_groups/industry | Get layer 7 attacks by target industries time series |
| GET | /radar/attacks/layer7/timeseries_groups/ip_version | Get layer 7 attacks by IP version time series |
| GET | /radar/attacks/layer7/timeseries_groups/managed_rules | Get layer 7 attacks by managed rules time series |
| GET | /radar/attacks/layer7/timeseries_groups/mitigation_product | Get layer 7 attacks by mitigation product time series |
| GET | /radar/attacks/layer7/timeseries_groups/vertical | Get layer 7 attacks by vertical time series |
| GET | /radar/attacks/layer7/timeseries_groups/{dimension} | Get layer 7 attacks time series grouped by dimension |
| GET | /radar/attacks/layer7/top/ases/origin | Get top origin ASes of layer 7 attacks |
| GET | /radar/attacks/layer7/top/attacks | Get top layer 7 attack pairs (origin and target locations) |
| GET | /radar/attacks/layer7/top/industry | Get top industries targeted by layer 7 attacks |
| GET | /radar/attacks/layer7/top/locations/origin | Get top origin locations of layer 7 attacks |
| GET | /radar/attacks/layer7/top/locations/target | Get top target locations of layer 7 attacks |
| GET | /radar/attacks/layer7/top/vertical | Get top verticals targeted by layer 7 attacks |
| GET | /radar/bgp/hijacks/events | Get BGP hijack events |
| GET | /radar/bgp/ips/timeseries | Get announced IP address space time series |
| GET | /radar/bgp/leaks/events | Get BGP route leak events |
| GET | /radar/bgp/routes/ases | List ASes from global routing tables |
| GET | /radar/bgp/routes/moas | Get Multi-Origin AS (MOAS) prefixes |
| GET | /radar/bgp/routes/pfx2as | Get prefix-to-ASN mapping |
| GET | /radar/bgp/routes/realtime | Get real-time BGP routes for a prefix |
| GET | /radar/bgp/routes/stats | Get BGP routing table stats |
| GET | /radar/bgp/rpki/aspa/changes | Get ASPA changes over time |
| GET | /radar/bgp/rpki/aspa/snapshot | Get ASPA objects snapshot |
| GET | /radar/bgp/rpki/aspa/timeseries | Get ASPA count time series |
| GET | /radar/bgp/timeseries | Get BGP time series |
| GET | /radar/bgp/top/ases | Get top ASes by BGP updates |
| GET | /radar/bgp/top/ases/prefixes | Get top ASes by prefix count |
| GET | /radar/bgp/top/prefixes | Get top prefixes by BGP updates |
| GET | /radar/bots | List bots |
| GET | /radar/bots/crawlers/summary/{dimension} | Get crawler HTTP request distribution by dimension |
| GET | /radar/bots/crawlers/timeseries_groups/{dimension} | Get time series of crawler HTTP request distribution by dimension |
| GET | /radar/bots/summary/{dimension} | Get bots HTTP requests distribution by dimension |
| GET | /radar/bots/timeseries | Get bots HTTP requests time series |
| GET | /radar/bots/timeseries_groups/{dimension} | Get time series distribution of bots HTTP requests by dimension. |
| GET | /radar/bots/{bot_slug} | Get bot details |
| GET | /radar/ct/authorities | List certificate authorities |
| GET | /radar/ct/authorities/{ca_slug} | Get certificate authority details |
| GET | /radar/ct/logs | List certificate logs |
| GET | /radar/ct/logs/{log_slug} | Get certificate log details |
| GET | /radar/ct/summary/{dimension} | Get certificate distribution by dimension |
| GET | /radar/ct/timeseries | Get certificates time series |
| GET | /radar/ct/timeseries_groups/{dimension} | Get time series of certificate distribution by dimension |
| GET | /radar/datasets | List datasets |
| POST | /radar/datasets/download | Get dataset download URL |
| GET | /radar/datasets/{alias} | Get dataset CSV stream |
| GET | /radar/dns/summary/cache_hit | Get DNS queries by cache status summary |
| GET | /radar/dns/summary/dnssec | Get DNS queries by DNSSEC support summary |
| GET | /radar/dns/summary/dnssec_aware | Get DNS queries by DNSSEC awareness summary |
| GET | /radar/dns/summary/dnssec_e2e | Get DNS queries by DNSSEC end-to-end summary |
| GET | /radar/dns/summary/ip_version | Get DNS queries by IP version summary |
| GET | /radar/dns/summary/matching_answer | Get DNS queries by matching answer summary |
| GET | /radar/dns/summary/protocol | Get DNS queries by protocol summary |
| GET | /radar/dns/summary/query_type | Get DNS queries by type summary |
| GET | /radar/dns/summary/response_code | Get DNS queries by response code summary |
| GET | /radar/dns/summary/response_ttl | Get DNS queries by response TTL summary |
| GET | /radar/dns/summary/{dimension} | Get DNS summary by dimension |
| GET | /radar/dns/timeseries | Get DNS queries time series |
| GET | /radar/dns/timeseries_groups/cache_hit | Get DNS queries by cache status time series |
| GET | /radar/dns/timeseries_groups/dnssec | Get DNS queries by DNSSEC support time series |
| GET | /radar/dns/timeseries_groups/dnssec_aware | Get DNS queries by DNSSEC awareness time series |
| GET | /radar/dns/timeseries_groups/dnssec_e2e | Get DNS queries by DNSSEC end-to-end time series |
| GET | /radar/dns/timeseries_groups/ip_version | Get DNS queries by IP version time series |
| GET | /radar/dns/timeseries_groups/matching_answer | Get DNS queries by matching answer time series |
| GET | /radar/dns/timeseries_groups/protocol | Get DNS queries by protocol time series |
| GET | /radar/dns/timeseries_groups/query_type | Get DNS queries by type time series |
| GET | /radar/dns/timeseries_groups/response_code | Get DNS queries by response code time series |
| GET | /radar/dns/timeseries_groups/response_ttl | Get DNS queries by response TTL time series |
| GET | /radar/dns/timeseries_groups/{dimension} | Get DNS time series grouped by dimension |
| GET | /radar/dns/top/ases | Get top ASes by DNS queries |
| GET | /radar/dns/top/locations | Get top locations by DNS queries |
| GET | /radar/email/routing/summary/arc | Get email ARC validation summary |
| GET | /radar/email/routing/summary/dkim | Get email DKIM validation summary |
| GET | /radar/email/routing/summary/dmarc | Get email DMARC validation summary |
| GET | /radar/email/routing/summary/encrypted | Get email encryption status summary |
| GET | /radar/email/routing/summary/ip_version | Get email IP version summary |
| GET | /radar/email/routing/summary/spf | Get email SPF validation summary |
| GET | /radar/email/routing/summary/{dimension} | Get email routing summary by dimension |
| GET | /radar/email/routing/timeseries_groups/arc | Get email ARC validation time series |
| GET | /radar/email/routing/timeseries_groups/dkim | Get email DKIM validation time series |
| GET | /radar/email/routing/timeseries_groups/dmarc | Get email DMARC validation time series |
| GET | /radar/email/routing/timeseries_groups/encrypted | Get email encryption status time series |
| GET | /radar/email/routing/timeseries_groups/ip_version | Get email IP version time series |
| GET | /radar/email/routing/timeseries_groups/spf | Get email SPF validation time series |
| GET | /radar/email/routing/timeseries_groups/{dimension} | Get email routing time series grouped by dimension |
| GET | /radar/email/security/summary/arc | Get email ARC validation summary |
| GET | /radar/email/security/summary/dkim | Get email DKIM validation summary |
| GET | /radar/email/security/summary/dmarc | Get email DMARC validation summary |
| GET | /radar/email/security/summary/malicious | Get email malicious classification summary |
| GET | /radar/email/security/summary/spam | Get email spam classification summary |
| GET | /radar/email/security/summary/spf | Get email SPF validation summary |
| GET | /radar/email/security/summary/spoof | Get email spoof classification summary |
| GET | /radar/email/security/summary/threat_category | Get email threat category summary |
| GET | /radar/email/security/summary/tls_version | Get email TLS version summary |
| GET | /radar/email/security/summary/{dimension} | Get email security summary by dimension |
| GET | /radar/email/security/timeseries_groups/arc | Get email ARC validation time series |
| GET | /radar/email/security/timeseries_groups/dkim | Get email DKIM validation time series |
| GET | /radar/email/security/timeseries_groups/dmarc | Get email DMARC validation time series |
| GET | /radar/email/security/timeseries_groups/malicious | Get email malicious classification time series |
| GET | /radar/email/security/timeseries_groups/spam | Get email spam classification time series |
| GET | /radar/email/security/timeseries_groups/spf | Get email SPF validation time series |
| GET | /radar/email/security/timeseries_groups/spoof | Get email spoof classification time series |
| GET | /radar/email/security/timeseries_groups/threat_category | Get email threat category time series |
| GET | /radar/email/security/timeseries_groups/tls_version | Get email TLS version time series |
| GET | /radar/email/security/timeseries_groups/{dimension} | Get email security time series grouped by dimension |
| GET | /radar/email/security/top/tlds | Get top TLDs by email message volume |
| GET | /radar/email/security/top/tlds/malicious/{malicious} | Get top TLDs by email malicious classification |
| GET | /radar/email/security/top/tlds/spam/{spam} | Get top TLDs by email spam classification |
| GET | /radar/email/security/top/tlds/spoof/{spoof} | Get top TLDs by email spoof classification |
| GET | /radar/entities/asns | List autonomous systems |
| GET | /radar/entities/asns/botnet_threat_feed | Get AS rankings by botnet threat feed activity |
| GET | /radar/entities/asns/ip | Get AS details by IP address |
| GET | /radar/entities/asns/{asn} | Get AS details by ASN |
| GET | /radar/entities/asns/{asn}/as_set | Get IRR AS-SETs that an AS is a member of |
| GET | /radar/entities/asns/{asn}/rel | Get AS-level relationships by ASN |
| GET | /radar/entities/ip | Get IP address details |
| GET | /radar/entities/locations | List locations |
| GET | /radar/entities/locations/{location} | Get location details |
| GET | /radar/geolocations | List Geolocations |
| GET | /radar/geolocations/{geo_id} | Get Geolocation details |
| GET | /radar/http/summary/bot_class | Get HTTP requests by bot class summary |
| GET | /radar/http/summary/device_type | Get HTTP requests by device type summary |
| GET | /radar/http/summary/http_protocol | Get HTTP requests by HTTP/HTTPS summary |
| GET | /radar/http/summary/http_version | Get HTTP requests by HTTP version summary |
| GET | /radar/http/summary/ip_version | Get HTTP requests by IP version summary |
| GET | /radar/http/summary/os | Get HTTP requests by OS summary |
| GET | /radar/http/summary/post_quantum | Get HTTP requests by post-quantum support summary |
| GET | /radar/http/summary/tls_version | Get HTTP requests by TLS version summary |
| GET | /radar/http/summary/{dimension} | Get HTTP requests summary by dimension |
| GET | /radar/http/timeseries | Get HTTP requests time series |
| GET | /radar/http/timeseries_groups/bot_class | Get HTTP requests by bot class time series |
| GET | /radar/http/timeseries_groups/browser | Get HTTP requests by user agent time series |
| GET | /radar/http/timeseries_groups/browser_family | Get HTTP requests by user agent family time series |
| GET | /radar/http/timeseries_groups/device_type | Get HTTP requests by device type time series |
| GET | /radar/http/timeseries_groups/http_protocol | Get HTTP requests by HTTP/HTTPS time series |
| GET | /radar/http/timeseries_groups/http_version | Get HTTP requests by HTTP version time series |
| GET | /radar/http/timeseries_groups/ip_version | Get HTTP requests by IP version time series |
| GET | /radar/http/timeseries_groups/os | Get HTTP requests by OS time series |
| GET | /radar/http/timeseries_groups/post_quantum | Get HTTP requests by post-quantum support time series |
| GET | /radar/http/timeseries_groups/tls_version | Get HTTP requests by TLS version time series |
| GET | /radar/http/timeseries_groups/{dimension} | Get HTTP requests time series grouped by dimension |
| GET | /radar/http/top/ases | Get top ASes by HTTP requests |
| GET | /radar/http/top/ases/bot_class/{bot_class} | Get top ASes by HTTP requests for a bot class |
| GET | /radar/http/top/ases/browser_family/{browser_family} | Get top ASes by HTTP requests for a browser family |
| GET | /radar/http/top/ases/device_type/{device_type} | Get top ASes by HTTP requests for a device type |
| GET | /radar/http/top/ases/http_protocol/{http_protocol} | Get top ASes by HTTP requests for an HTTP protocol |
| GET | /radar/http/top/ases/http_version/{http_version} | Get top ASes by HTTP requests for an HTTP version |
| GET | /radar/http/top/ases/ip_version/{ip_version} | Get top ASes by HTTP requests for an IP version |
| GET | /radar/http/top/ases/os/{os} | Get top ASes by HTTP requests for an OS |
| GET | /radar/http/top/ases/tls_version/{tls_version} | Get top ASes by HTTP requests for a TLS version |
| GET | /radar/http/top/browser | Get top user agents by HTTP requests |
| GET | /radar/http/top/browser_family | Get top user agent families by HTTP requests |
| GET | /radar/http/top/locations | Get top locations by HTTP requests |
| GET | /radar/http/top/locations/bot_class/{bot_class} | Get top locations by HTTP requests for a bot class |
| GET | /radar/http/top/locations/browser_family/{browser_family} | Get top locations by HTTP requests for a browser family |
| GET | /radar/http/top/locations/device_type/{device_type} | Get top locations by HTTP requests for a device type |
| GET | /radar/http/top/locations/http_protocol/{http_protocol} | Get top locations by HTTP requests for an HTTP protocol |
| GET | /radar/http/top/locations/http_version/{http_version} | Get top locations by HTTP requests for an HTTP version |
| GET | /radar/http/top/locations/ip_version/{ip_version} | Get top locations by HTTP requests for an IP version |
| GET | /radar/http/top/locations/os/{os} | Get top locations by HTTP requests for an OS |
| GET | /radar/http/top/locations/tls_version/{tls_version} | Get top locations by HTTP requests for a TLS version |
| GET | /radar/leaked_credential_checks/summary/bot_class | Get HTTP authentication requests by bot class summary |
| GET | /radar/leaked_credential_checks/summary/compromised | Get HTTP authentication requests by compromised credential status summary |
| GET | /radar/leaked_credential_checks/summary/{dimension} | Get HTTP authentication requests distribution by dimension |
| GET | /radar/leaked_credential_checks/timeseries_groups/bot_class | Get HTTP authentication requests by bot class time series |
| GET | /radar/leaked_credential_checks/timeseries_groups/compromised | Get HTTP authentication requests by compromised credential status time series |
| GET | /radar/leaked_credential_checks/timeseries_groups/{dimension} | Get time series distribution of HTTP authentication requests by dimension. |
| GET | /radar/netflows/summary | Get network traffic summary |
| GET | /radar/netflows/summary/{dimension} | Get network traffic distribution by dimension |
| GET | /radar/netflows/timeseries | Get network traffic time series |
| GET | /radar/netflows/timeseries_groups/{dimension} | Get time series distribution of network traffic by dimension |
| GET | /radar/netflows/top/ases | Get top ASes by network traffic |
| GET | /radar/netflows/top/locations | Get top locations by network traffic |
| GET | /radar/origins | List Origins |
| GET | /radar/origins/summary/{dimension} | Get origin metrics distribution by dimension |
| GET | /radar/origins/timeseries | Get origin metrics time series |
| GET | /radar/origins/timeseries_groups/{dimension} | Get origin metrics time series grouped by dimension |
| GET | /radar/origins/{slug} | Get Origin details |
| GET | /radar/post_quantum/origin/summary/{dimension} | Get Origin Post-Quantum Data Summary |
| GET | /radar/post_quantum/origin/timeseries_groups/{dimension} | Get Origin Post-Quantum Data Over Time |
| GET | /radar/post_quantum/tls/support | Check Post-Quantum TLS support |
| GET | /radar/quality/iqi/summary | Get Internet Quality Index (IQI) summary |
| GET | /radar/quality/iqi/timeseries_groups | Get Internet Quality Index (IQI) time series |
| GET | /radar/quality/speed/histogram | Get speed tests histogram |
| GET | /radar/quality/speed/summary | Get speed tests summary |
| GET | /radar/quality/speed/top/ases | Get top ASes by speed test results |
| GET | /radar/quality/speed/top/locations | Get top locations by speed test results |
| GET | /radar/ranking/domain/{domain} | Get domain rank details |
| GET | /radar/ranking/internet_services/categories | List Internet services categories |
| GET | /radar/ranking/internet_services/timeseries_groups | Get Internet services rank time series |
| GET | /radar/ranking/internet_services/top | Get top Internet services |
| GET | /radar/ranking/timeseries_groups | Get domains rank time series |
| GET | /radar/ranking/top | Get top or trending domains |
| GET | /radar/robots_txt/top/domain_categories | Get top domain categories by robots.txt files parsed |
| GET | /radar/robots_txt/top/user_agents/directive | Get top user agents on robots.txt files |
| GET | /radar/search/global | Search for locations, ASes, reports, and more |
| GET | /radar/tcp_resets_timeouts/summary | Get TCP resets and timeouts summary |
| GET | /radar/tcp_resets_timeouts/timeseries_groups | Get TCP resets and timeouts time series |
| GET | /radar/tlds | List TLDs |
| GET | /radar/tlds/{tld} | Get TLD details |
| GET | /radar/traffic_anomalies | Get latest Internet traffic anomalies |
| GET | /radar/traffic_anomalies/locations | Get top locations by total traffic anomalies |
| GET | /radar/verified_bots/top/bots | Get top verified bots by HTTP requests |
| GET | /radar/verified_bots/top/categories | Get top verified bot categories by HTTP requests |

### ready
| Method | Path | Description |
|--------|------|-------------|
| GET | /ready | Run readiness checks |

### signed-url
| Method | Path | Description |
|--------|------|-------------|
| GET | /signed-url | Internal route for testing signed URLs |

### system
| Method | Path | Description |
|--------|------|-------------|
| GET | /system/accounts/{account_tag}/stores | List account stores (System) |
| POST | /system/accounts/{account_tag}/stores | Create a store (System) |
| DELETE | /system/accounts/{account_tag}/stores/{store_id} | Delete a store (System) |
| DELETE | /system/accounts/{account_tag}/stores/{store_id}/secrets | Delete secrets (System) |
| GET | /system/accounts/{account_tag}/stores/{store_id}/secrets | List store secrets (System) |
| POST | /system/accounts/{account_tag}/stores/{store_id}/secrets | Create secrets (System) |
| DELETE | /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id} | Delete a secret (System) |
| GET | /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id} | Get a secret by ID (System) |
| PATCH | /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id} | Patch a secret (System) |
| POST | /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id}/duplicate | Duplicate secret (System) |

### tenants
| Method | Path | Description |
|--------|------|-------------|
| GET | /tenants/{tenant_id} | Get tenant |
| GET | /tenants/{tenant_id}/account_types | Get tenant account types |
| GET | /tenants/{tenant_id}/accounts | List tenant accounts |
| GET | /tenants/{tenant_id}/entitlements | List tenant entitlements |
| GET | /tenants/{tenant_id}/memberships | List tenant memberships |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user | User Details |
| PATCH | /user | Edit User |
| GET | /user/audit_logs | Get user audit logs |
| GET | /user/billing/history | Billing History Details |
| GET | /user/billing/profile | Billing Profile Details |
| GET | /user/firewall/access_rules/rules | List IP Access rules |
| POST | /user/firewall/access_rules/rules | Create an IP Access rule |
| DELETE | /user/firewall/access_rules/rules/{rule_id} | Delete an IP Access rule |
| PATCH | /user/firewall/access_rules/rules/{rule_id} | Update an IP Access rule |
| GET | /user/invites | List Invitations |
| GET | /user/invites/{invite_id} | Invitation Details |
| PATCH | /user/invites/{invite_id} | Respond to Invitation |
| GET | /user/load_balancers/monitors | List Monitors |
| POST | /user/load_balancers/monitors | Create Monitor |
| DELETE | /user/load_balancers/monitors/{monitor_id} | Delete Monitor |
| GET | /user/load_balancers/monitors/{monitor_id} | Monitor Details |
| PATCH | /user/load_balancers/monitors/{monitor_id} | Patch Monitor |
| PUT | /user/load_balancers/monitors/{monitor_id} | Update Monitor |
| POST | /user/load_balancers/monitors/{monitor_id}/preview | Preview Monitor |
| GET | /user/load_balancers/monitors/{monitor_id}/references | List Monitor References |
| GET | /user/load_balancers/pools | List Pools |
| PATCH | /user/load_balancers/pools | Patch Pools |
| POST | /user/load_balancers/pools | Create Pool |
| DELETE | /user/load_balancers/pools/{pool_id} | Delete Pool |
| GET | /user/load_balancers/pools/{pool_id} | Pool Details |
| PATCH | /user/load_balancers/pools/{pool_id} | Patch Pool |
| PUT | /user/load_balancers/pools/{pool_id} | Update Pool |
| GET | /user/load_balancers/pools/{pool_id}/health | Pool Health Details |
| POST | /user/load_balancers/pools/{pool_id}/preview | Preview Pool |
| GET | /user/load_balancers/pools/{pool_id}/references | List Pool References |
| GET | /user/load_balancers/preview/{preview_id} | Preview Result |
| GET | /user/load_balancing_analytics/events | List Healthcheck Events |
| GET | /user/organizations | List Organizations |
| DELETE | /user/organizations/{organization_id} | Leave Organization |
| GET | /user/organizations/{organization_id} | Organization Details |
| GET | /user/subscriptions | Get User Subscriptions |
| DELETE | /user/subscriptions/{identifier} | Delete User Subscription |
| PUT | /user/subscriptions/{identifier} | Update User Subscription |
| GET | /user/tokens | List Tokens |
| POST | /user/tokens | Create Token |
| GET | /user/tokens/permission_groups | List Token Permission Groups |
| GET | /user/tokens/verify | Verify Token |
| DELETE | /user/tokens/{token_id} | Delete Token |
| GET | /user/tokens/{token_id} | Token Details |
| PUT | /user/tokens/{token_id} | Update Token |
| PUT | /user/tokens/{token_id}/value | Roll Token |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/tenants | List user tenants |

### zones
| Method | Path | Description |
|--------|------|-------------|
| GET | /zones | List Zones |
| POST | /zones | Create Zone |
| GET | /zones/{zone_identifier}/analytics/colos | Get analytics by Co-locations |
| GET | /zones/{zone_identifier}/analytics/dashboard | Get dashboard |
| GET | /zones/{zone_identifier}/custom_pages | List custom pages |
| GET | /zones/{zone_identifier}/custom_pages/{identifier} | Get a custom page |
| PUT | /zones/{zone_identifier}/custom_pages/{identifier} | Update a custom page |
| DELETE | /zones/{zone_id} | Delete Zone |
| GET | /zones/{zone_id} | Zone Details |
| PATCH | /zones/{zone_id} | Edit Zone |
| GET | /zones/{zone_id}/access/apps | List Access Applications |
| POST | /zones/{zone_id}/access/apps | Add an Access application |
| GET | /zones/{zone_id}/access/apps/ca | List short-lived certificate CAs |
| DELETE | /zones/{zone_id}/access/apps/{app_id} | Delete an Access application |
| GET | /zones/{zone_id}/access/apps/{app_id} | Get an Access application |
| PUT | /zones/{zone_id}/access/apps/{app_id} | Update an Access application |
| DELETE | /zones/{zone_id}/access/apps/{app_id}/ca | Delete a short-lived certificate CA |
| GET | /zones/{zone_id}/access/apps/{app_id}/ca | Get a short-lived certificate CA |
| POST | /zones/{zone_id}/access/apps/{app_id}/ca | Create a short-lived certificate CA |
| GET | /zones/{zone_id}/access/apps/{app_id}/policies | List Access policies |
| POST | /zones/{zone_id}/access/apps/{app_id}/policies | Create an Access policy |
| DELETE | /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id} | Delete an Access policy |
| GET | /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id} | Get an Access policy |
| PUT | /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id} | Update an Access policy |
| POST | /zones/{zone_id}/access/apps/{app_id}/revoke_tokens | Revoke application tokens |
| PATCH | /zones/{zone_id}/access/apps/{app_id}/settings | Update application settings |
| PUT | /zones/{zone_id}/access/apps/{app_id}/settings | Update application settings |
| GET | /zones/{zone_id}/access/apps/{app_id}/user_policy_checks | Test Access policies |
| GET | /zones/{zone_id}/access/certificates | List mTLS certificates |
| POST | /zones/{zone_id}/access/certificates | Add an mTLS certificate |
| GET | /zones/{zone_id}/access/certificates/settings | List all mTLS hostname settings |
| PUT | /zones/{zone_id}/access/certificates/settings | Update an mTLS certificate's hostname settings |
| DELETE | /zones/{zone_id}/access/certificates/{certificate_id} | Delete an mTLS certificate |
| GET | /zones/{zone_id}/access/certificates/{certificate_id} | Get an mTLS certificate |
| PUT | /zones/{zone_id}/access/certificates/{certificate_id} | Update an mTLS certificate |
| GET | /zones/{zone_id}/access/groups | List Access groups |
| POST | /zones/{zone_id}/access/groups | Create an Access group |
| DELETE | /zones/{zone_id}/access/groups/{group_id} | Delete an Access group |
| GET | /zones/{zone_id}/access/groups/{group_id} | Get an Access group |
| PUT | /zones/{zone_id}/access/groups/{group_id} | Update an Access group |
| GET | /zones/{zone_id}/access/identity_providers | List Access identity providers |
| POST | /zones/{zone_id}/access/identity_providers | Add an Access identity provider |
| DELETE | /zones/{zone_id}/access/identity_providers/{identity_provider_id} | Delete an Access identity provider |
| GET | /zones/{zone_id}/access/identity_providers/{identity_provider_id} | Get an Access identity provider |
| PUT | /zones/{zone_id}/access/identity_providers/{identity_provider_id} | Update an Access identity provider |
| GET | /zones/{zone_id}/access/organizations | Get your Zero Trust organization |
| POST | /zones/{zone_id}/access/organizations | Create your Zero Trust organization |
| PUT | /zones/{zone_id}/access/organizations | Update your Zero Trust organization |
| POST | /zones/{zone_id}/access/organizations/revoke_user | Revoke all Access tokens for a user |
| GET | /zones/{zone_id}/access/service_tokens | List service tokens |
| POST | /zones/{zone_id}/access/service_tokens | Create a service token |
| DELETE | /zones/{zone_id}/access/service_tokens/{service_token_id} | Delete a service token |
| GET | /zones/{zone_id}/access/service_tokens/{service_token_id} | Get a service token |
| PUT | /zones/{zone_id}/access/service_tokens/{service_token_id} | Update a service token |
| GET | /zones/{zone_id}/acm/custom_trust_store | List Custom Origin Trust Store Details |
| POST | /zones/{zone_id}/acm/custom_trust_store | Upload Custom Origin Trust Store |
| DELETE | /zones/{zone_id}/acm/custom_trust_store/{custom_origin_trust_store_id} | Delete Custom Origin Trust Store |
| GET | /zones/{zone_id}/acm/custom_trust_store/{custom_origin_trust_store_id} | Custom Origin Trust Store Details |
| GET | /zones/{zone_id}/acm/total_tls | Total TLS Settings Details |
| POST | /zones/{zone_id}/acm/total_tls | Enable or Disable Total TLS |
| PUT | /zones/{zone_id}/activation_check | Rerun the Activation Check |
| GET | /zones/{zone_id}/addressing/regional_hostnames | List Regional Hostnames |
| POST | /zones/{zone_id}/addressing/regional_hostnames | Create Regional Hostname |
| DELETE | /zones/{zone_id}/addressing/regional_hostnames/{hostname} | Delete Regional Hostname |
| GET | /zones/{zone_id}/addressing/regional_hostnames/{hostname} | Fetch Regional Hostname |
| PATCH | /zones/{zone_id}/addressing/regional_hostnames/{hostname} | Update Regional Hostname |
| GET | /zones/{zone_id}/analytics/latency | Argo Analytics for a zone |
| GET | /zones/{zone_id}/analytics/latency/colos | Argo Analytics for a zone at different PoPs |
| GET | /zones/{zone_id}/api_gateway/configuration | Retrieve information about specific configuration properties |
| PUT | /zones/{zone_id}/api_gateway/configuration | Update configuration properties |
| GET | /zones/{zone_id}/api_gateway/discovery | Retrieve discovered operations on a zone rendered as OpenAPI schemas |
| GET | /zones/{zone_id}/api_gateway/discovery/operations | Retrieve discovered operations on a zone |
| PATCH | /zones/{zone_id}/api_gateway/discovery/operations | Patch discovered operations |
| PATCH | /zones/{zone_id}/api_gateway/discovery/operations/{operation_id} | Patch discovered operation |
| POST | /zones/{zone_id}/api_gateway/expression-template/fallthrough | Generate fallthrough WAF expression template from a set of API hosts |
| DELETE | /zones/{zone_id}/api_gateway/operations | Delete multiple operations |
| GET | /zones/{zone_id}/api_gateway/operations | Retrieve information about all operations on a zone |
| POST | /zones/{zone_id}/api_gateway/operations | Add operations to a zone |
| POST | /zones/{zone_id}/api_gateway/operations/item | Add one operation to a zone |
| PATCH | /zones/{zone_id}/api_gateway/operations/schema_validation | Update multiple operation-level schema validation settings |
| DELETE | /zones/{zone_id}/api_gateway/operations/{operation_id} | Delete an operation |
| GET | /zones/{zone_id}/api_gateway/operations/{operation_id} | Retrieve information about an operation |
| GET | /zones/{zone_id}/api_gateway/operations/{operation_id}/schema_validation | Retrieve operation-level schema validation settings |
| PUT | /zones/{zone_id}/api_gateway/operations/{operation_id}/schema_validation | Update operation-level schema validation settings |
| GET | /zones/{zone_id}/api_gateway/schemas | Retrieve operations and features as OpenAPI schemas |
| GET | /zones/{zone_id}/api_gateway/settings/schema_validation | Retrieve zone level schema validation settings |
| PATCH | /zones/{zone_id}/api_gateway/settings/schema_validation | Update zone level schema validation settings |
| PUT | /zones/{zone_id}/api_gateway/settings/schema_validation | Update zone level schema validation settings |
| GET | /zones/{zone_id}/api_gateway/user_schemas | Retrieve information about all schemas on a zone |
| POST | /zones/{zone_id}/api_gateway/user_schemas | Upload a schema to a zone |
| GET | /zones/{zone_id}/api_gateway/user_schemas/hosts | Retrieve schema hosts in a zone |
| DELETE | /zones/{zone_id}/api_gateway/user_schemas/{schema_id} | Delete a schema |
| GET | /zones/{zone_id}/api_gateway/user_schemas/{schema_id} | Retrieve information about a specific schema on a zone |
| PATCH | /zones/{zone_id}/api_gateway/user_schemas/{schema_id} | Enable validation for a schema |
| GET | /zones/{zone_id}/api_gateway/user_schemas/{schema_id}/operations | Retrieve all operations from a schema. |
| GET | /zones/{zone_id}/argo/smart_routing | Get Argo Smart Routing setting |
| PATCH | /zones/{zone_id}/argo/smart_routing | Patch Argo Smart Routing setting |
| GET | /zones/{zone_id}/argo/tiered_caching | Get Tiered Caching setting |
| PATCH | /zones/{zone_id}/argo/tiered_caching | Patch Tiered Caching setting |
| GET | /zones/{zone_id}/available_plans | List Available Plans |
| GET | /zones/{zone_id}/available_plans/{plan_identifier} | Available Plan Details |
| GET | /zones/{zone_id}/available_rate_plans | List Available Rate Plans |
| GET | /zones/{zone_id}/bot_management | Get Zone Bot Management Config |
| PUT | /zones/{zone_id}/bot_management | Update Zone Bot Management Config |
| GET | /zones/{zone_id}/bot_management/feedback | List zone feedback reports |
| POST | /zones/{zone_id}/bot_management/feedback | Submit a feedback report |
| GET | /zones/{zone_id}/cache/cache_reserve | Get Cache Reserve setting |
| PATCH | /zones/{zone_id}/cache/cache_reserve | Change Cache Reserve setting |
| GET | /zones/{zone_id}/cache/cache_reserve_clear | Get Cache Reserve Clear |
| POST | /zones/{zone_id}/cache/cache_reserve_clear | Start Cache Reserve Clear |
| GET | /zones/{zone_id}/cache/origin_post_quantum_encryption | Get Origin Post-Quantum Encryption setting |
| PUT | /zones/{zone_id}/cache/origin_post_quantum_encryption | Change Origin Post-Quantum Encryption setting |
| GET | /zones/{zone_id}/cache/regional_tiered_cache | Get Regional Tiered Cache setting |
| PATCH | /zones/{zone_id}/cache/regional_tiered_cache | Change Regional Tiered Cache setting |
| DELETE | /zones/{zone_id}/cache/tiered_cache_smart_topology_enable | Delete Smart Tiered Cache setting |
| GET | /zones/{zone_id}/cache/tiered_cache_smart_topology_enable | Get Smart Tiered Cache setting |
| PATCH | /zones/{zone_id}/cache/tiered_cache_smart_topology_enable | Patch Smart Tiered Cache setting |
| DELETE | /zones/{zone_id}/cache/variants | Delete variants setting |
| GET | /zones/{zone_id}/cache/variants | Get variants setting |
| PATCH | /zones/{zone_id}/cache/variants | Change variants setting |
| GET | /zones/{zone_id}/certificate_authorities/hostname_associations | List Hostname Associations |
| PUT | /zones/{zone_id}/certificate_authorities/hostname_associations | Replace Hostname Associations |
| GET | /zones/{zone_id}/client_certificates | List Client Certificates |
| POST | /zones/{zone_id}/client_certificates | Create Client Certificate |
| DELETE | /zones/{zone_id}/client_certificates/{client_certificate_id} | Revoke Client Certificate |
| GET | /zones/{zone_id}/client_certificates/{client_certificate_id} | Client Certificate Details |
| PATCH | /zones/{zone_id}/client_certificates/{client_certificate_id} | Reactivate Client Certificate |
| GET | /zones/{zone_id}/cloud_connector/rules | Rules |
| PUT | /zones/{zone_id}/cloud_connector/rules | Put Rules |
| POST | /zones/{zone_id}/content-upload-scan/disable | Disable Content Scanning |
| POST | /zones/{zone_id}/content-upload-scan/enable | Enable Content Scanning |
| GET | /zones/{zone_id}/content-upload-scan/payloads | List Existing Custom Scan Expressions |
| POST | /zones/{zone_id}/content-upload-scan/payloads | Add Custom Scan Expressions |
| DELETE | /zones/{zone_id}/content-upload-scan/payloads/{expression_id} | Delete a Custom Scan Expression |
| GET | /zones/{zone_id}/content-upload-scan/settings | Get Content Scanning Status |
| PUT | /zones/{zone_id}/content-upload-scan/settings | Update Content Scanning Status |
| GET | /zones/{zone_id}/custom_certificates | List SSL Configurations |
| POST | /zones/{zone_id}/custom_certificates | Create SSL Configuration |
| PUT | /zones/{zone_id}/custom_certificates/prioritize | Re-prioritize SSL Certificates |
| DELETE | /zones/{zone_id}/custom_certificates/{custom_certificate_id} | Delete SSL Configuration |
| GET | /zones/{zone_id}/custom_certificates/{custom_certificate_id} | SSL Configuration Details |
| PATCH | /zones/{zone_id}/custom_certificates/{custom_certificate_id} | Edit SSL Configuration |
| GET | /zones/{zone_id}/custom_hostnames | List Custom Hostnames |
| POST | /zones/{zone_id}/custom_hostnames | Create Custom Hostname |
| DELETE | /zones/{zone_id}/custom_hostnames/fallback_origin | Delete Fallback Origin for Custom Hostnames |
| GET | /zones/{zone_id}/custom_hostnames/fallback_origin | Get Fallback Origin for Custom Hostnames |
| PUT | /zones/{zone_id}/custom_hostnames/fallback_origin | Update Fallback Origin for Custom Hostnames |
| DELETE | /zones/{zone_id}/custom_hostnames/{custom_hostname_id} | Delete Custom Hostname (and any issued SSL certificates) |
| GET | /zones/{zone_id}/custom_hostnames/{custom_hostname_id} | Custom Hostname Details |
| PATCH | /zones/{zone_id}/custom_hostnames/{custom_hostname_id} | Edit Custom Hostname |
| DELETE | /zones/{zone_id}/custom_hostnames/{custom_hostname_id}/certificate_pack/{certificate_pack_id}/certificates/{certificate_id} | Delete Single Certificate And Key For Custom Hostname |
| PUT | /zones/{zone_id}/custom_hostnames/{custom_hostname_id}/certificate_pack/{certificate_pack_id}/certificates/{certificate_id} | Replace Custom Certificate and Custom Key In Custom Hostname |
| GET | /zones/{zone_id}/custom_ns | Get Account Custom Nameserver Related Zone Metadata |
| PUT | /zones/{zone_id}/custom_ns | Set Account Custom Nameserver Related Zone Metadata |
| GET | /zones/{zone_id}/dcv_delegation/uuid | Retrieve the DCV Delegation unique identifier. |
| GET | /zones/{zone_id}/devices/policy/certificates | Get device certificate provisioning status |
| PATCH | /zones/{zone_id}/devices/policy/certificates | Update device certificate provisioning status |
| GET | /zones/{zone_id}/dns_analytics/report | Table |
| GET | /zones/{zone_id}/dns_analytics/report/bytime | By Time |
| GET | /zones/{zone_id}/dns_records | List DNS Records |
| POST | /zones/{zone_id}/dns_records | Create DNS Record |
| POST | /zones/{zone_id}/dns_records/batch | Batch DNS Records |
| GET | /zones/{zone_id}/dns_records/export | Export DNS Records |
| POST | /zones/{zone_id}/dns_records/import | Import DNS Records |
| POST | /zones/{zone_id}/dns_records/scan | Scan DNS Records |
| GET | /zones/{zone_id}/dns_records/scan/review | List Scanned DNS Records |
| POST | /zones/{zone_id}/dns_records/scan/review | Review Scanned DNS Records |
| POST | /zones/{zone_id}/dns_records/scan/trigger | Trigger DNS Record Scan |
| GET | /zones/{zone_id}/dns_records/usage | Get DNS Record Usage |
| DELETE | /zones/{zone_id}/dns_records/{dns_record_id} | Delete DNS Record |
| GET | /zones/{zone_id}/dns_records/{dns_record_id} | DNS Record Details |
| PATCH | /zones/{zone_id}/dns_records/{dns_record_id} | Update DNS Record |
| PUT | /zones/{zone_id}/dns_records/{dns_record_id} | Overwrite DNS Record |
| GET | /zones/{zone_id}/dns_settings | Show DNS Settings |
| PATCH | /zones/{zone_id}/dns_settings | Update DNS Settings |
| DELETE | /zones/{zone_id}/dnssec | Delete DNSSEC records |
| GET | /zones/{zone_id}/dnssec | DNSSEC Details |
| PATCH | /zones/{zone_id}/dnssec | Edit DNSSEC Status |
| GET | /zones/{zone_id}/email/routing | Get Email Routing settings |
| POST | /zones/{zone_id}/email/routing/disable | Disable Email Routing |
| DELETE | /zones/{zone_id}/email/routing/dns | Disable Email Routing |
| GET | /zones/{zone_id}/email/routing/dns | Email Routing - DNS settings |
| PATCH | /zones/{zone_id}/email/routing/dns | Unlock Email Routing |
| POST | /zones/{zone_id}/email/routing/dns | Enable Email Routing |
| POST | /zones/{zone_id}/email/routing/enable | Enable Email Routing |
| GET | /zones/{zone_id}/email/routing/rules | List routing rules |
| POST | /zones/{zone_id}/email/routing/rules | Create routing rule |
| GET | /zones/{zone_id}/email/routing/rules/catch_all | Get catch-all rule |
| PUT | /zones/{zone_id}/email/routing/rules/catch_all | Update catch-all rule |
| DELETE | /zones/{zone_id}/email/routing/rules/{rule_identifier} | Delete routing rule |
| GET | /zones/{zone_id}/email/routing/rules/{rule_identifier} | Get routing rule |
| PUT | /zones/{zone_id}/email/routing/rules/{rule_identifier} | Update routing rule |
| DELETE | /zones/{zone_id}/filters | Delete filters |
| GET | /zones/{zone_id}/filters | List filters |
| POST | /zones/{zone_id}/filters | Create filters |
| PUT | /zones/{zone_id}/filters | Update filters |
| DELETE | /zones/{zone_id}/filters/{filter_id} | Delete a filter |
| GET | /zones/{zone_id}/filters/{filter_id} | Get a filter |
| PUT | /zones/{zone_id}/filters/{filter_id} | Update a filter |
| GET | /zones/{zone_id}/firewall/access_rules/rules | List IP Access rules |
| POST | /zones/{zone_id}/firewall/access_rules/rules | Create an IP Access rule |
| DELETE | /zones/{zone_id}/firewall/access_rules/rules/{rule_id} | Delete an IP Access rule |
| PATCH | /zones/{zone_id}/firewall/access_rules/rules/{rule_id} | Update an IP Access rule |
| GET | /zones/{zone_id}/firewall/lockdowns | List Zone Lockdown rules |
| POST | /zones/{zone_id}/firewall/lockdowns | Create a Zone Lockdown rule |
| DELETE | /zones/{zone_id}/firewall/lockdowns/{lock_downs_id} | Delete a Zone Lockdown rule |
| GET | /zones/{zone_id}/firewall/lockdowns/{lock_downs_id} | Get a Zone Lockdown rule |
| PUT | /zones/{zone_id}/firewall/lockdowns/{lock_downs_id} | Update a Zone Lockdown rule |
| DELETE | /zones/{zone_id}/firewall/rules | Delete firewall rules |
| GET | /zones/{zone_id}/firewall/rules | List firewall rules |
| PATCH | /zones/{zone_id}/firewall/rules | Update priority of firewall rules |
| POST | /zones/{zone_id}/firewall/rules | Create firewall rules |
| PUT | /zones/{zone_id}/firewall/rules | Update firewall rules |
| DELETE | /zones/{zone_id}/firewall/rules/{rule_id} | Delete a firewall rule |
| GET | /zones/{zone_id}/firewall/rules/{rule_id} | Get a firewall rule |
| PATCH | /zones/{zone_id}/firewall/rules/{rule_id} | Update priority of a firewall rule |
| PUT | /zones/{zone_id}/firewall/rules/{rule_id} | Update a firewall rule |
| GET | /zones/{zone_id}/firewall/ua_rules | List User Agent Blocking rules |
| POST | /zones/{zone_id}/firewall/ua_rules | Create a User Agent Blocking rule |
| DELETE | /zones/{zone_id}/firewall/ua_rules/{ua_rule_id} | Delete a User Agent Blocking rule |
| GET | /zones/{zone_id}/firewall/ua_rules/{ua_rule_id} | Get a User Agent Blocking rule |
| PUT | /zones/{zone_id}/firewall/ua_rules/{ua_rule_id} | Update a User Agent Blocking rule |
| GET | /zones/{zone_id}/firewall/waf/overrides | List WAF overrides |
| POST | /zones/{zone_id}/firewall/waf/overrides | Create a WAF override |
| DELETE | /zones/{zone_id}/firewall/waf/overrides/{overrides_id} | Delete a WAF override |
| GET | /zones/{zone_id}/firewall/waf/overrides/{overrides_id} | Get a WAF override |
| PUT | /zones/{zone_id}/firewall/waf/overrides/{overrides_id} | Update WAF override |
| GET | /zones/{zone_id}/firewall/waf/packages | List WAF packages |
| GET | /zones/{zone_id}/firewall/waf/packages/{package_id} | Get a WAF package |
| PATCH | /zones/{zone_id}/firewall/waf/packages/{package_id} | Update a WAF package |
| GET | /zones/{zone_id}/firewall/waf/packages/{package_id}/groups | List WAF rule groups |
| GET | /zones/{zone_id}/firewall/waf/packages/{package_id}/groups/{group_id} | Get a WAF rule group |
| PATCH | /zones/{zone_id}/firewall/waf/packages/{package_id}/groups/{group_id} | Update a WAF rule group |
| GET | /zones/{zone_id}/firewall/waf/packages/{package_id}/rules | List WAF rules |
| GET | /zones/{zone_id}/firewall/waf/packages/{package_id}/rules/{rule_id} | Get a WAF rule |
| PATCH | /zones/{zone_id}/firewall/waf/packages/{package_id}/rules/{rule_id} | Update a WAF rule |
| GET | /zones/{zone_id}/fraud_detection/settings | Get Fraud Detection Settings |
| PUT | /zones/{zone_id}/fraud_detection/settings | Update Fraud Detection Settings |
| GET | /zones/{zone_id}/healthchecks | List Health Checks |
| POST | /zones/{zone_id}/healthchecks | Create Health Check |
| POST | /zones/{zone_id}/healthchecks/preview | Create Preview Health Check |
| DELETE | /zones/{zone_id}/healthchecks/preview/{healthcheck_id} | Delete Preview Health Check |
| GET | /zones/{zone_id}/healthchecks/preview/{healthcheck_id} | Health Check Preview Details |
| DELETE | /zones/{zone_id}/healthchecks/{healthcheck_id} | Delete Health Check |
| GET | /zones/{zone_id}/healthchecks/{healthcheck_id} | Health Check Details |
| PATCH | /zones/{zone_id}/healthchecks/{healthcheck_id} | Patch Health Check |
| PUT | /zones/{zone_id}/healthchecks/{healthcheck_id} | Update Health Check |
| DELETE | /zones/{zone_id}/hold | Remove Zone Hold |
| GET | /zones/{zone_id}/hold | Get Zone Hold |
| PATCH | /zones/{zone_id}/hold | Update Zone Hold |
| POST | /zones/{zone_id}/hold | Create Zone Hold |
| GET | /zones/{zone_id}/hostnames/settings/{setting_id} | List TLS setting for hostnames |
| DELETE | /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname} | Delete TLS setting for hostname |
| GET | /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname} | Get TLS setting for hostname |
| PUT | /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname} | Edit TLS setting for hostname |
| GET | /zones/{zone_id}/keyless_certificates | List Keyless SSL Configurations |
| POST | /zones/{zone_id}/keyless_certificates | Create Keyless SSL Configuration |
| DELETE | /zones/{zone_id}/keyless_certificates/{keyless_certificate_id} | Delete Keyless SSL Configuration |
| GET | /zones/{zone_id}/keyless_certificates/{keyless_certificate_id} | Get Keyless SSL Configuration |
| PATCH | /zones/{zone_id}/keyless_certificates/{keyless_certificate_id} | Edit Keyless SSL Configuration |
| GET | /zones/{zone_id}/leaked-credential-checks | Get Leaked Credential Checks Status |
| POST | /zones/{zone_id}/leaked-credential-checks | Set Leaked Credential Checks Status |
| GET | /zones/{zone_id}/leaked-credential-checks/detections | List Leaked Credential Checks Custom Detections |
| POST | /zones/{zone_id}/leaked-credential-checks/detections | Create Leaked Credential Checks Custom Detection |
| DELETE | /zones/{zone_id}/leaked-credential-checks/detections/{detection_id} | Delete Leaked Credential Checks Custom Detection |
| GET | /zones/{zone_id}/leaked-credential-checks/detections/{detection_id} | Get Leaked Credential Checks Custom Detection |
| PUT | /zones/{zone_id}/leaked-credential-checks/detections/{detection_id} | Update Leaked Credential Checks Custom Detection |
| GET | /zones/{zone_id}/load_balancers | List Load Balancers |
| POST | /zones/{zone_id}/load_balancers | Create Load Balancer |
| DELETE | /zones/{zone_id}/load_balancers/{load_balancer_id} | Delete Load Balancer |
| GET | /zones/{zone_id}/load_balancers/{load_balancer_id} | Load Balancer Details |
| PATCH | /zones/{zone_id}/load_balancers/{load_balancer_id} | Patch Load Balancer |
| PUT | /zones/{zone_id}/load_balancers/{load_balancer_id} | Update Load Balancer |
| GET | /zones/{zone_id}/logpush/datasets/{dataset_id}/fields | List fields |
| GET | /zones/{zone_id}/logpush/datasets/{dataset_id}/jobs | List Logpush jobs for a dataset |
| GET | /zones/{zone_id}/logpush/edge/jobs | List Instant Logs jobs |
| POST | /zones/{zone_id}/logpush/edge/jobs | Create Instant Logs job |
| GET | /zones/{zone_id}/logpush/jobs | List Logpush jobs |
| POST | /zones/{zone_id}/logpush/jobs | Create Logpush job |
| DELETE | /zones/{zone_id}/logpush/jobs/{job_id} | Delete Logpush job |
| GET | /zones/{zone_id}/logpush/jobs/{job_id} | Get Logpush job details |
| PUT | /zones/{zone_id}/logpush/jobs/{job_id} | Update Logpush job |
| POST | /zones/{zone_id}/logpush/ownership | Get ownership challenge |
| POST | /zones/{zone_id}/logpush/ownership/validate | Validate ownership challenge |
| POST | /zones/{zone_id}/logpush/validate/destination | Validate destination |
| POST | /zones/{zone_id}/logpush/validate/destination/exists | Check destination exists |
| POST | /zones/{zone_id}/logpush/validate/origin | Validate origin |
| GET | /zones/{zone_id}/logs/control/retention/flag | Get log retention flag |
| POST | /zones/{zone_id}/logs/control/retention/flag | Update log retention flag |
| GET | /zones/{zone_id}/logs/rayids/{ray_id} | Get logs RayIDs |
| GET | /zones/{zone_id}/logs/received | Get logs received |
| GET | /zones/{zone_id}/logs/received/fields | List fields |
| DELETE | /zones/{zone_id}/managed_headers | Delete Managed Transforms |
| GET | /zones/{zone_id}/managed_headers | List Managed Transforms |
| PATCH | /zones/{zone_id}/managed_headers | Update Managed Transforms |
| GET | /zones/{zone_id}/origin_tls_client_auth | List Certificates |
| POST | /zones/{zone_id}/origin_tls_client_auth | Upload Certificate |
| PUT | /zones/{zone_id}/origin_tls_client_auth/hostnames | Enable or Disable a Hostname for Client Authentication |
| GET | /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates | List Certificates |
| POST | /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates | Upload a Hostname Client Certificate |
| DELETE | /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates/{certificate_id} | Delete Hostname Client Certificate |
| GET | /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates/{certificate_id} | Get the Hostname Client Certificate |
| GET | /zones/{zone_id}/origin_tls_client_auth/hostnames/{hostname} | Get the Hostname Status for Client Authentication |
| GET | /zones/{zone_id}/origin_tls_client_auth/settings | Get Enablement Setting for Zone |
| PUT | /zones/{zone_id}/origin_tls_client_auth/settings | Set Enablement for Zone |
| DELETE | /zones/{zone_id}/origin_tls_client_auth/{certificate_id} | Delete Certificate |
| GET | /zones/{zone_id}/origin_tls_client_auth/{certificate_id} | Get Certificate Details |
| GET | /zones/{zone_id}/page_shield | Get Page Shield settings |
| PUT | /zones/{zone_id}/page_shield | Update Page Shield settings |
| GET | /zones/{zone_id}/page_shield/connections | List Page Shield connections |
| GET | /zones/{zone_id}/page_shield/connections/{connection_id} | Get a Page Shield connection |
| GET | /zones/{zone_id}/page_shield/cookies | List Page Shield Cookies |
| GET | /zones/{zone_id}/page_shield/cookies/{cookie_id} | Get a Page Shield cookie |
| GET | /zones/{zone_id}/page_shield/policies | List Page Shield policies |
| POST | /zones/{zone_id}/page_shield/policies | Create a Page Shield policy |
| DELETE | /zones/{zone_id}/page_shield/policies/{policy_id} | Delete a Page Shield policy |
| GET | /zones/{zone_id}/page_shield/policies/{policy_id} | Get a Page Shield policy |
| PUT | /zones/{zone_id}/page_shield/policies/{policy_id} | Update a Page Shield policy |
| GET | /zones/{zone_id}/page_shield/scripts | List Page Shield scripts |
| GET | /zones/{zone_id}/page_shield/scripts/{script_id} | Get a Page Shield script |
| GET | /zones/{zone_id}/pagerules | List Page Rules |
| POST | /zones/{zone_id}/pagerules | Create a Page Rule |
| GET | /zones/{zone_id}/pagerules/settings | List available Page Rules settings |
| DELETE | /zones/{zone_id}/pagerules/{pagerule_id} | Delete a Page Rule |
| GET | /zones/{zone_id}/pagerules/{pagerule_id} | Get a Page Rule |
| PATCH | /zones/{zone_id}/pagerules/{pagerule_id} | Edit a Page Rule |
| PUT | /zones/{zone_id}/pagerules/{pagerule_id} | Update a Page Rule |
| GET | /zones/{zone_id}/pay-per-crawl/configuration | Get the pay-per-crawl config |
| PATCH | /zones/{zone_id}/pay-per-crawl/configuration | Changes pay-per-crawl config for a zone |
| POST | /zones/{zone_id}/pay-per-crawl/configuration | Creates pay-per-crawl config for a zone |
| POST | /zones/{zone_id}/purge_cache | Purge Cached Content |
| GET | /zones/{zone_id}/rate_limits | List rate limits |
| POST | /zones/{zone_id}/rate_limits | Create a rate limit |
| DELETE | /zones/{zone_id}/rate_limits/{rate_limit_id} | Delete a rate limit |
| GET | /zones/{zone_id}/rate_limits/{rate_limit_id} | Get a rate limit |
| PUT | /zones/{zone_id}/rate_limits/{rate_limit_id} | Update a rate limit |
| GET | /zones/{zone_id}/rulesets | List zone rulesets |
| POST | /zones/{zone_id}/rulesets | Create a zone ruleset |
| GET | /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint | Get a zone entry point ruleset |
| PUT | /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint | Update a zone entry point ruleset |
| GET | /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions | List a zone entry point ruleset's versions |
| GET | /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions/{ruleset_version} | Get a zone entry point ruleset version |
| DELETE | /zones/{zone_id}/rulesets/{ruleset_id} | Delete a zone ruleset |
| GET | /zones/{zone_id}/rulesets/{ruleset_id} | Get a zone ruleset |
| PUT | /zones/{zone_id}/rulesets/{ruleset_id} | Update a zone ruleset |
| POST | /zones/{zone_id}/rulesets/{ruleset_id}/rules | Create a zone ruleset rule |
| DELETE | /zones/{zone_id}/rulesets/{ruleset_id}/rules/{rule_id} | Delete a zone ruleset rule |
| PATCH | /zones/{zone_id}/rulesets/{ruleset_id}/rules/{rule_id} | Update a zone ruleset rule |
| GET | /zones/{zone_id}/rulesets/{ruleset_id}/versions | List a zone ruleset's versions |
| DELETE | /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version} | Delete a zone ruleset version |
| GET | /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version} | Get a zone ruleset version |
| GET | /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version}/by_tag/{rule_tag} | List a zone ruleset version's rules by tag |
| GET | /zones/{zone_id}/schema_validation/schemas | List all uploaded schemas |
| POST | /zones/{zone_id}/schema_validation/schemas | Upload a schema |
| GET | /zones/{zone_id}/schema_validation/schemas/hosts | List hosts covered by uploaded schemas |
| DELETE | /zones/{zone_id}/schema_validation/schemas/{schema_id} | Delete a schema |
| GET | /zones/{zone_id}/schema_validation/schemas/{schema_id} | Get details of a schema |
| PATCH | /zones/{zone_id}/schema_validation/schemas/{schema_id} | Edit details of a schema to enable validation |
| GET | /zones/{zone_id}/schema_validation/schemas/{schema_id}/operations | Retrieve all operations from the schema. |
| GET | /zones/{zone_id}/schema_validation/settings | Get global schema validation settings |
| PATCH | /zones/{zone_id}/schema_validation/settings | Edit global schema validation settings |
| PUT | /zones/{zone_id}/schema_validation/settings | Update global schema validation settings |
| GET | /zones/{zone_id}/schema_validation/settings/operations | List per-operation schema validation settings |
| PATCH | /zones/{zone_id}/schema_validation/settings/operations | Bulk edit per-operation schema validation settings |
| DELETE | /zones/{zone_id}/schema_validation/settings/operations/{operation_id} | Delete per-operation schema validation setting |
| GET | /zones/{zone_id}/schema_validation/settings/operations/{operation_id} | Get per-operation schema validation setting |
| PUT | /zones/{zone_id}/schema_validation/settings/operations/{operation_id} | Update per-operation schema validation setting |
| POST | /zones/{zone_id}/secondary_dns/force_axfr | Force AXFR |
| DELETE | /zones/{zone_id}/secondary_dns/incoming | Delete Secondary Zone Configuration |
| GET | /zones/{zone_id}/secondary_dns/incoming | Secondary Zone Configuration Details |
| POST | /zones/{zone_id}/secondary_dns/incoming | Create Secondary Zone Configuration |
| PUT | /zones/{zone_id}/secondary_dns/incoming | Update Secondary Zone Configuration |
| DELETE | /zones/{zone_id}/secondary_dns/outgoing | Delete Primary Zone Configuration |
| GET | /zones/{zone_id}/secondary_dns/outgoing | Primary Zone Configuration Details |
| POST | /zones/{zone_id}/secondary_dns/outgoing | Create Primary Zone Configuration |
| PUT | /zones/{zone_id}/secondary_dns/outgoing | Update Primary Zone Configuration |
| POST | /zones/{zone_id}/secondary_dns/outgoing/disable | Disable Outgoing Zone Transfers |
| POST | /zones/{zone_id}/secondary_dns/outgoing/enable | Enable Outgoing Zone Transfers |
| POST | /zones/{zone_id}/secondary_dns/outgoing/force_notify | Force DNS NOTIFY |
| GET | /zones/{zone_id}/secondary_dns/outgoing/status | Get Outgoing Zone Transfer Status |
| GET | /zones/{zone_id}/security-center/insights | Retrieves Zone Security Center Insights |
| GET | /zones/{zone_id}/security-center/insights/class | Retrieves Zone Security Center Insight Counts by Class |
| GET | /zones/{zone_id}/security-center/insights/severity | Retrieves Zone Security Center Insight Counts by Severity |
| GET | /zones/{zone_id}/security-center/insights/type | Retrieves Zone Security Center Insight Counts by Type |
| PUT | /zones/{zone_id}/security-center/insights/{issue_id}/dismiss | Archives Zone Security Center Insight |
| DELETE | /zones/{zone_id}/security-center/securitytxt | Deletes security.txt |
| GET | /zones/{zone_id}/security-center/securitytxt | Retrieves security.txt |
| PUT | /zones/{zone_id}/security-center/securitytxt | Updates security.txt |
| GET | /zones/{zone_id}/settings | Get all zone settings |
| PATCH | /zones/{zone_id}/settings | Edit multiple zone settings |
| GET | /zones/{zone_id}/settings/aegis | Get aegis setting |
| PATCH | /zones/{zone_id}/settings/aegis | Change aegis setting |
| GET | /zones/{zone_id}/settings/fonts | Get Cloudflare Fonts setting |
| PATCH | /zones/{zone_id}/settings/fonts | Change Cloudflare Fonts setting |
| GET | /zones/{zone_id}/settings/origin_h2_max_streams | Get Origin H2 Max Streams Setting |
| PATCH | /zones/{zone_id}/settings/origin_h2_max_streams | Change Origin H2 Max Streams Setting |
| GET | /zones/{zone_id}/settings/origin_max_http_version | Get Origin Max HTTP Version Setting |
| PATCH | /zones/{zone_id}/settings/origin_max_http_version | Change Origin Max HTTP Version Setting |
| GET | /zones/{zone_id}/settings/rum | Get RUM status for a zone |
| PATCH | /zones/{zone_id}/settings/rum | Toggle RUM on/off for a zone |
| GET | /zones/{zone_id}/settings/speed_brain | Get Cloudflare Speed Brain setting |
| PATCH | /zones/{zone_id}/settings/speed_brain | Change Cloudflare Speed Brain setting |
| GET | /zones/{zone_id}/settings/ssl_automatic_mode | Get Automatic SSL/TLS enrollment status for the given zone |
| PATCH | /zones/{zone_id}/settings/ssl_automatic_mode | Patch Automatic SSL/TLS Enrollment status for given zone |
| GET | /zones/{zone_id}/settings/zaraz/config | Get Zaraz configuration |
| PUT | /zones/{zone_id}/settings/zaraz/config | Update Zaraz configuration |
| GET | /zones/{zone_id}/settings/zaraz/default | Get default Zaraz configuration |
| GET | /zones/{zone_id}/settings/zaraz/export | Export Zaraz configuration |
| GET | /zones/{zone_id}/settings/zaraz/history | List Zaraz historical configuration records |
| PUT | /zones/{zone_id}/settings/zaraz/history | Restore Zaraz historical configuration by ID |
| GET | /zones/{zone_id}/settings/zaraz/history/configs | Get Zaraz historical configurations by ID(s) |
| POST | /zones/{zone_id}/settings/zaraz/publish | Publish Zaraz preview configuration |
| GET | /zones/{zone_id}/settings/zaraz/workflow | Get Zaraz workflow |
| PUT | /zones/{zone_id}/settings/zaraz/workflow | Update Zaraz workflow |
| GET | /zones/{zone_id}/settings/{setting_id} | Get zone setting |
| PATCH | /zones/{zone_id}/settings/{setting_id} | Edit zone setting |
| GET | /zones/{zone_id}/smart_shield | Get Smart Shield Settings |
| PATCH | /zones/{zone_id}/smart_shield | Patch Smart Shield Settings |
| GET | /zones/{zone_id}/smart_shield/cache_reserve_clear | Get Cache Reserve Clear |
| POST | /zones/{zone_id}/smart_shield/cache_reserve_clear | Start Cache Reserve Clear |
| GET | /zones/{zone_id}/smart_shield/healthchecks | List Health Checks |
| POST | /zones/{zone_id}/smart_shield/healthchecks | Create Health Check |
| DELETE | /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id} | Delete Health Check |
| GET | /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id} | Health Check Details |
| PATCH | /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id} | Patch Health Check |
| PUT | /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id} | Update Health Check |
| GET | /zones/{zone_id}/snippets | List zone snippets |
| DELETE | /zones/{zone_id}/snippets/snippet_rules | Delete zone snippet rules |
| GET | /zones/{zone_id}/snippets/snippet_rules | List zone snippet rules |
| PUT | /zones/{zone_id}/snippets/snippet_rules | Update zone snippet rules |
| DELETE | /zones/{zone_id}/snippets/{snippet_name} | Delete a zone snippet |
| GET | /zones/{zone_id}/snippets/{snippet_name} | Get a zone snippet |
| PUT | /zones/{zone_id}/snippets/{snippet_name} | Update a zone snippet |
| GET | /zones/{zone_id}/snippets/{snippet_name}/content | Get a zone snippet content |
| GET | /zones/{zone_id}/spectrum/analytics/aggregate/current | Get current aggregated analytics |
| GET | /zones/{zone_id}/spectrum/analytics/events/bytime | Get analytics by time |
| GET | /zones/{zone_id}/spectrum/analytics/events/summary | Get analytics summary |
| GET | /zones/{zone_id}/spectrum/apps | List Spectrum applications |
| POST | /zones/{zone_id}/spectrum/apps | Create Spectrum application using a name for the origin |
| DELETE | /zones/{zone_id}/spectrum/apps/{app_id} | Delete Spectrum application |
| GET | /zones/{zone_id}/spectrum/apps/{app_id} | Get Spectrum application configuration |
| PUT | /zones/{zone_id}/spectrum/apps/{app_id} | Update Spectrum application configuration using a name for the origin |
| GET | /zones/{zone_id}/speed_api/availabilities | Get quota and availability |
| GET | /zones/{zone_id}/speed_api/pages | List tested webpages |
| DELETE | /zones/{zone_id}/speed_api/pages/{url}/tests | Delete all page tests |
| GET | /zones/{zone_id}/speed_api/pages/{url}/tests | List page test history |
| POST | /zones/{zone_id}/speed_api/pages/{url}/tests | Start page test |
| GET | /zones/{zone_id}/speed_api/pages/{url}/tests/{test_id} | Get a page test result |
| GET | /zones/{zone_id}/speed_api/pages/{url}/trend | List core web vital metrics trend |
| DELETE | /zones/{zone_id}/speed_api/schedule/{url} | Delete scheduled page test |
| GET | /zones/{zone_id}/speed_api/schedule/{url} | Get a page test schedule |
| POST | /zones/{zone_id}/speed_api/schedule/{url} | Create scheduled page test |
| POST | /zones/{zone_id}/ssl/analyze | Analyze Certificate |
| GET | /zones/{zone_id}/ssl/certificate_packs | List Certificate Packs |
| POST | /zones/{zone_id}/ssl/certificate_packs/order | Order Advanced Certificate Manager Certificate Pack |
| GET | /zones/{zone_id}/ssl/certificate_packs/quota | Get Certificate Pack Quotas |
| DELETE | /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id} | Delete Advanced Certificate Manager Certificate Pack |
| GET | /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id} | Get Certificate Pack |
| PATCH | /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id} | Restart Validation or Update Advanced Certificate Manager Certificate Pack |
| GET | /zones/{zone_id}/ssl/recommendation | SSL/TLS Recommendation |
| GET | /zones/{zone_id}/ssl/universal/settings | Universal SSL Settings Details |
| PATCH | /zones/{zone_id}/ssl/universal/settings | Edit Universal SSL Settings |
| GET | /zones/{zone_id}/ssl/verification | SSL Verification Details |
| PATCH | /zones/{zone_id}/ssl/verification/{certificate_pack_id} | Edit SSL Certificate Pack Validation Method |
| GET | /zones/{zone_id}/subscription | Zone Subscription Details |
| POST | /zones/{zone_id}/subscription | Create Zone Subscription |
| PUT | /zones/{zone_id}/subscription | Update Zone Subscription |
| GET | /zones/{zone_id}/token_validation/config | List token validation configurations |
| POST | /zones/{zone_id}/token_validation/config | Create a new Token Validation configuration |
| DELETE | /zones/{zone_id}/token_validation/config/{config_id} | Delete Token Configuration |
| GET | /zones/{zone_id}/token_validation/config/{config_id} | Get a single Token Configuration |
| PATCH | /zones/{zone_id}/token_validation/config/{config_id} | Edit an existing Token Configuration |
| PUT | /zones/{zone_id}/token_validation/config/{config_id}/credentials | Update Token Configuration credentials |
| GET | /zones/{zone_id}/token_validation/rules | List token validation rules |
| POST | /zones/{zone_id}/token_validation/rules | Create a token validation rule |
| PATCH | /zones/{zone_id}/token_validation/rules/bulk | Bulk edit token validation rules |
| POST | /zones/{zone_id}/token_validation/rules/bulk | Bulk create token validation rules |
| POST | /zones/{zone_id}/token_validation/rules/preview | Preview operations covered by a Token Validation rule |
| DELETE | /zones/{zone_id}/token_validation/rules/{rule_id} | Delete a zone token validation rule |
| GET | /zones/{zone_id}/token_validation/rules/{rule_id} | Get a zone token validation rule |
| PATCH | /zones/{zone_id}/token_validation/rules/{rule_id} | Edit a zone token validation rule |
| DELETE | /zones/{zone_id}/url_normalization | Delete URL Normalization settings |
| GET | /zones/{zone_id}/url_normalization | Get URL Normalization settings |
| PUT | /zones/{zone_id}/url_normalization | Update URL Normalization settings |
| GET | /zones/{zone_id}/waiting_rooms | List waiting rooms for zone |
| POST | /zones/{zone_id}/waiting_rooms | Create waiting room |
| POST | /zones/{zone_id}/waiting_rooms/preview | Create a custom waiting room page preview |
| GET | /zones/{zone_id}/waiting_rooms/settings | Get zone-level Waiting Room settings |
| PATCH | /zones/{zone_id}/waiting_rooms/settings | Patch zone-level Waiting Room settings |
| PUT | /zones/{zone_id}/waiting_rooms/settings | Update zone-level Waiting Room settings |
| DELETE | /zones/{zone_id}/waiting_rooms/{waiting_room_id} | Delete waiting room |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id} | Waiting room details |
| PATCH | /zones/{zone_id}/waiting_rooms/{waiting_room_id} | Patch waiting room |
| PUT | /zones/{zone_id}/waiting_rooms/{waiting_room_id} | Update waiting room |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events | List events |
| POST | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events | Create event |
| DELETE | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id} | Delete event |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id} | Event details |
| PATCH | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id} | Patch event |
| PUT | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id} | Update event |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}/details | Preview active event details |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules | List Waiting Room Rules |
| POST | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules | Create Waiting Room Rule |
| PUT | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules | Replace Waiting Room Rules |
| DELETE | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules/{rule_id} | Delete Waiting Room Rule |
| PATCH | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules/{rule_id} | Patch Waiting Room Rule |
| GET | /zones/{zone_id}/waiting_rooms/{waiting_room_id}/status | Get waiting room status |
| GET | /zones/{zone_id}/web3/hostnames | List Web3 Hostnames |
| POST | /zones/{zone_id}/web3/hostnames | Create Web3 Hostname |
| DELETE | /zones/{zone_id}/web3/hostnames/{identifier} | Delete Web3 Hostname |
| GET | /zones/{zone_id}/web3/hostnames/{identifier} | Web3 Hostname Details |
| PATCH | /zones/{zone_id}/web3/hostnames/{identifier} | Edit Web3 Hostname |
| GET | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list | IPFS Universal Path Gateway Content List Details |
| PUT | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list | Update IPFS Universal Path Gateway Content List |
| GET | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries | List IPFS Universal Path Gateway Content List Entries |
| POST | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries | Create IPFS Universal Path Gateway Content List Entry |
| DELETE | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier} | Delete IPFS Universal Path Gateway Content List Entry |
| GET | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier} | IPFS Universal Path Gateway Content List Entry Details |
| PUT | /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier} | Edit IPFS Universal Path Gateway Content List Entry |
| GET | /zones/{zone_id}/workers/routes | List Routes |
| POST | /zones/{zone_id}/workers/routes | Create Route |
| DELETE | /zones/{zone_id}/workers/routes/{route_id} | Delete Route |
| GET | /zones/{zone_id}/workers/routes/{route_id} | Get Route |
| PUT | /zones/{zone_id}/workers/routes/{route_id} | Update Route |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all accounts?" -> GET /accounts
- "Create a account?" -> POST /accounts
- "Create a move?" -> POST /accounts/move
- "List all applications?" -> GET /accounts/{accountId}/resource-library/applications
- "Create a application?" -> POST /accounts/{accountId}/resource-library/applications
- "Get application details?" -> GET /accounts/{accountId}/resource-library/applications/{id}
- "Partially update a application?" -> PATCH /accounts/{accountId}/resource-library/applications/{id}
- "List all categories?" -> GET /accounts/{accountId}/resource-library/categories
- "Get category details?" -> GET /accounts/{accountId}/resource-library/categories/{id}
- "List all custom_pages?" -> GET /accounts/{account_identifier}/custom_pages
- "Get custom_page details?" -> GET /accounts/{account_identifier}/custom_pages/{identifier}
- "Update a custom_page?" -> PUT /accounts/{account_identifier}/custom_pages/{identifier}
- "Delete a account?" -> DELETE /accounts/{account_id}
- "Get account details?" -> GET /accounts/{account_id}
- "Update a account?" -> PUT /accounts/{account_id}
- "List all abuse-reports?" -> GET /accounts/{account_id}/abuse-reports
- "List all emails?" -> GET /accounts/{account_id}/abuse-reports/{report_id}/emails
- "List all mitigations?" -> GET /accounts/{account_id}/abuse-reports/{report_id}/mitigations
- "Create a appeal?" -> POST /accounts/{account_id}/abuse-reports/{report_id}/mitigations/appeal
- "Get abuse-report details?" -> GET /accounts/{account_id}/abuse-reports/{report_param}
- "Search portals?" -> GET /accounts/{account_id}/access/ai-controls/mcp/portals
- "Create a portal?" -> POST /accounts/{account_id}/access/ai-controls/mcp/portals
- "Delete a portal?" -> DELETE /accounts/{account_id}/access/ai-controls/mcp/portals/{id}
- "Get portal details?" -> GET /accounts/{account_id}/access/ai-controls/mcp/portals/{id}
- "Update a portal?" -> PUT /accounts/{account_id}/access/ai-controls/mcp/portals/{id}
- "Search servers?" -> GET /accounts/{account_id}/access/ai-controls/mcp/servers
- "Create a server?" -> POST /accounts/{account_id}/access/ai-controls/mcp/servers
- "Delete a server?" -> DELETE /accounts/{account_id}/access/ai-controls/mcp/servers/{id}
- "Get server details?" -> GET /accounts/{account_id}/access/ai-controls/mcp/servers/{id}
- "Update a server?" -> PUT /accounts/{account_id}/access/ai-controls/mcp/servers/{id}
- "Create a sync?" -> POST /accounts/{account_id}/access/ai-controls/mcp/servers/{id}/sync
- "Search apps?" -> GET /accounts/{account_id}/access/apps
- "Create a app?" -> POST /accounts/{account_id}/access/apps
- "List all ca?" -> GET /accounts/{account_id}/access/apps/ca
- "Delete a app?" -> DELETE /accounts/{account_id}/access/apps/{app_id}
- "Get app details?" -> GET /accounts/{account_id}/access/apps/{app_id}
- "Update a app?" -> PUT /accounts/{account_id}/access/apps/{app_id}
- "List all ca?" -> GET /accounts/{account_id}/access/apps/{app_id}/ca
- "Create a ca?" -> POST /accounts/{account_id}/access/apps/{app_id}/ca
- "List all policies?" -> GET /accounts/{account_id}/access/apps/{app_id}/policies
- "Create a policy?" -> POST /accounts/{account_id}/access/apps/{app_id}/policies
- "Delete a policy?" -> DELETE /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id}
- "Get policy details?" -> GET /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id}
- "Update a policy?" -> PUT /accounts/{account_id}/access/apps/{app_id}/policies/{policy_id}
- "Create a revoke_token?" -> POST /accounts/{account_id}/access/apps/{app_id}/revoke_tokens
- "List all user_policy_checks?" -> GET /accounts/{account_id}/access/apps/{app_id}/user_policy_checks
- "List all bookmarks?" -> GET /accounts/{account_id}/access/bookmarks
- "Delete a bookmark?" -> DELETE /accounts/{account_id}/access/bookmarks/{bookmark_id}
- "Get bookmark details?" -> GET /accounts/{account_id}/access/bookmarks/{bookmark_id}
- "Update a bookmark?" -> PUT /accounts/{account_id}/access/bookmarks/{bookmark_id}
- "List all certificates?" -> GET /accounts/{account_id}/access/certificates
- "Create a certificate?" -> POST /accounts/{account_id}/access/certificates
- "List all settings?" -> GET /accounts/{account_id}/access/certificates/settings
- "Delete a certificate?" -> DELETE /accounts/{account_id}/access/certificates/{certificate_id}
- "Get certificate details?" -> GET /accounts/{account_id}/access/certificates/{certificate_id}
- "Update a certificate?" -> PUT /accounts/{account_id}/access/certificates/{certificate_id}
- "List all custom_pages?" -> GET /accounts/{account_id}/access/custom_pages
- "Create a custom_page?" -> POST /accounts/{account_id}/access/custom_pages
- "Delete a custom_page?" -> DELETE /accounts/{account_id}/access/custom_pages/{custom_page_id}
- "Get custom_page details?" -> GET /accounts/{account_id}/access/custom_pages/{custom_page_id}
- "Update a custom_page?" -> PUT /accounts/{account_id}/access/custom_pages/{custom_page_id}
- "List all gateway_ca?" -> GET /accounts/{account_id}/access/gateway_ca
- "Create a gateway_ca?" -> POST /accounts/{account_id}/access/gateway_ca
- "Delete a gateway_ca?" -> DELETE /accounts/{account_id}/access/gateway_ca/{certificate_id}
- "Search groups?" -> GET /accounts/{account_id}/access/groups
- "Create a group?" -> POST /accounts/{account_id}/access/groups
- "Delete a group?" -> DELETE /accounts/{account_id}/access/groups/{group_id}
- "Get group details?" -> GET /accounts/{account_id}/access/groups/{group_id}
- "Update a group?" -> PUT /accounts/{account_id}/access/groups/{group_id}
- "List all identity_providers?" -> GET /accounts/{account_id}/access/identity_providers
- "Create a identity_provider?" -> POST /accounts/{account_id}/access/identity_providers
- "Delete a identity_provider?" -> DELETE /accounts/{account_id}/access/identity_providers/{identity_provider_id}
- "Get identity_provider details?" -> GET /accounts/{account_id}/access/identity_providers/{identity_provider_id}
- "Update a identity_provider?" -> PUT /accounts/{account_id}/access/identity_providers/{identity_provider_id}
- "List all groups?" -> GET /accounts/{account_id}/access/identity_providers/{identity_provider_id}/scim/groups
- "List all users?" -> GET /accounts/{account_id}/access/identity_providers/{identity_provider_id}/scim/users
- "List all keys?" -> GET /accounts/{account_id}/access/keys
- "Create a rotate?" -> POST /accounts/{account_id}/access/keys/rotate
- "List all access_requests?" -> GET /accounts/{account_id}/access/logs/access_requests
- "List all updates?" -> GET /accounts/{account_id}/access/logs/scim/updates
- "List all organizations?" -> GET /accounts/{account_id}/access/organizations
- "Create a organization?" -> POST /accounts/{account_id}/access/organizations
- "List all doh?" -> GET /accounts/{account_id}/access/organizations/doh
- "Create a revoke_user?" -> POST /accounts/{account_id}/access/organizations/revoke_user
- "List all policies?" -> GET /accounts/{account_id}/access/policies
- "Create a policy?" -> POST /accounts/{account_id}/access/policies
- "Delete a policy?" -> DELETE /accounts/{account_id}/access/policies/{policy_id}
- "Get policy details?" -> GET /accounts/{account_id}/access/policies/{policy_id}
- "Update a policy?" -> PUT /accounts/{account_id}/access/policies/{policy_id}
- "Create a policy-test?" -> POST /accounts/{account_id}/access/policy-tests
- "Get policy-test details?" -> GET /accounts/{account_id}/access/policy-tests/{policy_test_id}
- "List all users?" -> GET /accounts/{account_id}/access/policy-tests/{policy_test_id}/users
- "Search service_tokens?" -> GET /accounts/{account_id}/access/service_tokens
- "Create a service_token?" -> POST /accounts/{account_id}/access/service_tokens
- "Delete a service_token?" -> DELETE /accounts/{account_id}/access/service_tokens/{service_token_id}
- "Get service_token details?" -> GET /accounts/{account_id}/access/service_tokens/{service_token_id}
- "Update a service_token?" -> PUT /accounts/{account_id}/access/service_tokens/{service_token_id}
- "Create a refresh?" -> POST /accounts/{account_id}/access/service_tokens/{service_token_id}/refresh
- "Create a rotate?" -> POST /accounts/{account_id}/access/service_tokens/{service_token_id}/rotate
- "List all tags?" -> GET /accounts/{account_id}/access/tags
- "Create a tag?" -> POST /accounts/{account_id}/access/tags
- "Delete a tag?" -> DELETE /accounts/{account_id}/access/tags/{tag_name}
- "Get tag details?" -> GET /accounts/{account_id}/access/tags/{tag_name}
- "Update a tag?" -> PUT /accounts/{account_id}/access/tags/{tag_name}
- "Search users?" -> GET /accounts/{account_id}/access/users
- "Create a user?" -> POST /accounts/{account_id}/access/users
- "Delete a user?" -> DELETE /accounts/{account_id}/access/users/{user_id}
- "Get user details?" -> GET /accounts/{account_id}/access/users/{user_id}
- "Update a user?" -> PUT /accounts/{account_id}/access/users/{user_id}
- "List all active_sessions?" -> GET /accounts/{account_id}/access/users/{user_id}/active_sessions
- "Get active_session details?" -> GET /accounts/{account_id}/access/users/{user_id}/active_sessions/{nonce}
- "List all failed_logins?" -> GET /accounts/{account_id}/access/users/{user_id}/failed_logins
- "List all last_seen_identity?" -> GET /accounts/{account_id}/access/users/{user_id}/last_seen_identity
- "Delete a mfa_authenticator?" -> DELETE /accounts/{account_id}/access/users/{user_id}/mfa_authenticators/{authenticator_id}
- "List all address_maps?" -> GET /accounts/{account_id}/addressing/address_maps
- "Create a address_map?" -> POST /accounts/{account_id}/addressing/address_maps
- "Delete a address_map?" -> DELETE /accounts/{account_id}/addressing/address_maps/{address_map_id}
- "Get address_map details?" -> GET /accounts/{account_id}/addressing/address_maps/{address_map_id}
- "Partially update a address_map?" -> PATCH /accounts/{account_id}/addressing/address_maps/{address_map_id}
- "Delete a account?" -> DELETE /accounts/{account_id}/addressing/address_maps/{address_map_id}/accounts/{account_id}
- "Update a account?" -> PUT /accounts/{account_id}/addressing/address_maps/{address_map_id}/accounts/{account_id}
- "Delete a ip?" -> DELETE /accounts/{account_id}/addressing/address_maps/{address_map_id}/ips/{ip_address}
- "Update a ip?" -> PUT /accounts/{account_id}/addressing/address_maps/{address_map_id}/ips/{ip_address}
- "Delete a zone?" -> DELETE /accounts/{account_id}/addressing/address_maps/{address_map_id}/zones/{zone_id}
- "Update a zone?" -> PUT /accounts/{account_id}/addressing/address_maps/{address_map_id}/zones/{zone_id}
- "List all leases?" -> GET /accounts/{account_id}/addressing/leases
- "Create a loa_document?" -> POST /accounts/{account_id}/addressing/loa_documents
- "List all download?" -> GET /accounts/{account_id}/addressing/loa_documents/{loa_document_id}/download
- "List all prefixes?" -> GET /accounts/{account_id}/addressing/prefixes
- "Create a prefixe?" -> POST /accounts/{account_id}/addressing/prefixes
- "Delete a prefixe?" -> DELETE /accounts/{account_id}/addressing/prefixes/{prefix_id}
- "Get prefixe details?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}
- "Partially update a prefixe?" -> PATCH /accounts/{account_id}/addressing/prefixes/{prefix_id}
- "List all prefixes?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes
- "Create a prefixe?" -> POST /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes
- "Delete a prefixe?" -> DELETE /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id}
- "Get prefixe details?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id}
- "Partially update a prefixe?" -> PATCH /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/prefixes/{bgp_prefix_id}
- "List all status?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/bgp/status
- "List all bindings?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings
- "Create a binding?" -> POST /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings
- "Delete a binding?" -> DELETE /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings/{binding_id}
- "Get binding details?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/bindings/{binding_id}
- "List all delegations?" -> GET /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations
- "Create a delegation?" -> POST /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations
- "Delete a delegation?" -> DELETE /accounts/{account_id}/addressing/prefixes/{prefix_id}/delegations/{delegation_id}
- "Create a validate?" -> POST /accounts/{account_id}/addressing/prefixes/{prefix_id}/validate
- "List all regions?" -> GET /accounts/{account_id}/addressing/regional_hostnames/regions
- "List all services?" -> GET /accounts/{account_id}/addressing/services
- "List all evaluation-types?" -> GET /accounts/{account_id}/ai-gateway/evaluation-types
- "Search gateways?" -> GET /accounts/{account_id}/ai-gateway/gateways
- "Create a gateway?" -> POST /accounts/{account_id}/ai-gateway/gateways
- "Search datasets?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets
- "Create a dataset?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets
- "Delete a dataset?" -> DELETE /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id}
- "Get dataset details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id}
- "Update a dataset?" -> PUT /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/datasets/{id}
- "Search evaluations?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations
- "Create a evaluation?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations
- "Delete a evaluation?" -> DELETE /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations/{id}
- "Get evaluation details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/evaluations/{id}
- "Search logs?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs
- "Get log details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}
- "Partially update a log?" -> PATCH /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}
- "List all request?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}/request
- "List all response?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/logs/{id}/response
- "List all provider_configs?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs
- "Create a provider_config?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs
- "Delete a provider_config?" -> DELETE /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs/{id}
- "Update a provider_config?" -> PUT /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/provider_configs/{id}
- "List all routes?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes
- "Create a route?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes
- "Delete a route?" -> DELETE /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}
- "Get route details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}
- "Partially update a route?" -> PATCH /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}
- "List all deployments?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/deployments
- "Create a deployment?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/deployments
- "List all versions?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions
- "Create a version?" -> POST /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions
- "Get version details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/routes/{id}/versions/{version_id}
- "Get url details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{gateway_id}/url/{provider}
- "Delete a gateway?" -> DELETE /accounts/{account_id}/ai-gateway/gateways/{id}
- "Get gateway details?" -> GET /accounts/{account_id}/ai-gateway/gateways/{id}
- "Update a gateway?" -> PUT /accounts/{account_id}/ai-gateway/gateways/{id}
- "Search instances?" -> GET /accounts/{account_id}/ai-search/instances
- "Create a instance?" -> POST /accounts/{account_id}/ai-search/instances
- "Delete a instance?" -> DELETE /accounts/{account_id}/ai-search/instances/{id}
- "Get instance details?" -> GET /accounts/{account_id}/ai-search/instances/{id}
- "Update a instance?" -> PUT /accounts/{account_id}/ai-search/instances/{id}
- "Create a completion?" -> POST /accounts/{account_id}/ai-search/instances/{id}/chat/completions
- "Search items?" -> GET /accounts/{account_id}/ai-search/instances/{id}/items
- "Get item details?" -> GET /accounts/{account_id}/ai-search/instances/{id}/items/{item_id}
- "Partially update a item?" -> PATCH /accounts/{account_id}/ai-search/instances/{id}/items/{item_id}
- "List all jobs?" -> GET /accounts/{account_id}/ai-search/instances/{id}/jobs
- "Create a job?" -> POST /accounts/{account_id}/ai-search/instances/{id}/jobs
- "Get job details?" -> GET /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id}
- "Partially update a job?" -> PATCH /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id}
- "List all logs?" -> GET /accounts/{account_id}/ai-search/instances/{id}/jobs/{job_id}/logs
- "Create a search?" -> POST /accounts/{account_id}/ai-search/instances/{id}/search
- "List all stats?" -> GET /accounts/{account_id}/ai-search/instances/{id}/stats
- "List all tokens?" -> GET /accounts/{account_id}/ai-search/tokens
- "Create a token?" -> POST /accounts/{account_id}/ai-search/tokens
- "Delete a token?" -> DELETE /accounts/{account_id}/ai-search/tokens/{id}
- "Get token details?" -> GET /accounts/{account_id}/ai-search/tokens/{id}
- "Update a token?" -> PUT /accounts/{account_id}/ai-search/tokens/{id}
- "List all search?" -> GET /accounts/{account_id}/ai/authors/search
- "List all finetunes?" -> GET /accounts/{account_id}/ai/finetunes
- "Create a finetune?" -> POST /accounts/{account_id}/ai/finetunes
- "List all public?" -> GET /accounts/{account_id}/ai/finetunes/public
- "Create a finetune-asset?" -> POST /accounts/{account_id}/ai/finetunes/{finetune_id}/finetune-assets
- "List all schema?" -> GET /accounts/{account_id}/ai/models/schema
- "Search search?" -> GET /accounts/{account_id}/ai/models/search
- "Create a indictrans2-en-indic-1B?" -> POST /accounts/{account_id}/ai/run/@cf/ai4bharat/indictrans2-en-indic-1B
- "Create a omni-indictrans2-en-indic-1b?" -> POST /accounts/{account_id}/ai/run/@cf/ai4bharat/omni-indictrans2-en-indic-1b
- "Create a gemma-sea-lion-v4-27b-it?" -> POST /accounts/{account_id}/ai/run/@cf/aisingapore/gemma-sea-lion-v4-27b-it
- "Create a bge-base-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/bge-base-en-v1.5
- "Create a bge-large-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/bge-large-en-v1.5
- "Create a bge-m3?" -> POST /accounts/{account_id}/ai/run/@cf/baai/bge-m3
- "Create a bge-reranker-base?" -> POST /accounts/{account_id}/ai/run/@cf/baai/bge-reranker-base
- "Create a bge-small-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/bge-small-en-v1.5
- "Create a omni-bge-base-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/omni-bge-base-en-v1.5
- "Create a omni-bge-large-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/omni-bge-large-en-v1.5
- "Create a omni-bge-m3?" -> POST /accounts/{account_id}/ai/run/@cf/baai/omni-bge-m3
- "Create a omni-bge-small-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/omni-bge-small-en-v1.5
- "Create a ray-bge-large-en-v1.5?" -> POST /accounts/{account_id}/ai/run/@cf/baai/ray-bge-large-en-v1.5
- "Create a flux-1-schnell?" -> POST /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-1-schnell
- "Create a flux-2-dev?" -> POST /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-dev
- "Create a flux-2-klein-4b?" -> POST /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-klein-4b
- "Create a flux-2-klein-9b?" -> POST /accounts/{account_id}/ai/run/@cf/black-forest-labs/flux-2-klein-9b
- "Create a stable-diffusion-xl-lightning?" -> POST /accounts/{account_id}/ai/run/@cf/bytedance/stable-diffusion-xl-lightning
- "List all aura?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura
- "List all aura-1?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura-1
- "Create a aura-1?" -> POST /accounts/{account_id}/ai/run/@cf/deepgram/aura-1
- "List all aura-1-internal?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura-1-internal
- "List all aura-2?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura-2
- "List all aura-2-en?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-en
- "Create a aura-2-en?" -> POST /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-en
- "List all aura-2-es?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-es
- "Create a aura-2-e?" -> POST /accounts/{account_id}/ai/run/@cf/deepgram/aura-2-es
- "List all flux?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/flux
- "Create a flux?" -> POST /accounts/{account_id}/ai/run/@cf/deepgram/flux
- "List all nova-3?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/nova-3
- "Create a nova-3?" -> POST /accounts/{account_id}/ai/run/@cf/deepgram/nova-3
- "List all nova-3-internal?" -> GET /accounts/{account_id}/ai/run/@cf/deepgram/nova-3-internal
- "Create a deepseek-math-7b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/deepseek-ai/deepseek-math-7b-instruct
- "Create a deepseek-r1-distill-qwen-32b?" -> POST /accounts/{account_id}/ai/run/@cf/deepseek-ai/deepseek-r1-distill-qwen-32b
- "Create a sqlcoder-7b-2?" -> POST /accounts/{account_id}/ai/run/@cf/defog/sqlcoder-7b-2
- "Create a bart-large-cnn?" -> POST /accounts/{account_id}/ai/run/@cf/facebook/bart-large-cnn
- "Create a omni-bart-large-cnn?" -> POST /accounts/{account_id}/ai/run/@cf/facebook/omni-bart-large-cnn
- "Create a omni-detr-resnet-50?" -> POST /accounts/{account_id}/ai/run/@cf/facebook/omni-detr-resnet-50
- "Create a una-cybertron-7b-v2-bf16?" -> POST /accounts/{account_id}/ai/run/@cf/fblgit/una-cybertron-7b-v2-bf16
- "Create a embeddinggemma-300m?" -> POST /accounts/{account_id}/ai/run/@cf/google/embeddinggemma-300m
- "Create a gemma-2b-it-lora?" -> POST /accounts/{account_id}/ai/run/@cf/google/gemma-2b-it-lora
- "Create a gemma-3-12b-it?" -> POST /accounts/{account_id}/ai/run/@cf/google/gemma-3-12b-it
- "Create a gemma-7b-it-lora?" -> POST /accounts/{account_id}/ai/run/@cf/google/gemma-7b-it-lora
- "Create a omni-embeddinggemma-300m?" -> POST /accounts/{account_id}/ai/run/@cf/google/omni-embeddinggemma-300m
- "Create a distilbert-sst-2-int8?" -> POST /accounts/{account_id}/ai/run/@cf/huggingface/distilbert-sst-2-int8
- "Create a omni-distilbert-sst-2-int8?" -> POST /accounts/{account_id}/ai/run/@cf/huggingface/omni-distilbert-sst-2-int8
- "Create a granite-4.0-h-micro?" -> POST /accounts/{account_id}/ai/run/@cf/ibm-granite/granite-4.0-h-micro
- "Create a lucid-origin?" -> POST /accounts/{account_id}/ai/run/@cf/leonardo/lucid-origin
- "Create a phoenix-1.0?" -> POST /accounts/{account_id}/ai/run/@cf/leonardo/phoenix-1.0
- "Create a dreamshaper-8-lcm?" -> POST /accounts/{account_id}/ai/run/@cf/lykon/dreamshaper-8-lcm
- "Create a llama-2-7b-chat-hf-lora?" -> POST /accounts/{account_id}/ai/run/@cf/meta-llama/llama-2-7b-chat-hf-lora
- "Create a llama-2-7b-chat-fp16?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-2-7b-chat-fp16
- "Create a llama-2-7b-chat-int8?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-2-7b-chat-int8
- "Create a llama-3-8b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3-8b-instruct
- "Create a llama-3-8b-instruct-awq?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3-8b-instruct-awq
- "Create a llama-3.1-70b-instruct-fp8-fast?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-70b-instruct-fp8-fast
- "Create a llama-3.1-8b-instruct-awq?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-awq
- "Create a llama-3.1-8b-instruct-fp8?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-fp8
- "Create a llama-3.1-8b-instruct-fp8-fast?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.1-8b-instruct-fp8-fast
- "Create a llama-3.2-11b-vision-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-11b-vision-instruct
- "Create a llama-3.2-1b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-1b-instruct
- "Create a llama-3.2-3b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.2-3b-instruct
- "Create a llama-3.3-70b-instruct-fp8-fast?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-3.3-70b-instruct-fp8-fast
- "Create a llama-4-scout-17b-16e-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-4-scout-17b-16e-instruct
- "Create a llama-guard-3-8b?" -> POST /accounts/{account_id}/ai/run/@cf/meta/llama-guard-3-8b
- "Create a m2m100-1.2b?" -> POST /accounts/{account_id}/ai/run/@cf/meta/m2m100-1.2b
- "Create a phi-2?" -> POST /accounts/{account_id}/ai/run/@cf/microsoft/phi-2
- "Create a resnet-50?" -> POST /accounts/{account_id}/ai/run/@cf/microsoft/resnet-50
- "Create a mistral-7b-instruct-v0.1?" -> POST /accounts/{account_id}/ai/run/@cf/mistral/mistral-7b-instruct-v0.1
- "Create a mistral-7b-instruct-v0.2-lora?" -> POST /accounts/{account_id}/ai/run/@cf/mistral/mistral-7b-instruct-v0.2-lora
- "Create a mistral-small-3.1-24b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/mistralai/mistral-small-3.1-24b-instruct
- "Create a melott?" -> POST /accounts/{account_id}/ai/run/@cf/myshell-ai/melotts
- "Create a gpt-oss-120b?" -> POST /accounts/{account_id}/ai/run/@cf/openai/gpt-oss-120b
- "Create a gpt-oss-20b?" -> POST /accounts/{account_id}/ai/run/@cf/openai/gpt-oss-20b
- "Create a whisper?" -> POST /accounts/{account_id}/ai/run/@cf/openai/whisper
- "Create a whisper-large-v3-turbo?" -> POST /accounts/{account_id}/ai/run/@cf/openai/whisper-large-v3-turbo
- "Create a whisper-tiny-en?" -> POST /accounts/{account_id}/ai/run/@cf/openai/whisper-tiny-en
- "Create a openchat-3.5-0106?" -> POST /accounts/{account_id}/ai/run/@cf/openchat/openchat-3.5-0106
- "Create a plamo-embedding-1b?" -> POST /accounts/{account_id}/ai/run/@cf/pfnet/plamo-embedding-1b
- "List all smart-turn-v2?" -> GET /accounts/{account_id}/ai/run/@cf/pipecat-ai/smart-turn-v2
- "List all smart-turn-v3?" -> GET /accounts/{account_id}/ai/run/@cf/pipecat-ai/smart-turn-v3
- "Create a qwen1.5-0.5b-chat?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-0.5b-chat
- "Create a qwen1.5-1.8b-chat?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-1.8b-chat
- "Create a qwen1.5-14b-chat-awq?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-14b-chat-awq
- "Create a qwen1.5-7b-chat-awq?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen1.5-7b-chat-awq
- "Create a qwen2.5-coder-32b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen2.5-coder-32b-instruct
- "Create a qwen3-30b-a3b-fp8?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen3-30b-a3b-fp8
- "Create a qwen3-embedding-0.6b?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwen3-embedding-0.6b
- "Create a qwq-32b?" -> POST /accounts/{account_id}/ai/run/@cf/qwen/qwq-32b
- "Create a stable-diffusion-v1-5-img2img?" -> POST /accounts/{account_id}/ai/run/@cf/runwayml/stable-diffusion-v1-5-img2img
- "Create a stable-diffusion-v1-5-inpainting?" -> POST /accounts/{account_id}/ai/run/@cf/runwayml/stable-diffusion-v1-5-inpainting
- "Create a stable-diffusion-xl-base-1.0?" -> POST /accounts/{account_id}/ai/run/@cf/stabilityai/stable-diffusion-xl-base-1.0
- "List all test-pipe-http?" -> GET /accounts/{account_id}/ai/run/@cf/sven/test-pipe-http
- "List all hello-world-cog?" -> GET /accounts/{account_id}/ai/run/@cf/test/hello-world-cog
- "Create a discolm-german-7b-v1-awq?" -> POST /accounts/{account_id}/ai/run/@cf/thebloke/discolm-german-7b-v1-awq
- "Create a falcon-7b-instruct?" -> POST /accounts/{account_id}/ai/run/@cf/tiiuae/falcon-7b-instruct
- "Create a tinyllama-1.1b-chat-v1.0?" -> POST /accounts/{account_id}/ai/run/@cf/tinyllama/tinyllama-1.1b-chat-v1.0
- "Create a glm-4.7-flash?" -> POST /accounts/{account_id}/ai/run/@cf/zai-org/glm-4.7-flash
- "Create a gemma-7b-it?" -> POST /accounts/{account_id}/ai/run/@hf/google/gemma-7b-it
- "Create a mistral-7b-instruct-v0.2?" -> POST /accounts/{account_id}/ai/run/@hf/mistral/mistral-7b-instruct-v0.2
- "Create a starling-lm-7b-beta?" -> POST /accounts/{account_id}/ai/run/@hf/nexusflow/starling-lm-7b-beta
- "Create a hermes-2-pro-mistral-7b?" -> POST /accounts/{account_id}/ai/run/@hf/nousresearch/hermes-2-pro-mistral-7b
- "Create a deepseek-coder-6.7b-base-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/deepseek-coder-6.7b-base-awq
- "Create a deepseek-coder-6.7b-instruct-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/deepseek-coder-6.7b-instruct-awq
- "Create a llama-2-13b-chat-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/llama-2-13b-chat-awq
- "Create a mistral-7b-instruct-v0.1-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/mistral-7b-instruct-v0.1-awq
- "Create a neural-chat-7b-v3-1-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/neural-chat-7b-v3-1-awq
- "Create a openhermes-2.5-mistral-7b-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/openhermes-2.5-mistral-7b-awq
- "Create a zephyr-7b-beta-awq?" -> POST /accounts/{account_id}/ai/run/@hf/thebloke/zephyr-7b-beta-awq
- "List all search?" -> GET /accounts/{account_id}/ai/tasks/search
- "Create a tomarkdown?" -> POST /accounts/{account_id}/ai/tomarkdown
- "List all supported?" -> GET /accounts/{account_id}/ai/tomarkdown/supported
- "List all available_alerts?" -> GET /accounts/{account_id}/alerting/v3/available_alerts
- "List all eligible?" -> GET /accounts/{account_id}/alerting/v3/destinations/eligible
- "List all pagerduty?" -> GET /accounts/{account_id}/alerting/v3/destinations/pagerduty
- "Create a connect?" -> POST /accounts/{account_id}/alerting/v3/destinations/pagerduty/connect
- "Get connect details?" -> GET /accounts/{account_id}/alerting/v3/destinations/pagerduty/connect/{token_id}
- "List all webhooks?" -> GET /accounts/{account_id}/alerting/v3/destinations/webhooks
- "Create a webhook?" -> POST /accounts/{account_id}/alerting/v3/destinations/webhooks
- "Delete a webhook?" -> DELETE /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id}
- "Get webhook details?" -> GET /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id}
- "Update a webhook?" -> PUT /accounts/{account_id}/alerting/v3/destinations/webhooks/{webhook_id}
- "List all history?" -> GET /accounts/{account_id}/alerting/v3/history
- "List all policies?" -> GET /accounts/{account_id}/alerting/v3/policies
- "Create a policy?" -> POST /accounts/{account_id}/alerting/v3/policies
- "Delete a policy?" -> DELETE /accounts/{account_id}/alerting/v3/policies/{policy_id}
- "Get policy details?" -> GET /accounts/{account_id}/alerting/v3/policies/{policy_id}
- "Update a policy?" -> PUT /accounts/{account_id}/alerting/v3/policies/{policy_id}
- "List all silences?" -> GET /accounts/{account_id}/alerting/v3/silences
- "Create a silence?" -> POST /accounts/{account_id}/alerting/v3/silences
- "Delete a silence?" -> DELETE /accounts/{account_id}/alerting/v3/silences/{silence_id}
- "Get silence details?" -> GET /accounts/{account_id}/alerting/v3/silences/{silence_id}
- "List all audit_logs?" -> GET /accounts/{account_id}/audit_logs
- "Create a ai-search?" -> POST /accounts/{account_id}/autorag/rags/{id}/ai-search
- "Search files?" -> GET /accounts/{account_id}/autorag/rags/{id}/files
- "List all jobs?" -> GET /accounts/{account_id}/autorag/rags/{id}/jobs
- "Get job details?" -> GET /accounts/{account_id}/autorag/rags/{id}/jobs/{job_id}
- "List all logs?" -> GET /accounts/{account_id}/autorag/rags/{id}/jobs/{job_id}/logs
- "Create a search?" -> POST /accounts/{account_id}/autorag/rags/{id}/search
- "List all profile?" -> GET /accounts/{account_id}/billing/profile
- "List all day_report?" -> GET /accounts/{account_id}/botnet_feed/asn/{asn_id}/day_report
- "List all full_report?" -> GET /accounts/{account_id}/botnet_feed/asn/{asn_id}/full_report
- "List all asn?" -> GET /accounts/{account_id}/botnet_feed/configs/asn
- "Delete a asn?" -> DELETE /accounts/{account_id}/botnet_feed/configs/asn/{asn_id}
- "List all alerts?" -> GET /accounts/{account_id}/brand-protection/alerts
- "List all brands?" -> GET /accounts/{account_id}/brand-protection/brands
- "Create a brand?" -> POST /accounts/{account_id}/brand-protection/brands
- "List all patterns?" -> GET /accounts/{account_id}/brand-protection/brands/patterns
- "Create a pattern?" -> POST /accounts/{account_id}/brand-protection/brands/patterns
- "List all domain-info?" -> GET /accounts/{account_id}/brand-protection/domain-info
- "List all logo-matches?" -> GET /accounts/{account_id}/brand-protection/logo-matches
- "List all download?" -> GET /accounts/{account_id}/brand-protection/logo-matches/download
- "List all logos?" -> GET /accounts/{account_id}/brand-protection/logos
- "Create a logo?" -> POST /accounts/{account_id}/brand-protection/logos
- "Delete a logo?" -> DELETE /accounts/{account_id}/brand-protection/logos/{logo_id}
- "Get logo details?" -> GET /accounts/{account_id}/brand-protection/logos/{logo_id}
- "List all matches?" -> GET /accounts/{account_id}/brand-protection/matches
- "List all download?" -> GET /accounts/{account_id}/brand-protection/matches/download
- "List all queries?" -> GET /accounts/{account_id}/brand-protection/queries
- "Create a query?" -> POST /accounts/{account_id}/brand-protection/queries
- "Create a bulk?" -> POST /accounts/{account_id}/brand-protection/queries/bulk
- "List all recent-submissions?" -> GET /accounts/{account_id}/brand-protection/recent-submissions
- "Create a scan-logo?" -> POST /accounts/{account_id}/brand-protection/scan-logo
- "Create a scan-page?" -> POST /accounts/{account_id}/brand-protection/scan-page
- "Create a search?" -> POST /accounts/{account_id}/brand-protection/search
- "List all submission-info?" -> GET /accounts/{account_id}/brand-protection/submission-info
- "Create a submit?" -> POST /accounts/{account_id}/brand-protection/submit
- "List all total-queries?" -> GET /accounts/{account_id}/brand-protection/total-queries
- "List all tracked-domains?" -> GET /accounts/{account_id}/brand-protection/tracked-domains
- "List all url-info?" -> GET /accounts/{account_id}/brand-protection/url-info
- "Create a content?" -> POST /accounts/{account_id}/browser-rendering/content
- "Create a json?" -> POST /accounts/{account_id}/browser-rendering/json
- "Create a link?" -> POST /accounts/{account_id}/browser-rendering/links
- "Create a markdown?" -> POST /accounts/{account_id}/browser-rendering/markdown
- "Create a pdf?" -> POST /accounts/{account_id}/browser-rendering/pdf
- "Create a scrape?" -> POST /accounts/{account_id}/browser-rendering/scrape
- "Create a screenshot?" -> POST /accounts/{account_id}/browser-rendering/screenshot
- "Create a snapshot?" -> POST /accounts/{account_id}/browser-rendering/snapshot
- "List all limits?" -> GET /accounts/{account_id}/builds/account/limits
- "List all builds?" -> GET /accounts/{account_id}/builds/builds
- "List all latest?" -> GET /accounts/{account_id}/builds/builds/latest
- "Get build details?" -> GET /accounts/{account_id}/builds/builds/{build_uuid}
- "List all logs?" -> GET /accounts/{account_id}/builds/builds/{build_uuid}/logs
- "Delete a connection?" -> DELETE /accounts/{account_id}/builds/repos/connections/{repo_connection_uuid}
- "List all config_autofill?" -> GET /accounts/{account_id}/builds/repos/{provider_type}/{provider_account_id}/{repo_id}/config_autofill
- "List all tokens?" -> GET /accounts/{account_id}/builds/tokens
- "Create a token?" -> POST /accounts/{account_id}/builds/tokens
- "Delete a token?" -> DELETE /accounts/{account_id}/builds/tokens/{build_token_uuid}
- "Create a trigger?" -> POST /accounts/{account_id}/builds/triggers
- "Delete a trigger?" -> DELETE /accounts/{account_id}/builds/triggers/{trigger_uuid}
- "Partially update a trigger?" -> PATCH /accounts/{account_id}/builds/triggers/{trigger_uuid}
- "Create a build?" -> POST /accounts/{account_id}/builds/triggers/{trigger_uuid}/builds
- "List all environment_variables?" -> GET /accounts/{account_id}/builds/triggers/{trigger_uuid}/environment_variables
- "Delete a environment_variable?" -> DELETE /accounts/{account_id}/builds/triggers/{trigger_uuid}/environment_variables/{environment_variable_key}
- "Create a purge_build_cache?" -> POST /accounts/{account_id}/builds/triggers/{trigger_uuid}/purge_build_cache
- "List all builds?" -> GET /accounts/{account_id}/builds/workers/{external_script_id}/builds
- "List all triggers?" -> GET /accounts/{account_id}/builds/workers/{external_script_id}/triggers
- "List all apps?" -> GET /accounts/{account_id}/calls/apps
- "Create a app?" -> POST /accounts/{account_id}/calls/apps
- "Delete a app?" -> DELETE /accounts/{account_id}/calls/apps/{app_id}
- "Get app details?" -> GET /accounts/{account_id}/calls/apps/{app_id}
- "Update a app?" -> PUT /accounts/{account_id}/calls/apps/{app_id}
- "List all turn_keys?" -> GET /accounts/{account_id}/calls/turn_keys
- "Create a turn_key?" -> POST /accounts/{account_id}/calls/turn_keys
- "Delete a turn_key?" -> DELETE /accounts/{account_id}/calls/turn_keys/{key_id}
- "Get turn_key details?" -> GET /accounts/{account_id}/calls/turn_keys/{key_id}
- "Update a turn_key?" -> PUT /accounts/{account_id}/calls/turn_keys/{key_id}
- "List all cfd_tunnel?" -> GET /accounts/{account_id}/cfd_tunnel
- "Create a cfd_tunnel?" -> POST /accounts/{account_id}/cfd_tunnel
- "Delete a cfd_tunnel?" -> DELETE /accounts/{account_id}/cfd_tunnel/{tunnel_id}
- "Get cfd_tunnel details?" -> GET /accounts/{account_id}/cfd_tunnel/{tunnel_id}
- "Partially update a cfd_tunnel?" -> PATCH /accounts/{account_id}/cfd_tunnel/{tunnel_id}
- "List all configurations?" -> GET /accounts/{account_id}/cfd_tunnel/{tunnel_id}/configurations
- "List all connections?" -> GET /accounts/{account_id}/cfd_tunnel/{tunnel_id}/connections
- "Get connector details?" -> GET /accounts/{account_id}/cfd_tunnel/{tunnel_id}/connectors/{connector_id}
- "Create a management?" -> POST /accounts/{account_id}/cfd_tunnel/{tunnel_id}/management
- "List all token?" -> GET /accounts/{account_id}/cfd_tunnel/{tunnel_id}/token
- "List all widgets?" -> GET /accounts/{account_id}/challenges/widgets
- "Create a widget?" -> POST /accounts/{account_id}/challenges/widgets
- "Delete a widget?" -> DELETE /accounts/{account_id}/challenges/widgets/{sitekey}
- "Get widget details?" -> GET /accounts/{account_id}/challenges/widgets/{sitekey}
- "Update a widget?" -> PUT /accounts/{account_id}/challenges/widgets/{sitekey}
- "Create a rotate_secret?" -> POST /accounts/{account_id}/challenges/widgets/{sitekey}/rotate_secret
- "Create a binary?" -> POST /accounts/{account_id}/cloudforce-one/binary
- "Get binary details?" -> GET /accounts/{account_id}/cloudforce-one/binary/{hash}
- "Search events?" -> GET /accounts/{account_id}/cloudforce-one/events
- "List all aggregate?" -> GET /accounts/{account_id}/cloudforce-one/events/aggregate
- "List all attackers?" -> GET /accounts/{account_id}/cloudforce-one/events/attackers
- "List all categories?" -> GET /accounts/{account_id}/cloudforce-one/events/categories
- "List all catalog?" -> GET /accounts/{account_id}/cloudforce-one/events/categories/catalog
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/categories/create
- "Delete a category?" -> DELETE /accounts/{account_id}/cloudforce-one/events/categories/{category_id}
- "Get category details?" -> GET /accounts/{account_id}/cloudforce-one/events/categories/{category_id}
- "Partially update a category?" -> PATCH /accounts/{account_id}/cloudforce-one/events/categories/{category_id}
- "List all countries?" -> GET /accounts/{account_id}/cloudforce-one/events/countries
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/create
- "Create a bulk?" -> POST /accounts/{account_id}/cloudforce-one/events/create/bulk
- "Create a relationship?" -> POST /accounts/{account_id}/cloudforce-one/events/create/bulk/relationships
- "List all dataset?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/dataset/create
- "Delete a dataset?" -> DELETE /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}
- "Get dataset details?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}
- "Partially update a dataset?" -> PATCH /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}
- "Get event details?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/events/{event_id}
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicatorTypes/create
- "Search indicators?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators
- "Create a bulk?" -> POST /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/bulk
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/create
- "List all tags?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/tags
- "Delete a indicator?" -> DELETE /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id}
- "Get indicator details?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id}
- "Partially update a indicator?" -> PATCH /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/indicators/{indicator_id}
- "Create a move?" -> POST /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/move
- "List all indicators?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/tags/{tag_uuid}/indicators
- "List all targetIndustries?" -> GET /accounts/{account_id}/cloudforce-one/events/dataset/{dataset_id}/targetIndustries
- "Create a populate?" -> POST /accounts/{account_id}/cloudforce-one/events/datasets/populate
- "Delete a event_tag?" -> DELETE /accounts/{account_id}/cloudforce-one/events/event_tag/{event_id}
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/event_tag/{event_id}/create
- "List all indicator-types?" -> GET /accounts/{account_id}/cloudforce-one/events/indicator-types
- "List all indicatorTypes?" -> GET /accounts/{account_id}/cloudforce-one/events/indicatorTypes
- "Search indicators?" -> GET /accounts/{account_id}/cloudforce-one/events/indicators
- "List all queries?" -> GET /accounts/{account_id}/cloudforce-one/events/queries
- "List all alerts?" -> GET /accounts/{account_id}/cloudforce-one/events/queries/alerts
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/queries/alerts/create
- "Delete a alert?" -> DELETE /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id}
- "Get alert details?" -> GET /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id}
- "Partially update a alert?" -> PATCH /accounts/{account_id}/cloudforce-one/events/queries/alerts/{alert_id}
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/queries/create
- "Delete a query?" -> DELETE /accounts/{account_id}/cloudforce-one/events/queries/{query_id}
- "Get query details?" -> GET /accounts/{account_id}/cloudforce-one/events/queries/{query_id}
- "Partially update a query?" -> PATCH /accounts/{account_id}/cloudforce-one/events/queries/{query_id}
- "Get raw details?" -> GET /accounts/{account_id}/cloudforce-one/events/raw/{dataset_id}/{event_id}
- "Delete a relate?" -> DELETE /accounts/{account_id}/cloudforce-one/events/relate/{event_id}
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/relate/{event_id}/create
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/relationships/create
- "Search tags?" -> GET /accounts/{account_id}/cloudforce-one/events/tags
- "Search categories?" -> GET /accounts/{account_id}/cloudforce-one/events/tags/categories
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/tags/categories/create
- "Delete a category?" -> DELETE /accounts/{account_id}/cloudforce-one/events/tags/categories/{category_uuid}
- "Partially update a category?" -> PATCH /accounts/{account_id}/cloudforce-one/events/tags/categories/{category_uuid}
- "Create a create?" -> POST /accounts/{account_id}/cloudforce-one/events/tags/create
- "Delete a tag?" -> DELETE /accounts/{account_id}/cloudforce-one/events/tags/{tag_uuid}
- "Partially update a tag?" -> PATCH /accounts/{account_id}/cloudforce-one/events/tags/{tag_uuid}
- "List all targetIndustries?" -> GET /accounts/{account_id}/cloudforce-one/events/targetIndustries
- "List all catalog?" -> GET /accounts/{account_id}/cloudforce-one/events/targetIndustries/catalog
- "Create a revert-do?" -> POST /accounts/{account_id}/cloudforce-one/events/{dataset_id}/revert-do
- "Get event details?" -> GET /accounts/{account_id}/cloudforce-one/events/{event_id}
- "Partially update a event?" -> PATCH /accounts/{account_id}/cloudforce-one/events/{event_id}
- "Get raw details?" -> GET /accounts/{account_id}/cloudforce-one/events/{event_id}/raw/{raw_id}
- "Partially update a raw?" -> PATCH /accounts/{account_id}/cloudforce-one/events/{event_id}/raw/{raw_id}
- "List all relationships?" -> GET /accounts/{account_id}/cloudforce-one/events/{event_id}/relationships
- "Create a request?" -> POST /accounts/{account_id}/cloudforce-one/requests
- "List all constants?" -> GET /accounts/{account_id}/cloudforce-one/requests/constants
- "Create a new?" -> POST /accounts/{account_id}/cloudforce-one/requests/new
- "Create a priority?" -> POST /accounts/{account_id}/cloudforce-one/requests/priority
- "Create a new?" -> POST /accounts/{account_id}/cloudforce-one/requests/priority/new
- "List all quota?" -> GET /accounts/{account_id}/cloudforce-one/requests/priority/quota
- "Delete a priority?" -> DELETE /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id}
- "Get priority details?" -> GET /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id}
- "Update a priority?" -> PUT /accounts/{account_id}/cloudforce-one/requests/priority/{priority_id}
- "List all quota?" -> GET /accounts/{account_id}/cloudforce-one/requests/quota
- "List all types?" -> GET /accounts/{account_id}/cloudforce-one/requests/types
- "Delete a request?" -> DELETE /accounts/{account_id}/cloudforce-one/requests/{request_id}
- "Get request details?" -> GET /accounts/{account_id}/cloudforce-one/requests/{request_id}
- "Update a request?" -> PUT /accounts/{account_id}/cloudforce-one/requests/{request_id}
- "Create a asset?" -> POST /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset
- "Create a new?" -> POST /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/new
- "Delete a asset?" -> DELETE /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id}
- "Get asset details?" -> GET /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id}
- "Update a asset?" -> PUT /accounts/{account_id}/cloudforce-one/requests/{request_id}/asset/{asset_id}
- "Create a message?" -> POST /accounts/{account_id}/cloudforce-one/requests/{request_id}/message
- "Create a new?" -> POST /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/new
- "Delete a message?" -> DELETE /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/{message_id}
- "Update a message?" -> PUT /accounts/{account_id}/cloudforce-one/requests/{request_id}/message/{message_id}
- "List all config?" -> GET /accounts/{account_id}/cloudforce-one/scans/config
- "Create a config?" -> POST /accounts/{account_id}/cloudforce-one/scans/config
- "Delete a config?" -> DELETE /accounts/{account_id}/cloudforce-one/scans/config/{config_id}
- "Partially update a config?" -> PATCH /accounts/{account_id}/cloudforce-one/scans/config/{config_id}
- "Get result details?" -> GET /accounts/{account_id}/cloudforce-one/scans/results/{config_id}
- "Create a graphql?" -> POST /accounts/{account_id}/cloudforce-one/v2/events/graphql
- "List all cnis?" -> GET /accounts/{account_id}/cni/cnis
- "Create a cnis?" -> POST /accounts/{account_id}/cni/cnis
- "Delete a cnis?" -> DELETE /accounts/{account_id}/cni/cnis/{cni}
- "Get cnis details?" -> GET /accounts/{account_id}/cni/cnis/{cni}
- "Update a cnis?" -> PUT /accounts/{account_id}/cni/cnis/{cni}
- "List all interconnects?" -> GET /accounts/{account_id}/cni/interconnects
- "Create a interconnect?" -> POST /accounts/{account_id}/cni/interconnects
- "Delete a interconnect?" -> DELETE /accounts/{account_id}/cni/interconnects/{icon}
- "Get interconnect details?" -> GET /accounts/{account_id}/cni/interconnects/{icon}
- "List all loa?" -> GET /accounts/{account_id}/cni/interconnects/{icon}/loa
- "List all status?" -> GET /accounts/{account_id}/cni/interconnects/{icon}/status
- "List all settings?" -> GET /accounts/{account_id}/cni/settings
- "List all slots?" -> GET /accounts/{account_id}/cni/slots
- "Get slot details?" -> GET /accounts/{account_id}/cni/slots/{slot}
- "List all services?" -> GET /accounts/{account_id}/connectivity/directory/services
- "Create a service?" -> POST /accounts/{account_id}/connectivity/directory/services
- "Delete a service?" -> DELETE /accounts/{account_id}/connectivity/directory/services/{service_id}
- "Get service details?" -> GET /accounts/{account_id}/connectivity/directory/services/{service_id}
- "Update a service?" -> PUT /accounts/{account_id}/connectivity/directory/services/{service_id}
- "List all containers?" -> GET /accounts/{account_id}/containers
- "Create a credential?" -> POST /accounts/{account_id}/containers/registries/{domain}/credentials
- "List all custom_ns?" -> GET /accounts/{account_id}/custom_ns
- "Create a custom_n?" -> POST /accounts/{account_id}/custom_ns
- "Delete a custom_n?" -> DELETE /accounts/{account_id}/custom_ns/{custom_ns_id}
- "List all database?" -> GET /accounts/{account_id}/d1/database
- "Create a database?" -> POST /accounts/{account_id}/d1/database
- "Delete a database?" -> DELETE /accounts/{account_id}/d1/database/{database_id}
- "Get database details?" -> GET /accounts/{account_id}/d1/database/{database_id}
- "Partially update a database?" -> PATCH /accounts/{account_id}/d1/database/{database_id}
- "Update a database?" -> PUT /accounts/{account_id}/d1/database/{database_id}
- "Create a export?" -> POST /accounts/{account_id}/d1/database/{database_id}/export
- "Create a import?" -> POST /accounts/{account_id}/d1/database/{database_id}/import
- "Create a query?" -> POST /accounts/{account_id}/d1/database/{database_id}/query
- "Create a raw?" -> POST /accounts/{account_id}/d1/database/{database_id}/raw
- "List all bookmark?" -> GET /accounts/{account_id}/d1/database/{database_id}/time_travel/bookmark
- "Create a restore?" -> POST /accounts/{account_id}/d1/database/{database_id}/time_travel/restore
- "List all devices?" -> GET /accounts/{account_id}/devices
- "List all ip-profiles?" -> GET /accounts/{account_id}/devices/ip-profiles
- "Create a ip-profile?" -> POST /accounts/{account_id}/devices/ip-profiles
- "Delete a ip-profile?" -> DELETE /accounts/{account_id}/devices/ip-profiles/{profile_id}
- "Get ip-profile details?" -> GET /accounts/{account_id}/devices/ip-profiles/{profile_id}
- "Partially update a ip-profile?" -> PATCH /accounts/{account_id}/devices/ip-profiles/{profile_id}
- "List all networks?" -> GET /accounts/{account_id}/devices/networks
- "Create a network?" -> POST /accounts/{account_id}/devices/networks
- "Delete a network?" -> DELETE /accounts/{account_id}/devices/networks/{network_id}
- "Get network details?" -> GET /accounts/{account_id}/devices/networks/{network_id}
- "Update a network?" -> PUT /accounts/{account_id}/devices/networks/{network_id}
- "Search physical-devices?" -> GET /accounts/{account_id}/devices/physical-devices
- "Delete a physical-device?" -> DELETE /accounts/{account_id}/devices/physical-devices/{device_id}
- "Get physical-device details?" -> GET /accounts/{account_id}/devices/physical-devices/{device_id}
- "Create a revoke?" -> POST /accounts/{account_id}/devices/physical-devices/{device_id}/revoke
- "List all policies?" -> GET /accounts/{account_id}/devices/policies
- "List all policy?" -> GET /accounts/{account_id}/devices/policy
- "Create a policy?" -> POST /accounts/{account_id}/devices/policy
- "List all exclude?" -> GET /accounts/{account_id}/devices/policy/exclude
- "List all fallback_domains?" -> GET /accounts/{account_id}/devices/policy/fallback_domains
- "List all include?" -> GET /accounts/{account_id}/devices/policy/include
- "Delete a policy?" -> DELETE /accounts/{account_id}/devices/policy/{policy_id}
- "Get policy details?" -> GET /accounts/{account_id}/devices/policy/{policy_id}
- "Partially update a policy?" -> PATCH /accounts/{account_id}/devices/policy/{policy_id}
- "List all exclude?" -> GET /accounts/{account_id}/devices/policy/{policy_id}/exclude
- "List all fallback_domains?" -> GET /accounts/{account_id}/devices/policy/{policy_id}/fallback_domains
- "List all include?" -> GET /accounts/{account_id}/devices/policy/{policy_id}/include
- "List all posture?" -> GET /accounts/{account_id}/devices/posture
- "Create a posture?" -> POST /accounts/{account_id}/devices/posture
- "List all integration?" -> GET /accounts/{account_id}/devices/posture/integration
- "Create a integration?" -> POST /accounts/{account_id}/devices/posture/integration
- "Delete a integration?" -> DELETE /accounts/{account_id}/devices/posture/integration/{integration_id}
- "Get integration details?" -> GET /accounts/{account_id}/devices/posture/integration/{integration_id}
- "Partially update a integration?" -> PATCH /accounts/{account_id}/devices/posture/integration/{integration_id}
- "Delete a posture?" -> DELETE /accounts/{account_id}/devices/posture/{rule_id}
- "Get posture details?" -> GET /accounts/{account_id}/devices/posture/{rule_id}
- "Update a posture?" -> PUT /accounts/{account_id}/devices/posture/{rule_id}
- "Search registrations?" -> GET /accounts/{account_id}/devices/registrations
- "Create a revoke?" -> POST /accounts/{account_id}/devices/registrations/revoke
- "Create a unrevoke?" -> POST /accounts/{account_id}/devices/registrations/unrevoke
- "Delete a registration?" -> DELETE /accounts/{account_id}/devices/registrations/{registration_id}
- "Get registration details?" -> GET /accounts/{account_id}/devices/registrations/{registration_id}
- "List all override_codes?" -> GET /accounts/{account_id}/devices/registrations/{registration_id}/override_codes
- "List all disconnect?" -> GET /accounts/{account_id}/devices/resilience/disconnect
- "Create a disconnect?" -> POST /accounts/{account_id}/devices/resilience/disconnect
- "Create a revoke?" -> POST /accounts/{account_id}/devices/revoke
- "List all settings?" -> GET /accounts/{account_id}/devices/settings
- "Create a unrevoke?" -> POST /accounts/{account_id}/devices/unrevoke
- "Get device details?" -> GET /accounts/{account_id}/devices/{device_id}
- "List all override_codes?" -> GET /accounts/{account_id}/devices/{device_id}/override_codes
- "List all colos?" -> GET /accounts/{account_id}/dex/colos
- "List all commands?" -> GET /accounts/{account_id}/dex/commands
- "Create a command?" -> POST /accounts/{account_id}/dex/commands
- "Search devices?" -> GET /accounts/{account_id}/dex/commands/devices
- "List all quota?" -> GET /accounts/{account_id}/dex/commands/quota
- "Get download details?" -> GET /accounts/{account_id}/dex/commands/{command_id}/downloads/{filename}
- "List all dex_tests?" -> GET /accounts/{account_id}/dex/devices/dex_tests
- "Create a dex_test?" -> POST /accounts/{account_id}/dex/devices/dex_tests
- "Delete a dex_test?" -> DELETE /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id}
- "Get dex_test details?" -> GET /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id}
- "Update a dex_test?" -> PUT /accounts/{account_id}/dex/devices/dex_tests/{dex_test_id}
- "List all live?" -> GET /accounts/{account_id}/dex/devices/{device_id}/fleet-status/live
- "List all devices?" -> GET /accounts/{account_id}/dex/fleet-status/devices
- "List all live?" -> GET /accounts/{account_id}/dex/fleet-status/live
- "List all over-time?" -> GET /accounts/{account_id}/dex/fleet-status/over-time
- "Get http-test details?" -> GET /accounts/{account_id}/dex/http-tests/{test_id}
- "List all percentiles?" -> GET /accounts/{account_id}/dex/http-tests/{test_id}/percentiles
- "List all rules?" -> GET /accounts/{account_id}/dex/rules
- "Create a rule?" -> POST /accounts/{account_id}/dex/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/dex/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/dex/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/dex/rules/{rule_id}
- "List all overview?" -> GET /accounts/{account_id}/dex/tests/overview
- "List all unique-devices?" -> GET /accounts/{account_id}/dex/tests/unique-devices
- "List all network-path?" -> GET /accounts/{account_id}/dex/traceroute-test-results/{test_result_id}/network-path
- "Get traceroute-test details?" -> GET /accounts/{account_id}/dex/traceroute-tests/{test_id}
- "List all network-path?" -> GET /accounts/{account_id}/dex/traceroute-tests/{test_id}/network-path
- "List all percentiles?" -> GET /accounts/{account_id}/dex/traceroute-tests/{test_id}/percentiles
- "List all warp-change-events?" -> GET /accounts/{account_id}/dex/warp-change-events
- "List all endpoint-healthchecks?" -> GET /accounts/{account_id}/diagnostics/endpoint-healthchecks
- "Create a endpoint-healthcheck?" -> POST /accounts/{account_id}/diagnostics/endpoint-healthchecks
- "Delete a endpoint-healthcheck?" -> DELETE /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id}
- "Get endpoint-healthcheck details?" -> GET /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id}
- "Update a endpoint-healthcheck?" -> PUT /accounts/{account_id}/diagnostics/endpoint-healthchecks/{id}
- "Create a traceroute?" -> POST /accounts/{account_id}/diagnostics/traceroute
- "List all datasets?" -> GET /accounts/{account_id}/dlp/datasets
- "Create a dataset?" -> POST /accounts/{account_id}/dlp/datasets
- "Delete a dataset?" -> DELETE /accounts/{account_id}/dlp/datasets/{dataset_id}
- "Get dataset details?" -> GET /accounts/{account_id}/dlp/datasets/{dataset_id}
- "Update a dataset?" -> PUT /accounts/{account_id}/dlp/datasets/{dataset_id}
- "Create a upload?" -> POST /accounts/{account_id}/dlp/datasets/{dataset_id}/upload
- "List all document_fingerprints?" -> GET /accounts/{account_id}/dlp/document_fingerprints
- "Create a document_fingerprint?" -> POST /accounts/{account_id}/dlp/document_fingerprints
- "Delete a document_fingerprint?" -> DELETE /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id}
- "Get document_fingerprint details?" -> GET /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id}
- "Update a document_fingerprint?" -> PUT /accounts/{account_id}/dlp/document_fingerprints/{document_fingerprint_id}
- "List all account_mapping?" -> GET /accounts/{account_id}/dlp/email/account_mapping
- "Create a account_mapping?" -> POST /accounts/{account_id}/dlp/email/account_mapping
- "List all rules?" -> GET /accounts/{account_id}/dlp/email/rules
- "Create a rule?" -> POST /accounts/{account_id}/dlp/email/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/dlp/email/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/dlp/email/rules/{rule_id}
- "Update a rule?" -> PUT /accounts/{account_id}/dlp/email/rules/{rule_id}
- "List all entries?" -> GET /accounts/{account_id}/dlp/entries
- "Create a entry?" -> POST /accounts/{account_id}/dlp/entries
- "Update a custom?" -> PUT /accounts/{account_id}/dlp/entries/custom/{entry_id}
- "Create a integration?" -> POST /accounts/{account_id}/dlp/entries/integration
- "Delete a integration?" -> DELETE /accounts/{account_id}/dlp/entries/integration/{entry_id}
- "Update a integration?" -> PUT /accounts/{account_id}/dlp/entries/integration/{entry_id}
- "Create a predefined?" -> POST /accounts/{account_id}/dlp/entries/predefined
- "Delete a predefined?" -> DELETE /accounts/{account_id}/dlp/entries/predefined/{entry_id}
- "Update a predefined?" -> PUT /accounts/{account_id}/dlp/entries/predefined/{entry_id}
- "Delete a entry?" -> DELETE /accounts/{account_id}/dlp/entries/{entry_id}
- "Get entry details?" -> GET /accounts/{account_id}/dlp/entries/{entry_id}
- "Update a entry?" -> PUT /accounts/{account_id}/dlp/entries/{entry_id}
- "List all limits?" -> GET /accounts/{account_id}/dlp/limits
- "Create a validate?" -> POST /accounts/{account_id}/dlp/patterns/validate
- "List all payload_log?" -> GET /accounts/{account_id}/dlp/payload_log
- "List all profiles?" -> GET /accounts/{account_id}/dlp/profiles
- "List all custom?" -> GET /accounts/{account_id}/dlp/profiles/custom
- "Create a custom?" -> POST /accounts/{account_id}/dlp/profiles/custom
- "Delete a custom?" -> DELETE /accounts/{account_id}/dlp/profiles/custom/{profile_id}
- "Get custom details?" -> GET /accounts/{account_id}/dlp/profiles/custom/{profile_id}
- "Update a custom?" -> PUT /accounts/{account_id}/dlp/profiles/custom/{profile_id}
- "Create a predefined?" -> POST /accounts/{account_id}/dlp/profiles/predefined
- "Delete a predefined?" -> DELETE /accounts/{account_id}/dlp/profiles/predefined/{profile_id}
- "Get predefined details?" -> GET /accounts/{account_id}/dlp/profiles/predefined/{profile_id}
- "Update a predefined?" -> PUT /accounts/{account_id}/dlp/profiles/predefined/{profile_id}
- "List all config?" -> GET /accounts/{account_id}/dlp/profiles/predefined/{profile_id}/config
- "Create a config?" -> POST /accounts/{account_id}/dlp/profiles/predefined/{profile_id}/config
- "Get profile details?" -> GET /accounts/{account_id}/dlp/profiles/{profile_id}
- "List all dns_firewall?" -> GET /accounts/{account_id}/dns_firewall
- "Create a dns_firewall?" -> POST /accounts/{account_id}/dns_firewall
- "Delete a dns_firewall?" -> DELETE /accounts/{account_id}/dns_firewall/{dns_firewall_id}
- "Get dns_firewall details?" -> GET /accounts/{account_id}/dns_firewall/{dns_firewall_id}
- "Partially update a dns_firewall?" -> PATCH /accounts/{account_id}/dns_firewall/{dns_firewall_id}
- "List all report?" -> GET /accounts/{account_id}/dns_firewall/{dns_firewall_id}/dns_analytics/report
- "List all bytime?" -> GET /accounts/{account_id}/dns_firewall/{dns_firewall_id}/dns_analytics/report/bytime
- "List all reverse_dns?" -> GET /accounts/{account_id}/dns_firewall/{dns_firewall_id}/reverse_dns
- "List all usage?" -> GET /accounts/{account_id}/dns_records/usage
- "List all dns_settings?" -> GET /accounts/{account_id}/dns_settings
- "List all views?" -> GET /accounts/{account_id}/dns_settings/views
- "Create a view?" -> POST /accounts/{account_id}/dns_settings/views
- "Delete a view?" -> DELETE /accounts/{account_id}/dns_settings/views/{view_id}
- "Get view details?" -> GET /accounts/{account_id}/dns_settings/views/{view_id}
- "Partially update a view?" -> PATCH /accounts/{account_id}/dns_settings/views/{view_id}
- "Search investigate?" -> GET /accounts/{account_id}/email-security/investigate
- "Create a move?" -> POST /accounts/{account_id}/email-security/investigate/move
- "Create a preview?" -> POST /accounts/{account_id}/email-security/investigate/preview
- "Create a release?" -> POST /accounts/{account_id}/email-security/investigate/release
- "Get investigate details?" -> GET /accounts/{account_id}/email-security/investigate/{postfix_id}
- "List all detections?" -> GET /accounts/{account_id}/email-security/investigate/{postfix_id}/detections
- "Create a move?" -> POST /accounts/{account_id}/email-security/investigate/{postfix_id}/move
- "List all preview?" -> GET /accounts/{account_id}/email-security/investigate/{postfix_id}/preview
- "List all raw?" -> GET /accounts/{account_id}/email-security/investigate/{postfix_id}/raw
- "Create a reclassify?" -> POST /accounts/{account_id}/email-security/investigate/{postfix_id}/reclassify
- "List all trace?" -> GET /accounts/{account_id}/email-security/investigate/{postfix_id}/trace
- "List all reports?" -> GET /accounts/{account_id}/email-security/phishguard/reports
- "Search allow_policies?" -> GET /accounts/{account_id}/email-security/settings/allow_policies
- "Create a allow_policy?" -> POST /accounts/{account_id}/email-security/settings/allow_policies
- "Create a batch?" -> POST /accounts/{account_id}/email-security/settings/allow_policies/batch
- "Delete a allow_policy?" -> DELETE /accounts/{account_id}/email-security/settings/allow_policies/{policy_id}
- "Get allow_policy details?" -> GET /accounts/{account_id}/email-security/settings/allow_policies/{policy_id}
- "Partially update a allow_policy?" -> PATCH /accounts/{account_id}/email-security/settings/allow_policies/{policy_id}
- "Search block_senders?" -> GET /accounts/{account_id}/email-security/settings/block_senders
- "Create a block_sender?" -> POST /accounts/{account_id}/email-security/settings/block_senders
- "Create a batch?" -> POST /accounts/{account_id}/email-security/settings/block_senders/batch
- "Delete a block_sender?" -> DELETE /accounts/{account_id}/email-security/settings/block_senders/{pattern_id}
- "Get block_sender details?" -> GET /accounts/{account_id}/email-security/settings/block_senders/{pattern_id}
- "Partially update a block_sender?" -> PATCH /accounts/{account_id}/email-security/settings/block_senders/{pattern_id}
- "Search domains?" -> GET /accounts/{account_id}/email-security/settings/domains
- "Delete a domain?" -> DELETE /accounts/{account_id}/email-security/settings/domains/{domain_id}
- "Get domain details?" -> GET /accounts/{account_id}/email-security/settings/domains/{domain_id}
- "Partially update a domain?" -> PATCH /accounts/{account_id}/email-security/settings/domains/{domain_id}
- "Search impersonation_registry?" -> GET /accounts/{account_id}/email-security/settings/impersonation_registry
- "Create a impersonation_registry?" -> POST /accounts/{account_id}/email-security/settings/impersonation_registry
- "Delete a impersonation_registry?" -> DELETE /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id}
- "Get impersonation_registry details?" -> GET /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id}
- "Partially update a impersonation_registry?" -> PATCH /accounts/{account_id}/email-security/settings/impersonation_registry/{display_name_id}
- "Create a batch?" -> POST /accounts/{account_id}/email-security/settings/sending_domain_restrictions/batch
- "Search trusted_domains?" -> GET /accounts/{account_id}/email-security/settings/trusted_domains
- "Create a trusted_domain?" -> POST /accounts/{account_id}/email-security/settings/trusted_domains
- "Create a batch?" -> POST /accounts/{account_id}/email-security/settings/trusted_domains/batch
- "Delete a trusted_domain?" -> DELETE /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id}
- "Get trusted_domain details?" -> GET /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id}
- "Partially update a trusted_domain?" -> PATCH /accounts/{account_id}/email-security/settings/trusted_domains/{trusted_domain_id}
- "Search submissions?" -> GET /accounts/{account_id}/email-security/submissions
- "List all addresses?" -> GET /accounts/{account_id}/email/routing/addresses
- "Create a address?" -> POST /accounts/{account_id}/email/routing/addresses
- "Delete a address?" -> DELETE /accounts/{account_id}/email/routing/addresses/{destination_address_identifier}
- "Get address details?" -> GET /accounts/{account_id}/email/routing/addresses/{destination_address_identifier}
- "List all configuration?" -> GET /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration
- "Delete a queue?" -> DELETE /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id}
- "Get queue details?" -> GET /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id}
- "Update a queue?" -> PUT /accounts/{account_id}/event_notifications/r2/{bucket_name}/configuration/queues/{queue_id}
- "List all subscriptions?" -> GET /accounts/{account_id}/event_subscriptions/subscriptions
- "Create a subscription?" -> POST /accounts/{account_id}/event_subscriptions/subscriptions
- "Delete a subscription?" -> DELETE /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id}
- "Get subscription details?" -> GET /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id}
- "Partially update a subscription?" -> PATCH /accounts/{account_id}/event_subscriptions/subscriptions/{subscription_id}
- "List all rules?" -> GET /accounts/{account_id}/firewall/access_rules/rules
- "Create a rule?" -> POST /accounts/{account_id}/firewall/access_rules/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/firewall/access_rules/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/firewall/access_rules/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/firewall/access_rules/rules/{rule_id}
- "List all gateway?" -> GET /accounts/{account_id}/gateway
- "Create a gateway?" -> POST /accounts/{account_id}/gateway
- "List all app_types?" -> GET /accounts/{account_id}/gateway/app_types
- "List all review_status?" -> GET /accounts/{account_id}/gateway/apps/review_status
- "List all audit_ssh_settings?" -> GET /accounts/{account_id}/gateway/audit_ssh_settings
- "Create a rotate_seed?" -> POST /accounts/{account_id}/gateway/audit_ssh_settings/rotate_seed
- "List all categories?" -> GET /accounts/{account_id}/gateway/categories
- "List all certificates?" -> GET /accounts/{account_id}/gateway/certificates
- "Create a certificate?" -> POST /accounts/{account_id}/gateway/certificates
- "Delete a certificate?" -> DELETE /accounts/{account_id}/gateway/certificates/{certificate_id}
- "Get certificate details?" -> GET /accounts/{account_id}/gateway/certificates/{certificate_id}
- "Create a activate?" -> POST /accounts/{account_id}/gateway/certificates/{certificate_id}/activate
- "Create a deactivate?" -> POST /accounts/{account_id}/gateway/certificates/{certificate_id}/deactivate
- "List all configuration?" -> GET /accounts/{account_id}/gateway/configuration
- "List all custom_certificate?" -> GET /accounts/{account_id}/gateway/configuration/custom_certificate
- "List all lists?" -> GET /accounts/{account_id}/gateway/lists
- "Create a list?" -> POST /accounts/{account_id}/gateway/lists
- "Delete a list?" -> DELETE /accounts/{account_id}/gateway/lists/{list_id}
- "Get list details?" -> GET /accounts/{account_id}/gateway/lists/{list_id}
- "Partially update a list?" -> PATCH /accounts/{account_id}/gateway/lists/{list_id}
- "Update a list?" -> PUT /accounts/{account_id}/gateway/lists/{list_id}
- "List all items?" -> GET /accounts/{account_id}/gateway/lists/{list_id}/items
- "List all locations?" -> GET /accounts/{account_id}/gateway/locations
- "Create a location?" -> POST /accounts/{account_id}/gateway/locations
- "Delete a location?" -> DELETE /accounts/{account_id}/gateway/locations/{location_id}
- "Get location details?" -> GET /accounts/{account_id}/gateway/locations/{location_id}
- "Update a location?" -> PUT /accounts/{account_id}/gateway/locations/{location_id}
- "List all logging?" -> GET /accounts/{account_id}/gateway/logging
- "List all pacfiles?" -> GET /accounts/{account_id}/gateway/pacfiles
- "Create a pacfile?" -> POST /accounts/{account_id}/gateway/pacfiles
- "Delete a pacfile?" -> DELETE /accounts/{account_id}/gateway/pacfiles/{pacfile_id}
- "Get pacfile details?" -> GET /accounts/{account_id}/gateway/pacfiles/{pacfile_id}
- "Update a pacfile?" -> PUT /accounts/{account_id}/gateway/pacfiles/{pacfile_id}
- "List all proxy_endpoints?" -> GET /accounts/{account_id}/gateway/proxy_endpoints
- "Create a proxy_endpoint?" -> POST /accounts/{account_id}/gateway/proxy_endpoints
- "Delete a proxy_endpoint?" -> DELETE /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id}
- "Get proxy_endpoint details?" -> GET /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id}
- "Partially update a proxy_endpoint?" -> PATCH /accounts/{account_id}/gateway/proxy_endpoints/{proxy_endpoint_id}
- "List all rules?" -> GET /accounts/{account_id}/gateway/rules
- "Create a rule?" -> POST /accounts/{account_id}/gateway/rules
- "List all tenant?" -> GET /accounts/{account_id}/gateway/rules/tenant
- "Delete a rule?" -> DELETE /accounts/{account_id}/gateway/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/gateway/rules/{rule_id}
- "Update a rule?" -> PUT /accounts/{account_id}/gateway/rules/{rule_id}
- "Create a reset_expiration?" -> POST /accounts/{account_id}/gateway/rules/{rule_id}/reset_expiration
- "List all configs?" -> GET /accounts/{account_id}/hyperdrive/configs
- "Create a config?" -> POST /accounts/{account_id}/hyperdrive/configs
- "Delete a config?" -> DELETE /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id}
- "Get config details?" -> GET /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id}
- "Partially update a config?" -> PATCH /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id}
- "Update a config?" -> PUT /accounts/{account_id}/hyperdrive/configs/{hyperdrive_id}
- "List all permission_groups?" -> GET /accounts/{account_id}/iam/permission_groups
- "Get permission_group details?" -> GET /accounts/{account_id}/iam/permission_groups/{permission_group_id}
- "List all resource_groups?" -> GET /accounts/{account_id}/iam/resource_groups
- "Create a resource_group?" -> POST /accounts/{account_id}/iam/resource_groups
- "Delete a resource_group?" -> DELETE /accounts/{account_id}/iam/resource_groups/{resource_group_id}
- "Get resource_group details?" -> GET /accounts/{account_id}/iam/resource_groups/{resource_group_id}
- "Update a resource_group?" -> PUT /accounts/{account_id}/iam/resource_groups/{resource_group_id}
- "List all user_groups?" -> GET /accounts/{account_id}/iam/user_groups
- "Create a user_group?" -> POST /accounts/{account_id}/iam/user_groups
- "Delete a user_group?" -> DELETE /accounts/{account_id}/iam/user_groups/{user_group_id}
- "Get user_group details?" -> GET /accounts/{account_id}/iam/user_groups/{user_group_id}
- "Update a user_group?" -> PUT /accounts/{account_id}/iam/user_groups/{user_group_id}
- "List all members?" -> GET /accounts/{account_id}/iam/user_groups/{user_group_id}/members
- "Create a member?" -> POST /accounts/{account_id}/iam/user_groups/{user_group_id}/members
- "Delete a member?" -> DELETE /accounts/{account_id}/iam/user_groups/{user_group_id}/members/{member_id}
- "List all images?" -> GET /accounts/{account_id}/images/v1
- "Create a image?" -> POST /accounts/{account_id}/images/v1
- "List all keys?" -> GET /accounts/{account_id}/images/v1/keys
- "Delete a key?" -> DELETE /accounts/{account_id}/images/v1/keys/{signing_key_name}
- "Update a key?" -> PUT /accounts/{account_id}/images/v1/keys/{signing_key_name}
- "List all stats?" -> GET /accounts/{account_id}/images/v1/stats
- "List all variants?" -> GET /accounts/{account_id}/images/v1/variants
- "Create a variant?" -> POST /accounts/{account_id}/images/v1/variants
- "Delete a variant?" -> DELETE /accounts/{account_id}/images/v1/variants/{variant_id}
- "Get variant details?" -> GET /accounts/{account_id}/images/v1/variants/{variant_id}
- "Partially update a variant?" -> PATCH /accounts/{account_id}/images/v1/variants/{variant_id}
- "Delete a image?" -> DELETE /accounts/{account_id}/images/v1/{image_id}
- "Get image details?" -> GET /accounts/{account_id}/images/v1/{image_id}
- "Partially update a image?" -> PATCH /accounts/{account_id}/images/v1/{image_id}
- "List all blob?" -> GET /accounts/{account_id}/images/v1/{image_id}/blob
- "List all images?" -> GET /accounts/{account_id}/images/v2
- "Create a direct_upload?" -> POST /accounts/{account_id}/images/v2/direct_upload
- "List all targets?" -> GET /accounts/{account_id}/infrastructure/targets
- "Create a target?" -> POST /accounts/{account_id}/infrastructure/targets
- "Create a batch_delete?" -> POST /accounts/{account_id}/infrastructure/targets/batch_delete
- "Delete a target?" -> DELETE /accounts/{account_id}/infrastructure/targets/{target_id}
- "Get target details?" -> GET /accounts/{account_id}/infrastructure/targets/{target_id}
- "Update a target?" -> PUT /accounts/{account_id}/infrastructure/targets/{target_id}
- "Get asn details?" -> GET /accounts/{account_id}/intel/asn/{asn}
- "List all subnets?" -> GET /accounts/{account_id}/intel/asn/{asn}/subnets
- "List all issue-types?" -> GET /accounts/{account_id}/intel/attack-surface-report/issue-types
- "List all issues?" -> GET /accounts/{account_id}/intel/attack-surface-report/issues
- "List all class?" -> GET /accounts/{account_id}/intel/attack-surface-report/issues/class
- "List all severity?" -> GET /accounts/{account_id}/intel/attack-surface-report/issues/severity
- "List all type?" -> GET /accounts/{account_id}/intel/attack-surface-report/issues/type
- "List all dns?" -> GET /accounts/{account_id}/intel/dns
- "List all domain?" -> GET /accounts/{account_id}/intel/domain
- "List all domain-history?" -> GET /accounts/{account_id}/intel/domain-history
- "List all bulk?" -> GET /accounts/{account_id}/intel/domain/bulk
- "List all indicator-feeds?" -> GET /accounts/{account_id}/intel/indicator-feeds
- "Create a indicator-feed?" -> POST /accounts/{account_id}/intel/indicator-feeds
- "List all view?" -> GET /accounts/{account_id}/intel/indicator-feeds/permissions/view
- "Get indicator-feed details?" -> GET /accounts/{account_id}/intel/indicator-feeds/{feed_id}
- "Update a indicator-feed?" -> PUT /accounts/{account_id}/intel/indicator-feeds/{feed_id}
- "List all data?" -> GET /accounts/{account_id}/intel/indicator-feeds/{feed_id}/data
- "List all download?" -> GET /accounts/{account_id}/intel/indicator-feeds/{feed_id}/download
- "List all ip?" -> GET /accounts/{account_id}/intel/ip
- "List all ip-lists?" -> GET /accounts/{account_id}/intel/ip-lists
- "Create a miscategorization?" -> POST /accounts/{account_id}/intel/miscategorization
- "List all sinkholes?" -> GET /accounts/{account_id}/intel/sinkholes
- "List all whois?" -> GET /accounts/{account_id}/intel/whois
- "List all monitor_groups?" -> GET /accounts/{account_id}/load_balancers/monitor_groups
- "Create a monitor_group?" -> POST /accounts/{account_id}/load_balancers/monitor_groups
- "Delete a monitor_group?" -> DELETE /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}
- "Get monitor_group details?" -> GET /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}
- "Partially update a monitor_group?" -> PATCH /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}
- "Update a monitor_group?" -> PUT /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}
- "List all references?" -> GET /accounts/{account_id}/load_balancers/monitor_groups/{monitor_group_id}/references
- "List all monitors?" -> GET /accounts/{account_id}/load_balancers/monitors
- "Create a monitor?" -> POST /accounts/{account_id}/load_balancers/monitors
- "Delete a monitor?" -> DELETE /accounts/{account_id}/load_balancers/monitors/{monitor_id}
- "Get monitor details?" -> GET /accounts/{account_id}/load_balancers/monitors/{monitor_id}
- "Partially update a monitor?" -> PATCH /accounts/{account_id}/load_balancers/monitors/{monitor_id}
- "Update a monitor?" -> PUT /accounts/{account_id}/load_balancers/monitors/{monitor_id}
- "Create a preview?" -> POST /accounts/{account_id}/load_balancers/monitors/{monitor_id}/preview
- "List all references?" -> GET /accounts/{account_id}/load_balancers/monitors/{monitor_id}/references
- "List all pools?" -> GET /accounts/{account_id}/load_balancers/pools
- "Create a pool?" -> POST /accounts/{account_id}/load_balancers/pools
- "Delete a pool?" -> DELETE /accounts/{account_id}/load_balancers/pools/{pool_id}
- "Get pool details?" -> GET /accounts/{account_id}/load_balancers/pools/{pool_id}
- "Partially update a pool?" -> PATCH /accounts/{account_id}/load_balancers/pools/{pool_id}
- "Update a pool?" -> PUT /accounts/{account_id}/load_balancers/pools/{pool_id}
- "List all health?" -> GET /accounts/{account_id}/load_balancers/pools/{pool_id}/health
- "Create a preview?" -> POST /accounts/{account_id}/load_balancers/pools/{pool_id}/preview
- "List all references?" -> GET /accounts/{account_id}/load_balancers/pools/{pool_id}/references
- "Get preview details?" -> GET /accounts/{account_id}/load_balancers/preview/{preview_id}
- "List all regions?" -> GET /accounts/{account_id}/load_balancers/regions
- "Get region details?" -> GET /accounts/{account_id}/load_balancers/regions/{region_id}
- "Search search?" -> GET /accounts/{account_id}/load_balancers/search
- "List all fields?" -> GET /accounts/{account_id}/logpush/datasets/{dataset_id}/fields
- "List all jobs?" -> GET /accounts/{account_id}/logpush/datasets/{dataset_id}/jobs
- "List all jobs?" -> GET /accounts/{account_id}/logpush/jobs
- "Create a job?" -> POST /accounts/{account_id}/logpush/jobs
- "Delete a job?" -> DELETE /accounts/{account_id}/logpush/jobs/{job_id}
- "Get job details?" -> GET /accounts/{account_id}/logpush/jobs/{job_id}
- "Update a job?" -> PUT /accounts/{account_id}/logpush/jobs/{job_id}
- "Create a ownership?" -> POST /accounts/{account_id}/logpush/ownership
- "Create a validate?" -> POST /accounts/{account_id}/logpush/ownership/validate
- "Create a destination?" -> POST /accounts/{account_id}/logpush/validate/destination
- "Create a exist?" -> POST /accounts/{account_id}/logpush/validate/destination/exists
- "Create a origin?" -> POST /accounts/{account_id}/logpush/validate/origin
- "List all audit?" -> GET /accounts/{account_id}/logs/audit
- "List all config?" -> GET /accounts/{account_id}/logs/control/cmb/config
- "Create a config?" -> POST /accounts/{account_id}/logs/control/cmb/config
- "List all rules?" -> GET /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules
- "Create a rule?" -> POST /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/magic/advanced_dns_protection/configs/dns_protection/rules/{rule_id}
- "List all allowlist?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist
- "Create a allowlist?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist
- "Delete a allowlist?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id}
- "Get allowlist details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id}
- "Partially update a allowlist?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/allowlist/{prefix_id}
- "List all prefixes?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes
- "Create a prefixe?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes
- "Create a bulk?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/bulk
- "Delete a prefixe?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id}
- "Get prefixe details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id}
- "Partially update a prefixe?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/prefixes/{prefix_id}
- "List all filters?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters
- "Create a filter?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters
- "Delete a filter?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id}
- "Get filter details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id}
- "Partially update a filter?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/filters/{filter_id}
- "List all rules?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules
- "Create a rule?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/syn_protection/rules/{rule_id}
- "List all filters?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters
- "Create a filter?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters
- "Delete a filter?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id}
- "Get filter details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id}
- "Partially update a filter?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/filters/{filter_id}
- "List all rules?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules
- "Create a rule?" -> POST /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_flow_protection/rules/{rule_id}
- "List all tcp_protection_status?" -> GET /accounts/{account_id}/magic/advanced_tcp_protection/configs/tcp_protection_status
- "List all apps?" -> GET /accounts/{account_id}/magic/apps
- "Create a app?" -> POST /accounts/{account_id}/magic/apps
- "Delete a app?" -> DELETE /accounts/{account_id}/magic/apps/{account_app_id}
- "Partially update a app?" -> PATCH /accounts/{account_id}/magic/apps/{account_app_id}
- "Update a app?" -> PUT /accounts/{account_id}/magic/apps/{account_app_id}
- "List all cf_interconnects?" -> GET /accounts/{account_id}/magic/cf_interconnects
- "Get cf_interconnect details?" -> GET /accounts/{account_id}/magic/cf_interconnects/{cf_interconnect_id}
- "Update a cf_interconnect?" -> PUT /accounts/{account_id}/magic/cf_interconnects/{cf_interconnect_id}
- "List all catalog-syncs?" -> GET /accounts/{account_id}/magic/cloud/catalog-syncs
- "Create a catalog-sync?" -> POST /accounts/{account_id}/magic/cloud/catalog-syncs
- "List all prebuilt-policies?" -> GET /accounts/{account_id}/magic/cloud/catalog-syncs/prebuilt-policies
- "Delete a catalog-sync?" -> DELETE /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}
- "Get catalog-sync details?" -> GET /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}
- "Partially update a catalog-sync?" -> PATCH /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}
- "Update a catalog-sync?" -> PUT /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}
- "Create a refresh?" -> POST /accounts/{account_id}/magic/cloud/catalog-syncs/{sync_id}/refresh
- "List all onramps?" -> GET /accounts/{account_id}/magic/cloud/onramps
- "Create a onramp?" -> POST /accounts/{account_id}/magic/cloud/onramps
- "List all magic_wan_address_space?" -> GET /accounts/{account_id}/magic/cloud/onramps/magic_wan_address_space
- "Delete a onramp?" -> DELETE /accounts/{account_id}/magic/cloud/onramps/{onramp_id}
- "Get onramp details?" -> GET /accounts/{account_id}/magic/cloud/onramps/{onramp_id}
- "Partially update a onramp?" -> PATCH /accounts/{account_id}/magic/cloud/onramps/{onramp_id}
- "Update a onramp?" -> PUT /accounts/{account_id}/magic/cloud/onramps/{onramp_id}
- "Create a apply?" -> POST /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/apply
- "Create a export?" -> POST /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/export
- "Create a plan?" -> POST /accounts/{account_id}/magic/cloud/onramps/{onramp_id}/plan
- "List all providers?" -> GET /accounts/{account_id}/magic/cloud/providers
- "Create a provider?" -> POST /accounts/{account_id}/magic/cloud/providers
- "Create a discover?" -> POST /accounts/{account_id}/magic/cloud/providers/discover
- "Delete a provider?" -> DELETE /accounts/{account_id}/magic/cloud/providers/{provider_id}
- "Get provider details?" -> GET /accounts/{account_id}/magic/cloud/providers/{provider_id}
- "Partially update a provider?" -> PATCH /accounts/{account_id}/magic/cloud/providers/{provider_id}
- "Update a provider?" -> PUT /accounts/{account_id}/magic/cloud/providers/{provider_id}
- "Create a discover?" -> POST /accounts/{account_id}/magic/cloud/providers/{provider_id}/discover
- "List all initial_setup?" -> GET /accounts/{account_id}/magic/cloud/providers/{provider_id}/initial_setup
- "Search resources?" -> GET /accounts/{account_id}/magic/cloud/resources
- "Search export?" -> GET /accounts/{account_id}/magic/cloud/resources/export
- "Create a policy-preview?" -> POST /accounts/{account_id}/magic/cloud/resources/policy-preview
- "Get resource details?" -> GET /accounts/{account_id}/magic/cloud/resources/{resource_id}
- "List all connectors?" -> GET /accounts/{account_id}/magic/connectors
- "Create a connector?" -> POST /accounts/{account_id}/magic/connectors
- "Delete a connector?" -> DELETE /accounts/{account_id}/magic/connectors/{connector_id}
- "Get connector details?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}
- "Partially update a connector?" -> PATCH /accounts/{account_id}/magic/connectors/{connector_id}
- "Update a connector?" -> PUT /accounts/{account_id}/magic/connectors/{connector_id}
- "List all events?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events
- "List all latest?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events/latest
- "Get event details?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/events/{event_t}.{event_n}
- "List all snapshots?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots
- "List all latest?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots/latest
- "Get snapshot details?" -> GET /accounts/{account_id}/magic/connectors/{connector_id}/telemetry/snapshots/{snapshot_t}
- "List all gre_tunnels?" -> GET /accounts/{account_id}/magic/gre_tunnels
- "Create a gre_tunnel?" -> POST /accounts/{account_id}/magic/gre_tunnels
- "Delete a gre_tunnel?" -> DELETE /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id}
- "Get gre_tunnel details?" -> GET /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id}
- "Update a gre_tunnel?" -> PUT /accounts/{account_id}/magic/gre_tunnels/{gre_tunnel_id}
- "List all ipsec_tunnels?" -> GET /accounts/{account_id}/magic/ipsec_tunnels
- "Create a ipsec_tunnel?" -> POST /accounts/{account_id}/magic/ipsec_tunnels
- "Delete a ipsec_tunnel?" -> DELETE /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id}
- "Get ipsec_tunnel details?" -> GET /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id}
- "Update a ipsec_tunnel?" -> PUT /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id}
- "Create a psk_generate?" -> POST /accounts/{account_id}/magic/ipsec_tunnels/{ipsec_tunnel_id}/psk_generate
- "List all routes?" -> GET /accounts/{account_id}/magic/routes
- "Create a route?" -> POST /accounts/{account_id}/magic/routes
- "Delete a route?" -> DELETE /accounts/{account_id}/magic/routes/{route_id}
- "Get route details?" -> GET /accounts/{account_id}/magic/routes/{route_id}
- "Update a route?" -> PUT /accounts/{account_id}/magic/routes/{route_id}
- "List all sites?" -> GET /accounts/{account_id}/magic/sites
- "Create a site?" -> POST /accounts/{account_id}/magic/sites
- "Delete a site?" -> DELETE /accounts/{account_id}/magic/sites/{site_id}
- "Get site details?" -> GET /accounts/{account_id}/magic/sites/{site_id}
- "Partially update a site?" -> PATCH /accounts/{account_id}/magic/sites/{site_id}
- "Update a site?" -> PUT /accounts/{account_id}/magic/sites/{site_id}
- "List all acls?" -> GET /accounts/{account_id}/magic/sites/{site_id}/acls
- "Create a acl?" -> POST /accounts/{account_id}/magic/sites/{site_id}/acls
- "Delete a acl?" -> DELETE /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id}
- "Get acl details?" -> GET /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id}
- "Partially update a acl?" -> PATCH /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id}
- "Update a acl?" -> PUT /accounts/{account_id}/magic/sites/{site_id}/acls/{acl_id}
- "List all app_configs?" -> GET /accounts/{account_id}/magic/sites/{site_id}/app_configs
- "Create a app_config?" -> POST /accounts/{account_id}/magic/sites/{site_id}/app_configs
- "Delete a app_config?" -> DELETE /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id}
- "Partially update a app_config?" -> PATCH /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id}
- "Update a app_config?" -> PUT /accounts/{account_id}/magic/sites/{site_id}/app_configs/{app_config_id}
- "List all lans?" -> GET /accounts/{account_id}/magic/sites/{site_id}/lans
- "Create a lan?" -> POST /accounts/{account_id}/magic/sites/{site_id}/lans
- "Delete a lan?" -> DELETE /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id}
- "Get lan details?" -> GET /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id}
- "Partially update a lan?" -> PATCH /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id}
- "Update a lan?" -> PUT /accounts/{account_id}/magic/sites/{site_id}/lans/{lan_id}
- "List all netflow_config?" -> GET /accounts/{account_id}/magic/sites/{site_id}/netflow_config
- "Create a netflow_config?" -> POST /accounts/{account_id}/magic/sites/{site_id}/netflow_config
- "List all wans?" -> GET /accounts/{account_id}/magic/sites/{site_id}/wans
- "Create a wan?" -> POST /accounts/{account_id}/magic/sites/{site_id}/wans
- "Delete a wan?" -> DELETE /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id}
- "Get wan details?" -> GET /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id}
- "Partially update a wan?" -> PATCH /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id}
- "Update a wan?" -> PUT /accounts/{account_id}/magic/sites/{site_id}/wans/{wan_id}
- "List all members?" -> GET /accounts/{account_id}/members
- "Create a member?" -> POST /accounts/{account_id}/members
- "Delete a member?" -> DELETE /accounts/{account_id}/members/{member_id}
- "Get member details?" -> GET /accounts/{account_id}/members/{member_id}
- "Update a member?" -> PUT /accounts/{account_id}/members/{member_id}
- "List all config?" -> GET /accounts/{account_id}/mnm/config
- "Create a config?" -> POST /accounts/{account_id}/mnm/config
- "List all full?" -> GET /accounts/{account_id}/mnm/config/full
- "List all rules?" -> GET /accounts/{account_id}/mnm/rules
- "Create a rule?" -> POST /accounts/{account_id}/mnm/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/mnm/rules/{rule_id}
- "Get rule details?" -> GET /accounts/{account_id}/mnm/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/mnm/rules/{rule_id}
- "Create a token?" -> POST /accounts/{account_id}/mnm/vpc-flows/token
- "Create a move?" -> POST /accounts/{account_id}/move
- "List all mtls_certificates?" -> GET /accounts/{account_id}/mtls_certificates
- "Create a mtls_certificate?" -> POST /accounts/{account_id}/mtls_certificates
- "Delete a mtls_certificate?" -> DELETE /accounts/{account_id}/mtls_certificates/{mtls_certificate_id}
- "Get mtls_certificate details?" -> GET /accounts/{account_id}/mtls_certificates/{mtls_certificate_id}
- "List all associations?" -> GET /accounts/{account_id}/mtls_certificates/{mtls_certificate_id}/associations
- "List all organizations?" -> GET /accounts/{account_id}/organizations
- "List all projects?" -> GET /accounts/{account_id}/pages/projects
- "Create a project?" -> POST /accounts/{account_id}/pages/projects
- "Delete a project?" -> DELETE /accounts/{account_id}/pages/projects/{project_name}
- "Get project details?" -> GET /accounts/{account_id}/pages/projects/{project_name}
- "Partially update a project?" -> PATCH /accounts/{account_id}/pages/projects/{project_name}
- "List all deployments?" -> GET /accounts/{account_id}/pages/projects/{project_name}/deployments
- "Create a deployment?" -> POST /accounts/{account_id}/pages/projects/{project_name}/deployments
- "Delete a deployment?" -> DELETE /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}
- "Get deployment details?" -> GET /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}
- "List all logs?" -> GET /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/history/logs
- "Create a retry?" -> POST /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/retry
- "Create a rollback?" -> POST /accounts/{account_id}/pages/projects/{project_name}/deployments/{deployment_id}/rollback
- "List all domains?" -> GET /accounts/{account_id}/pages/projects/{project_name}/domains
- "Create a domain?" -> POST /accounts/{account_id}/pages/projects/{project_name}/domains
- "Delete a domain?" -> DELETE /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name}
- "Get domain details?" -> GET /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name}
- "Partially update a domain?" -> PATCH /accounts/{account_id}/pages/projects/{project_name}/domains/{domain_name}
- "Create a purge_build_cache?" -> POST /accounts/{account_id}/pages/projects/{project_name}/purge_build_cache
- "List all stripe?" -> GET /accounts/{account_id}/pay-per-crawl/crawler/stripe
- "Create a stripe?" -> POST /accounts/{account_id}/pay-per-crawl/crawler/stripe
- "List all stripe?" -> GET /accounts/{account_id}/pay-per-crawl/publisher/stripe
- "Create a stripe?" -> POST /accounts/{account_id}/pay-per-crawl/publisher/stripe
- "Create a query?" -> POST /accounts/{account_id}/pay-per-crawl/zones_can_be_enabled/query
- "List all pcaps?" -> GET /accounts/{account_id}/pcaps
- "Create a pcap?" -> POST /accounts/{account_id}/pcaps
- "List all ownership?" -> GET /accounts/{account_id}/pcaps/ownership
- "Create a ownership?" -> POST /accounts/{account_id}/pcaps/ownership
- "Create a validate?" -> POST /accounts/{account_id}/pcaps/ownership/validate
- "Delete a ownership?" -> DELETE /accounts/{account_id}/pcaps/ownership/{ownership_id}
- "Get pcap details?" -> GET /accounts/{account_id}/pcaps/{pcap_id}
- "List all download?" -> GET /accounts/{account_id}/pcaps/{pcap_id}/download
- "Search pipelines?" -> GET /accounts/{account_id}/pipelines
- "Create a pipeline?" -> POST /accounts/{account_id}/pipelines
- "List all pipelines?" -> GET /accounts/{account_id}/pipelines/v1/pipelines
- "Create a pipeline?" -> POST /accounts/{account_id}/pipelines/v1/pipelines
- "Delete a pipeline?" -> DELETE /accounts/{account_id}/pipelines/v1/pipelines/{pipeline_id}
- "Get pipeline details?" -> GET /accounts/{account_id}/pipelines/v1/pipelines/{pipeline_id}
- "List all sinks?" -> GET /accounts/{account_id}/pipelines/v1/sinks
- "Create a sink?" -> POST /accounts/{account_id}/pipelines/v1/sinks
- "Delete a sink?" -> DELETE /accounts/{account_id}/pipelines/v1/sinks/{sink_id}
- "Get sink details?" -> GET /accounts/{account_id}/pipelines/v1/sinks/{sink_id}
- "List all streams?" -> GET /accounts/{account_id}/pipelines/v1/streams
- "Create a stream?" -> POST /accounts/{account_id}/pipelines/v1/streams
- "Delete a stream?" -> DELETE /accounts/{account_id}/pipelines/v1/streams/{stream_id}
- "Get stream details?" -> GET /accounts/{account_id}/pipelines/v1/streams/{stream_id}
- "Partially update a stream?" -> PATCH /accounts/{account_id}/pipelines/v1/streams/{stream_id}
- "Create a validate_sql?" -> POST /accounts/{account_id}/pipelines/v1/validate_sql
- "Delete a pipeline?" -> DELETE /accounts/{account_id}/pipelines/{pipeline_name}
- "Get pipeline details?" -> GET /accounts/{account_id}/pipelines/{pipeline_name}
- "Update a pipeline?" -> PUT /accounts/{account_id}/pipelines/{pipeline_name}
- "List all profile?" -> GET /accounts/{account_id}/profile
- "List all queues?" -> GET /accounts/{account_id}/queues
- "Create a queue?" -> POST /accounts/{account_id}/queues
- "Delete a queue?" -> DELETE /accounts/{account_id}/queues/{queue_id}
- "Get queue details?" -> GET /accounts/{account_id}/queues/{queue_id}
- "Partially update a queue?" -> PATCH /accounts/{account_id}/queues/{queue_id}
- "Update a queue?" -> PUT /accounts/{account_id}/queues/{queue_id}
- "List all consumers?" -> GET /accounts/{account_id}/queues/{queue_id}/consumers
- "Create a consumer?" -> POST /accounts/{account_id}/queues/{queue_id}/consumers
- "Delete a consumer?" -> DELETE /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id}
- "Get consumer details?" -> GET /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id}
- "Update a consumer?" -> PUT /accounts/{account_id}/queues/{queue_id}/consumers/{consumer_id}
- "Create a message?" -> POST /accounts/{account_id}/queues/{queue_id}/messages
- "Create a ack?" -> POST /accounts/{account_id}/queues/{queue_id}/messages/ack
- "Create a batch?" -> POST /accounts/{account_id}/queues/{queue_id}/messages/batch
- "Create a pull?" -> POST /accounts/{account_id}/queues/{queue_id}/messages/pull
- "List all purge?" -> GET /accounts/{account_id}/queues/{queue_id}/purge
- "Create a purge?" -> POST /accounts/{account_id}/queues/{queue_id}/purge
- "List all r2-catalog?" -> GET /accounts/{account_id}/r2-catalog
- "Get r2-catalog details?" -> GET /accounts/{account_id}/r2-catalog/{bucket_name}
- "Create a credential?" -> POST /accounts/{account_id}/r2-catalog/{bucket_name}/credential
- "Create a disable?" -> POST /accounts/{account_id}/r2-catalog/{bucket_name}/disable
- "Create a enable?" -> POST /accounts/{account_id}/r2-catalog/{bucket_name}/enable
- "List all maintenance-configs?" -> GET /accounts/{account_id}/r2-catalog/{bucket_name}/maintenance-configs
- "Create a maintenance-config?" -> POST /accounts/{account_id}/r2-catalog/{bucket_name}/maintenance-configs
- "List all namespaces?" -> GET /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces
- "List all tables?" -> GET /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables
- "List all maintenance-configs?" -> GET /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables/{table_name}/maintenance-configs
- "Create a maintenance-config?" -> POST /accounts/{account_id}/r2-catalog/{bucket_name}/namespaces/{namespace}/tables/{table_name}/maintenance-configs
- "List all buckets?" -> GET /accounts/{account_id}/r2/buckets
- "Create a bucket?" -> POST /accounts/{account_id}/r2/buckets
- "Delete a bucket?" -> DELETE /accounts/{account_id}/r2/buckets/{bucket_name}
- "Get bucket details?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}
- "Partially update a bucket?" -> PATCH /accounts/{account_id}/r2/buckets/{bucket_name}
- "List all cors?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/cors
- "List all custom?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom
- "Create a custom?" -> POST /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom
- "Delete a custom?" -> DELETE /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain}
- "Get custom details?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain}
- "Update a custom?" -> PUT /accounts/{account_id}/r2/buckets/{bucket_name}/domains/custom/{domain}
- "List all managed?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/domains/managed
- "List all lifecycle?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/lifecycle
- "List all local-uploads?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/local-uploads
- "List all lock?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/lock
- "List all sippy?" -> GET /accounts/{account_id}/r2/buckets/{bucket_name}/sippy
- "List all metrics?" -> GET /accounts/{account_id}/r2/metrics
- "Create a temp-access-credential?" -> POST /accounts/{account_id}/r2/temp-access-credentials
- "List all apps?" -> GET /accounts/{account_id}/realtime/kit/apps
- "Create a app?" -> POST /accounts/{account_id}/realtime/kit/apps
- "List all daywise?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/analytics/daywise
- "List all overall?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/analytics/livestreams/overall
- "List all livestreams?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/livestreams
- "Create a livestream?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/livestreams
- "Get session details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/livestreams/sessions/{livestream-session-id}
- "Get livestream details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/livestreams/{livestream_id}
- "List all active-livestream-session?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/livestreams/{livestream_id}/active-livestream-session
- "Search meetings?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings
- "Create a meeting?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings
- "Get meeting details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}
- "Partially update a meeting?" -> PATCH /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}
- "Update a meeting?" -> PUT /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}
- "List all active-livestream?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-livestream
- "Create a stop?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-livestream/stop
- "List all active-session?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session
- "Create a kick?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/kick
- "Create a kick-all?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/kick-all
- "Create a mute?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/mute
- "Create a mute-all?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/mute-all
- "Create a poll?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/active-session/poll
- "List all livestream?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/livestream
- "Create a livestream?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/livestreams
- "List all participants?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants
- "Create a participant?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants
- "Delete a participant?" -> DELETE /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id}
- "Get participant details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id}
- "Partially update a participant?" -> PATCH /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id}
- "Create a token?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/meetings/{meeting_id}/participants/{participant_id}/token
- "List all presets?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/presets
- "Create a preset?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/presets
- "Delete a preset?" -> DELETE /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id}
- "Get preset details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id}
- "Partially update a preset?" -> PATCH /accounts/{account_id}/realtime/kit/{app_id}/presets/{preset_id}
- "Search recordings?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/recordings
- "Create a recording?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/recordings
- "Get active-recording details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/recordings/active-recording/{meeting_id}
- "Create a track?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/recordings/track
- "Get recording details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/recordings/{recording_id}
- "Update a recording?" -> PUT /accounts/{account_id}/realtime/kit/{app_id}/recordings/{recording_id}
- "Search sessions?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions
- "Get peer-report details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/peer-report/{peer_id}
- "Get session details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}
- "List all chat?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/chat
- "List all livestream-sessions?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/livestream-sessions
- "Search participants?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/participants
- "Get participant details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/participants/{participant_id}
- "List all summary?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/summary
- "Create a summary?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/summary
- "List all transcript?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/sessions/{session_id}/transcript
- "List all webhooks?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/webhooks
- "Create a webhook?" -> POST /accounts/{account_id}/realtime/kit/{app_id}/webhooks
- "Delete a webhook?" -> DELETE /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id}
- "Get webhook details?" -> GET /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id}
- "Partially update a webhook?" -> PATCH /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id}
- "Update a webhook?" -> PUT /accounts/{account_id}/realtime/kit/{app_id}/webhooks/{webhook_id}
- "List all domains?" -> GET /accounts/{account_id}/registrar/domains
- "Get domain details?" -> GET /accounts/{account_id}/registrar/domains/{domain_name}
- "Update a domain?" -> PUT /accounts/{account_id}/registrar/domains/{domain_name}
- "Create a trace?" -> POST /accounts/{account_id}/request-tracer/trace
- "List all roles?" -> GET /accounts/{account_id}/roles
- "Get role details?" -> GET /accounts/{account_id}/roles/{role_id}
- "List all lists?" -> GET /accounts/{account_id}/rules/lists
- "Create a list?" -> POST /accounts/{account_id}/rules/lists
- "Get bulk_operation details?" -> GET /accounts/{account_id}/rules/lists/bulk_operations/{operation_id}
- "Delete a list?" -> DELETE /accounts/{account_id}/rules/lists/{list_id}
- "Get list details?" -> GET /accounts/{account_id}/rules/lists/{list_id}
- "Update a list?" -> PUT /accounts/{account_id}/rules/lists/{list_id}
- "Search items?" -> GET /accounts/{account_id}/rules/lists/{list_id}/items
- "Create a item?" -> POST /accounts/{account_id}/rules/lists/{list_id}/items
- "Get item details?" -> GET /accounts/{account_id}/rules/lists/{list_id}/items/{item_id}
- "List all rulesets?" -> GET /accounts/{account_id}/rulesets
- "Create a ruleset?" -> POST /accounts/{account_id}/rulesets
- "List all entrypoint?" -> GET /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint
- "List all versions?" -> GET /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions
- "Get version details?" -> GET /accounts/{account_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions/{ruleset_version}
- "Delete a ruleset?" -> DELETE /accounts/{account_id}/rulesets/{ruleset_id}
- "Get ruleset details?" -> GET /accounts/{account_id}/rulesets/{ruleset_id}
- "Update a ruleset?" -> PUT /accounts/{account_id}/rulesets/{ruleset_id}
- "Create a rule?" -> POST /accounts/{account_id}/rulesets/{ruleset_id}/rules
- "Delete a rule?" -> DELETE /accounts/{account_id}/rulesets/{ruleset_id}/rules/{rule_id}
- "Partially update a rule?" -> PATCH /accounts/{account_id}/rulesets/{ruleset_id}/rules/{rule_id}
- "List all versions?" -> GET /accounts/{account_id}/rulesets/{ruleset_id}/versions
- "Delete a version?" -> DELETE /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version}
- "Get version details?" -> GET /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version}
- "Get by_tag details?" -> GET /accounts/{account_id}/rulesets/{ruleset_id}/versions/{ruleset_version}/by_tag/{rule_tag}
- "Create a site_info?" -> POST /accounts/{account_id}/rum/site_info
- "List all list?" -> GET /accounts/{account_id}/rum/site_info/list
- "Delete a site_info?" -> DELETE /accounts/{account_id}/rum/site_info/{site_id}
- "Get site_info details?" -> GET /accounts/{account_id}/rum/site_info/{site_id}
- "Update a site_info?" -> PUT /accounts/{account_id}/rum/site_info/{site_id}
- "Create a rule?" -> POST /accounts/{account_id}/rum/v2/{ruleset_id}/rule
- "Delete a rule?" -> DELETE /accounts/{account_id}/rum/v2/{ruleset_id}/rule/{rule_id}
- "Update a rule?" -> PUT /accounts/{account_id}/rum/v2/{ruleset_id}/rule/{rule_id}
- "List all rules?" -> GET /accounts/{account_id}/rum/v2/{ruleset_id}/rules
- "Create a rule?" -> POST /accounts/{account_id}/rum/v2/{ruleset_id}/rules
- "List all acls?" -> GET /accounts/{account_id}/secondary_dns/acls
- "Create a acl?" -> POST /accounts/{account_id}/secondary_dns/acls
- "Delete a acl?" -> DELETE /accounts/{account_id}/secondary_dns/acls/{acl_id}
- "Get acl details?" -> GET /accounts/{account_id}/secondary_dns/acls/{acl_id}
- "Update a acl?" -> PUT /accounts/{account_id}/secondary_dns/acls/{acl_id}
- "List all peers?" -> GET /accounts/{account_id}/secondary_dns/peers
- "Create a peer?" -> POST /accounts/{account_id}/secondary_dns/peers
- "Delete a peer?" -> DELETE /accounts/{account_id}/secondary_dns/peers/{peer_id}
- "Get peer details?" -> GET /accounts/{account_id}/secondary_dns/peers/{peer_id}
- "Update a peer?" -> PUT /accounts/{account_id}/secondary_dns/peers/{peer_id}
- "List all tsigs?" -> GET /accounts/{account_id}/secondary_dns/tsigs
- "Create a tsig?" -> POST /accounts/{account_id}/secondary_dns/tsigs
- "Delete a tsig?" -> DELETE /accounts/{account_id}/secondary_dns/tsigs/{tsig_id}
- "Get tsig details?" -> GET /accounts/{account_id}/secondary_dns/tsigs/{tsig_id}
- "Update a tsig?" -> PUT /accounts/{account_id}/secondary_dns/tsigs/{tsig_id}
- "List all quota?" -> GET /accounts/{account_id}/secrets_store/quota
- "List all stores?" -> GET /accounts/{account_id}/secrets_store/stores
- "Create a store?" -> POST /accounts/{account_id}/secrets_store/stores
- "Delete a store?" -> DELETE /accounts/{account_id}/secrets_store/stores/{store_id}
- "Search secrets?" -> GET /accounts/{account_id}/secrets_store/stores/{store_id}/secrets
- "Create a secret?" -> POST /accounts/{account_id}/secrets_store/stores/{store_id}/secrets
- "Delete a secret?" -> DELETE /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id}
- "Get secret details?" -> GET /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id}
- "Partially update a secret?" -> PATCH /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id}
- "Create a duplicate?" -> POST /accounts/{account_id}/secrets_store/stores/{store_id}/secrets/{secret_id}/duplicate
- "List all insights?" -> GET /accounts/{account_id}/security-center/insights
- "List all class?" -> GET /accounts/{account_id}/security-center/insights/class
- "List all severity?" -> GET /accounts/{account_id}/security-center/insights/severity
- "List all type?" -> GET /accounts/{account_id}/security-center/insights/type
- "List all shares?" -> GET /accounts/{account_id}/shares
- "Create a share?" -> POST /accounts/{account_id}/shares
- "Delete a share?" -> DELETE /accounts/{account_id}/shares/{share_id}
- "Get share details?" -> GET /accounts/{account_id}/shares/{share_id}
- "Update a share?" -> PUT /accounts/{account_id}/shares/{share_id}
- "List all recipients?" -> GET /accounts/{account_id}/shares/{share_id}/recipients
- "Create a recipient?" -> POST /accounts/{account_id}/shares/{share_id}/recipients
- "Delete a recipient?" -> DELETE /accounts/{account_id}/shares/{share_id}/recipients/{recipient_id}
- "Get recipient details?" -> GET /accounts/{account_id}/shares/{share_id}/recipients/{recipient_id}
- "List all resources?" -> GET /accounts/{account_id}/shares/{share_id}/resources
- "Create a resource?" -> POST /accounts/{account_id}/shares/{share_id}/resources
- "Delete a resource?" -> DELETE /accounts/{account_id}/shares/{share_id}/resources/{resource_id}
- "Get resource details?" -> GET /accounts/{account_id}/shares/{share_id}/resources/{resource_id}
- "Update a resource?" -> PUT /accounts/{account_id}/shares/{share_id}/resources/{resource_id}
- "List all jobs?" -> GET /accounts/{account_id}/slurper/jobs
- "Create a job?" -> POST /accounts/{account_id}/slurper/jobs
- "Get job details?" -> GET /accounts/{account_id}/slurper/jobs/{job_id}
- "List all logs?" -> GET /accounts/{account_id}/slurper/jobs/{job_id}/logs
- "List all progress?" -> GET /accounts/{account_id}/slurper/jobs/{job_id}/progress
- "List all sso_connectors?" -> GET /accounts/{account_id}/sso_connectors
- "Create a sso_connector?" -> POST /accounts/{account_id}/sso_connectors
- "Delete a sso_connector?" -> DELETE /accounts/{account_id}/sso_connectors/{sso_connector_id}
- "Get sso_connector details?" -> GET /accounts/{account_id}/sso_connectors/{sso_connector_id}
- "Partially update a sso_connector?" -> PATCH /accounts/{account_id}/sso_connectors/{sso_connector_id}
- "Create a begin_verification?" -> POST /accounts/{account_id}/sso_connectors/{sso_connector_id}/begin_verification
- "List all namespaces?" -> GET /accounts/{account_id}/storage/kv/namespaces
- "Create a namespace?" -> POST /accounts/{account_id}/storage/kv/namespaces
- "Delete a namespace?" -> DELETE /accounts/{account_id}/storage/kv/namespaces/{namespace_id}
- "Get namespace details?" -> GET /accounts/{account_id}/storage/kv/namespaces/{namespace_id}
- "Update a namespace?" -> PUT /accounts/{account_id}/storage/kv/namespaces/{namespace_id}
- "Create a delete?" -> POST /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk/delete
- "Create a get?" -> POST /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/bulk/get
- "List all keys?" -> GET /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/keys
- "Get metadata details?" -> GET /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/metadata/{key_name}
- "Delete a value?" -> DELETE /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name}
- "Get value details?" -> GET /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name}
- "Update a value?" -> PUT /accounts/{account_id}/storage/kv/namespaces/{namespace_id}/values/{key_name}
- "Search stream?" -> GET /accounts/{account_id}/stream
- "Create a stream?" -> POST /accounts/{account_id}/stream
- "Create a clip?" -> POST /accounts/{account_id}/stream/clip
- "Create a copy?" -> POST /accounts/{account_id}/stream/copy
- "Create a direct_upload?" -> POST /accounts/{account_id}/stream/direct_upload
- "List all keys?" -> GET /accounts/{account_id}/stream/keys
- "Create a key?" -> POST /accounts/{account_id}/stream/keys
- "Delete a key?" -> DELETE /accounts/{account_id}/stream/keys/{identifier}
- "List all live_inputs?" -> GET /accounts/{account_id}/stream/live_inputs
- "Create a live_input?" -> POST /accounts/{account_id}/stream/live_inputs
- "Delete a live_input?" -> DELETE /accounts/{account_id}/stream/live_inputs/{live_input_identifier}
- "Get live_input details?" -> GET /accounts/{account_id}/stream/live_inputs/{live_input_identifier}
- "Update a live_input?" -> PUT /accounts/{account_id}/stream/live_inputs/{live_input_identifier}
- "Create a disable?" -> POST /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/disable
- "Create a enable?" -> POST /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/enable
- "List all outputs?" -> GET /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs
- "Create a output?" -> POST /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs
- "Delete a output?" -> DELETE /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs/{output_identifier}
- "Update a output?" -> PUT /accounts/{account_id}/stream/live_inputs/{live_input_identifier}/outputs/{output_identifier}
- "List all storage-usage?" -> GET /accounts/{account_id}/stream/storage-usage
- "List all watermarks?" -> GET /accounts/{account_id}/stream/watermarks
- "Create a watermark?" -> POST /accounts/{account_id}/stream/watermarks
- "Delete a watermark?" -> DELETE /accounts/{account_id}/stream/watermarks/{identifier}
- "Get watermark details?" -> GET /accounts/{account_id}/stream/watermarks/{identifier}
- "List all webhook?" -> GET /accounts/{account_id}/stream/webhook
- "Delete a stream?" -> DELETE /accounts/{account_id}/stream/{identifier}
- "Get stream details?" -> GET /accounts/{account_id}/stream/{identifier}
- "List all audio?" -> GET /accounts/{account_id}/stream/{identifier}/audio
- "Create a copy?" -> POST /accounts/{account_id}/stream/{identifier}/audio/copy
- "Delete a audio?" -> DELETE /accounts/{account_id}/stream/{identifier}/audio/{audio_identifier}
- "Partially update a audio?" -> PATCH /accounts/{account_id}/stream/{identifier}/audio/{audio_identifier}
- "List all captions?" -> GET /accounts/{account_id}/stream/{identifier}/captions
- "Delete a caption?" -> DELETE /accounts/{account_id}/stream/{identifier}/captions/{language}
- "Get caption details?" -> GET /accounts/{account_id}/stream/{identifier}/captions/{language}
- "Update a caption?" -> PUT /accounts/{account_id}/stream/{identifier}/captions/{language}
- "Create a generate?" -> POST /accounts/{account_id}/stream/{identifier}/captions/{language}/generate
- "List all vtt?" -> GET /accounts/{account_id}/stream/{identifier}/captions/{language}/vtt
- "List all downloads?" -> GET /accounts/{account_id}/stream/{identifier}/downloads
- "Create a download?" -> POST /accounts/{account_id}/stream/{identifier}/downloads
- "Delete a download?" -> DELETE /accounts/{account_id}/stream/{identifier}/downloads/{download_type}
- "List all embed?" -> GET /accounts/{account_id}/stream/{identifier}/embed
- "Create a token?" -> POST /accounts/{account_id}/stream/{identifier}/token
- "List all subscriptions?" -> GET /accounts/{account_id}/subscriptions
- "Create a subscription?" -> POST /accounts/{account_id}/subscriptions
- "Delete a subscription?" -> DELETE /accounts/{account_id}/subscriptions/{subscription_identifier}
- "Update a subscription?" -> PUT /accounts/{account_id}/subscriptions/{subscription_identifier}
- "List all routes?" -> GET /accounts/{account_id}/teamnet/routes
- "Create a route?" -> POST /accounts/{account_id}/teamnet/routes
- "Get ip details?" -> GET /accounts/{account_id}/teamnet/routes/ip/{ip}
- "Delete a network?" -> DELETE /accounts/{account_id}/teamnet/routes/network/{ip_network_encoded}
- "Partially update a network?" -> PATCH /accounts/{account_id}/teamnet/routes/network/{ip_network_encoded}
- "Delete a route?" -> DELETE /accounts/{account_id}/teamnet/routes/{route_id}
- "Get route details?" -> GET /accounts/{account_id}/teamnet/routes/{route_id}
- "Partially update a route?" -> PATCH /accounts/{account_id}/teamnet/routes/{route_id}
- "List all virtual_networks?" -> GET /accounts/{account_id}/teamnet/virtual_networks
- "Create a virtual_network?" -> POST /accounts/{account_id}/teamnet/virtual_networks
- "Delete a virtual_network?" -> DELETE /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id}
- "Get virtual_network details?" -> GET /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id}
- "Partially update a virtual_network?" -> PATCH /accounts/{account_id}/teamnet/virtual_networks/{virtual_network_id}
- "List all tokens?" -> GET /accounts/{account_id}/tokens
- "Create a token?" -> POST /accounts/{account_id}/tokens
- "List all permission_groups?" -> GET /accounts/{account_id}/tokens/permission_groups
- "List all verify?" -> GET /accounts/{account_id}/tokens/verify
- "Delete a token?" -> DELETE /accounts/{account_id}/tokens/{token_id}
- "Get token details?" -> GET /accounts/{account_id}/tokens/{token_id}
- "Update a token?" -> PUT /accounts/{account_id}/tokens/{token_id}
- "List all tunnels?" -> GET /accounts/{account_id}/tunnels
- "Get response details?" -> GET /accounts/{account_id}/urlscanner/response/{response_id}
- "List all scan?" -> GET /accounts/{account_id}/urlscanner/scan
- "Create a scan?" -> POST /accounts/{account_id}/urlscanner/scan
- "Get scan details?" -> GET /accounts/{account_id}/urlscanner/scan/{scan_id}
- "List all har?" -> GET /accounts/{account_id}/urlscanner/scan/{scan_id}/har
- "List all screenshot?" -> GET /accounts/{account_id}/urlscanner/scan/{scan_id}/screenshot
- "Create a bulk?" -> POST /accounts/{account_id}/urlscanner/v2/bulk
- "Get dom details?" -> GET /accounts/{account_id}/urlscanner/v2/dom/{scan_id}
- "Get har details?" -> GET /accounts/{account_id}/urlscanner/v2/har/{scan_id}
- "Get response details?" -> GET /accounts/{account_id}/urlscanner/v2/responses/{response_id}
- "Get result details?" -> GET /accounts/{account_id}/urlscanner/v2/result/{scan_id}
- "Create a scan?" -> POST /accounts/{account_id}/urlscanner/v2/scan
- "Get screenshot details?" -> GET /accounts/{account_id}/urlscanner/v2/screenshots/{scan_id}.png
- "Search search?" -> GET /accounts/{account_id}/urlscanner/v2/search
- "List all indexes?" -> GET /accounts/{account_id}/vectorize/indexes
- "Create a indexe?" -> POST /accounts/{account_id}/vectorize/indexes
- "Delete a indexe?" -> DELETE /accounts/{account_id}/vectorize/indexes/{index_name}
- "Get indexe details?" -> GET /accounts/{account_id}/vectorize/indexes/{index_name}
- "Update a indexe?" -> PUT /accounts/{account_id}/vectorize/indexes/{index_name}
- "Create a delete-by-id?" -> POST /accounts/{account_id}/vectorize/indexes/{index_name}/delete-by-ids
- "Create a get-by-id?" -> POST /accounts/{account_id}/vectorize/indexes/{index_name}/get-by-ids
- "Create a insert?" -> POST /accounts/{account_id}/vectorize/indexes/{index_name}/insert
- "Create a query?" -> POST /accounts/{account_id}/vectorize/indexes/{index_name}/query
- "Create a upsert?" -> POST /accounts/{account_id}/vectorize/indexes/{index_name}/upsert
- "List all indexes?" -> GET /accounts/{account_id}/vectorize/v2/indexes
- "Create a indexe?" -> POST /accounts/{account_id}/vectorize/v2/indexes
- "Delete a indexe?" -> DELETE /accounts/{account_id}/vectorize/v2/indexes/{index_name}
- "Get indexe details?" -> GET /accounts/{account_id}/vectorize/v2/indexes/{index_name}
- "Create a delete_by_id?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/delete_by_ids
- "Create a get_by_id?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/get_by_ids
- "List all info?" -> GET /accounts/{account_id}/vectorize/v2/indexes/{index_name}/info
- "Create a insert?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/insert
- "List all list?" -> GET /accounts/{account_id}/vectorize/v2/indexes/{index_name}/list
- "Create a create?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/create
- "Create a delete?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/delete
- "List all list?" -> GET /accounts/{account_id}/vectorize/v2/indexes/{index_name}/metadata_index/list
- "Create a query?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/query
- "Create a upsert?" -> POST /accounts/{account_id}/vectorize/v2/indexes/{index_name}/upsert
- "List all waiting_rooms?" -> GET /accounts/{account_id}/waiting_rooms
- "List all warp_connector?" -> GET /accounts/{account_id}/warp_connector
- "Create a warp_connector?" -> POST /accounts/{account_id}/warp_connector
- "Delete a warp_connector?" -> DELETE /accounts/{account_id}/warp_connector/{tunnel_id}
- "Get warp_connector details?" -> GET /accounts/{account_id}/warp_connector/{tunnel_id}
- "Partially update a warp_connector?" -> PATCH /accounts/{account_id}/warp_connector/{tunnel_id}
- "List all token?" -> GET /accounts/{account_id}/warp_connector/{tunnel_id}/token
- "List all account-settings?" -> GET /accounts/{account_id}/workers/account-settings
- "Create a upload?" -> POST /accounts/{account_id}/workers/assets/upload
- "List all namespaces?" -> GET /accounts/{account_id}/workers/dispatch/namespaces
- "Create a namespace?" -> POST /accounts/{account_id}/workers/dispatch/namespaces
- "Delete a namespace?" -> DELETE /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}
- "Get namespace details?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}
- "Partially update a namespace?" -> PATCH /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}
- "Update a namespace?" -> PUT /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}
- "List all scripts?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts
- "Delete a script?" -> DELETE /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}
- "Get script details?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}
- "Update a script?" -> PUT /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}
- "Create a assets-upload-session?" -> POST /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/assets-upload-session
- "List all bindings?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/bindings
- "List all content?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/content
- "List all secrets?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets
- "Delete a secret?" -> DELETE /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets/{secret_name}
- "Get secret details?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/secrets/{secret_name}
- "List all settings?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/settings
- "List all tags?" -> GET /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags
- "Delete a tag?" -> DELETE /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags/{tag}
- "Update a tag?" -> PUT /accounts/{account_id}/workers/dispatch/namespaces/{dispatch_namespace}/scripts/{script_name}/tags/{tag}
- "List all domains?" -> GET /accounts/{account_id}/workers/domains
- "Delete a domain?" -> DELETE /accounts/{account_id}/workers/domains/{domain_id}
- "Get domain details?" -> GET /accounts/{account_id}/workers/domains/{domain_id}
- "List all namespaces?" -> GET /accounts/{account_id}/workers/durable_objects/namespaces
- "List all objects?" -> GET /accounts/{account_id}/workers/durable_objects/namespaces/{id}/objects
- "List all destinations?" -> GET /accounts/{account_id}/workers/observability/destinations
- "Create a destination?" -> POST /accounts/{account_id}/workers/observability/destinations
- "Delete a destination?" -> DELETE /accounts/{account_id}/workers/observability/destinations/{slug}
- "Partially update a destination?" -> PATCH /accounts/{account_id}/workers/observability/destinations/{slug}
- "Create a key?" -> POST /accounts/{account_id}/workers/observability/telemetry/keys
- "Create a query?" -> POST /accounts/{account_id}/workers/observability/telemetry/query
- "Create a value?" -> POST /accounts/{account_id}/workers/observability/telemetry/values
- "List all regions?" -> GET /accounts/{account_id}/workers/placement/regions
- "List all scripts?" -> GET /accounts/{account_id}/workers/scripts
- "List all scripts-search?" -> GET /accounts/{account_id}/workers/scripts-search
- "Delete a script?" -> DELETE /accounts/{account_id}/workers/scripts/{script_name}
- "Get script details?" -> GET /accounts/{account_id}/workers/scripts/{script_name}
- "Update a script?" -> PUT /accounts/{account_id}/workers/scripts/{script_name}
- "Create a assets-upload-session?" -> POST /accounts/{account_id}/workers/scripts/{script_name}/assets-upload-session
- "List all content?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/content/v2
- "List all deployments?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/deployments
- "Create a deployment?" -> POST /accounts/{account_id}/workers/scripts/{script_name}/deployments
- "Delete a deployment?" -> DELETE /accounts/{account_id}/workers/scripts/{script_name}/deployments/{deployment_id}
- "Get deployment details?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/deployments/{deployment_id}
- "List all schedules?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/schedules
- "List all script-settings?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/script-settings
- "List all secrets?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/secrets
- "Delete a secret?" -> DELETE /accounts/{account_id}/workers/scripts/{script_name}/secrets/{secret_name}
- "Get secret details?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/secrets/{secret_name}
- "List all settings?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/settings
- "List all subdomain?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/subdomain
- "Create a subdomain?" -> POST /accounts/{account_id}/workers/scripts/{script_name}/subdomain
- "List all tails?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/tails
- "Create a tail?" -> POST /accounts/{account_id}/workers/scripts/{script_name}/tails
- "Delete a tail?" -> DELETE /accounts/{account_id}/workers/scripts/{script_name}/tails/{id}
- "List all usage-model?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/usage-model
- "List all versions?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/versions
- "Create a version?" -> POST /accounts/{account_id}/workers/scripts/{script_name}/versions
- "Get version details?" -> GET /accounts/{account_id}/workers/scripts/{script_name}/versions/{version_id}
- "List all content?" -> GET /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/content
- "List all settings?" -> GET /accounts/{account_id}/workers/services/{service_name}/environments/{environment_name}/settings
- "List all subdomain?" -> GET /accounts/{account_id}/workers/subdomain
- "List all workers?" -> GET /accounts/{account_id}/workers/workers
- "Create a worker?" -> POST /accounts/{account_id}/workers/workers
- "Delete a worker?" -> DELETE /accounts/{account_id}/workers/workers/{worker_id}
- "Get worker details?" -> GET /accounts/{account_id}/workers/workers/{worker_id}
- "Partially update a worker?" -> PATCH /accounts/{account_id}/workers/workers/{worker_id}
- "Update a worker?" -> PUT /accounts/{account_id}/workers/workers/{worker_id}
- "List all versions?" -> GET /accounts/{account_id}/workers/workers/{worker_id}/versions
- "Create a version?" -> POST /accounts/{account_id}/workers/workers/{worker_id}/versions
- "Delete a version?" -> DELETE /accounts/{account_id}/workers/workers/{worker_id}/versions/{version_id}
- "Get version details?" -> GET /accounts/{account_id}/workers/workers/{worker_id}/versions/{version_id}
- "Search workflows?" -> GET /accounts/{account_id}/workflows
- "Delete a workflow?" -> DELETE /accounts/{account_id}/workflows/{workflow_name}
- "Get workflow details?" -> GET /accounts/{account_id}/workflows/{workflow_name}
- "Update a workflow?" -> PUT /accounts/{account_id}/workflows/{workflow_name}
- "List all instances?" -> GET /accounts/{account_id}/workflows/{workflow_name}/instances
- "Create a instance?" -> POST /accounts/{account_id}/workflows/{workflow_name}/instances
- "Create a batch?" -> POST /accounts/{account_id}/workflows/{workflow_name}/instances/batch
- "Create a terminate?" -> POST /accounts/{account_id}/workflows/{workflow_name}/instances/batch/terminate
- "List all terminate?" -> GET /accounts/{account_id}/workflows/{workflow_name}/instances/terminate
- "Get instance details?" -> GET /accounts/{account_id}/workflows/{workflow_name}/instances/{instance_id}
- "List all versions?" -> GET /accounts/{account_id}/workflows/{workflow_name}/versions
- "Get version details?" -> GET /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id}
- "List all dag?" -> GET /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id}/dag
- "List all graph?" -> GET /accounts/{account_id}/workflows/{workflow_name}/versions/{version_id}/graph
- "List all connectivity_settings?" -> GET /accounts/{account_id}/zerotrust/connectivity_settings
- "List all hostname?" -> GET /accounts/{account_id}/zerotrust/routes/hostname
- "Create a hostname?" -> POST /accounts/{account_id}/zerotrust/routes/hostname
- "Delete a hostname?" -> DELETE /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id}
- "Get hostname details?" -> GET /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id}
- "Partially update a hostname?" -> PATCH /accounts/{account_id}/zerotrust/routes/hostname/{hostname_route_id}
- "List all subnets?" -> GET /accounts/{account_id}/zerotrust/subnets
- "Partially update a cloudflare_source?" -> PATCH /accounts/{account_id}/zerotrust/subnets/cloudflare_source/{address_family}
- "Create a warp?" -> POST /accounts/{account_id}/zerotrust/subnets/warp
- "Delete a warp?" -> DELETE /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id}
- "Get warp details?" -> GET /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id}
- "Partially update a warp?" -> PATCH /accounts/{account_id}/zerotrust/subnets/warp/{subnet_id}
- "List all behaviors?" -> GET /accounts/{account_id}/zt_risk_scoring/behaviors
- "List all integrations?" -> GET /accounts/{account_id}/zt_risk_scoring/integrations
- "Create a integration?" -> POST /accounts/{account_id}/zt_risk_scoring/integrations
- "Get reference_id details?" -> GET /accounts/{account_id}/zt_risk_scoring/integrations/reference_id/{reference_id}
- "Delete a integration?" -> DELETE /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id}
- "Get integration details?" -> GET /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id}
- "Update a integration?" -> PUT /accounts/{account_id}/zt_risk_scoring/integrations/{integration_id}
- "List all summary?" -> GET /accounts/{account_id}/zt_risk_scoring/summary
- "Get zt_risk_scoring details?" -> GET /accounts/{account_id}/zt_risk_scoring/{user_id}
- "Create a reset?" -> POST /accounts/{account_id}/zt_risk_scoring/{user_id}/reset
- "List all certificates?" -> GET /certificates
- "Create a certificate?" -> POST /certificates
- "Delete a certificate?" -> DELETE /certificates/{certificate_id}
- "Get certificate details?" -> GET /certificates/{certificate_id}
- "Create a submit?" -> POST /internal/submit
- "List all ips?" -> GET /ips
- "List all live?" -> GET /live
- "List all memberships?" -> GET /memberships
- "Delete a membership?" -> DELETE /memberships/{membership_id}
- "Get membership details?" -> GET /memberships/{membership_id}
- "Update a membership?" -> PUT /memberships/{membership_id}
- "List all organizations?" -> GET /organizations
- "Create a organization?" -> POST /organizations
- "Delete a organization?" -> DELETE /organizations/{organization_id}
- "Get organization details?" -> GET /organizations/{organization_id}
- "Update a organization?" -> PUT /organizations/{organization_id}
- "List all accounts?" -> GET /organizations/{organization_id}/accounts
- "List all members?" -> GET /organizations/{organization_id}/members
- "Create a member?" -> POST /organizations/{organization_id}/members
- "Delete a member?" -> DELETE /organizations/{organization_id}/members/{member_id}
- "Get member details?" -> GET /organizations/{organization_id}/members/{member_id}
- "Create a members:batchCreate?" -> POST /organizations/{organization_id}/members:batchCreate
- "List all profile?" -> GET /organizations/{organization_id}/profile
- "List all shares?" -> GET /organizations/{organization_id}/shares
- "List all user_agent?" -> GET /radar/ai/bots/summary/user_agent
- "Get summary details?" -> GET /radar/ai/bots/summary/{dimension}
- "List all timeseries?" -> GET /radar/ai/bots/timeseries
- "List all user_agent?" -> GET /radar/ai/bots/timeseries_groups/user_agent
- "Get timeseries_group details?" -> GET /radar/ai/bots/timeseries_groups/{dimension}
- "List all model?" -> GET /radar/ai/inference/summary/model
- "List all task?" -> GET /radar/ai/inference/summary/task
- "Get summary details?" -> GET /radar/ai/inference/summary/{dimension}
- "List all model?" -> GET /radar/ai/inference/timeseries_groups/model
- "List all task?" -> GET /radar/ai/inference/timeseries_groups/task
- "Get timeseries_group details?" -> GET /radar/ai/inference/timeseries_groups/{dimension}
- "List all annotations?" -> GET /radar/annotations
- "List all outages?" -> GET /radar/annotations/outages
- "List all locations?" -> GET /radar/annotations/outages/locations
- "List all dnssec?" -> GET /radar/as112/summary/dnssec
- "List all edns?" -> GET /radar/as112/summary/edns
- "List all ip_version?" -> GET /radar/as112/summary/ip_version
- "List all protocol?" -> GET /radar/as112/summary/protocol
- "List all query_type?" -> GET /radar/as112/summary/query_type
- "List all response_codes?" -> GET /radar/as112/summary/response_codes
- "Get summary details?" -> GET /radar/as112/summary/{dimension}
- "List all timeseries?" -> GET /radar/as112/timeseries
- "List all dnssec?" -> GET /radar/as112/timeseries_groups/dnssec
- "List all edns?" -> GET /radar/as112/timeseries_groups/edns
- "List all ip_version?" -> GET /radar/as112/timeseries_groups/ip_version
- "List all protocol?" -> GET /radar/as112/timeseries_groups/protocol
- "List all query_type?" -> GET /radar/as112/timeseries_groups/query_type
- "List all response_codes?" -> GET /radar/as112/timeseries_groups/response_codes
- "Get timeseries_group details?" -> GET /radar/as112/timeseries_groups/{dimension}
- "List all locations?" -> GET /radar/as112/top/locations
- "Get dnssec details?" -> GET /radar/as112/top/locations/dnssec/{dnssec}
- "Get edn details?" -> GET /radar/as112/top/locations/edns/{edns}
- "Get ip_version details?" -> GET /radar/as112/top/locations/ip_version/{ip_version}
- "List all bitrate?" -> GET /radar/attacks/layer3/summary/bitrate
- "List all duration?" -> GET /radar/attacks/layer3/summary/duration
- "List all industry?" -> GET /radar/attacks/layer3/summary/industry
- "List all ip_version?" -> GET /radar/attacks/layer3/summary/ip_version
- "List all protocol?" -> GET /radar/attacks/layer3/summary/protocol
- "List all vector?" -> GET /radar/attacks/layer3/summary/vector
- "List all vertical?" -> GET /radar/attacks/layer3/summary/vertical
- "Get summary details?" -> GET /radar/attacks/layer3/summary/{dimension}
- "List all timeseries?" -> GET /radar/attacks/layer3/timeseries
- "List all bitrate?" -> GET /radar/attacks/layer3/timeseries_groups/bitrate
- "List all duration?" -> GET /radar/attacks/layer3/timeseries_groups/duration
- "List all industry?" -> GET /radar/attacks/layer3/timeseries_groups/industry
- "List all ip_version?" -> GET /radar/attacks/layer3/timeseries_groups/ip_version
- "List all protocol?" -> GET /radar/attacks/layer3/timeseries_groups/protocol
- "List all vector?" -> GET /radar/attacks/layer3/timeseries_groups/vector
- "List all vertical?" -> GET /radar/attacks/layer3/timeseries_groups/vertical
- "Get timeseries_group details?" -> GET /radar/attacks/layer3/timeseries_groups/{dimension}
- "List all attacks?" -> GET /radar/attacks/layer3/top/attacks
- "List all industry?" -> GET /radar/attacks/layer3/top/industry
- "List all origin?" -> GET /radar/attacks/layer3/top/locations/origin
- "List all target?" -> GET /radar/attacks/layer3/top/locations/target
- "List all vertical?" -> GET /radar/attacks/layer3/top/vertical
- "List all http_method?" -> GET /radar/attacks/layer7/summary/http_method
- "List all http_version?" -> GET /radar/attacks/layer7/summary/http_version
- "List all industry?" -> GET /radar/attacks/layer7/summary/industry
- "List all ip_version?" -> GET /radar/attacks/layer7/summary/ip_version
- "List all managed_rules?" -> GET /radar/attacks/layer7/summary/managed_rules
- "List all mitigation_product?" -> GET /radar/attacks/layer7/summary/mitigation_product
- "List all vertical?" -> GET /radar/attacks/layer7/summary/vertical
- "Get summary details?" -> GET /radar/attacks/layer7/summary/{dimension}
- "List all timeseries?" -> GET /radar/attacks/layer7/timeseries
- "List all http_method?" -> GET /radar/attacks/layer7/timeseries_groups/http_method
- "List all http_version?" -> GET /radar/attacks/layer7/timeseries_groups/http_version
- "List all industry?" -> GET /radar/attacks/layer7/timeseries_groups/industry
- "List all ip_version?" -> GET /radar/attacks/layer7/timeseries_groups/ip_version
- "List all managed_rules?" -> GET /radar/attacks/layer7/timeseries_groups/managed_rules
- "List all mitigation_product?" -> GET /radar/attacks/layer7/timeseries_groups/mitigation_product
- "List all vertical?" -> GET /radar/attacks/layer7/timeseries_groups/vertical
- "Get timeseries_group details?" -> GET /radar/attacks/layer7/timeseries_groups/{dimension}
- "List all origin?" -> GET /radar/attacks/layer7/top/ases/origin
- "List all attacks?" -> GET /radar/attacks/layer7/top/attacks
- "List all industry?" -> GET /radar/attacks/layer7/top/industry
- "List all origin?" -> GET /radar/attacks/layer7/top/locations/origin
- "List all target?" -> GET /radar/attacks/layer7/top/locations/target
- "List all vertical?" -> GET /radar/attacks/layer7/top/vertical
- "List all events?" -> GET /radar/bgp/hijacks/events
- "List all timeseries?" -> GET /radar/bgp/ips/timeseries
- "List all events?" -> GET /radar/bgp/leaks/events
- "List all ases?" -> GET /radar/bgp/routes/ases
- "List all moas?" -> GET /radar/bgp/routes/moas
- "List all pfx2as?" -> GET /radar/bgp/routes/pfx2as
- "List all realtime?" -> GET /radar/bgp/routes/realtime
- "List all stats?" -> GET /radar/bgp/routes/stats
- "List all changes?" -> GET /radar/bgp/rpki/aspa/changes
- "List all snapshot?" -> GET /radar/bgp/rpki/aspa/snapshot
- "List all timeseries?" -> GET /radar/bgp/rpki/aspa/timeseries
- "List all timeseries?" -> GET /radar/bgp/timeseries
- "List all ases?" -> GET /radar/bgp/top/ases
- "List all prefixes?" -> GET /radar/bgp/top/ases/prefixes
- "List all prefixes?" -> GET /radar/bgp/top/prefixes
- "List all bots?" -> GET /radar/bots
- "Get summary details?" -> GET /radar/bots/crawlers/summary/{dimension}
- "Get timeseries_group details?" -> GET /radar/bots/crawlers/timeseries_groups/{dimension}
- "Get summary details?" -> GET /radar/bots/summary/{dimension}
- "List all timeseries?" -> GET /radar/bots/timeseries
- "Get timeseries_group details?" -> GET /radar/bots/timeseries_groups/{dimension}
- "Get bot details?" -> GET /radar/bots/{bot_slug}
- "List all authorities?" -> GET /radar/ct/authorities
- "Get authority details?" -> GET /radar/ct/authorities/{ca_slug}
- "List all logs?" -> GET /radar/ct/logs
- "Get log details?" -> GET /radar/ct/logs/{log_slug}
- "Get summary details?" -> GET /radar/ct/summary/{dimension}
- "List all timeseries?" -> GET /radar/ct/timeseries
- "Get timeseries_group details?" -> GET /radar/ct/timeseries_groups/{dimension}
- "List all datasets?" -> GET /radar/datasets
- "Create a download?" -> POST /radar/datasets/download
- "Get dataset details?" -> GET /radar/datasets/{alias}
- "List all cache_hit?" -> GET /radar/dns/summary/cache_hit
- "List all dnssec?" -> GET /radar/dns/summary/dnssec
- "List all dnssec_aware?" -> GET /radar/dns/summary/dnssec_aware
- "List all dnssec_e2e?" -> GET /radar/dns/summary/dnssec_e2e
- "List all ip_version?" -> GET /radar/dns/summary/ip_version
- "List all matching_answer?" -> GET /radar/dns/summary/matching_answer
- "List all protocol?" -> GET /radar/dns/summary/protocol
- "List all query_type?" -> GET /radar/dns/summary/query_type
- "List all response_code?" -> GET /radar/dns/summary/response_code
- "List all response_ttl?" -> GET /radar/dns/summary/response_ttl
- "Get summary details?" -> GET /radar/dns/summary/{dimension}
- "List all timeseries?" -> GET /radar/dns/timeseries
- "List all cache_hit?" -> GET /radar/dns/timeseries_groups/cache_hit
- "List all dnssec?" -> GET /radar/dns/timeseries_groups/dnssec
- "List all dnssec_aware?" -> GET /radar/dns/timeseries_groups/dnssec_aware
- "List all dnssec_e2e?" -> GET /radar/dns/timeseries_groups/dnssec_e2e
- "List all ip_version?" -> GET /radar/dns/timeseries_groups/ip_version
- "List all matching_answer?" -> GET /radar/dns/timeseries_groups/matching_answer
- "List all protocol?" -> GET /radar/dns/timeseries_groups/protocol
- "List all query_type?" -> GET /radar/dns/timeseries_groups/query_type
- "List all response_code?" -> GET /radar/dns/timeseries_groups/response_code
- "List all response_ttl?" -> GET /radar/dns/timeseries_groups/response_ttl
- "Get timeseries_group details?" -> GET /radar/dns/timeseries_groups/{dimension}
- "List all ases?" -> GET /radar/dns/top/ases
- "List all locations?" -> GET /radar/dns/top/locations
- "List all arc?" -> GET /radar/email/routing/summary/arc
- "List all dkim?" -> GET /radar/email/routing/summary/dkim
- "List all dmarc?" -> GET /radar/email/routing/summary/dmarc
- "List all encrypted?" -> GET /radar/email/routing/summary/encrypted
- "List all ip_version?" -> GET /radar/email/routing/summary/ip_version
- "List all spf?" -> GET /radar/email/routing/summary/spf
- "Get summary details?" -> GET /radar/email/routing/summary/{dimension}
- "List all arc?" -> GET /radar/email/routing/timeseries_groups/arc
- "List all dkim?" -> GET /radar/email/routing/timeseries_groups/dkim
- "List all dmarc?" -> GET /radar/email/routing/timeseries_groups/dmarc
- "List all encrypted?" -> GET /radar/email/routing/timeseries_groups/encrypted
- "List all ip_version?" -> GET /radar/email/routing/timeseries_groups/ip_version
- "List all spf?" -> GET /radar/email/routing/timeseries_groups/spf
- "Get timeseries_group details?" -> GET /radar/email/routing/timeseries_groups/{dimension}
- "List all arc?" -> GET /radar/email/security/summary/arc
- "List all dkim?" -> GET /radar/email/security/summary/dkim
- "List all dmarc?" -> GET /radar/email/security/summary/dmarc
- "List all malicious?" -> GET /radar/email/security/summary/malicious
- "List all spam?" -> GET /radar/email/security/summary/spam
- "List all spf?" -> GET /radar/email/security/summary/spf
- "List all spoof?" -> GET /radar/email/security/summary/spoof
- "List all threat_category?" -> GET /radar/email/security/summary/threat_category
- "List all tls_version?" -> GET /radar/email/security/summary/tls_version
- "Get summary details?" -> GET /radar/email/security/summary/{dimension}
- "List all arc?" -> GET /radar/email/security/timeseries_groups/arc
- "List all dkim?" -> GET /radar/email/security/timeseries_groups/dkim
- "List all dmarc?" -> GET /radar/email/security/timeseries_groups/dmarc
- "List all malicious?" -> GET /radar/email/security/timeseries_groups/malicious
- "List all spam?" -> GET /radar/email/security/timeseries_groups/spam
- "List all spf?" -> GET /radar/email/security/timeseries_groups/spf
- "List all spoof?" -> GET /radar/email/security/timeseries_groups/spoof
- "List all threat_category?" -> GET /radar/email/security/timeseries_groups/threat_category
- "List all tls_version?" -> GET /radar/email/security/timeseries_groups/tls_version
- "Get timeseries_group details?" -> GET /radar/email/security/timeseries_groups/{dimension}
- "List all tlds?" -> GET /radar/email/security/top/tlds
- "Get malicious details?" -> GET /radar/email/security/top/tlds/malicious/{malicious}
- "Get spam details?" -> GET /radar/email/security/top/tlds/spam/{spam}
- "Get spoof details?" -> GET /radar/email/security/top/tlds/spoof/{spoof}
- "List all asns?" -> GET /radar/entities/asns
- "List all botnet_threat_feed?" -> GET /radar/entities/asns/botnet_threat_feed
- "List all ip?" -> GET /radar/entities/asns/ip
- "Get asn details?" -> GET /radar/entities/asns/{asn}
- "List all as_set?" -> GET /radar/entities/asns/{asn}/as_set
- "List all rel?" -> GET /radar/entities/asns/{asn}/rel
- "List all ip?" -> GET /radar/entities/ip
- "List all locations?" -> GET /radar/entities/locations
- "Get location details?" -> GET /radar/entities/locations/{location}
- "List all geolocations?" -> GET /radar/geolocations
- "Get geolocation details?" -> GET /radar/geolocations/{geo_id}
- "List all bot_class?" -> GET /radar/http/summary/bot_class
- "List all device_type?" -> GET /radar/http/summary/device_type
- "List all http_protocol?" -> GET /radar/http/summary/http_protocol
- "List all http_version?" -> GET /radar/http/summary/http_version
- "List all ip_version?" -> GET /radar/http/summary/ip_version
- "List all os?" -> GET /radar/http/summary/os
- "List all post_quantum?" -> GET /radar/http/summary/post_quantum
- "List all tls_version?" -> GET /radar/http/summary/tls_version
- "Get summary details?" -> GET /radar/http/summary/{dimension}
- "List all timeseries?" -> GET /radar/http/timeseries
- "List all bot_class?" -> GET /radar/http/timeseries_groups/bot_class
- "List all browser?" -> GET /radar/http/timeseries_groups/browser
- "List all browser_family?" -> GET /radar/http/timeseries_groups/browser_family
- "List all device_type?" -> GET /radar/http/timeseries_groups/device_type
- "List all http_protocol?" -> GET /radar/http/timeseries_groups/http_protocol
- "List all http_version?" -> GET /radar/http/timeseries_groups/http_version
- "List all ip_version?" -> GET /radar/http/timeseries_groups/ip_version
- "List all os?" -> GET /radar/http/timeseries_groups/os
- "List all post_quantum?" -> GET /radar/http/timeseries_groups/post_quantum
- "List all tls_version?" -> GET /radar/http/timeseries_groups/tls_version
- "Get timeseries_group details?" -> GET /radar/http/timeseries_groups/{dimension}
- "List all ases?" -> GET /radar/http/top/ases
- "Get bot_class details?" -> GET /radar/http/top/ases/bot_class/{bot_class}
- "Get browser_family details?" -> GET /radar/http/top/ases/browser_family/{browser_family}
- "Get device_type details?" -> GET /radar/http/top/ases/device_type/{device_type}
- "Get http_protocol details?" -> GET /radar/http/top/ases/http_protocol/{http_protocol}
- "Get http_version details?" -> GET /radar/http/top/ases/http_version/{http_version}
- "Get ip_version details?" -> GET /radar/http/top/ases/ip_version/{ip_version}
- "Get o details?" -> GET /radar/http/top/ases/os/{os}
- "Get tls_version details?" -> GET /radar/http/top/ases/tls_version/{tls_version}
- "List all browser?" -> GET /radar/http/top/browser
- "List all browser_family?" -> GET /radar/http/top/browser_family
- "List all locations?" -> GET /radar/http/top/locations
- "Get bot_class details?" -> GET /radar/http/top/locations/bot_class/{bot_class}
- "Get browser_family details?" -> GET /radar/http/top/locations/browser_family/{browser_family}
- "Get device_type details?" -> GET /radar/http/top/locations/device_type/{device_type}
- "Get http_protocol details?" -> GET /radar/http/top/locations/http_protocol/{http_protocol}
- "Get http_version details?" -> GET /radar/http/top/locations/http_version/{http_version}
- "Get ip_version details?" -> GET /radar/http/top/locations/ip_version/{ip_version}
- "Get o details?" -> GET /radar/http/top/locations/os/{os}
- "Get tls_version details?" -> GET /radar/http/top/locations/tls_version/{tls_version}
- "List all bot_class?" -> GET /radar/leaked_credential_checks/summary/bot_class
- "List all compromised?" -> GET /radar/leaked_credential_checks/summary/compromised
- "Get summary details?" -> GET /radar/leaked_credential_checks/summary/{dimension}
- "List all bot_class?" -> GET /radar/leaked_credential_checks/timeseries_groups/bot_class
- "List all compromised?" -> GET /radar/leaked_credential_checks/timeseries_groups/compromised
- "Get timeseries_group details?" -> GET /radar/leaked_credential_checks/timeseries_groups/{dimension}
- "List all summary?" -> GET /radar/netflows/summary
- "Get summary details?" -> GET /radar/netflows/summary/{dimension}
- "List all timeseries?" -> GET /radar/netflows/timeseries
- "Get timeseries_group details?" -> GET /radar/netflows/timeseries_groups/{dimension}
- "List all ases?" -> GET /radar/netflows/top/ases
- "List all locations?" -> GET /radar/netflows/top/locations
- "List all origins?" -> GET /radar/origins
- "Get summary details?" -> GET /radar/origins/summary/{dimension}
- "List all timeseries?" -> GET /radar/origins/timeseries
- "Get timeseries_group details?" -> GET /radar/origins/timeseries_groups/{dimension}
- "Get origin details?" -> GET /radar/origins/{slug}
- "Get summary details?" -> GET /radar/post_quantum/origin/summary/{dimension}
- "Get timeseries_group details?" -> GET /radar/post_quantum/origin/timeseries_groups/{dimension}
- "List all support?" -> GET /radar/post_quantum/tls/support
- "List all summary?" -> GET /radar/quality/iqi/summary
- "List all timeseries_groups?" -> GET /radar/quality/iqi/timeseries_groups
- "List all histogram?" -> GET /radar/quality/speed/histogram
- "List all summary?" -> GET /radar/quality/speed/summary
- "List all ases?" -> GET /radar/quality/speed/top/ases
- "List all locations?" -> GET /radar/quality/speed/top/locations
- "Get domain details?" -> GET /radar/ranking/domain/{domain}
- "List all categories?" -> GET /radar/ranking/internet_services/categories
- "List all timeseries_groups?" -> GET /radar/ranking/internet_services/timeseries_groups
- "List all top?" -> GET /radar/ranking/internet_services/top
- "List all timeseries_groups?" -> GET /radar/ranking/timeseries_groups
- "List all top?" -> GET /radar/ranking/top
- "List all domain_categories?" -> GET /radar/robots_txt/top/domain_categories
- "List all directive?" -> GET /radar/robots_txt/top/user_agents/directive
- "Search global?" -> GET /radar/search/global
- "List all summary?" -> GET /radar/tcp_resets_timeouts/summary
- "List all timeseries_groups?" -> GET /radar/tcp_resets_timeouts/timeseries_groups
- "List all tlds?" -> GET /radar/tlds
- "Get tld details?" -> GET /radar/tlds/{tld}
- "List all traffic_anomalies?" -> GET /radar/traffic_anomalies
- "List all locations?" -> GET /radar/traffic_anomalies/locations
- "List all bots?" -> GET /radar/verified_bots/top/bots
- "List all categories?" -> GET /radar/verified_bots/top/categories
- "List all ready?" -> GET /ready
- "List all signed-url?" -> GET /signed-url
- "List all stores?" -> GET /system/accounts/{account_tag}/stores
- "Create a store?" -> POST /system/accounts/{account_tag}/stores
- "Delete a store?" -> DELETE /system/accounts/{account_tag}/stores/{store_id}
- "Search secrets?" -> GET /system/accounts/{account_tag}/stores/{store_id}/secrets
- "Create a secret?" -> POST /system/accounts/{account_tag}/stores/{store_id}/secrets
- "Delete a secret?" -> DELETE /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id}
- "Get secret details?" -> GET /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id}
- "Partially update a secret?" -> PATCH /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id}
- "Create a duplicate?" -> POST /system/accounts/{account_tag}/stores/{store_id}/secrets/{secret_id}/duplicate
- "Get tenant details?" -> GET /tenants/{tenant_id}
- "List all account_types?" -> GET /tenants/{tenant_id}/account_types
- "List all accounts?" -> GET /tenants/{tenant_id}/accounts
- "List all entitlements?" -> GET /tenants/{tenant_id}/entitlements
- "List all memberships?" -> GET /tenants/{tenant_id}/memberships
- "List all user?" -> GET /user
- "List all audit_logs?" -> GET /user/audit_logs
- "List all history?" -> GET /user/billing/history
- "List all profile?" -> GET /user/billing/profile
- "List all rules?" -> GET /user/firewall/access_rules/rules
- "Create a rule?" -> POST /user/firewall/access_rules/rules
- "Delete a rule?" -> DELETE /user/firewall/access_rules/rules/{rule_id}
- "Partially update a rule?" -> PATCH /user/firewall/access_rules/rules/{rule_id}
- "List all invites?" -> GET /user/invites
- "Get invite details?" -> GET /user/invites/{invite_id}
- "Partially update a invite?" -> PATCH /user/invites/{invite_id}
- "List all monitors?" -> GET /user/load_balancers/monitors
- "Create a monitor?" -> POST /user/load_balancers/monitors
- "Delete a monitor?" -> DELETE /user/load_balancers/monitors/{monitor_id}
- "Get monitor details?" -> GET /user/load_balancers/monitors/{monitor_id}
- "Partially update a monitor?" -> PATCH /user/load_balancers/monitors/{monitor_id}
- "Update a monitor?" -> PUT /user/load_balancers/monitors/{monitor_id}
- "Create a preview?" -> POST /user/load_balancers/monitors/{monitor_id}/preview
- "List all references?" -> GET /user/load_balancers/monitors/{monitor_id}/references
- "List all pools?" -> GET /user/load_balancers/pools
- "Create a pool?" -> POST /user/load_balancers/pools
- "Delete a pool?" -> DELETE /user/load_balancers/pools/{pool_id}
- "Get pool details?" -> GET /user/load_balancers/pools/{pool_id}
- "Partially update a pool?" -> PATCH /user/load_balancers/pools/{pool_id}
- "Update a pool?" -> PUT /user/load_balancers/pools/{pool_id}
- "List all health?" -> GET /user/load_balancers/pools/{pool_id}/health
- "Create a preview?" -> POST /user/load_balancers/pools/{pool_id}/preview
- "List all references?" -> GET /user/load_balancers/pools/{pool_id}/references
- "Get preview details?" -> GET /user/load_balancers/preview/{preview_id}
- "List all events?" -> GET /user/load_balancing_analytics/events
- "List all organizations?" -> GET /user/organizations
- "Delete a organization?" -> DELETE /user/organizations/{organization_id}
- "Get organization details?" -> GET /user/organizations/{organization_id}
- "List all subscriptions?" -> GET /user/subscriptions
- "Delete a subscription?" -> DELETE /user/subscriptions/{identifier}
- "Update a subscription?" -> PUT /user/subscriptions/{identifier}
- "List all tokens?" -> GET /user/tokens
- "Create a token?" -> POST /user/tokens
- "List all permission_groups?" -> GET /user/tokens/permission_groups
- "List all verify?" -> GET /user/tokens/verify
- "Delete a token?" -> DELETE /user/tokens/{token_id}
- "Get token details?" -> GET /user/tokens/{token_id}
- "Update a token?" -> PUT /user/tokens/{token_id}
- "List all tenants?" -> GET /users/tenants
- "List all zones?" -> GET /zones
- "Create a zone?" -> POST /zones
- "List all colos?" -> GET /zones/{zone_identifier}/analytics/colos
- "List all dashboard?" -> GET /zones/{zone_identifier}/analytics/dashboard
- "List all custom_pages?" -> GET /zones/{zone_identifier}/custom_pages
- "Get custom_page details?" -> GET /zones/{zone_identifier}/custom_pages/{identifier}
- "Update a custom_page?" -> PUT /zones/{zone_identifier}/custom_pages/{identifier}
- "Delete a zone?" -> DELETE /zones/{zone_id}
- "Get zone details?" -> GET /zones/{zone_id}
- "Partially update a zone?" -> PATCH /zones/{zone_id}
- "List all apps?" -> GET /zones/{zone_id}/access/apps
- "Create a app?" -> POST /zones/{zone_id}/access/apps
- "List all ca?" -> GET /zones/{zone_id}/access/apps/ca
- "Delete a app?" -> DELETE /zones/{zone_id}/access/apps/{app_id}
- "Get app details?" -> GET /zones/{zone_id}/access/apps/{app_id}
- "Update a app?" -> PUT /zones/{zone_id}/access/apps/{app_id}
- "List all ca?" -> GET /zones/{zone_id}/access/apps/{app_id}/ca
- "Create a ca?" -> POST /zones/{zone_id}/access/apps/{app_id}/ca
- "List all policies?" -> GET /zones/{zone_id}/access/apps/{app_id}/policies
- "Create a policy?" -> POST /zones/{zone_id}/access/apps/{app_id}/policies
- "Delete a policy?" -> DELETE /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id}
- "Get policy details?" -> GET /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id}
- "Update a policy?" -> PUT /zones/{zone_id}/access/apps/{app_id}/policies/{policy_id}
- "Create a revoke_token?" -> POST /zones/{zone_id}/access/apps/{app_id}/revoke_tokens
- "List all user_policy_checks?" -> GET /zones/{zone_id}/access/apps/{app_id}/user_policy_checks
- "List all certificates?" -> GET /zones/{zone_id}/access/certificates
- "Create a certificate?" -> POST /zones/{zone_id}/access/certificates
- "List all settings?" -> GET /zones/{zone_id}/access/certificates/settings
- "Delete a certificate?" -> DELETE /zones/{zone_id}/access/certificates/{certificate_id}
- "Get certificate details?" -> GET /zones/{zone_id}/access/certificates/{certificate_id}
- "Update a certificate?" -> PUT /zones/{zone_id}/access/certificates/{certificate_id}
- "List all groups?" -> GET /zones/{zone_id}/access/groups
- "Create a group?" -> POST /zones/{zone_id}/access/groups
- "Delete a group?" -> DELETE /zones/{zone_id}/access/groups/{group_id}
- "Get group details?" -> GET /zones/{zone_id}/access/groups/{group_id}
- "Update a group?" -> PUT /zones/{zone_id}/access/groups/{group_id}
- "List all identity_providers?" -> GET /zones/{zone_id}/access/identity_providers
- "Create a identity_provider?" -> POST /zones/{zone_id}/access/identity_providers
- "Delete a identity_provider?" -> DELETE /zones/{zone_id}/access/identity_providers/{identity_provider_id}
- "Get identity_provider details?" -> GET /zones/{zone_id}/access/identity_providers/{identity_provider_id}
- "Update a identity_provider?" -> PUT /zones/{zone_id}/access/identity_providers/{identity_provider_id}
- "List all organizations?" -> GET /zones/{zone_id}/access/organizations
- "Create a organization?" -> POST /zones/{zone_id}/access/organizations
- "Create a revoke_user?" -> POST /zones/{zone_id}/access/organizations/revoke_user
- "List all service_tokens?" -> GET /zones/{zone_id}/access/service_tokens
- "Create a service_token?" -> POST /zones/{zone_id}/access/service_tokens
- "Delete a service_token?" -> DELETE /zones/{zone_id}/access/service_tokens/{service_token_id}
- "Get service_token details?" -> GET /zones/{zone_id}/access/service_tokens/{service_token_id}
- "Update a service_token?" -> PUT /zones/{zone_id}/access/service_tokens/{service_token_id}
- "List all custom_trust_store?" -> GET /zones/{zone_id}/acm/custom_trust_store
- "Create a custom_trust_store?" -> POST /zones/{zone_id}/acm/custom_trust_store
- "Delete a custom_trust_store?" -> DELETE /zones/{zone_id}/acm/custom_trust_store/{custom_origin_trust_store_id}
- "Get custom_trust_store details?" -> GET /zones/{zone_id}/acm/custom_trust_store/{custom_origin_trust_store_id}
- "List all total_tls?" -> GET /zones/{zone_id}/acm/total_tls
- "Create a total_tl?" -> POST /zones/{zone_id}/acm/total_tls
- "List all regional_hostnames?" -> GET /zones/{zone_id}/addressing/regional_hostnames
- "Create a regional_hostname?" -> POST /zones/{zone_id}/addressing/regional_hostnames
- "Delete a regional_hostname?" -> DELETE /zones/{zone_id}/addressing/regional_hostnames/{hostname}
- "Get regional_hostname details?" -> GET /zones/{zone_id}/addressing/regional_hostnames/{hostname}
- "Partially update a regional_hostname?" -> PATCH /zones/{zone_id}/addressing/regional_hostnames/{hostname}
- "List all latency?" -> GET /zones/{zone_id}/analytics/latency
- "List all colos?" -> GET /zones/{zone_id}/analytics/latency/colos
- "List all configuration?" -> GET /zones/{zone_id}/api_gateway/configuration
- "List all discovery?" -> GET /zones/{zone_id}/api_gateway/discovery
- "List all operations?" -> GET /zones/{zone_id}/api_gateway/discovery/operations
- "Partially update a operation?" -> PATCH /zones/{zone_id}/api_gateway/discovery/operations/{operation_id}
- "Create a fallthrough?" -> POST /zones/{zone_id}/api_gateway/expression-template/fallthrough
- "List all operations?" -> GET /zones/{zone_id}/api_gateway/operations
- "Create a operation?" -> POST /zones/{zone_id}/api_gateway/operations
- "Create a item?" -> POST /zones/{zone_id}/api_gateway/operations/item
- "Delete a operation?" -> DELETE /zones/{zone_id}/api_gateway/operations/{operation_id}
- "Get operation details?" -> GET /zones/{zone_id}/api_gateway/operations/{operation_id}
- "List all schema_validation?" -> GET /zones/{zone_id}/api_gateway/operations/{operation_id}/schema_validation
- "List all schemas?" -> GET /zones/{zone_id}/api_gateway/schemas
- "List all schema_validation?" -> GET /zones/{zone_id}/api_gateway/settings/schema_validation
- "List all user_schemas?" -> GET /zones/{zone_id}/api_gateway/user_schemas
- "Create a user_schema?" -> POST /zones/{zone_id}/api_gateway/user_schemas
- "List all hosts?" -> GET /zones/{zone_id}/api_gateway/user_schemas/hosts
- "Delete a user_schema?" -> DELETE /zones/{zone_id}/api_gateway/user_schemas/{schema_id}
- "Get user_schema details?" -> GET /zones/{zone_id}/api_gateway/user_schemas/{schema_id}
- "Partially update a user_schema?" -> PATCH /zones/{zone_id}/api_gateway/user_schemas/{schema_id}
- "List all operations?" -> GET /zones/{zone_id}/api_gateway/user_schemas/{schema_id}/operations
- "List all smart_routing?" -> GET /zones/{zone_id}/argo/smart_routing
- "List all tiered_caching?" -> GET /zones/{zone_id}/argo/tiered_caching
- "List all available_plans?" -> GET /zones/{zone_id}/available_plans
- "Get available_plan details?" -> GET /zones/{zone_id}/available_plans/{plan_identifier}
- "List all available_rate_plans?" -> GET /zones/{zone_id}/available_rate_plans
- "List all bot_management?" -> GET /zones/{zone_id}/bot_management
- "List all feedback?" -> GET /zones/{zone_id}/bot_management/feedback
- "Create a feedback?" -> POST /zones/{zone_id}/bot_management/feedback
- "List all cache_reserve?" -> GET /zones/{zone_id}/cache/cache_reserve
- "List all cache_reserve_clear?" -> GET /zones/{zone_id}/cache/cache_reserve_clear
- "Create a cache_reserve_clear?" -> POST /zones/{zone_id}/cache/cache_reserve_clear
- "List all origin_post_quantum_encryption?" -> GET /zones/{zone_id}/cache/origin_post_quantum_encryption
- "List all regional_tiered_cache?" -> GET /zones/{zone_id}/cache/regional_tiered_cache
- "List all tiered_cache_smart_topology_enable?" -> GET /zones/{zone_id}/cache/tiered_cache_smart_topology_enable
- "List all variants?" -> GET /zones/{zone_id}/cache/variants
- "List all hostname_associations?" -> GET /zones/{zone_id}/certificate_authorities/hostname_associations
- "List all client_certificates?" -> GET /zones/{zone_id}/client_certificates
- "Create a client_certificate?" -> POST /zones/{zone_id}/client_certificates
- "Delete a client_certificate?" -> DELETE /zones/{zone_id}/client_certificates/{client_certificate_id}
- "Get client_certificate details?" -> GET /zones/{zone_id}/client_certificates/{client_certificate_id}
- "Partially update a client_certificate?" -> PATCH /zones/{zone_id}/client_certificates/{client_certificate_id}
- "List all rules?" -> GET /zones/{zone_id}/cloud_connector/rules
- "Create a disable?" -> POST /zones/{zone_id}/content-upload-scan/disable
- "Create a enable?" -> POST /zones/{zone_id}/content-upload-scan/enable
- "List all payloads?" -> GET /zones/{zone_id}/content-upload-scan/payloads
- "Create a payload?" -> POST /zones/{zone_id}/content-upload-scan/payloads
- "Delete a payload?" -> DELETE /zones/{zone_id}/content-upload-scan/payloads/{expression_id}
- "List all settings?" -> GET /zones/{zone_id}/content-upload-scan/settings
- "List all custom_certificates?" -> GET /zones/{zone_id}/custom_certificates
- "Create a custom_certificate?" -> POST /zones/{zone_id}/custom_certificates
- "Delete a custom_certificate?" -> DELETE /zones/{zone_id}/custom_certificates/{custom_certificate_id}
- "Get custom_certificate details?" -> GET /zones/{zone_id}/custom_certificates/{custom_certificate_id}
- "Partially update a custom_certificate?" -> PATCH /zones/{zone_id}/custom_certificates/{custom_certificate_id}
- "List all custom_hostnames?" -> GET /zones/{zone_id}/custom_hostnames
- "Create a custom_hostname?" -> POST /zones/{zone_id}/custom_hostnames
- "List all fallback_origin?" -> GET /zones/{zone_id}/custom_hostnames/fallback_origin
- "Delete a custom_hostname?" -> DELETE /zones/{zone_id}/custom_hostnames/{custom_hostname_id}
- "Get custom_hostname details?" -> GET /zones/{zone_id}/custom_hostnames/{custom_hostname_id}
- "Partially update a custom_hostname?" -> PATCH /zones/{zone_id}/custom_hostnames/{custom_hostname_id}
- "Delete a certificate?" -> DELETE /zones/{zone_id}/custom_hostnames/{custom_hostname_id}/certificate_pack/{certificate_pack_id}/certificates/{certificate_id}
- "Update a certificate?" -> PUT /zones/{zone_id}/custom_hostnames/{custom_hostname_id}/certificate_pack/{certificate_pack_id}/certificates/{certificate_id}
- "List all custom_ns?" -> GET /zones/{zone_id}/custom_ns
- "List all uuid?" -> GET /zones/{zone_id}/dcv_delegation/uuid
- "List all certificates?" -> GET /zones/{zone_id}/devices/policy/certificates
- "List all report?" -> GET /zones/{zone_id}/dns_analytics/report
- "List all bytime?" -> GET /zones/{zone_id}/dns_analytics/report/bytime
- "Search dns_records?" -> GET /zones/{zone_id}/dns_records
- "Create a dns_record?" -> POST /zones/{zone_id}/dns_records
- "Create a batch?" -> POST /zones/{zone_id}/dns_records/batch
- "List all export?" -> GET /zones/{zone_id}/dns_records/export
- "Create a import?" -> POST /zones/{zone_id}/dns_records/import
- "Create a scan?" -> POST /zones/{zone_id}/dns_records/scan
- "List all review?" -> GET /zones/{zone_id}/dns_records/scan/review
- "Create a review?" -> POST /zones/{zone_id}/dns_records/scan/review
- "Create a trigger?" -> POST /zones/{zone_id}/dns_records/scan/trigger
- "List all usage?" -> GET /zones/{zone_id}/dns_records/usage
- "Delete a dns_record?" -> DELETE /zones/{zone_id}/dns_records/{dns_record_id}
- "Get dns_record details?" -> GET /zones/{zone_id}/dns_records/{dns_record_id}
- "Partially update a dns_record?" -> PATCH /zones/{zone_id}/dns_records/{dns_record_id}
- "Update a dns_record?" -> PUT /zones/{zone_id}/dns_records/{dns_record_id}
- "List all dns_settings?" -> GET /zones/{zone_id}/dns_settings
- "List all dnssec?" -> GET /zones/{zone_id}/dnssec
- "List all routing?" -> GET /zones/{zone_id}/email/routing
- "Create a disable?" -> POST /zones/{zone_id}/email/routing/disable
- "List all dns?" -> GET /zones/{zone_id}/email/routing/dns
- "Create a dn?" -> POST /zones/{zone_id}/email/routing/dns
- "Create a enable?" -> POST /zones/{zone_id}/email/routing/enable
- "List all rules?" -> GET /zones/{zone_id}/email/routing/rules
- "Create a rule?" -> POST /zones/{zone_id}/email/routing/rules
- "List all catch_all?" -> GET /zones/{zone_id}/email/routing/rules/catch_all
- "Delete a rule?" -> DELETE /zones/{zone_id}/email/routing/rules/{rule_identifier}
- "Get rule details?" -> GET /zones/{zone_id}/email/routing/rules/{rule_identifier}
- "Update a rule?" -> PUT /zones/{zone_id}/email/routing/rules/{rule_identifier}
- "List all filters?" -> GET /zones/{zone_id}/filters
- "Create a filter?" -> POST /zones/{zone_id}/filters
- "Delete a filter?" -> DELETE /zones/{zone_id}/filters/{filter_id}
- "Get filter details?" -> GET /zones/{zone_id}/filters/{filter_id}
- "Update a filter?" -> PUT /zones/{zone_id}/filters/{filter_id}
- "List all rules?" -> GET /zones/{zone_id}/firewall/access_rules/rules
- "Create a rule?" -> POST /zones/{zone_id}/firewall/access_rules/rules
- "Delete a rule?" -> DELETE /zones/{zone_id}/firewall/access_rules/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/firewall/access_rules/rules/{rule_id}
- "List all lockdowns?" -> GET /zones/{zone_id}/firewall/lockdowns
- "Create a lockdown?" -> POST /zones/{zone_id}/firewall/lockdowns
- "Delete a lockdown?" -> DELETE /zones/{zone_id}/firewall/lockdowns/{lock_downs_id}
- "Get lockdown details?" -> GET /zones/{zone_id}/firewall/lockdowns/{lock_downs_id}
- "Update a lockdown?" -> PUT /zones/{zone_id}/firewall/lockdowns/{lock_downs_id}
- "List all rules?" -> GET /zones/{zone_id}/firewall/rules
- "Create a rule?" -> POST /zones/{zone_id}/firewall/rules
- "Delete a rule?" -> DELETE /zones/{zone_id}/firewall/rules/{rule_id}
- "Get rule details?" -> GET /zones/{zone_id}/firewall/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/firewall/rules/{rule_id}
- "Update a rule?" -> PUT /zones/{zone_id}/firewall/rules/{rule_id}
- "List all ua_rules?" -> GET /zones/{zone_id}/firewall/ua_rules
- "Create a ua_rule?" -> POST /zones/{zone_id}/firewall/ua_rules
- "Delete a ua_rule?" -> DELETE /zones/{zone_id}/firewall/ua_rules/{ua_rule_id}
- "Get ua_rule details?" -> GET /zones/{zone_id}/firewall/ua_rules/{ua_rule_id}
- "Update a ua_rule?" -> PUT /zones/{zone_id}/firewall/ua_rules/{ua_rule_id}
- "List all overrides?" -> GET /zones/{zone_id}/firewall/waf/overrides
- "Create a override?" -> POST /zones/{zone_id}/firewall/waf/overrides
- "Delete a override?" -> DELETE /zones/{zone_id}/firewall/waf/overrides/{overrides_id}
- "Get override details?" -> GET /zones/{zone_id}/firewall/waf/overrides/{overrides_id}
- "Update a override?" -> PUT /zones/{zone_id}/firewall/waf/overrides/{overrides_id}
- "List all packages?" -> GET /zones/{zone_id}/firewall/waf/packages
- "Get package details?" -> GET /zones/{zone_id}/firewall/waf/packages/{package_id}
- "Partially update a package?" -> PATCH /zones/{zone_id}/firewall/waf/packages/{package_id}
- "List all groups?" -> GET /zones/{zone_id}/firewall/waf/packages/{package_id}/groups
- "Get group details?" -> GET /zones/{zone_id}/firewall/waf/packages/{package_id}/groups/{group_id}
- "Partially update a group?" -> PATCH /zones/{zone_id}/firewall/waf/packages/{package_id}/groups/{group_id}
- "List all rules?" -> GET /zones/{zone_id}/firewall/waf/packages/{package_id}/rules
- "Get rule details?" -> GET /zones/{zone_id}/firewall/waf/packages/{package_id}/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/firewall/waf/packages/{package_id}/rules/{rule_id}
- "List all settings?" -> GET /zones/{zone_id}/fraud_detection/settings
- "List all healthchecks?" -> GET /zones/{zone_id}/healthchecks
- "Create a healthcheck?" -> POST /zones/{zone_id}/healthchecks
- "Create a preview?" -> POST /zones/{zone_id}/healthchecks/preview
- "Delete a preview?" -> DELETE /zones/{zone_id}/healthchecks/preview/{healthcheck_id}
- "Get preview details?" -> GET /zones/{zone_id}/healthchecks/preview/{healthcheck_id}
- "Delete a healthcheck?" -> DELETE /zones/{zone_id}/healthchecks/{healthcheck_id}
- "Get healthcheck details?" -> GET /zones/{zone_id}/healthchecks/{healthcheck_id}
- "Partially update a healthcheck?" -> PATCH /zones/{zone_id}/healthchecks/{healthcheck_id}
- "Update a healthcheck?" -> PUT /zones/{zone_id}/healthchecks/{healthcheck_id}
- "List all hold?" -> GET /zones/{zone_id}/hold
- "Create a hold?" -> POST /zones/{zone_id}/hold
- "Get setting details?" -> GET /zones/{zone_id}/hostnames/settings/{setting_id}
- "Delete a setting?" -> DELETE /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname}
- "Get setting details?" -> GET /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname}
- "Update a setting?" -> PUT /zones/{zone_id}/hostnames/settings/{setting_id}/{hostname}
- "List all keyless_certificates?" -> GET /zones/{zone_id}/keyless_certificates
- "Create a keyless_certificate?" -> POST /zones/{zone_id}/keyless_certificates
- "Delete a keyless_certificate?" -> DELETE /zones/{zone_id}/keyless_certificates/{keyless_certificate_id}
- "Get keyless_certificate details?" -> GET /zones/{zone_id}/keyless_certificates/{keyless_certificate_id}
- "Partially update a keyless_certificate?" -> PATCH /zones/{zone_id}/keyless_certificates/{keyless_certificate_id}
- "List all leaked-credential-checks?" -> GET /zones/{zone_id}/leaked-credential-checks
- "Create a leaked-credential-check?" -> POST /zones/{zone_id}/leaked-credential-checks
- "List all detections?" -> GET /zones/{zone_id}/leaked-credential-checks/detections
- "Create a detection?" -> POST /zones/{zone_id}/leaked-credential-checks/detections
- "Delete a detection?" -> DELETE /zones/{zone_id}/leaked-credential-checks/detections/{detection_id}
- "Get detection details?" -> GET /zones/{zone_id}/leaked-credential-checks/detections/{detection_id}
- "Update a detection?" -> PUT /zones/{zone_id}/leaked-credential-checks/detections/{detection_id}
- "List all load_balancers?" -> GET /zones/{zone_id}/load_balancers
- "Create a load_balancer?" -> POST /zones/{zone_id}/load_balancers
- "Delete a load_balancer?" -> DELETE /zones/{zone_id}/load_balancers/{load_balancer_id}
- "Get load_balancer details?" -> GET /zones/{zone_id}/load_balancers/{load_balancer_id}
- "Partially update a load_balancer?" -> PATCH /zones/{zone_id}/load_balancers/{load_balancer_id}
- "Update a load_balancer?" -> PUT /zones/{zone_id}/load_balancers/{load_balancer_id}
- "List all fields?" -> GET /zones/{zone_id}/logpush/datasets/{dataset_id}/fields
- "List all jobs?" -> GET /zones/{zone_id}/logpush/datasets/{dataset_id}/jobs
- "List all jobs?" -> GET /zones/{zone_id}/logpush/edge/jobs
- "Create a job?" -> POST /zones/{zone_id}/logpush/edge/jobs
- "List all jobs?" -> GET /zones/{zone_id}/logpush/jobs
- "Create a job?" -> POST /zones/{zone_id}/logpush/jobs
- "Delete a job?" -> DELETE /zones/{zone_id}/logpush/jobs/{job_id}
- "Get job details?" -> GET /zones/{zone_id}/logpush/jobs/{job_id}
- "Update a job?" -> PUT /zones/{zone_id}/logpush/jobs/{job_id}
- "Create a ownership?" -> POST /zones/{zone_id}/logpush/ownership
- "Create a validate?" -> POST /zones/{zone_id}/logpush/ownership/validate
- "Create a destination?" -> POST /zones/{zone_id}/logpush/validate/destination
- "Create a exist?" -> POST /zones/{zone_id}/logpush/validate/destination/exists
- "Create a origin?" -> POST /zones/{zone_id}/logpush/validate/origin
- "List all flag?" -> GET /zones/{zone_id}/logs/control/retention/flag
- "Create a flag?" -> POST /zones/{zone_id}/logs/control/retention/flag
- "Get rayid details?" -> GET /zones/{zone_id}/logs/rayids/{ray_id}
- "List all received?" -> GET /zones/{zone_id}/logs/received
- "List all fields?" -> GET /zones/{zone_id}/logs/received/fields
- "List all managed_headers?" -> GET /zones/{zone_id}/managed_headers
- "List all origin_tls_client_auth?" -> GET /zones/{zone_id}/origin_tls_client_auth
- "Create a origin_tls_client_auth?" -> POST /zones/{zone_id}/origin_tls_client_auth
- "List all certificates?" -> GET /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates
- "Create a certificate?" -> POST /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates
- "Delete a certificate?" -> DELETE /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates/{certificate_id}
- "Get certificate details?" -> GET /zones/{zone_id}/origin_tls_client_auth/hostnames/certificates/{certificate_id}
- "Get hostname details?" -> GET /zones/{zone_id}/origin_tls_client_auth/hostnames/{hostname}
- "List all settings?" -> GET /zones/{zone_id}/origin_tls_client_auth/settings
- "Delete a origin_tls_client_auth?" -> DELETE /zones/{zone_id}/origin_tls_client_auth/{certificate_id}
- "Get origin_tls_client_auth details?" -> GET /zones/{zone_id}/origin_tls_client_auth/{certificate_id}
- "List all page_shield?" -> GET /zones/{zone_id}/page_shield
- "List all connections?" -> GET /zones/{zone_id}/page_shield/connections
- "Get connection details?" -> GET /zones/{zone_id}/page_shield/connections/{connection_id}
- "List all cookies?" -> GET /zones/{zone_id}/page_shield/cookies
- "Get cooky details?" -> GET /zones/{zone_id}/page_shield/cookies/{cookie_id}
- "List all policies?" -> GET /zones/{zone_id}/page_shield/policies
- "Create a policy?" -> POST /zones/{zone_id}/page_shield/policies
- "Delete a policy?" -> DELETE /zones/{zone_id}/page_shield/policies/{policy_id}
- "Get policy details?" -> GET /zones/{zone_id}/page_shield/policies/{policy_id}
- "Update a policy?" -> PUT /zones/{zone_id}/page_shield/policies/{policy_id}
- "List all scripts?" -> GET /zones/{zone_id}/page_shield/scripts
- "Get script details?" -> GET /zones/{zone_id}/page_shield/scripts/{script_id}
- "List all pagerules?" -> GET /zones/{zone_id}/pagerules
- "Create a pagerule?" -> POST /zones/{zone_id}/pagerules
- "List all settings?" -> GET /zones/{zone_id}/pagerules/settings
- "Delete a pagerule?" -> DELETE /zones/{zone_id}/pagerules/{pagerule_id}
- "Get pagerule details?" -> GET /zones/{zone_id}/pagerules/{pagerule_id}
- "Partially update a pagerule?" -> PATCH /zones/{zone_id}/pagerules/{pagerule_id}
- "Update a pagerule?" -> PUT /zones/{zone_id}/pagerules/{pagerule_id}
- "List all configuration?" -> GET /zones/{zone_id}/pay-per-crawl/configuration
- "Create a configuration?" -> POST /zones/{zone_id}/pay-per-crawl/configuration
- "Create a purge_cache?" -> POST /zones/{zone_id}/purge_cache
- "List all rate_limits?" -> GET /zones/{zone_id}/rate_limits
- "Create a rate_limit?" -> POST /zones/{zone_id}/rate_limits
- "Delete a rate_limit?" -> DELETE /zones/{zone_id}/rate_limits/{rate_limit_id}
- "Get rate_limit details?" -> GET /zones/{zone_id}/rate_limits/{rate_limit_id}
- "Update a rate_limit?" -> PUT /zones/{zone_id}/rate_limits/{rate_limit_id}
- "List all rulesets?" -> GET /zones/{zone_id}/rulesets
- "Create a ruleset?" -> POST /zones/{zone_id}/rulesets
- "List all entrypoint?" -> GET /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint
- "List all versions?" -> GET /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions
- "Get version details?" -> GET /zones/{zone_id}/rulesets/phases/{ruleset_phase}/entrypoint/versions/{ruleset_version}
- "Delete a ruleset?" -> DELETE /zones/{zone_id}/rulesets/{ruleset_id}
- "Get ruleset details?" -> GET /zones/{zone_id}/rulesets/{ruleset_id}
- "Update a ruleset?" -> PUT /zones/{zone_id}/rulesets/{ruleset_id}
- "Create a rule?" -> POST /zones/{zone_id}/rulesets/{ruleset_id}/rules
- "Delete a rule?" -> DELETE /zones/{zone_id}/rulesets/{ruleset_id}/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/rulesets/{ruleset_id}/rules/{rule_id}
- "List all versions?" -> GET /zones/{zone_id}/rulesets/{ruleset_id}/versions
- "Delete a version?" -> DELETE /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version}
- "Get version details?" -> GET /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version}
- "Get by_tag details?" -> GET /zones/{zone_id}/rulesets/{ruleset_id}/versions/{ruleset_version}/by_tag/{rule_tag}
- "List all schemas?" -> GET /zones/{zone_id}/schema_validation/schemas
- "Create a schema?" -> POST /zones/{zone_id}/schema_validation/schemas
- "List all hosts?" -> GET /zones/{zone_id}/schema_validation/schemas/hosts
- "Delete a schema?" -> DELETE /zones/{zone_id}/schema_validation/schemas/{schema_id}
- "Get schema details?" -> GET /zones/{zone_id}/schema_validation/schemas/{schema_id}
- "Partially update a schema?" -> PATCH /zones/{zone_id}/schema_validation/schemas/{schema_id}
- "List all operations?" -> GET /zones/{zone_id}/schema_validation/schemas/{schema_id}/operations
- "List all settings?" -> GET /zones/{zone_id}/schema_validation/settings
- "List all operations?" -> GET /zones/{zone_id}/schema_validation/settings/operations
- "Delete a operation?" -> DELETE /zones/{zone_id}/schema_validation/settings/operations/{operation_id}
- "Get operation details?" -> GET /zones/{zone_id}/schema_validation/settings/operations/{operation_id}
- "Update a operation?" -> PUT /zones/{zone_id}/schema_validation/settings/operations/{operation_id}
- "Create a force_axfr?" -> POST /zones/{zone_id}/secondary_dns/force_axfr
- "List all incoming?" -> GET /zones/{zone_id}/secondary_dns/incoming
- "Create a incoming?" -> POST /zones/{zone_id}/secondary_dns/incoming
- "List all outgoing?" -> GET /zones/{zone_id}/secondary_dns/outgoing
- "Create a outgoing?" -> POST /zones/{zone_id}/secondary_dns/outgoing
- "Create a disable?" -> POST /zones/{zone_id}/secondary_dns/outgoing/disable
- "Create a enable?" -> POST /zones/{zone_id}/secondary_dns/outgoing/enable
- "Create a force_notify?" -> POST /zones/{zone_id}/secondary_dns/outgoing/force_notify
- "List all status?" -> GET /zones/{zone_id}/secondary_dns/outgoing/status
- "List all insights?" -> GET /zones/{zone_id}/security-center/insights
- "List all class?" -> GET /zones/{zone_id}/security-center/insights/class
- "List all severity?" -> GET /zones/{zone_id}/security-center/insights/severity
- "List all type?" -> GET /zones/{zone_id}/security-center/insights/type
- "List all securitytxt?" -> GET /zones/{zone_id}/security-center/securitytxt
- "List all settings?" -> GET /zones/{zone_id}/settings
- "List all aegis?" -> GET /zones/{zone_id}/settings/aegis
- "List all fonts?" -> GET /zones/{zone_id}/settings/fonts
- "List all origin_h2_max_streams?" -> GET /zones/{zone_id}/settings/origin_h2_max_streams
- "List all origin_max_http_version?" -> GET /zones/{zone_id}/settings/origin_max_http_version
- "List all rum?" -> GET /zones/{zone_id}/settings/rum
- "List all speed_brain?" -> GET /zones/{zone_id}/settings/speed_brain
- "List all ssl_automatic_mode?" -> GET /zones/{zone_id}/settings/ssl_automatic_mode
- "List all config?" -> GET /zones/{zone_id}/settings/zaraz/config
- "List all default?" -> GET /zones/{zone_id}/settings/zaraz/default
- "List all export?" -> GET /zones/{zone_id}/settings/zaraz/export
- "List all history?" -> GET /zones/{zone_id}/settings/zaraz/history
- "List all configs?" -> GET /zones/{zone_id}/settings/zaraz/history/configs
- "Create a publish?" -> POST /zones/{zone_id}/settings/zaraz/publish
- "List all workflow?" -> GET /zones/{zone_id}/settings/zaraz/workflow
- "Get setting details?" -> GET /zones/{zone_id}/settings/{setting_id}
- "Partially update a setting?" -> PATCH /zones/{zone_id}/settings/{setting_id}
- "List all smart_shield?" -> GET /zones/{zone_id}/smart_shield
- "List all cache_reserve_clear?" -> GET /zones/{zone_id}/smart_shield/cache_reserve_clear
- "Create a cache_reserve_clear?" -> POST /zones/{zone_id}/smart_shield/cache_reserve_clear
- "List all healthchecks?" -> GET /zones/{zone_id}/smart_shield/healthchecks
- "Create a healthcheck?" -> POST /zones/{zone_id}/smart_shield/healthchecks
- "Delete a healthcheck?" -> DELETE /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id}
- "Get healthcheck details?" -> GET /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id}
- "Partially update a healthcheck?" -> PATCH /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id}
- "Update a healthcheck?" -> PUT /zones/{zone_id}/smart_shield/healthchecks/{healthcheck_id}
- "List all snippets?" -> GET /zones/{zone_id}/snippets
- "List all snippet_rules?" -> GET /zones/{zone_id}/snippets/snippet_rules
- "Delete a snippet?" -> DELETE /zones/{zone_id}/snippets/{snippet_name}
- "Get snippet details?" -> GET /zones/{zone_id}/snippets/{snippet_name}
- "Update a snippet?" -> PUT /zones/{zone_id}/snippets/{snippet_name}
- "List all content?" -> GET /zones/{zone_id}/snippets/{snippet_name}/content
- "List all current?" -> GET /zones/{zone_id}/spectrum/analytics/aggregate/current
- "List all bytime?" -> GET /zones/{zone_id}/spectrum/analytics/events/bytime
- "List all summary?" -> GET /zones/{zone_id}/spectrum/analytics/events/summary
- "List all apps?" -> GET /zones/{zone_id}/spectrum/apps
- "Create a app?" -> POST /zones/{zone_id}/spectrum/apps
- "Delete a app?" -> DELETE /zones/{zone_id}/spectrum/apps/{app_id}
- "Get app details?" -> GET /zones/{zone_id}/spectrum/apps/{app_id}
- "Update a app?" -> PUT /zones/{zone_id}/spectrum/apps/{app_id}
- "List all availabilities?" -> GET /zones/{zone_id}/speed_api/availabilities
- "List all pages?" -> GET /zones/{zone_id}/speed_api/pages
- "List all tests?" -> GET /zones/{zone_id}/speed_api/pages/{url}/tests
- "Create a test?" -> POST /zones/{zone_id}/speed_api/pages/{url}/tests
- "Get test details?" -> GET /zones/{zone_id}/speed_api/pages/{url}/tests/{test_id}
- "List all trend?" -> GET /zones/{zone_id}/speed_api/pages/{url}/trend
- "Delete a schedule?" -> DELETE /zones/{zone_id}/speed_api/schedule/{url}
- "Get schedule details?" -> GET /zones/{zone_id}/speed_api/schedule/{url}
- "Create a analyze?" -> POST /zones/{zone_id}/ssl/analyze
- "List all certificate_packs?" -> GET /zones/{zone_id}/ssl/certificate_packs
- "Create a order?" -> POST /zones/{zone_id}/ssl/certificate_packs/order
- "List all quota?" -> GET /zones/{zone_id}/ssl/certificate_packs/quota
- "Delete a certificate_pack?" -> DELETE /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id}
- "Get certificate_pack details?" -> GET /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id}
- "Partially update a certificate_pack?" -> PATCH /zones/{zone_id}/ssl/certificate_packs/{certificate_pack_id}
- "List all recommendation?" -> GET /zones/{zone_id}/ssl/recommendation
- "List all settings?" -> GET /zones/{zone_id}/ssl/universal/settings
- "List all verification?" -> GET /zones/{zone_id}/ssl/verification
- "Partially update a verification?" -> PATCH /zones/{zone_id}/ssl/verification/{certificate_pack_id}
- "List all subscription?" -> GET /zones/{zone_id}/subscription
- "Create a subscription?" -> POST /zones/{zone_id}/subscription
- "List all config?" -> GET /zones/{zone_id}/token_validation/config
- "Create a config?" -> POST /zones/{zone_id}/token_validation/config
- "Delete a config?" -> DELETE /zones/{zone_id}/token_validation/config/{config_id}
- "Get config details?" -> GET /zones/{zone_id}/token_validation/config/{config_id}
- "Partially update a config?" -> PATCH /zones/{zone_id}/token_validation/config/{config_id}
- "List all rules?" -> GET /zones/{zone_id}/token_validation/rules
- "Create a rule?" -> POST /zones/{zone_id}/token_validation/rules
- "Create a bulk?" -> POST /zones/{zone_id}/token_validation/rules/bulk
- "Create a preview?" -> POST /zones/{zone_id}/token_validation/rules/preview
- "Delete a rule?" -> DELETE /zones/{zone_id}/token_validation/rules/{rule_id}
- "Get rule details?" -> GET /zones/{zone_id}/token_validation/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/token_validation/rules/{rule_id}
- "List all url_normalization?" -> GET /zones/{zone_id}/url_normalization
- "List all waiting_rooms?" -> GET /zones/{zone_id}/waiting_rooms
- "Create a waiting_room?" -> POST /zones/{zone_id}/waiting_rooms
- "Create a preview?" -> POST /zones/{zone_id}/waiting_rooms/preview
- "List all settings?" -> GET /zones/{zone_id}/waiting_rooms/settings
- "Delete a waiting_room?" -> DELETE /zones/{zone_id}/waiting_rooms/{waiting_room_id}
- "Get waiting_room details?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}
- "Partially update a waiting_room?" -> PATCH /zones/{zone_id}/waiting_rooms/{waiting_room_id}
- "Update a waiting_room?" -> PUT /zones/{zone_id}/waiting_rooms/{waiting_room_id}
- "List all events?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events
- "Create a event?" -> POST /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events
- "Delete a event?" -> DELETE /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}
- "Get event details?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}
- "Partially update a event?" -> PATCH /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}
- "Update a event?" -> PUT /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}
- "List all details?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}/events/{event_id}/details
- "List all rules?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules
- "Create a rule?" -> POST /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules
- "Delete a rule?" -> DELETE /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules/{rule_id}
- "Partially update a rule?" -> PATCH /zones/{zone_id}/waiting_rooms/{waiting_room_id}/rules/{rule_id}
- "List all status?" -> GET /zones/{zone_id}/waiting_rooms/{waiting_room_id}/status
- "List all hostnames?" -> GET /zones/{zone_id}/web3/hostnames
- "Create a hostname?" -> POST /zones/{zone_id}/web3/hostnames
- "Delete a hostname?" -> DELETE /zones/{zone_id}/web3/hostnames/{identifier}
- "Get hostname details?" -> GET /zones/{zone_id}/web3/hostnames/{identifier}
- "Partially update a hostname?" -> PATCH /zones/{zone_id}/web3/hostnames/{identifier}
- "List all content_list?" -> GET /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list
- "List all entries?" -> GET /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries
- "Create a entry?" -> POST /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries
- "Delete a entry?" -> DELETE /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier}
- "Get entry details?" -> GET /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier}
- "Update a entry?" -> PUT /zones/{zone_id}/web3/hostnames/{identifier}/ipfs_universal_path/content_list/entries/{content_list_entry_identifier}
- "List all routes?" -> GET /zones/{zone_id}/workers/routes
- "Create a route?" -> POST /zones/{zone_id}/workers/routes
- "Delete a route?" -> DELETE /zones/{zone_id}/workers/routes/{route_id}
- "Get route details?" -> GET /zones/{zone_id}/workers/routes/{route_id}
- "Update a route?" -> PUT /zones/{zone_id}/workers/routes/{route_id}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
