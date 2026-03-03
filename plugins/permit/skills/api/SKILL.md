---
name: permitio-api
description: "Permit.io API skill. Use when working with Permit.io for members, api-key, orgs. Covers 258 endpoints."
version: 1.0.0
generator: lapsh
---

# Permit.io API
API version: 2.0.0

## Auth
Bearer bearer

## Base URL
Not specified.

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/members/me -- verify access
3. POST /v2/members -- create first members

## Endpoints

258 endpoints across 14 groups. See references/api-spec.lap for full details.

### members
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/members/me | Get the authenticated account member |
| GET | /v2/members | List Organization Members |
| POST | /v2/members | Invite new members |
| DELETE | /v2/members | Remove permission |
| GET | /v2/members/{member_id} | Get Organization Member |
| DELETE | /v2/members/{member_id} | Remove member |
| PATCH | /v2/members/{member_id} | Edit members |

### api-key
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/api-key/{proj_id}/{env_id} | Get Environment Api Key |
| GET | /v2/api-key/scope | Get Api Key Scope |
| GET | /v2/api-key | List Api Keys |
| POST | /v2/api-key | Create Api Key |
| GET | /v2/api-key/{api_key_id} | Get Api Key |
| DELETE | /v2/api-key/{api_key_id} | Delete Api Key |
| POST | /v2/api-key/{api_key_id}/rotate-secret | Rotate API Key |

### orgs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/orgs | List Organizations |
| POST | /v2/orgs | Create Organization |
| GET | /v2/orgs/{org_id} | Get Organization |
| DELETE | /v2/orgs/{org_id} | Delete Organization |
| PATCH | /v2/orgs/{org_id} | Update Organization |
| GET | /v2/orgs/active/org | Get Active Organization |
| GET | /v2/orgs/{org_id}/stats | Stats Organization |
| GET | /v2/orgs/{org_id}/invites | List Organization Invites |
| POST | /v2/orgs/{org_id}/invites | Invite Members To Organization |
| DELETE | /v2/orgs/{org_id}/invites/{invite_id} | Cancel Invite |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/projects | List Projects |
| POST | /v2/projects | Create Project |
| GET | /v2/projects/{proj_id} | Get Project |
| DELETE | /v2/projects/{proj_id} | Delete Project |
| PATCH | /v2/projects/{proj_id} | Update Project |
| GET | /v2/projects/{proj_id}/envs/{env_id}/stats | Stats Environments |
| GET | /v2/projects/{proj_id}/envs | List Environments |
| POST | /v2/projects/{proj_id}/envs | Create Environment |
| GET | /v2/projects/{proj_id}/envs/{env_id} | Get Environment |
| DELETE | /v2/projects/{proj_id}/envs/{env_id} | Delete Environment |
| PATCH | /v2/projects/{proj_id}/envs/{env_id} | Update Environment |
| POST | /v2/projects/{proj_id}/envs/{env_id}/copy | Copy Environment |
| POST | /v2/projects/{proj_id}/envs/{env_id}/copy/async | Copy Environment Async |
| GET | /v2/projects/{proj_id}/envs/{env_id}/copy/async/{task_id}/result | Get Copy Environment Task Result |
| POST | /v2/projects/{proj_id}/envs/{env_id}/test_jwks | Test Jwks By Url |
| GET | /v2/projects/{proj_id}/repos | List Policy Repos |
| POST | /v2/projects/{proj_id}/repos | Create Policy Repo |
| GET | /v2/projects/{proj_id}/repos/active | Get Active Policy Repo |
| PUT | /v2/projects/{proj_id}/repos/disable | Disable Active Policy Repo |
| PUT | /v2/projects/{proj_id}/repos/{repo_id}/activate | Activate Policy Repo |
| GET | /v2/projects/{proj_id}/repos/{repo_id} | Get Policy Repo |
| DELETE | /v2/projects/{proj_id}/repos/{repo_id} | Delete Policy Repo |
| GET | /v2/projects/{proj_id}/{env_id}/opal_scope | Get Scope Config |
| PUT | /v2/projects/{proj_id}/{env_id}/opal_scope | Set Scope Config |
| DELETE | /v2/projects/{proj_id}/{env_id}/opal_scope | Reset Scope Config |

### schema
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v2/schema/{proj_id}/{env_id}/bulk/roles | Bulk Create Or Replace Roles |
| GET | /v2/schema/{proj_id}/{env_id}/condition_sets | List Condition Sets |
| POST | /v2/schema/{proj_id}/{env_id}/condition_sets | Create Condition Set |
| GET | /v2/schema/{proj_id}/{env_id}/condition_sets/{condition_set_id} | Get Condition Set |
| DELETE | /v2/schema/{proj_id}/{env_id}/condition_sets/{condition_set_id} | Delete Condition Set |
| PATCH | /v2/schema/{proj_id}/{env_id}/condition_sets/{condition_set_id} | Update Condition Set |
| GET | /v2/schema/{proj_id}/{env_id}/condition_sets/{condition_set_id}/ancestors | Get Condition Set Ancestors |
| GET | /v2/schema/{proj_id}/{env_id}/condition_sets/{condition_set_id}/descendants | Get Condition Set Descendants |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/implicit_grants | Create Implicit Grant |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/implicit_grants | Delete Implicit Grant |
| PUT | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/implicit_grants/conditions | Update Implicit Grants Conditions |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/action_groups | List Resource Action Groups |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/action_groups | Create Resource Action Group |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/action_groups/{action_group_id} | Get Resource Action Group |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/action_groups/{action_group_id} | Delete Resource Action Group |
| PATCH | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/action_groups/{action_group_id} | Update Resource Action Group |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/actions | List Resource Actions |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/actions | Create Resource Action |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/actions/{action_id} | Get Resource Action |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/actions/{action_id} | Delete Resource Action |
| PATCH | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/actions/{action_id} | Update Resource Action |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/attributes | List Resource Attributes |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/attributes | Create Resource Attribute |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/attributes/{attribute_id} | Get Resource Attribute |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/attributes/{attribute_id} | Delete Resource Attribute |
| PATCH | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/attributes/{attribute_id} | Update Resource Attribute |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/relations | List Resource Relations |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/relations | Create Resource Relation |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/relations/{relation_id} | Get Resource Relation |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/relations/{relation_id} | Delete Resource Relation |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles | List Resource Roles |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles | Create Resource Role |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id} | Get Resource Role |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id} | Delete Resource Role |
| PATCH | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id} | Update Resource Role |
| POST | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/permissions | Assign Permissions to Role |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/permissions | Remove Permissions from Role |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/ancestors | Get Resource Role Ancestors |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id}/descendants | Get Resource Role Descendants |
| GET | /v2/schema/{proj_id}/{env_id}/resources | List Resources |
| POST | /v2/schema/{proj_id}/{env_id}/resources | Create Resource |
| GET | /v2/schema/{proj_id}/{env_id}/resources/{resource_id} | Get Resource |
| PUT | /v2/schema/{proj_id}/{env_id}/resources/{resource_id} | Replace Resource |
| DELETE | /v2/schema/{proj_id}/{env_id}/resources/{resource_id} | Delete Resource |
| PATCH | /v2/schema/{proj_id}/{env_id}/resources/{resource_id} | Update Resource |
| GET | /v2/schema/{proj_id}/{env_id}/roles | List Roles |
| POST | /v2/schema/{proj_id}/{env_id}/roles | Create Role |
| GET | /v2/schema/{proj_id}/{env_id}/roles/{role_id} | Get Role |
| DELETE | /v2/schema/{proj_id}/{env_id}/roles/{role_id} | Delete Role |
| PATCH | /v2/schema/{proj_id}/{env_id}/roles/{role_id} | Update Role |
| POST | /v2/schema/{proj_id}/{env_id}/roles/{role_id}/permissions | Assign Permissions To Role |
| DELETE | /v2/schema/{proj_id}/{env_id}/roles/{role_id}/permissions | Remove Permissions From Role |
| GET | /v2/schema/{proj_id}/{env_id}/roles/{role_id}/ancestors | Get Role Ancestors |
| GET | /v2/schema/{proj_id}/{env_id}/roles/{role_id}/descendants | Get Role Descendants |
| GET | /v2/schema/{proj_id}/{env_id}/users/attributes | List User Attributes |
| POST | /v2/schema/{proj_id}/{env_id}/users/attributes | Create User Attribute |
| GET | /v2/schema/{proj_id}/{env_id}/users/attributes/{attribute_id} | Get User Attribute |
| DELETE | /v2/schema/{proj_id}/{env_id}/users/attributes/{attribute_id} | Delete User Attribute |
| PATCH | /v2/schema/{proj_id}/{env_id}/users/attributes/{attribute_id} | Update User Attribute |
| GET | /v2/schema/{proj_id}/{env_id}/groups/direct | List Direct Group |
| GET | /v2/schema/{proj_id}/{env_id}/groups/direct/{group_instance_key} | Get Direct Group |
| GET | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/children | List group children (EAP) |
| GET | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/parents | List group parents (EAP) |
| GET | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/users | List group users (EAP) |
| GET | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/roles | List group roles (EAP) |
| POST | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/roles | Assign Role To Group |
| DELETE | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/roles | Remove Role From Group |
| GET | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key} | Get Group |
| DELETE | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key} | Delete Group |
| GET | /v2/schema/{proj_id}/{env_id}/groups | List Group |
| POST | /v2/schema/{proj_id}/{env_id}/groups | Create Group |
| PUT | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/users/{user_id} | Assign User To Group |
| DELETE | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/users/{user_id} | Remove User From Group |
| PUT | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/assign_group | Assign Group To Group |
| DELETE | /v2/schema/{proj_id}/{env_id}/groups/{group_instance_key}/assign_group | Remove Group From Group |

### facts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/facts/{proj_id}/{env_id}/users | List Users |
| POST | /v2/facts/{proj_id}/{env_id}/users | Create User |
| GET | /v2/facts/{proj_id}/{env_id}/users/{user_id} | Get User |
| PUT | /v2/facts/{proj_id}/{env_id}/users/{user_id} | Replace User |
| DELETE | /v2/facts/{proj_id}/{env_id}/users/{user_id} | Delete User |
| PATCH | /v2/facts/{proj_id}/{env_id}/users/{user_id} | Update User |
| POST | /v2/facts/{proj_id}/{env_id}/users/{user_id}/roles | Assign Role To User |
| DELETE | /v2/facts/{proj_id}/{env_id}/users/{user_id}/roles | Unassign Role From User |
| GET | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id}/users | List Tenant Users |
| POST | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id}/users | Add User To Tenant |
| GET | /v2/facts/{proj_id}/{env_id}/tenants | List Tenants |
| POST | /v2/facts/{proj_id}/{env_id}/tenants | Create Tenant |
| GET | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id} | Get Tenant |
| DELETE | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id} | Delete Tenant |
| PATCH | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id} | Update Tenant |
| DELETE | /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id}/users/{user_id} | Delete Tenant User |
| GET | /v2/facts/{proj_id}/{env_id}/role_assignments/detailed | List Role Assignments Detailed |
| GET | /v2/facts/{proj_id}/{env_id}/role_assignments | List Role Assignments |
| POST | /v2/facts/{proj_id}/{env_id}/role_assignments | Assign Role |
| DELETE | /v2/facts/{proj_id}/{env_id}/role_assignments | Unassign Role |
| POST | /v2/facts/{proj_id}/{env_id}/role_assignments/bulk | Bulk create role assignments |
| DELETE | /v2/facts/{proj_id}/{env_id}/role_assignments/bulk | Bulk Unassign Role |
| GET | /v2/facts/{proj_id}/{env_id}/set_rules | List Set Permissions |
| POST | /v2/facts/{proj_id}/{env_id}/set_rules | Assign Set Permissions |
| DELETE | /v2/facts/{proj_id}/{env_id}/set_rules | Unassign Set Permissions |
| GET | /v2/facts/{proj_id}/{env_id}/resource_instances/detailed | List Resource Instances Detailed |
| GET | /v2/facts/{proj_id}/{env_id}/resource_instances | List Resource Instances |
| POST | /v2/facts/{proj_id}/{env_id}/resource_instances | Create Resource Instance |
| GET | /v2/facts/{proj_id}/{env_id}/resource_instances/{instance_id} | Get Resource Instance |
| DELETE | /v2/facts/{proj_id}/{env_id}/resource_instances/{instance_id} | Delete Resource Instance |
| PATCH | /v2/facts/{proj_id}/{env_id}/resource_instances/{instance_id} | Update Resource Instance |
| GET | /v2/facts/{proj_id}/{env_id}/proxy_configs | List Proxy Configs |
| POST | /v2/facts/{proj_id}/{env_id}/proxy_configs | Create Proxy Config |
| GET | /v2/facts/{proj_id}/{env_id}/proxy_configs/{proxy_config_id} | Get Proxy Config |
| DELETE | /v2/facts/{proj_id}/{env_id}/proxy_configs/{proxy_config_id} | Delete Proxy Config |
| PATCH | /v2/facts/{proj_id}/{env_id}/proxy_configs/{proxy_config_id} | Update Proxy Config |
| PUT | /v2/facts/{proj_id}/{env_id}/bulk/users | Bulk Replace Users |
| POST | /v2/facts/{proj_id}/{env_id}/bulk/users | Bulk Create Users |
| DELETE | /v2/facts/{proj_id}/{env_id}/bulk/users | Bulk Delete Users |
| POST | /v2/facts/{proj_id}/{env_id}/bulk/tenants | Bulk Create Tenants |
| DELETE | /v2/facts/{proj_id}/{env_id}/bulk/tenants | Bulk Delete Tenants |
| PUT | /v2/facts/{proj_id}/{env_id}/bulk/resource_instances | Bulk Replace Resource Instances |
| DELETE | /v2/facts/{proj_id}/{env_id}/bulk/resource_instances | Bulk Delete Resource Instances |
| GET | /v2/facts/{proj_id}/{env_id}/email_configurations | Get Email Configuration |
| POST | /v2/facts/{proj_id}/{env_id}/email_configurations | Create Or Update Email Configuration |
| POST | /v2/facts/{proj_id}/{env_id}/email_configurations/send_test_email | Send Test Email |
| GET | /v2/facts/{proj_id}/{env_id}/email_templates/ | List Templates |
| GET | /v2/facts/{proj_id}/{env_id}/email_templates/{template_type} | Get Template By Type |
| POST | /v2/facts/{proj_id}/{env_id}/email_templates/{template_type} | Update Template By Type |
| POST | /v2/facts/{proj_id}/{env_id}/email_templates/{template_type}/send_test_email | Send Test Email By Type |
| GET | /v2/facts/{proj_id}/{env_id}/relationship_tuples/detailed | List Relationship Tuples Detailed |
| GET | /v2/facts/{proj_id}/{env_id}/relationship_tuples | List Relationship Tuples |
| POST | /v2/facts/{proj_id}/{env_id}/relationship_tuples | Create Relationship Tuple |
| DELETE | /v2/facts/{proj_id}/{env_id}/relationship_tuples | Delete Relationship Tuple |
| POST | /v2/facts/{proj_id}/{env_id}/relationship_tuples/bulk | Bulk create relationship tuples |
| DELETE | /v2/facts/{proj_id}/{env_id}/relationship_tuples/bulk | Bulk Delete Relationship Tuples |
| GET | /v2/facts/{proj_id}/{env_id}/user_invites | List User Invites |
| POST | /v2/facts/{proj_id}/{env_id}/user_invites | Create User Invite |
| GET | /v2/facts/{proj_id}/{env_id}/user_invites/{user_invite_id} | Get User Invite |
| DELETE | /v2/facts/{proj_id}/{env_id}/user_invites/{user_invite_id} | Delete User Invite |
| PATCH | /v2/facts/{proj_id}/{env_id}/user_invites/{user_invite_id} | Update User Invite |
| POST | /v2/facts/{proj_id}/{env_id}/user_invites/{user_invite_id}/approve | Approve User Invite |
| GET | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id} | List Access Requests |
| POST | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id} | Create Access Request |
| GET | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id}/{access_request_id} | Get Access Request |
| PATCH | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id}/{access_request_id}/reviewer | Update Access Request Reviewer |
| PUT | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id}/{access_request_id}/approve | Approve Access Request |
| PUT | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id}/{access_request_id}/deny | Deny Access Request |
| PUT | /v2/facts/{proj_id}/{env_id}/access_requests/{elements_config_id}/user/{user_id}/tenant/{tenant_id}/{access_request_id}/cancel | Cancel Access Request |

### pdps
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/pdps/{proj_id}/{env_id}/configs | List PDP configurations |
| GET | /v2/pdps/{proj_id}/{env_id}/configs/{pdp_id}/values | Get PDP configuration |
| PUT | /v2/pdps/{proj_id}/{env_id}/configs/{pdp_id}/debug-audit-logs/enable | Enable debug audit logs |
| PUT | /v2/pdps/{proj_id}/{env_id}/configs/{pdp_id}/debug-audit-logs/disable | Disable debug audit logs |
| POST | /v2/pdps/{proj_id}/{env_id}/configs/{pdp_id}/rotate-api-key | Rotate PDP API Key |
| POST | /v2/pdps/{proj_id}/{env_id}/configs/migrate-shards | Migrate PDP Config number of shards |
| GET | /v2/pdps/{proj_id}/{env_id}/audit_logs | List Audit Logs |
| GET | /v2/pdps/{proj_id}/{env_id}/audit_logs/{log_id} | Get detailed audit log |

### elements
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/elements/{proj_id}/{env_id}/config | List Elements Configs |
| POST | /v2/elements/{proj_id}/{env_id}/config | Create Elements Config |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id} | Get Elements Config |
| PATCH | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id} | Update Elements Config |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/runtime | Get Elements Config Runtime |
| DELETE | /v2/elements/{proj_id}/{env_id}/{elements_config_id} | Delete Elements Config |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users | List users |
| POST | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users | Create user |
| DELETE | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users/{user_id} | Delete user |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/user-invites | List all Elements User Invites |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/roles | List roles |
| POST | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users/{user_id}/roles | Assign role to user |
| DELETE | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users/{user_id}/roles | Unassign role from user |
| POST | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/active | Set Config Active |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/audit_logs | List audit logs |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests | List Access Requests |
| POST | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests | Create Access Request |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id} | Get Access Request |
| PATCH | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id}/reviewer | Update Access Request Reviewer |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id}/approve | Approve Access Request |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id}/deny | Deny Access Request |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id}/cancel | Cancel Access Request |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval | List Operation Approvals |
| POST | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval | Create Operation Approval |
| GET | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval/{operation_approval_id} | Get Operation Approval |
| PATCH | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval/{operation_approval_id}/reviewer | Update Operation Approval Reviewer |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval/{operation_approval_id}/approve | Approve Operation Approval |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval/{operation_approval_id}/deny | Deny Operation Approval |
| PUT | /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/operation_approval/{operation_approval_id}/cancel | Cancel Operation Approval |

### deprecated
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/deprecated/history | List Api Events |
| GET | /v2/deprecated/history/{event_id} | Get Api Event |
| GET | /v2/deprecated/history/{event_id}/request | Get Request Body |
| GET | /v2/deprecated/history/{event_id}/response | Get Response Body |
| GET | /v2/deprecated/activity | List Activity Events |
| GET | /v2/deprecated/activity/types | List Activity Types |

### history
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/history | List Api Events |
| GET | /v2/history/{event_id} | Get Api Event |
| GET | /v2/history/{event_id}/request | Get Request Body |
| GET | /v2/history/{event_id}/response | Get Response Body |

### activity
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/activity | List Activity Events |
| GET | /v2/activity/types | List Activity Types |

### policy_guards
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/policy_guards/scopes | List Policy Guard Scopes |
| POST | /v2/policy_guards/scopes | Create Policy Guard Scope |
| GET | /v2/policy_guards/scopes/{policy_guard_scope_id} | Get Policy Guard Scope |
| DELETE | /v2/policy_guards/scopes/{policy_guard_scope_id} | Delete Policy Guard Scope |
| POST | /v2/policy_guards/scopes/{policy_guard_scope_id}/associate | Associate Policy Guard Scope |
| DELETE | /v2/policy_guards/scopes/{policy_guard_scope_id}/disassociate | Disassociate Policy Guard Scope |
| GET | /v2/policy_guards/scopes/{policy_guard_scope_id}/rules | List Policy Guard Rules |
| POST | /v2/policy_guards/scopes/{policy_guard_scope_id}/rules | Create Policy Guard Rule |
| DELETE | /v2/policy_guards/scopes/{policy_guard_scope_id}/rules | Delete Policy Guard Rule |

### audit-log-replay
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/audit-log-replay | Run the audit log replay |

### internal
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id}/optimized | Get All Data Optimized |
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id} | Get All Data |
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id}/users | Get All Users Data |
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id}/role_assignments | Get All Role Assignments Data |
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id}/resource_instances | Get All Resource Instances Data |
| GET | /v2/internal/opal_data/{org_id}/{proj_id}/{env_id}/relationships | Get All Relationships Data |

## Enhanced Skill Content
## Question Mapping

- "Who am I logged in as?" -> GET /v2/members/me
- "List all members in my organization" -> GET /v2/members
- "Invite a new member with specific permissions" -> POST /v2/members
- "What API keys exist for this environment?" -> GET /v2/api-key/{proj_id}/{env_id}
- "Rotate the secret for an API key" -> POST /v2/api-key/{api_key_id}/rotate-secret
- "What scope does my current API key have?" -> GET /v2/api-key/scope
- "Show me all roles defined in this environment" -> GET /v2/schema/{proj_id}/{env_id}/roles
- "Assign a role to a user in a tenant" -> POST /v2/facts/{proj_id}/{env_id}/users/{user_id}/roles
- "List all tenants in my environment" -> GET /v2/facts/{proj_id}/{env_id}/tenants
- "Who has access to a specific tenant?" -> GET /v2/facts/{proj_id}/{env_id}/tenants/{tenant_id}/users
- "Check the audit log for denied decisions" -> GET /v2/pdps/{proj_id}/{env_id}/audit_logs
- "Copy an environment's config to another environment" -> POST /v2/projects/{proj_id}/envs/{env_id}/copy
- "What resources are defined in my schema?" -> GET /v2/schema/{proj_id}/{env_id}/resources
- "Bulk-create users with role assignments" -> PUT /v2/facts/{proj_id}/{env_id}/bulk/users
- "Review pending access requests for an Elements config" -> GET /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests

## Response Tips

- **Paginated lists** (members, keys, tenants, users, roles, resources, audit logs): Look for `data` array with `total_count` and `page_count`; default is `page=1, per_page=30`. Some endpoints use `pagination_count` instead of `page_count` (audit logs, history, activity).
- **Schema objects** (resources, roles, actions, conditions): Responses nest deeply -- `resource` contains inline `actions`, `roles`, `relations`, and `attributes` maps; roles include `permissions[]`, `extends[]`, and `granted_to`.
- **Bulk operations**: Return counts (`assignments_created`, `assignments_removed`) not individual records; errors surface as 422 with validation details.
- **Async tasks** (env copy, policy guard association): Return `{task_id, status, result, error}` -- poll the task result endpoint until `status` is no longer pending.
- **Delete endpoints**: Return 204 with no body on success; a 200 with the deleted object only when `return_deleted=True` is passed (role assignments).
- **All errors**: The API uses 422 uniformly for validation errors; 404 only appears on role assignment deletion when the assignment does not exist.

## Anomaly Flags

- **API key `last_used_at` is null or very old**: The key may be stale or orphaned -- recommend rotation or deletion.
- **`is_onboarding` still true on a member**: User has not completed setup; follow up or reset `onboarding_step`.
- **Organization `usage_limits` approaching thresholds**: Surface `historical_usage.current_month.mau` and `tenants` counts from GET /v2/orgs/{org_id}/stats relative to plan limits.
- **Async env copy stuck**: If polling GET .../copy/async/{task_id}/result returns a non-terminal `status` for more than a few minutes, surface the `error` field and warn of possible timeout.
- **Deprecated endpoint usage**: Flag any calls routed through `/v2/deprecated/...` paths -- these mirror `/v2/history` and `/v2/activity` but may be removed without notice.
- **PDP audit log `decision: false` spikes**: A sudden increase in denied decisions may indicate misconfigured policies or an authorization incident.
- **Bulk delete responses with zero removals**: `assignments_removed: 0` or `0` records deleted likely means the identifiers were wrong or already gone.
- **`v1compat_*` fields present on schema objects**: These indicate legacy migration shims are still active; recommend completing the v2 migration.

## Playbook

### 1. Bootstrap a New Project with RBAC

1. Create the project: POST /v2/projects with `key`, `name`, and optional `initial_environments` (defaults to dev + production).
2. Define resource types: POST /v2/schema/{proj_id}/{env_id}/resources with `key`, `name`, and `actions` map (e.g., `{"read": {}, "write": {}, "delete": {}}`).
3. Create roles: POST /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles with `key`, `name`, and `permissions` list referencing action keys.
4. Set up tenants: POST /v2/facts/{proj_id}/{env_id}/tenants with `key` and `name`.
5. Sync users: PUT /v2/facts/{proj_id}/{env_id}/bulk/users with user objects including `role_assignments` per tenant.
6. Generate a PDP API key: POST /v2/api-key scoped to the environment for your PDP sidecar.

### 2. Rotate an API Key Without Downtime

1. Identify the key: GET /v2/api-key to list keys; note the `id` and `last_used_at`.
2. Rotate the secret: POST /v2/api-key/{api_key_id}/rotate-secret -- save the new `secret` from the response immediately (it is only shown once).
3. Update your PDP or application config with the new secret.
4. Verify connectivity by checking PDP logs or calling GET /v2/api-key/scope with the new token.
5. Optionally check GET /v2/api-key/{api_key_id} to confirm `last_used_at` updates with the new secret.

### 3. Clone an Environment for Staging

1. List environments: GET /v2/projects/{proj_id}/envs.
2. Kick off async copy: POST /v2/projects/{proj_id}/envs/{env_id}/copy/async with `target_env` set to the destination environment key or ID, and `conflict_strategy` set to `fail` or `overwrite`.
3. Poll for completion: GET /v2/projects/{proj_id}/envs/{env_id}/copy/async/{task_id}/result until `status` is terminal.
4. Verify the target: GET /v2/projects/{proj_id}/envs/{target_env_id}/stats to confirm resources, roles, and users carried over.

### 4. Investigate a Permission Denial

1. Pull audit logs: GET /v2/pdps/{proj_id}/{env_id}/audit_logs with `decision=false`, `users=[user_key]`, and a `timestamp_from` window.
2. Inspect a specific log: GET /v2/pdps/{proj_id}/{env_id}/audit_logs/{log_id} -- check `resource_type`, `action`, `tenant`, `reason`, and `context`.
3. Verify the user's role assignments: GET /v2/facts/{proj_id}/{env_id}/users/{user_id} and examine `roles[]` and `associated_tenants[]`.
4. Check the role's permissions: GET /v2/schema/{proj_id}/{env_id}/resources/{resource_id}/roles/{role_id} -- confirm the required action is in `permissions[]`.
5. If using condition sets, check set rules: GET /v2/facts/{proj_id}/{env_id}/set_rules filtered by the relevant `user_set` and `resource_set`.

### 5. Set Up Permit Elements with Access Requests

1. Create an Elements config: POST /v2/elements/{proj_id}/{env_id}/config with `elements_type`, `settings`, and `roles_to_levels` mapping.
2. Activate it: POST /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/active.
3. Add users: POST /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/users with `key` and optional `role`.
4. When a user submits an access request: POST /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests with `access_request_details`.
5. Review and approve: PUT /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/access_requests/{access_request_id}/approve with optional `reviewer_comment`.
6. Monitor via audit logs: GET /v2/elements/{proj_id}/{env_id}/config/{elements_config_id}/data/audit_logs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
