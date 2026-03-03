---
name: digitalocean-api
description: "DigitalOcean API skill. Use when working with DigitalOcean for 1-clicks, account, actions. Covers 558 endpoints."
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

558 endpoints across 39 groups. See references/api-spec.lap for full details.

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
| GET | /v2/monitoring/metrics/database/mysql/cpu_usage |  |
| GET | /v2/monitoring/metrics/database/mysql/load |  |
| GET | /v2/monitoring/metrics/database/mysql/memory_usage |  |
| GET | /v2/monitoring/metrics/database/mysql/disk_usage |  |
| GET | /v2/monitoring/metrics/database/mysql/threads_connected |  |
| GET | /v2/monitoring/metrics/database/mysql/threads_created_rate |  |
| GET | /v2/monitoring/metrics/database/mysql/threads_active |  |
| GET | /v2/monitoring/metrics/database/mysql/index_vs_sequential_reads |  |
| GET | /v2/monitoring/metrics/database/mysql/op_rates |  |
| GET | /v2/monitoring/metrics/database/mysql/schema_throughput |  |
| GET | /v2/monitoring/metrics/database/mysql/schema_latency |  |
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
| POST | /v2/gen-ai/agents/{agent_uuid}/guardrails |  |
| DELETE | /v2/gen-ai/agents/{agent_uuid}/guardrails/{guardrail_uuid} |  |
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

- "What droplets do I have running?" -> GET /v2/droplets
- "How do I create a new droplet?" -> POST /v2/droplets
- "What's my current account balance?" -> GET /v2/customers/my/balance
- "Show me my billing history" -> GET /v2/customers/my/billing_history
- "How do I add a domain and set up DNS records?" -> POST /v2/domains, then POST /v2/domains/{domain_name}/records
- "What Kubernetes clusters exist in my account?" -> GET /v2/kubernetes/clusters
- "How do I scale a database cluster?" -> PUT /v2/databases/{database_cluster_uuid}/resize
- "What firewall rules are applied to my droplet?" -> GET /v2/droplets/{droplet_id}/firewalls
- "How do I deploy a new version of my app?" -> POST /v2/apps/{app_id}/deployments
- "Show me CPU and memory metrics for a droplet" -> GET /v2/monitoring/metrics/droplet/cpu, GET /v2/monitoring/metrics/droplet/memory_available
- "How do I set up an uptime check with alerts?" -> POST /v2/uptime/checks, then POST /v2/uptime/checks/{check_id}/alerts
- "What container images are in my registry?" -> GET /v2/registry/{registry_name}/repositoriesV2
- "How do I rollback an app deployment?" -> POST /v2/apps/{app_id}/rollback, then POST /v2/apps/{app_id}/rollback/commit
- "How do I safely delete a droplet and all its resources?" -> GET /v2/droplets/{droplet_id}/destroy_with_associated_resources, then DELETE /v2/droplets/{droplet_id}/destroy_with_associated_resources/selective
- "How do I create a Gen AI agent with a knowledge base?" -> POST /v2/gen-ai/agents, POST /v2/gen-ai/knowledge_bases, then POST /v2/gen-ai/agents/{agent_uuid}/knowledge_bases

## Response Tips

- **Droplets, Domains, Volumes, and other list endpoints**: Responses are paginated; look for `links.pages.next` and `meta.total` to iterate. Default page size is 20.
- **Actions** (droplet actions, image actions, floating IP actions): Return an `action` object with `status` field -- poll until `status` changes from `in-progress` to `completed` or `errored`.
- **Databases**: Responses nest cluster details under `database`; replicas, users, pools, and topics are under their own plural keys. Config is engine-specific.
- **Apps**: Deployments return nested `deployment.services[].spec` and `deployment.phase` -- watch for `ACTIVE`, `DEPLOYING`, `ERROR` phases.
- **Monitoring metrics**: Returns Prometheus-style time-series data with `data.result[].values` arrays of `[timestamp, value]` pairs. Specify `start`, `end`, and `host_id` query params.
- **Billing/Invoices**: Balance returns `month_to_date_usage`, `account_balance`, and `generated_at`. Invoice CSV/PDF endpoints return file content, not JSON.
- **Kubernetes**: Kubeconfig endpoint returns YAML, not JSON. Credentials include `token` and `certificate_authority_data` for direct cluster access.
- **Gen AI**: Agent responses include nested `functions`, `guardrails`, `knowledge_bases`, and `child_agents` arrays. Evaluation run results paginate by `prompt_id`.

## Anomaly Flags

- **Rate limiting**: DigitalOcean returns `429 Too Many Requests` with `Retry-After` and `RateLimit-Remaining` headers. Surface a warning when `RateLimit-Remaining` drops below 50.
- **Action stuck in-progress**: If a droplet/volume/image action stays `in-progress` for more than 10 minutes, flag it -- something may need manual intervention.
- **Unexpected 5xx on create/delete**: Transient 500/503 errors on provisioning indicate platform issues. Surface and recommend retry with backoff rather than re-creating resources.
- **Droplet destroy with associated resources**: The `dangerous` variant permanently deletes all attached volumes, snapshots, and volume snapshots. Always flag when this path is chosen over `selective`.
- **Database maintenance pending**: If `maintenance_window.pending` is true in database cluster config, surface it -- an unscheduled restart may occur.
- **Kubernetes upgrade available**: When GET /v2/kubernetes/clusters/{id}/upgrades returns non-empty results, proactively notify that a newer k8s version is available.
- **Registry garbage collection**: If repository storage is growing but no garbage collection has run (GET garbage-collections returns empty or stale dates), recommend triggering one.
- **App deployment failures**: When `deployment.phase` is `ERROR`, surface the component-level logs endpoint to help diagnose the issue.
- **Invoice overdue or high balance**: If `customers/my/balance` shows `account_balance` significantly negative (credits exhausted), flag potential service disruption risk.
- **Deprecated floating_ips**: The `floating_ips` group is superseded by `reserved_ips`. Flag usage and recommend migration.

## Playbook

### 1. Provision a Droplet with Firewall and Monitoring

1. GET /v2/regions -- list available regions, pick one
2. GET /v2/sizes -- list available sizes, pick one matching your workload
3. GET /v2/images?type=distribution -- find the OS image slug
4. POST /v2/droplets -- create the droplet with chosen region, size, image, and SSH key IDs
5. Poll GET /v2/actions/{action_id} until `status` is `completed`
6. POST /v2/firewalls -- create a firewall with inbound rules (e.g., SSH 22, HTTP 80, HTTPS 443)
7. POST /v2/firewalls/{firewall_id}/droplets -- attach the new droplet to the firewall
8. POST /v2/monitoring/alerts -- create CPU/memory alerts targeting the droplet
9. Verify with GET /v2/droplets/{droplet_id} to confirm networking and status

### 2. Deploy and Manage an App Platform Application

1. GET /v2/apps/regions -- check available App Platform regions
2. POST /v2/apps/propose -- validate your app spec before deploying
3. POST /v2/apps -- create the app with the validated spec
4. GET /v2/apps/{app_id}/deployments -- monitor the initial deployment
5. GET /v2/apps/{app_id}/components/{component_name}/logs -- check build/runtime logs if issues arise
6. To update: PUT /v2/apps/{id} with modified spec, which triggers a new deployment
7. If a deployment fails: POST /v2/apps/{app_id}/rollback to revert, then POST /v2/apps/{app_id}/rollback/commit to confirm
8. GET /v2/apps/{app_id}/metrics/bandwidth_daily -- monitor bandwidth usage

### 3. Set Up a Managed Database with Replicas and Connection Pooling

1. GET /v2/databases/options -- check available engines, versions, regions, and sizes
2. POST /v2/databases -- create the cluster (specify engine, version, size, region, num_nodes)
3. Poll GET /v2/databases/{uuid} until `status` is `online`
4. PATCH /v2/databases/{uuid}/config -- tune engine-specific settings
5. PUT /v2/databases/{uuid}/firewall -- restrict access to specific droplet or tag sources
6. POST /v2/databases/{uuid}/replicas -- add a read replica
7. POST /v2/databases/{uuid}/pools -- create a connection pool (PostgreSQL only)
8. POST /v2/databases/{uuid}/users -- create application-specific database users
9. GET /v2/databases/{uuid}/ca -- download the CA certificate for TLS connections

### 4. Set Up a Kubernetes Cluster with Container Registry

1. GET /v2/kubernetes/options -- check available k8s versions and node sizes
2. POST /v2/kubernetes/clusters -- create cluster with desired version, region, and node pools
3. Poll GET /v2/kubernetes/clusters/{id} until `status.state` is `running`
4. GET /v2/kubernetes/clusters/{id}/kubeconfig -- download kubeconfig for kubectl access
5. POST /v2/registry -- create a container registry (if not already created)
6. POST /v2/kubernetes/registry -- integrate the registry with the cluster for image pulling
7. POST /v2/kubernetes/clusters/{id}/node_pools -- add specialized node pools (e.g., GPU, high-memory)
8. POST /v2/kubernetes/clusters/{id}/clusterlint -- run cluster lint to identify configuration issues
9. GET /v2/kubernetes/clusters/{id}/upgrades -- check for available version upgrades

### 5. Build a Gen AI Agent with Knowledge Base and Evaluation

1. POST /v2/gen-ai/knowledge_bases -- create a knowledge base
2. POST /v2/gen-ai/knowledge_bases/data_sources/file_upload_presigned_urls -- get upload URLs for documents
3. POST /v2/gen-ai/knowledge_bases/{kb_uuid}/data_sources -- register uploaded data sources
4. POST /v2/gen-ai/indexing_jobs -- trigger indexing of the knowledge base
5. Poll GET /v2/gen-ai/indexing_jobs/{uuid} until indexing completes
6. POST /v2/gen-ai/agents -- create the AI agent with model and system prompt
7. POST /v2/gen-ai/agents/{agent_uuid}/knowledge_bases -- attach the knowledge base
8. POST /v2/gen-ai/agents/{agent_uuid}/guardrails -- add safety guardrails
9. POST /v2/gen-ai/agents/{agent_uuid}/api_keys -- generate an API key for the agent endpoint
10. POST /v2/gen-ai/evaluation_test_cases -- create test cases for quality assessment
11. POST /v2/gen-ai/evaluation_runs -- run evaluation and review results via GET /v2/gen-ai/evaluation_runs/{uuid}/results


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
