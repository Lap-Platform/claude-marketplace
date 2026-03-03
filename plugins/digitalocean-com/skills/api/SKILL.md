---
name: digitalocean-api
description: "DigitalOcean API skill. Use when working with DigitalOcean for 1-clicks, account, actions. Covers 545 endpoints."
version: 1.0.0
generator: lapsh
---

# DigitalOcean API
API version: 2.0

## Auth
Bearer bearer

## Base URL
https://api.digitalocean.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/1-clicks -- verify access
3. POST /v2/1-clicks/kubernetes -- create first kubernetes

## Endpoints

545 endpoints across 39 groups. See references/api-spec.lap for full details.

### 1-clicks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/1-clicks |  |
| POST | /v2/1-clicks/kubernetes |  |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/account |  |
| GET | /v2/account/keys |  |
| POST | /v2/account/keys |  |
| GET | /v2/account/keys/{ssh_key_identifier} |  |
| PUT | /v2/account/keys/{ssh_key_identifier} |  |
| DELETE | /v2/account/keys/{ssh_key_identifier} |  |

### actions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/actions |  |
| GET | /v2/actions/{action_id} |  |

### add-ons
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/add-ons/apps |  |
| GET | /v2/add-ons/apps/{app_slug}/metadata |  |
| GET | /v2/add-ons/saas |  |
| POST | /v2/add-ons/saas |  |
| GET | /v2/add-ons/saas/{resource_uuid} |  |
| DELETE | /v2/add-ons/saas/{resource_uuid} |  |
| PATCH | /v2/add-ons/saas/{resource_uuid} |  |
| PATCH | /v2/add-ons/saas/{resource_uuid}/plan |  |

### apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/apps |  |
| POST | /v2/apps |  |
| DELETE | /v2/apps/{id} |  |
| GET | /v2/apps/{id} |  |
| PUT | /v2/apps/{id} |  |
| POST | /v2/apps/{app_id}/restart |  |
| GET | /v2/apps/{app_id}/components/{component_name}/logs |  |
| GET | /v2/apps/{app_id}/components/{component_name}/exec |  |
| GET | /v2/apps/{app_id}/instances |  |
| GET | /v2/apps/{app_id}/deployments |  |
| POST | /v2/apps/{app_id}/deployments |  |
| GET | /v2/apps/{app_id}/deployments/{deployment_id} |  |
| POST | /v2/apps/{app_id}/deployments/{deployment_id}/cancel |  |
| GET | /v2/apps/{app_id}/deployments/{deployment_id}/components/{component_name}/logs |  |
| GET | /v2/apps/{app_id}/deployments/{deployment_id}/logs |  |
| GET | /v2/apps/{app_id}/deployments/{deployment_id}/components/{component_name}/exec |  |
| GET | /v2/apps/{app_id}/logs |  |
| GET | /v2/apps/{app_id}/job-invocations |  |
| GET | /v2/apps/{app_id}/job-invocations/{job_invocation_id} |  |
| POST | /v2/apps/{app_id}/job-invocations/{job_invocation_id}/cancel |  |
| GET | /v2/apps/{app_id}/jobs/{job_name}/invocations/{job_invocation_id}/logs |  |
| GET | /v2/apps/tiers/instance_sizes |  |
| GET | /v2/apps/tiers/instance_sizes/{slug} |  |
| GET | /v2/apps/regions |  |
| POST | /v2/apps/propose |  |
| GET | /v2/apps/{app_id}/alerts |  |
| POST | /v2/apps/{app_id}/alerts/{alert_id}/destinations |  |
| POST | /v2/apps/{app_id}/rollback |  |
| POST | /v2/apps/{app_id}/rollback/validate |  |
| POST | /v2/apps/{app_id}/rollback/commit |  |
| POST | /v2/apps/{app_id}/rollback/revert |  |
| GET | /v2/apps/{app_id}/metrics/bandwidth_daily |  |
| POST | /v2/apps/metrics/bandwidth_daily |  |
| GET | /v2/apps/{app_id}/health |  |

### cdn
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/cdn/endpoints |  |
| POST | /v2/cdn/endpoints |  |
| GET | /v2/cdn/endpoints/{cdn_id} |  |
| PUT | /v2/cdn/endpoints/{cdn_id} |  |
| DELETE | /v2/cdn/endpoints/{cdn_id} |  |
| DELETE | /v2/cdn/endpoints/{cdn_id}/cache |  |

### certificates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/certificates |  |
| POST | /v2/certificates |  |
| GET | /v2/certificates/{certificate_id} |  |
| DELETE | /v2/certificates/{certificate_id} |  |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/customers/my/balance |  |
| GET | /v2/customers/my/billing_history |  |
| GET | /v2/customers/my/invoices |  |
| GET | /v2/customers/my/invoices/{invoice_uuid} |  |
| GET | /v2/customers/my/invoices/{invoice_uuid}/csv |  |
| GET | /v2/customers/my/invoices/{invoice_uuid}/pdf |  |
| GET | /v2/customers/my/invoices/{invoice_uuid}/summary |  |

### billing
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/billing/{account_urn}/insights/{start_date}/{end_date} |  |

### databases
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/databases/options |  |
| GET | /v2/databases |  |
| POST | /v2/databases |  |
| GET | /v2/databases/{database_cluster_uuid} |  |
| DELETE | /v2/databases/{database_cluster_uuid} |  |
| GET | /v2/databases/{database_cluster_uuid}/config |  |
| PATCH | /v2/databases/{database_cluster_uuid}/config |  |
| GET | /v2/databases/{database_cluster_uuid}/ca |  |
| GET | /v2/databases/{database_cluster_uuid}/online-migration |  |
| PUT | /v2/databases/{database_cluster_uuid}/online-migration |  |
| DELETE | /v2/databases/{database_cluster_uuid}/online-migration/{migration_id} |  |
| PUT | /v2/databases/{database_cluster_uuid}/migrate |  |
| PUT | /v2/databases/{database_cluster_uuid}/resize |  |
| GET | /v2/databases/{database_cluster_uuid}/firewall |  |
| PUT | /v2/databases/{database_cluster_uuid}/firewall |  |
| PUT | /v2/databases/{database_cluster_uuid}/maintenance |  |
| PUT | /v2/databases/{database_cluster_uuid}/install_update |  |
| GET | /v2/databases/{database_cluster_uuid}/backups |  |
| GET | /v2/databases/{database_cluster_uuid}/replicas |  |
| POST | /v2/databases/{database_cluster_uuid}/replicas |  |
| GET | /v2/databases/{database_cluster_uuid}/events |  |
| GET | /v2/databases/{database_cluster_uuid}/replicas/{replica_name} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/replicas/{replica_name} |  |
| PUT | /v2/databases/{database_cluster_uuid}/replicas/{replica_name}/promote |  |
| GET | /v2/databases/{database_cluster_uuid}/users |  |
| POST | /v2/databases/{database_cluster_uuid}/users |  |
| GET | /v2/databases/{database_cluster_uuid}/users/{username} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/users/{username} |  |
| PUT | /v2/databases/{database_cluster_uuid}/users/{username} |  |
| POST | /v2/databases/{database_cluster_uuid}/users/{username}/reset_auth |  |
| GET | /v2/databases/{database_cluster_uuid}/dbs |  |
| POST | /v2/databases/{database_cluster_uuid}/dbs |  |
| GET | /v2/databases/{database_cluster_uuid}/dbs/{database_name} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/dbs/{database_name} |  |
| GET | /v2/databases/{database_cluster_uuid}/pools |  |
| POST | /v2/databases/{database_cluster_uuid}/pools |  |
| GET | /v2/databases/{database_cluster_uuid}/pools/{pool_name} |  |
| PUT | /v2/databases/{database_cluster_uuid}/pools/{pool_name} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/pools/{pool_name} |  |
| GET | /v2/databases/{database_cluster_uuid}/eviction_policy |  |
| PUT | /v2/databases/{database_cluster_uuid}/eviction_policy |  |
| GET | /v2/databases/{database_cluster_uuid}/sql_mode |  |
| PUT | /v2/databases/{database_cluster_uuid}/sql_mode |  |
| PUT | /v2/databases/{database_cluster_uuid}/upgrade |  |
| GET | /v2/databases/{database_cluster_uuid}/autoscale |  |
| PUT | /v2/databases/{database_cluster_uuid}/autoscale |  |
| GET | /v2/databases/{database_cluster_uuid}/topics |  |
| POST | /v2/databases/{database_cluster_uuid}/topics |  |
| GET | /v2/databases/{database_cluster_uuid}/topics/{topic_name} |  |
| PUT | /v2/databases/{database_cluster_uuid}/topics/{topic_name} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/topics/{topic_name} |  |
| GET | /v2/databases/{database_cluster_uuid}/logsink |  |
| POST | /v2/databases/{database_cluster_uuid}/logsink |  |
| GET | /v2/databases/{database_cluster_uuid}/logsink/{logsink_id} |  |
| PUT | /v2/databases/{database_cluster_uuid}/logsink/{logsink_id} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/logsink/{logsink_id} |  |
| GET | /v2/databases/{database_cluster_uuid}/schema-registry |  |
| POST | /v2/databases/{database_cluster_uuid}/schema-registry |  |
| GET | /v2/databases/{database_cluster_uuid}/schema-registry/{subject_name} |  |
| DELETE | /v2/databases/{database_cluster_uuid}/schema-registry/{subject_name} |  |
| GET | /v2/databases/{database_cluster_uuid}/schema-registry/{subject_name}/versions/{version} |  |
| GET | /v2/databases/{database_cluster_uuid}/schema-registry/config |  |
| PUT | /v2/databases/{database_cluster_uuid}/schema-registry/config |  |
| GET | /v2/databases/{database_cluster_uuid}/schema-registry/config/{subject_name} |  |
| PUT | /v2/databases/{database_cluster_uuid}/schema-registry/config/{subject_name} |  |
| GET | /v2/databases/metrics/credentials |  |
| PUT | /v2/databases/metrics/credentials |  |
| GET | /v2/databases/{database_cluster_uuid}/indexes |  |
| DELETE | /v2/databases/{database_cluster_uuid}/indexes/{index_name} |  |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/domains |  |
| POST | /v2/domains |  |
| GET | /v2/domains/{domain_name} |  |
| DELETE | /v2/domains/{domain_name} |  |
| GET | /v2/domains/{domain_name}/records |  |
| POST | /v2/domains/{domain_name}/records |  |
| GET | /v2/domains/{domain_name}/records/{domain_record_id} |  |
| PATCH | /v2/domains/{domain_name}/records/{domain_record_id} |  |
| PUT | /v2/domains/{domain_name}/records/{domain_record_id} |  |
| DELETE | /v2/domains/{domain_name}/records/{domain_record_id} |  |

### droplets
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/droplets |  |
| POST | /v2/droplets |  |
| DELETE | /v2/droplets |  |
| GET | /v2/droplets/{droplet_id} |  |
| DELETE | /v2/droplets/{droplet_id} |  |
| GET | /v2/droplets/{droplet_id}/backups |  |
| GET | /v2/droplets/{droplet_id}/backups/policy |  |
| GET | /v2/droplets/backups/policies |  |
| GET | /v2/droplets/backups/supported_policies |  |
| GET | /v2/droplets/{droplet_id}/snapshots |  |
| GET | /v2/droplets/{droplet_id}/actions |  |
| POST | /v2/droplets/{droplet_id}/actions |  |
| POST | /v2/droplets/actions |  |
| GET | /v2/droplets/{droplet_id}/actions/{action_id} |  |
| GET | /v2/droplets/{droplet_id}/kernels |  |
| GET | /v2/droplets/{droplet_id}/firewalls |  |
| GET | /v2/droplets/{droplet_id}/neighbors |  |
| GET | /v2/droplets/{droplet_id}/destroy_with_associated_resources |  |
| DELETE | /v2/droplets/{droplet_id}/destroy_with_associated_resources/selective |  |
| DELETE | /v2/droplets/{droplet_id}/destroy_with_associated_resources/dangerous |  |
| GET | /v2/droplets/{droplet_id}/destroy_with_associated_resources/status |  |
| POST | /v2/droplets/{droplet_id}/destroy_with_associated_resources/retry |  |
| GET | /v2/droplets/autoscale |  |
| POST | /v2/droplets/autoscale |  |
| GET | /v2/droplets/autoscale/{autoscale_pool_id} |  |
| PUT | /v2/droplets/autoscale/{autoscale_pool_id} |  |
| DELETE | /v2/droplets/autoscale/{autoscale_pool_id} |  |
| DELETE | /v2/droplets/autoscale/{autoscale_pool_id}/dangerous |  |
| GET | /v2/droplets/autoscale/{autoscale_pool_id}/members |  |
| GET | /v2/droplets/autoscale/{autoscale_pool_id}/history |  |

### firewalls
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/firewalls |  |
| POST | /v2/firewalls |  |
| GET | /v2/firewalls/{firewall_id} |  |
| PUT | /v2/firewalls/{firewall_id} |  |
| DELETE | /v2/firewalls/{firewall_id} |  |
| POST | /v2/firewalls/{firewall_id}/droplets |  |
| DELETE | /v2/firewalls/{firewall_id}/droplets |  |
| POST | /v2/firewalls/{firewall_id}/tags |  |
| DELETE | /v2/firewalls/{firewall_id}/tags |  |
| POST | /v2/firewalls/{firewall_id}/rules |  |
| DELETE | /v2/firewalls/{firewall_id}/rules |  |

### floating_ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/floating_ips |  |
| POST | /v2/floating_ips |  |
| GET | /v2/floating_ips/{floating_ip} |  |
| DELETE | /v2/floating_ips/{floating_ip} |  |
| GET | /v2/floating_ips/{floating_ip}/actions |  |
| POST | /v2/floating_ips/{floating_ip}/actions |  |
| GET | /v2/floating_ips/{floating_ip}/actions/{action_id} |  |

### functions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/functions/namespaces |  |
| POST | /v2/functions/namespaces |  |
| GET | /v2/functions/namespaces/{namespace_id} |  |
| DELETE | /v2/functions/namespaces/{namespace_id} |  |
| GET | /v2/functions/namespaces/{namespace_id}/triggers |  |
| POST | /v2/functions/namespaces/{namespace_id}/triggers |  |
| GET | /v2/functions/namespaces/{namespace_id}/triggers/{trigger_name} |  |
| PUT | /v2/functions/namespaces/{namespace_id}/triggers/{trigger_name} |  |
| DELETE | /v2/functions/namespaces/{namespace_id}/triggers/{trigger_name} |  |

### images
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/images |  |
| POST | /v2/images |  |
| GET | /v2/images/{image_id} |  |
| PUT | /v2/images/{image_id} |  |
| DELETE | /v2/images/{image_id} |  |
| GET | /v2/images/{image_id}/actions |  |
| POST | /v2/images/{image_id}/actions |  |
| GET | /v2/images/{image_id}/actions/{action_id} |  |

### kubernetes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/kubernetes/clusters |  |
| POST | /v2/kubernetes/clusters |  |
| GET | /v2/kubernetes/clusters/{cluster_id} |  |
| PUT | /v2/kubernetes/clusters/{cluster_id} |  |
| DELETE | /v2/kubernetes/clusters/{cluster_id} |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/destroy_with_associated_resources |  |
| DELETE | /v2/kubernetes/clusters/{cluster_id}/destroy_with_associated_resources/selective |  |
| DELETE | /v2/kubernetes/clusters/{cluster_id}/destroy_with_associated_resources/dangerous |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/kubeconfig |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/credentials |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/upgrades |  |
| POST | /v2/kubernetes/clusters/{cluster_id}/upgrade |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/node_pools |  |
| POST | /v2/kubernetes/clusters/{cluster_id}/node_pools |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/node_pools/{node_pool_id} |  |
| PUT | /v2/kubernetes/clusters/{cluster_id}/node_pools/{node_pool_id} |  |
| DELETE | /v2/kubernetes/clusters/{cluster_id}/node_pools/{node_pool_id} |  |
| DELETE | /v2/kubernetes/clusters/{cluster_id}/node_pools/{node_pool_id}/nodes/{node_id} |  |
| POST | /v2/kubernetes/clusters/{cluster_id}/node_pools/{node_pool_id}/recycle |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/user |  |
| GET | /v2/kubernetes/options |  |
| POST | /v2/kubernetes/clusters/{cluster_id}/clusterlint |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/clusterlint |  |
| POST | /v2/kubernetes/registry |  |
| DELETE | /v2/kubernetes/registry |  |
| POST | /v2/kubernetes/registries |  |
| DELETE | /v2/kubernetes/registries |  |
| GET | /v2/kubernetes/clusters/{cluster_id}/status_messages |  |

### load_balancers
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/load_balancers |  |
| GET | /v2/load_balancers |  |
| GET | /v2/load_balancers/{lb_id} |  |
| PUT | /v2/load_balancers/{lb_id} |  |
| DELETE | /v2/load_balancers/{lb_id} |  |
| DELETE | /v2/load_balancers/{lb_id}/cache |  |
| POST | /v2/load_balancers/{lb_id}/droplets |  |
| DELETE | /v2/load_balancers/{lb_id}/droplets |  |
| POST | /v2/load_balancers/{lb_id}/forwarding_rules |  |
| DELETE | /v2/load_balancers/{lb_id}/forwarding_rules |  |

### monitoring
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/monitoring/alerts |  |
| POST | /v2/monitoring/alerts |  |
| GET | /v2/monitoring/alerts/{alert_uuid} |  |
| PUT | /v2/monitoring/alerts/{alert_uuid} |  |
| DELETE | /v2/monitoring/alerts/{alert_uuid} |  |
| GET | /v2/monitoring/metrics/droplet/bandwidth |  |
| GET | /v2/monitoring/metrics/droplet/cpu |  |
| GET | /v2/monitoring/metrics/droplet/filesystem_free |  |
| GET | /v2/monitoring/metrics/droplet/filesystem_size |  |
| GET | /v2/monitoring/metrics/droplet/load_1 |  |
| GET | /v2/monitoring/metrics/droplet/load_5 |  |
| GET | /v2/monitoring/metrics/droplet/load_15 |  |
| GET | /v2/monitoring/metrics/droplet/memory_cached |  |
| GET | /v2/monitoring/metrics/droplet/memory_free |  |
| GET | /v2/monitoring/metrics/droplet/memory_total |  |
| GET | /v2/monitoring/metrics/droplet/memory_available |  |
| GET | /v2/monitoring/metrics/apps/memory_percentage |  |
| GET | /v2/monitoring/metrics/apps/cpu_percentage |  |
| GET | /v2/monitoring/metrics/apps/restart_count |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_connections_current |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_connections_limit |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_cpu_utilization |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_firewall_dropped_bytes |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_firewall_dropped_packets |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_http_responses |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_http_requests_per_second |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_network_throughput_http |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_network_throughput_udp |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_network_throughput_tcp |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_nlb_tcp_network_throughput |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_nlb_udp_network_throughput |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_tls_connections_current |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_tls_connections_limit |  |
| GET | /v2/monitoring/metrics/load_balancer/frontend_tls_connections_exceeding_rate_limit |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_session_duration_avg |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_session_duration_50p |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_session_duration_95p |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_response_time_avg |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_response_time_50p |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_response_time_95p |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_response_time_99p |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_queue_size |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_http_responses |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_connections |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_health_checks |  |
| GET | /v2/monitoring/metrics/load_balancer/droplets_downtime |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/current_instances |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/target_instances |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/current_cpu_utilization |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/target_cpu_utilization |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/current_memory_utilization |  |
| GET | /v2/monitoring/metrics/droplet_autoscale/target_memory_utilization |  |
| POST | /v2/monitoring/sinks/destinations |  |
| GET | /v2/monitoring/sinks/destinations |  |
| GET | /v2/monitoring/sinks/destinations/{destination_uuid} |  |
| POST | /v2/monitoring/sinks/destinations/{destination_uuid} |  |
| DELETE | /v2/monitoring/sinks/destinations/{destination_uuid} |  |
| POST | /v2/monitoring/sinks |  |
| GET | /v2/monitoring/sinks |  |
| GET | /v2/monitoring/sinks/{sink_uuid} |  |
| DELETE | /v2/monitoring/sinks/{sink_uuid} |  |

### nfs
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/nfs |  |
| GET | /v2/nfs |  |
| GET | /v2/nfs/{nfs_id} |  |
| DELETE | /v2/nfs/{nfs_id} |  |
| POST | /v2/nfs/{nfs_id}/actions |  |
| GET | /v2/nfs/snapshots |  |
| GET | /v2/nfs/snapshots/{nfs_snapshot_id} |  |
| DELETE | /v2/nfs/snapshots/{nfs_snapshot_id} |  |

### partner_network_connect
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/partner_network_connect/attachments |  |
| POST | /v2/partner_network_connect/attachments |  |
| GET | /v2/partner_network_connect/attachments/{pa_id} |  |
| PATCH | /v2/partner_network_connect/attachments/{pa_id} |  |
| DELETE | /v2/partner_network_connect/attachments/{pa_id} |  |
| GET | /v2/partner_network_connect/attachments/{pa_id}/bgp_auth_key |  |
| GET | /v2/partner_network_connect/attachments/{pa_id}/remote_routes |  |
| GET | /v2/partner_network_connect/attachments/{pa_id}/service_key |  |
| POST | /v2/partner_network_connect/attachments/{pa_id}/service_key |  |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/projects |  |
| POST | /v2/projects |  |
| GET | /v2/projects/default |  |
| PUT | /v2/projects/default |  |
| PATCH | /v2/projects/default |  |
| GET | /v2/projects/{project_id} |  |
| PUT | /v2/projects/{project_id} |  |
| PATCH | /v2/projects/{project_id} |  |
| DELETE | /v2/projects/{project_id} |  |
| GET | /v2/projects/{project_id}/resources |  |
| POST | /v2/projects/{project_id}/resources |  |
| GET | /v2/projects/default/resources |  |
| POST | /v2/projects/default/resources |  |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/regions |  |

### registries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/registries |  |
| POST | /v2/registries |  |
| GET | /v2/registries/{registry_name} |  |
| DELETE | /v2/registries/{registry_name} |  |
| GET | /v2/registries/{registry_name}/docker-credentials |  |
| GET | /v2/registries/subscription |  |
| POST | /v2/registries/subscription |  |
| GET | /v2/registries/options |  |
| GET | /v2/registries/{registry_name}/garbage-collection |  |
| POST | /v2/registries/{registry_name}/garbage-collection |  |
| GET | /v2/registries/{registry_name}/garbage-collections |  |
| PUT | /v2/registries/{registry_name}/garbage-collection/{garbage_collection_uuid} |  |
| GET | /v2/registries/{registry_name}/repositoriesV2 |  |
| DELETE | /v2/registries/{registry_name}/repositories/{repository_name} |  |
| GET | /v2/registries/{registry_name}/repositories/{repository_name}/tags |  |
| DELETE | /v2/registries/{registry_name}/repositories/{repository_name}/tags/{repository_tag} |  |
| GET | /v2/registries/{registry_name}/repositories/{repository_name}/digests |  |
| DELETE | /v2/registries/{registry_name}/repositories/{repository_name}/digests/{manifest_digest} |  |
| POST | /v2/registries/validate-name |  |

### registry
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/registry |  |
| POST | /v2/registry |  |
| DELETE | /v2/registry |  |
| GET | /v2/registry/subscription |  |
| POST | /v2/registry/subscription |  |
| GET | /v2/registry/docker-credentials |  |
| POST | /v2/registry/validate-name |  |
| GET | /v2/registry/{registry_name}/repositories |  |
| GET | /v2/registry/{registry_name}/repositoriesV2 |  |
| GET | /v2/registry/{registry_name}/repositories/{repository_name}/tags |  |
| DELETE | /v2/registry/{registry_name}/repositories/{repository_name}/tags/{repository_tag} |  |
| GET | /v2/registry/{registry_name}/repositories/{repository_name}/digests |  |
| DELETE | /v2/registry/{registry_name}/repositories/{repository_name}/digests/{manifest_digest} |  |
| POST | /v2/registry/{registry_name}/garbage-collection |  |
| GET | /v2/registry/{registry_name}/garbage-collection |  |
| GET | /v2/registry/{registry_name}/garbage-collections |  |
| PUT | /v2/registry/{registry_name}/garbage-collection/{garbage_collection_uuid} |  |
| GET | /v2/registry/options |  |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/reports/droplet_neighbors_ids |  |

### reserved_ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/reserved_ips |  |
| POST | /v2/reserved_ips |  |
| GET | /v2/reserved_ips/{reserved_ip} |  |
| DELETE | /v2/reserved_ips/{reserved_ip} |  |
| GET | /v2/reserved_ips/{reserved_ip}/actions |  |
| POST | /v2/reserved_ips/{reserved_ip}/actions |  |
| GET | /v2/reserved_ips/{reserved_ip}/actions/{action_id} |  |

### reserved_ipv6
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/reserved_ipv6 |  |
| POST | /v2/reserved_ipv6 |  |
| GET | /v2/reserved_ipv6/{reserved_ipv6} |  |
| DELETE | /v2/reserved_ipv6/{reserved_ipv6} |  |
| POST | /v2/reserved_ipv6/{reserved_ipv6}/actions |  |

### byoip_prefixes
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/byoip_prefixes |  |
| GET | /v2/byoip_prefixes |  |
| GET | /v2/byoip_prefixes/{byoip_prefix_uuid} |  |
| DELETE | /v2/byoip_prefixes/{byoip_prefix_uuid} |  |
| PATCH | /v2/byoip_prefixes/{byoip_prefix_uuid} |  |
| GET | /v2/byoip_prefixes/{byoip_prefix_uuid}/ips |  |

### sizes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/sizes |  |

### snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/snapshots |  |
| GET | /v2/snapshots/{snapshot_id} |  |
| DELETE | /v2/snapshots/{snapshot_id} |  |

### spaces
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/spaces/keys |  |
| POST | /v2/spaces/keys |  |
| GET | /v2/spaces/keys/{access_key} |  |
| DELETE | /v2/spaces/keys/{access_key} |  |
| PUT | /v2/spaces/keys/{access_key} |  |
| PATCH | /v2/spaces/keys/{access_key} |  |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/tags |  |
| POST | /v2/tags |  |
| GET | /v2/tags/{tag_id} |  |
| DELETE | /v2/tags/{tag_id} |  |
| POST | /v2/tags/{tag_id}/resources |  |
| DELETE | /v2/tags/{tag_id}/resources |  |

### volumes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/volumes |  |
| POST | /v2/volumes |  |
| DELETE | /v2/volumes |  |
| POST | /v2/volumes/actions |  |
| GET | /v2/volumes/snapshots/{snapshot_id} |  |
| DELETE | /v2/volumes/snapshots/{snapshot_id} |  |
| GET | /v2/volumes/{volume_id} |  |
| DELETE | /v2/volumes/{volume_id} |  |
| GET | /v2/volumes/{volume_id}/actions |  |
| POST | /v2/volumes/{volume_id}/actions |  |
| GET | /v2/volumes/{volume_id}/actions/{action_id} |  |
| GET | /v2/volumes/{volume_id}/snapshots |  |
| POST | /v2/volumes/{volume_id}/snapshots |  |

### vpcs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/vpcs |  |
| POST | /v2/vpcs |  |
| GET | /v2/vpcs/{vpc_id} |  |
| PUT | /v2/vpcs/{vpc_id} |  |
| PATCH | /v2/vpcs/{vpc_id} |  |
| DELETE | /v2/vpcs/{vpc_id} |  |
| GET | /v2/vpcs/{vpc_id}/members |  |
| GET | /v2/vpcs/{vpc_id}/peerings |  |
| POST | /v2/vpcs/{vpc_id}/peerings |  |
| PATCH | /v2/vpcs/{vpc_id}/peerings/{vpc_peering_id} |  |

### vpc_peerings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/vpc_peerings |  |
| POST | /v2/vpc_peerings |  |
| GET | /v2/vpc_peerings/{vpc_peering_id} |  |
| PATCH | /v2/vpc_peerings/{vpc_peering_id} |  |
| DELETE | /v2/vpc_peerings/{vpc_peering_id} |  |

### vpc_nat_gateways
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/vpc_nat_gateways |  |
| POST | /v2/vpc_nat_gateways |  |
| GET | /v2/vpc_nat_gateways/{id} |  |
| PUT | /v2/vpc_nat_gateways/{id} |  |
| DELETE | /v2/vpc_nat_gateways/{id} |  |

### uptime
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/uptime/checks |  |
| POST | /v2/uptime/checks |  |
| GET | /v2/uptime/checks/{check_id} |  |
| PUT | /v2/uptime/checks/{check_id} |  |
| DELETE | /v2/uptime/checks/{check_id} |  |
| GET | /v2/uptime/checks/{check_id}/state |  |
| GET | /v2/uptime/checks/{check_id}/alerts |  |
| POST | /v2/uptime/checks/{check_id}/alerts |  |
| GET | /v2/uptime/checks/{check_id}/alerts/{alert_id} |  |
| PUT | /v2/uptime/checks/{check_id}/alerts/{alert_id} |  |
| DELETE | /v2/uptime/checks/{check_id}/alerts/{alert_id} |  |

### gen-ai
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/gen-ai/agents |  |
| POST | /v2/gen-ai/agents |  |
| GET | /v2/gen-ai/agents/{agent_uuid}/api_keys |  |
| POST | /v2/gen-ai/agents/{agent_uuid}/api_keys |  |
| PUT | /v2/gen-ai/agents/{agent_uuid}/api_keys/{api_key_uuid} |  |
| DELETE | /v2/gen-ai/agents/{agent_uuid}/api_keys/{api_key_uuid} |  |
| PUT | /v2/gen-ai/agents/{agent_uuid}/api_keys/{api_key_uuid}/regenerate |  |
| POST | /v2/gen-ai/agents/{agent_uuid}/functions |  |
| PUT | /v2/gen-ai/agents/{agent_uuid}/functions/{function_uuid} |  |
| DELETE | /v2/gen-ai/agents/{agent_uuid}/functions/{function_uuid} |  |
| POST | /v2/gen-ai/agents/{agent_uuid}/knowledge_bases |  |
| POST | /v2/gen-ai/agents/{agent_uuid}/knowledge_bases/{knowledge_base_uuid} |  |
| DELETE | /v2/gen-ai/agents/{agent_uuid}/knowledge_bases/{knowledge_base_uuid} |  |
| POST | /v2/gen-ai/agents/{parent_agent_uuid}/child_agents/{child_agent_uuid} |  |
| PUT | /v2/gen-ai/agents/{parent_agent_uuid}/child_agents/{child_agent_uuid} |  |
| DELETE | /v2/gen-ai/agents/{parent_agent_uuid}/child_agents/{child_agent_uuid} |  |
| GET | /v2/gen-ai/agents/{uuid} |  |
| PUT | /v2/gen-ai/agents/{uuid} |  |
| DELETE | /v2/gen-ai/agents/{uuid} |  |
| GET | /v2/gen-ai/agents/{uuid}/child_agents |  |
| PUT | /v2/gen-ai/agents/{uuid}/deployment_visibility |  |
| GET | /v2/gen-ai/agents/{uuid}/usage |  |
| GET | /v2/gen-ai/agents/{uuid}/versions |  |
| PUT | /v2/gen-ai/agents/{uuid}/versions |  |
| GET | /v2/gen-ai/anthropic/keys |  |
| POST | /v2/gen-ai/anthropic/keys |  |
| GET | /v2/gen-ai/anthropic/keys/{api_key_uuid} |  |
| PUT | /v2/gen-ai/anthropic/keys/{api_key_uuid} |  |
| DELETE | /v2/gen-ai/anthropic/keys/{api_key_uuid} |  |
| GET | /v2/gen-ai/anthropic/keys/{uuid}/agents |  |
| POST | /v2/gen-ai/evaluation_datasets |  |
| POST | /v2/gen-ai/evaluation_datasets/file_upload_presigned_urls |  |
| GET | /v2/gen-ai/evaluation_metrics |  |
| POST | /v2/gen-ai/evaluation_runs |  |
| GET | /v2/gen-ai/evaluation_runs/{evaluation_run_uuid} |  |
| GET | /v2/gen-ai/evaluation_runs/{evaluation_run_uuid}/results |  |
| GET | /v2/gen-ai/evaluation_runs/{evaluation_run_uuid}/results/{prompt_id} |  |
| GET | /v2/gen-ai/evaluation_test_cases |  |
| POST | /v2/gen-ai/evaluation_test_cases |  |
| GET | /v2/gen-ai/evaluation_test_cases/{evaluation_test_case_uuid}/evaluation_runs |  |
| GET | /v2/gen-ai/evaluation_test_cases/{test_case_uuid} |  |
| PUT | /v2/gen-ai/evaluation_test_cases/{test_case_uuid} |  |
| GET | /v2/gen-ai/indexing_jobs |  |
| POST | /v2/gen-ai/indexing_jobs |  |
| GET | /v2/gen-ai/indexing_jobs/{indexing_job_uuid}/data_sources |  |
| GET | /v2/gen-ai/indexing_jobs/{indexing_job_uuid}/details_signed_url |  |
| GET | /v2/gen-ai/indexing_jobs/{uuid} |  |
| PUT | /v2/gen-ai/indexing_jobs/{uuid}/cancel |  |
| GET | /v2/gen-ai/knowledge_bases |  |
| POST | /v2/gen-ai/knowledge_bases |  |
| POST | /v2/gen-ai/knowledge_bases/data_sources/file_upload_presigned_urls |  |
| GET | /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/data_sources |  |
| POST | /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/data_sources |  |
| PUT | /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/data_sources/{data_source_uuid} |  |
| DELETE | /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/data_sources/{data_source_uuid} |  |
| GET | /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/indexing_jobs |  |
| GET | /v2/gen-ai/knowledge_bases/{uuid} |  |
| PUT | /v2/gen-ai/knowledge_bases/{uuid} |  |
| DELETE | /v2/gen-ai/knowledge_bases/{uuid} |  |
| GET | /v2/gen-ai/models |  |
| GET | /v2/gen-ai/models/api_keys |  |
| POST | /v2/gen-ai/models/api_keys |  |
| PUT | /v2/gen-ai/models/api_keys/{api_key_uuid} |  |
| DELETE | /v2/gen-ai/models/api_keys/{api_key_uuid} |  |
| PUT | /v2/gen-ai/models/api_keys/{api_key_uuid}/regenerate |  |
| POST | /v2/gen-ai/oauth2/dropbox/tokens |  |
| GET | /v2/gen-ai/oauth2/url |  |
| GET | /v2/gen-ai/openai/keys |  |
| POST | /v2/gen-ai/openai/keys |  |
| GET | /v2/gen-ai/openai/keys/{api_key_uuid} |  |
| PUT | /v2/gen-ai/openai/keys/{api_key_uuid} |  |
| DELETE | /v2/gen-ai/openai/keys/{api_key_uuid} |  |
| GET | /v2/gen-ai/openai/keys/{uuid}/agents |  |
| GET | /v2/gen-ai/regions |  |
| POST | /v2/gen-ai/scheduled-indexing |  |
| GET | /v2/gen-ai/scheduled-indexing/knowledge-base/{knowledge_base_uuid} |  |
| DELETE | /v2/gen-ai/scheduled-indexing/{uuid} |  |
| GET | /v2/gen-ai/workspaces |  |
| POST | /v2/gen-ai/workspaces |  |
| GET | /v2/gen-ai/workspaces/{workspace_uuid} |  |
| PUT | /v2/gen-ai/workspaces/{workspace_uuid} |  |
| DELETE | /v2/gen-ai/workspaces/{workspace_uuid} |  |
| GET | /v2/gen-ai/workspaces/{workspace_uuid}/agents |  |
| PUT | /v2/gen-ai/workspaces/{workspace_uuid}/agents |  |
| GET | /v2/gen-ai/workspaces/{workspace_uuid}/evaluation_test_cases |  |

## Enhanced Skill Content
## Question Mapping

- "What droplets do I have?" -> GET /v2/droplets
- "How do I create a new droplet?" -> POST /v2/droplets
- "What is my account balance?" -> GET /v2/customers/my/balance
- "Show me my billing history" -> GET /v2/customers/my/billing_history
- "What databases are running?" -> GET /v2/databases
- "How do I add a domain?" -> POST /v2/domains
- "What DNS records exist for my domain?" -> GET /v2/domains/{domain_name}/records
- "How do I deploy an app?" -> POST /v2/apps
- "What Kubernetes clusters do I have?" -> GET /v2/kubernetes/clusters
- "How do I get my kubeconfig?" -> GET /v2/kubernetes/clusters/{cluster_id}/kubeconfig
- "What firewall rules are configured?" -> GET /v2/firewalls/{firewall_id}
- "How do I check CPU metrics for a droplet?" -> GET /v2/monitoring/metrics/droplet/cpu
- "What container images are in my registry?" -> GET /v2/registry/{registry_name}/repositoriesV2
- "How do I create a VPC?" -> POST /v2/vpcs
- "What AI agents have I deployed?" -> GET /v2/gen-ai/agents

## Response Tips

- **List endpoints** (droplets, databases, domains, apps): Paginated via `page` and `per_page` query params; results nested under a plural key (e.g., `{"droplets": [...]}`), with a `meta.total` count and `links.pages` for next/prev.
- **Single resource** (GET by ID/UUID): Object nested under singular key (e.g., `{"droplet": {...}}`); includes `id`, `status`, timestamps, and embedded related objects (e.g., `region`, `image`, `size`).
- **Action endpoints** (POST actions, resize, migrate): Return an `action` object with `id`, `status` (in-progress/completed/errored), and `type`; poll the action ID to track completion.
- **Delete endpoints**: Return `204 No Content` on success with empty body; a `404` means the resource was already gone.
- **Monitoring metrics**: Return Prometheus-style time series with `data.result[]` containing `metric` labels and `values` arrays of `[timestamp, value]` pairs.
- **Billing/invoices**: Amounts are strings representing USD values; `billing_history` entries have a `type` field distinguishing charges, credits, and payments.
- **Gen-AI endpoints**: UUIDs are used throughout; nested relationships (agents -> knowledge_bases -> data_sources) require chained lookups.

## Anomaly Flags

- **Rate limiting**: Surface `ratelimit-remaining` and `ratelimit-reset` headers when remaining drops below 20% of the limit (default 5000/hr).
- **Action failures**: Flag any action response where `status` is `errored` -- include the `type` and resource ID for quick diagnosis.
- **Droplet status anomalies**: Alert when a droplet status is `off`, `archive`, or `new` for longer than expected after a create/power-on action.
- **Database cluster warnings**: Surface when `status` is `migrating`, `forking`, or `maintenance` as these indicate reduced availability.
- **Kubernetes upgrade available**: When `GET .../upgrades` returns non-empty, proactively mention available versions.
- **Registry garbage collection needed**: If repository digest counts are growing significantly, suggest running garbage collection.
- **Deprecated floating IPs**: The `floating_ips` group is legacy; flag usage and recommend migrating to `reserved_ips`.
- **Billing spikes**: When `balance.month_to_date_usage` exceeds the previous month's total, surface a cost alert.
- **Destroy with associated resources**: When deleting droplets or K8s clusters, flag the `destroy_with_associated_resources` endpoints to prevent orphaned volumes, snapshots, or load balancers.
- **SSL certificate expiry**: Surface certificates approaching expiry from the certificates list.

## Playbook

### 1. Provision a Droplet with Networking and Firewall

1. List available regions: `GET /v2/regions`
2. List available sizes: `GET /v2/sizes`
3. List available images: `GET /v2/images`
4. Create a VPC in the target region: `POST /v2/vpcs`
5. Create the droplet inside the VPC: `POST /v2/droplets` (include `vpc_uuid`, `region`, `size`, `image`, and `ssh_keys`)
6. Create a firewall with inbound/outbound rules: `POST /v2/firewalls`
7. Attach the droplet to the firewall: `POST /v2/firewalls/{firewall_id}/droplets`
8. Optionally assign a reserved IP: `POST /v2/reserved_ips` then `POST /v2/reserved_ips/{reserved_ip}/actions` to assign

### 2. Deploy and Monitor an App Platform Application

1. Check available regions: `GET /v2/apps/regions`
2. Validate the app spec: `POST /v2/apps/propose`
3. Create the app: `POST /v2/apps`
4. Monitor deployment: `GET /v2/apps/{app_id}/deployments` (poll until `phase` is `ACTIVE`)
5. View logs if deployment fails: `GET /v2/apps/{app_id}/deployments/{deployment_id}/logs`
6. Check app health: `GET /v2/apps/{app_id}/health`
7. Set up alerts: `GET /v2/apps/{app_id}/alerts` then `POST /v2/apps/{app_id}/alerts/{alert_id}/destinations`
8. If issues arise, rollback: `POST /v2/apps/{app_id}/rollback/validate` then `POST /v2/apps/{app_id}/rollback`

### 3. Set Up a Managed Database with Replicas and Users

1. Check available database engines and versions: `GET /v2/databases/options`
2. Create the database cluster: `POST /v2/databases`
3. Poll cluster status until `online`: `GET /v2/databases/{database_cluster_uuid}`
4. Configure firewall trusted sources: `PUT /v2/databases/{database_cluster_uuid}/firewall`
5. Create application databases: `POST /v2/databases/{database_cluster_uuid}/dbs`
6. Create users with appropriate roles: `POST /v2/databases/{database_cluster_uuid}/users`
7. Add a read replica: `POST /v2/databases/{database_cluster_uuid}/replicas`
8. Set maintenance window: `PUT /v2/databases/{database_cluster_uuid}/maintenance`
9. Optionally configure connection pools (PostgreSQL): `POST /v2/databases/{database_cluster_uuid}/pools`

### 4. Set Up Domain with DNS Records and Uptime Monitoring

1. Add the domain: `POST /v2/domains`
2. Create A record pointing to your droplet/load balancer IP: `POST /v2/domains/{domain_name}/records`
3. Add any CNAME, MX, or TXT records needed: `POST /v2/domains/{domain_name}/records` (repeat)
4. Create an uptime check for the domain: `POST /v2/uptime/checks`
5. Configure an alert for downtime: `POST /v2/uptime/checks/{check_id}/alerts`
6. Verify check state: `GET /v2/uptime/checks/{check_id}/state`

### 5. Build and Deploy a Gen-AI Agent with Knowledge Base

1. Create a workspace: `POST /v2/gen-ai/workspaces`
2. Create a knowledge base: `POST /v2/gen-ai/knowledge_bases`
3. Get presigned URLs for file uploads: `POST /v2/gen-ai/knowledge_bases/data_sources/file_upload_presigned_urls`
4. Add data sources to the knowledge base: `POST /v2/gen-ai/knowledge_bases/{knowledge_base_uuid}/data_sources`
5. Trigger an indexing job: `POST /v2/gen-ai/indexing_jobs`
6. Poll indexing status until complete: `GET /v2/gen-ai/indexing_jobs/{uuid}`
7. Create the agent: `POST /v2/gen-ai/agents`
8. Attach the knowledge base to the agent: `POST /v2/gen-ai/agents/{agent_uuid}/knowledge_bases`
9. Generate an API key for the agent: `POST /v2/gen-ai/agents/{agent_uuid}/api_keys`
10. Set deployment visibility: `PUT /v2/gen-ai/agents/{uuid}/deployment_visibility`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
