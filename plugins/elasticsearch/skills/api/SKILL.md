---
name: elasticsearch-request-response-specification
description: "Elasticsearch Request & Response Specification API skill. Use when working with Elasticsearch Request & Response Specification for _async_search, {index}, _bulk. Covers 823 endpoints."
version: 1.0.0
generator: lapsh
---

# Elasticsearch Request & Response Specification

## Auth
ApiKey ids in path

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /_cat/aliases -- verify access
3. POST /_async_search -- create first _async_search

## Endpoints

823 endpoints across 79 groups. See references/api-spec.lap for full details.

### _async_search
| Method | Path | Description |
|--------|------|-------------|
| GET | /_async_search/{id} | Get async search results |
| DELETE | /_async_search/{id} | Delete an async search |
| GET | /_async_search/status/{id} | Get the async search status |
| POST | /_async_search | Run an async search |

### {index}
| Method | Path | Description |
|--------|------|-------------|
| POST | /{index}/_async_search | Run an async search |
| PUT | /{index}/_bulk | Bulk index or delete documents |
| POST | /{index}/_bulk | Bulk index or delete documents |
| PUT | /{index}/_ccr/follow | Create a follower |
| GET | /{index}/_ccr/info | Get follower information |
| GET | /{index}/_ccr/stats | Get follower stats |
| POST | /{index}/_ccr/forget_follower | Forget a follower |
| POST | /{index}/_ccr/pause_follow | Pause a follower |
| POST | /{index}/_ccr/resume_follow | Resume a follower |
| POST | /{index}/_ccr/unfollow | Unfollow an index |
| GET | /{index}/_count | Count search results |
| POST | /{index}/_count | Count search results |
| PUT | /{index}/_create/{id} | Create a new document in the index |
| POST | /{index}/_create/{id} | Create a new document in the index |
| GET | /{index}/_doc/{id} | Get a document by its ID |
| PUT | /{index}/_doc/{id} | Create or update a document in an index |
| POST | /{index}/_doc/{id} | Create or update a document in an index |
| DELETE | /{index}/_doc/{id} | Delete a document |
| HEAD | /{index}/_doc/{id} | Check a document |
| POST | /{index}/_delete_by_query | Delete documents |
| GET | /{index}/_eql/search | Get EQL search results |
| POST | /{index}/_eql/search | Get EQL search results |
| GET | /{index}/_source/{id} | Get a document's source |
| HEAD | /{index}/_source/{id} | Check for a document source |
| GET | /{index}/_explain/{id} | Explain a document match result |
| POST | /{index}/_explain/{id} | Explain a document match result |
| GET | /{index}/_field_caps | Get the field capabilities |
| POST | /{index}/_field_caps | Get the field capabilities |
| GET | /{index}/_fleet/global_checkpoints | Get global checkpoints |
| GET | /{index}/_fleet/_fleet_msearch | Run multiple Fleet searches |
| POST | /{index}/_fleet/_fleet_msearch | Run multiple Fleet searches |
| GET | /{index}/_fleet/_fleet_search | Run a Fleet search |
| POST | /{index}/_fleet/_fleet_search | Run a Fleet search |
| GET | /{index}/_graph/explore | Explore graph analytics |
| POST | /{index}/_graph/explore | Explore graph analytics |
| GET | /{index}/_ilm/explain | Explain the lifecycle state |
| POST | /{index}/_ilm/remove | Remove policies from an index |
| POST | /{index}/_ilm/retry | Retry a policy |
| POST | /{index}/_doc | Create or update a document in an index |
| PUT | /{index}/_block/{block} | Add an index block |
| DELETE | /{index}/_block/{block} | Remove an index block |
| GET | /{index}/_analyze | Get tokens from text analysis |
| POST | /{index}/_analyze | Get tokens from text analysis |
| POST | /{index}/_cache/clear | Clear the cache |
| PUT | /{index}/_clone/{target} | Clone an index |
| POST | /{index}/_clone/{target} | Clone an index |
| POST | /{index}/_close | Close an index |
| GET | /{index} | Get index information |
| PUT | /{index} | Create an index |
| DELETE | /{index} | Delete indices |
| HEAD | /{index} | Check indices |
| GET | /{index}/_alias/{name} | Get aliases |
| PUT | /{index}/_alias/{name} | Create or update an alias |
| POST | /{index}/_alias/{name} | Create or update an alias |
| DELETE | /{index}/_alias/{name} | Delete an alias |
| HEAD | /{index}/_alias/{name} | Check aliases |
| PUT | /{index}/_aliases/{name} | Create or update an alias |
| POST | /{index}/_aliases/{name} | Create or update an alias |
| DELETE | /{index}/_aliases/{name} | Delete an alias |
| POST | /{index}/_disk_usage | Analyze the index disk usage |
| POST | /{index}/_downsample/{target_index} | Downsample an index |
| GET | /{index}/_lifecycle/explain | Get the status for a data stream lifecycle |
| GET | /{index}/_field_usage_stats | Get field usage stats |
| GET | /{index}/_flush | Flush data streams or indices |
| POST | /{index}/_flush | Flush data streams or indices |
| POST | /{index}/_forcemerge | Force a merge |
| GET | /{index}/_alias | Get aliases |
| GET | /{index}/_mapping/field/{fields} | Get mapping definitions |
| GET | /{index}/_mapping | Get mapping definitions |
| PUT | /{index}/_mapping | Update field mappings |
| POST | /{index}/_mapping | Update field mappings |
| GET | /{index}/_settings | Get index settings |
| PUT | /{index}/_settings | Update index settings |
| GET | /{index}/_settings/{name} | Get index settings |
| POST | /{index}/_open | Open a closed index |
| GET | /{index}/_recovery | Get index recovery information |
| GET | /{index}/_refresh | Refresh an index |
| POST | /{index}/_refresh | Refresh an index |
| GET | /{index}/_reload_search_analyzers | Reload search analyzers |
| POST | /{index}/_reload_search_analyzers | Reload search analyzers |
| GET | /{index}/_segments | Get index segments |
| GET | /{index}/_shard_stores | Get index shard stores |
| PUT | /{index}/_shrink/{target} | Shrink an index |
| POST | /{index}/_shrink/{target} | Shrink an index |
| PUT | /{index}/_split/{target} | Split an index |
| POST | /{index}/_split/{target} | Split an index |
| GET | /{index}/_stats | Get index statistics |
| GET | /{index}/_stats/{metric} | Get index statistics |
| GET | /{index}/_validate/query | Validate a query |
| POST | /{index}/_validate/query | Validate a query |
| GET | /{index}/_mget | Get multiple documents |
| POST | /{index}/_mget | Get multiple documents |
| GET | /{index}/_migration/deprecations | Get deprecation information |
| GET | /{index}/_msearch | Run multiple searches |
| POST | /{index}/_msearch | Run multiple searches |
| GET | /{index}/_msearch/template | Run multiple templated searches |
| POST | /{index}/_msearch/template | Run multiple templated searches |
| GET | /{index}/_mtermvectors | Get multiple term vectors |
| POST | /{index}/_mtermvectors | Get multiple term vectors |
| POST | /{index}/_pit | Open a point in time |
| GET | /{index}/_rank_eval | Evaluate ranked search results |
| POST | /{index}/_rank_eval | Evaluate ranked search results |
| GET | /{index}/_rollup/data | Get the rollup index capabilities |
| GET | /{index}/_rollup_search | Search rolled-up data |
| POST | /{index}/_rollup_search | Search rolled-up data |
| GET | /{index}/_search | Run a search |
| POST | /{index}/_search | Run a search |
| GET | /{index}/_mvt/{field}/{zoom}/{x}/{y} | Search a vector tile |
| POST | /{index}/_mvt/{field}/{zoom}/{x}/{y} | Search a vector tile |
| GET | /{index}/_search_shards | Get the search shards |
| POST | /{index}/_search_shards | Get the search shards |
| GET | /{index}/_search/template | Run a search with a search template |
| POST | /{index}/_search/template | Run a search with a search template |
| POST | /{index}/_searchable_snapshots/cache/clear | Clear the cache |
| GET | /{index}/_searchable_snapshots/stats | Get searchable snapshot statistics |
| GET | /{index}/_terms_enum | Get terms in an index |
| POST | /{index}/_terms_enum | Get terms in an index |
| GET | /{index}/_termvectors/{id} | Get term vector information |
| POST | /{index}/_termvectors/{id} | Get term vector information |
| GET | /{index}/_termvectors | Get term vector information |
| POST | /{index}/_termvectors | Get term vector information |
| POST | /{index}/_update/{id} | Update a document |
| POST | /{index}/_update_by_query | Update documents |

### _bulk
| Method | Path | Description |
|--------|------|-------------|
| PUT | /_bulk | Bulk index or delete documents |
| POST | /_bulk | Bulk index or delete documents |

### _cat
| Method | Path | Description |
|--------|------|-------------|
| GET | /_cat/aliases | Get aliases |
| GET | /_cat/aliases/{name} | Get aliases |
| GET | /_cat/allocation | Get shard allocation information |
| GET | /_cat/allocation/{node_id} | Get shard allocation information |
| GET | /_cat/circuit_breaker | Get circuit breakers statistics |
| GET | /_cat/circuit_breaker/{circuit_breaker_patterns} | Get circuit breakers statistics |
| GET | /_cat/component_templates | Get component templates |
| GET | /_cat/component_templates/{name} | Get component templates |
| GET | /_cat/count | Get a document count |
| POST | /_cat/count | Get a document count |
| GET | /_cat/count/{index} | Get a document count |
| POST | /_cat/count/{index} | Get a document count |
| GET | /_cat/fielddata | Get field data cache information |
| GET | /_cat/fielddata/{fields} | Get field data cache information |
| GET | /_cat/health | Get the cluster health status |
| GET | /_cat | Get CAT help |
| GET | /_cat/indices | Get index information |
| GET | /_cat/indices/{index} | Get index information |
| GET | /_cat/master | Get master node information |
| GET | /_cat/ml/data_frame/analytics | Get data frame analytics jobs |
| GET | /_cat/ml/data_frame/analytics/{id} | Get data frame analytics jobs |
| GET | /_cat/ml/datafeeds | Get datafeeds |
| GET | /_cat/ml/datafeeds/{datafeed_id} | Get datafeeds |
| GET | /_cat/ml/anomaly_detectors | Get anomaly detection jobs |
| GET | /_cat/ml/anomaly_detectors/{job_id} | Get anomaly detection jobs |
| GET | /_cat/ml/trained_models | Get trained models |
| GET | /_cat/ml/trained_models/{model_id} | Get trained models |
| GET | /_cat/nodeattrs | Get node attribute information |
| GET | /_cat/nodes | Get node information |
| GET | /_cat/pending_tasks | Get pending task information |
| GET | /_cat/plugins | Get plugin information |
| GET | /_cat/recovery | Get shard recovery information |
| GET | /_cat/recovery/{index} | Get shard recovery information |
| GET | /_cat/repositories | Get snapshot repository information |
| GET | /_cat/segments | Get segment information |
| GET | /_cat/segments/{index} | Get segment information |
| GET | /_cat/shards | Get shard information |
| GET | /_cat/shards/{index} | Get shard information |
| GET | /_cat/snapshots | Get snapshot information |
| GET | /_cat/snapshots/{repository} | Get snapshot information |
| GET | /_cat/tasks | Get task information |
| GET | /_cat/templates | Get index template information |
| GET | /_cat/templates/{name} | Get index template information |
| GET | /_cat/thread_pool | Get thread pool statistics |
| GET | /_cat/thread_pool/{thread_pool_patterns} | Get thread pool statistics |
| GET | /_cat/transforms | Get transform information |
| GET | /_cat/transforms/{transform_id} | Get transform information |

### _ccr
| Method | Path | Description |
|--------|------|-------------|
| GET | /_ccr/auto_follow/{name} | Get auto-follow patterns |
| PUT | /_ccr/auto_follow/{name} | Create or update auto-follow patterns |
| DELETE | /_ccr/auto_follow/{name} | Delete auto-follow patterns |
| GET | /_ccr/auto_follow | Get auto-follow patterns |
| POST | /_ccr/auto_follow/{name}/pause | Pause an auto-follow pattern |
| POST | /_ccr/auto_follow/{name}/resume | Resume an auto-follow pattern |
| GET | /_ccr/stats | Get cross-cluster replication stats |

### _search
| Method | Path | Description |
|--------|------|-------------|
| GET | /_search/scroll | Run a scrolling search |
| POST | /_search/scroll | Run a scrolling search |
| DELETE | /_search/scroll | Clear a scrolling search |
| GET | /_search/scroll/{scroll_id} | Run a scrolling search |
| POST | /_search/scroll/{scroll_id} | Run a scrolling search |
| DELETE | /_search/scroll/{scroll_id} | Clear a scrolling search |
| GET | /_search | Run a search |
| POST | /_search | Run a search |
| GET | /_search/template | Run a search with a search template |
| POST | /_search/template | Run a search with a search template |

### _pit
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /_pit | Close a point in time |

### _cluster
| Method | Path | Description |
|--------|------|-------------|
| GET | /_cluster/allocation/explain | Explain the shard allocations |
| POST | /_cluster/allocation/explain | Explain the shard allocations |
| POST | /_cluster/voting_config_exclusions | Update voting configuration exclusions |
| DELETE | /_cluster/voting_config_exclusions | Clear cluster voting config exclusions |
| GET | /_cluster/settings | Get cluster-wide settings |
| PUT | /_cluster/settings | Update the cluster settings |
| GET | /_cluster/health | Get the cluster health status |
| GET | /_cluster/health/{index} | Get the cluster health status |
| GET | /_cluster/pending_tasks | Get the pending cluster tasks |
| POST | /_cluster/reroute | Reroute the cluster |
| GET | /_cluster/state | Get the cluster state |
| GET | /_cluster/state/{metric} | Get the cluster state |
| GET | /_cluster/state/{metric}/{index} | Get the cluster state |
| GET | /_cluster/stats | Get cluster statistics |
| GET | /_cluster/stats/nodes/{node_id} | Get cluster statistics |

### _component_template
| Method | Path | Description |
|--------|------|-------------|
| GET | /_component_template/{name} | Get component templates |
| PUT | /_component_template/{name} | Create or update a component template |
| POST | /_component_template/{name} | Create or update a component template |
| DELETE | /_component_template/{name} | Delete component templates |
| HEAD | /_component_template/{name} | Check component templates |
| GET | /_component_template | Get component templates |

### _info
| Method | Path | Description |
|--------|------|-------------|
| GET | /_info/{target} | Get cluster info |

### _remote
| Method | Path | Description |
|--------|------|-------------|
| GET | /_remote/info | Get remote cluster information |

### _connector
| Method | Path | Description |
|--------|------|-------------|
| PUT | /_connector/{connector_id}/_check_in | Check in a connector |
| GET | /_connector/{connector_id} | Get a connector |
| PUT | /_connector/{connector_id} | Create or update a connector |
| DELETE | /_connector/{connector_id} | Delete a connector |
| GET | /_connector | Get all connectors |
| PUT | /_connector | Create or update a connector |
| POST | /_connector | Create a connector |
| PUT | /_connector/_sync_job/{connector_sync_job_id}/_cancel | Cancel a connector sync job |
| PUT | /_connector/_sync_job/{connector_sync_job_id}/_check_in | Check in a connector sync job |
| PUT | /_connector/_sync_job/{connector_sync_job_id}/_claim | Claim a connector sync job |
| GET | /_connector/_sync_job/{connector_sync_job_id} | Get a connector sync job |
| DELETE | /_connector/_sync_job/{connector_sync_job_id} | Delete a connector sync job |
| PUT | /_connector/_sync_job/{connector_sync_job_id}/_error | Set a connector sync job error |
| GET | /_connector/_sync_job | Get all connector sync jobs |
| POST | /_connector/_sync_job | Create a connector sync job |
| PUT | /_connector/_sync_job/{connector_sync_job_id}/_stats | Set the connector sync job stats |
| PUT | /_connector/{connector_id}/_filtering/_activate | Activate the connector draft filter |
| PUT | /_connector/{connector_id}/_api_key_id | Update the connector API key ID |
| PUT | /_connector/{connector_id}/_configuration | Update the connector configuration |
| PUT | /_connector/{connector_id}/_error | Update the connector error field |
| PUT | /_connector/{connector_id}/_features | Update the connector features |
| PUT | /_connector/{connector_id}/_filtering | Update the connector filtering |
| PUT | /_connector/{connector_id}/_filtering/_validation | Update the connector draft filtering validation |
| PUT | /_connector/{connector_id}/_index_name | Update the connector index name |
| PUT | /_connector/{connector_id}/_name | Update the connector name and description |
| PUT | /_connector/{connector_id}/_native | Update the connector is_native flag |
| PUT | /_connector/{connector_id}/_pipeline | Update the connector pipeline |
| PUT | /_connector/{connector_id}/_scheduling | Update the connector scheduling |
| PUT | /_connector/{connector_id}/_service_type | Update the connector service type |
| PUT | /_connector/{connector_id}/_status | Update the connector status |

### _count
| Method | Path | Description |
|--------|------|-------------|
| GET | /_count | Count search results |
| POST | /_count | Count search results |

### _dangling
| Method | Path | Description |
|--------|------|-------------|
| POST | /_dangling/{index_uuid} | Import a dangling index |
| DELETE | /_dangling/{index_uuid} | Delete a dangling index |
| GET | /_dangling | Get the dangling indices |

### _delete_by_query
| Method | Path | Description |
|--------|------|-------------|
| POST | /_delete_by_query/{task_id}/_rethrottle | Throttle a delete by query operation |

### _scripts
| Method | Path | Description |
|--------|------|-------------|
| GET | /_scripts/{id} | Get a script or search template |
| PUT | /_scripts/{id} | Create or update a script or search template |
| POST | /_scripts/{id} | Create or update a script or search template |
| DELETE | /_scripts/{id} | Delete a script or search template |
| PUT | /_scripts/{id}/{context} | Create or update a script or search template |
| POST | /_scripts/{id}/{context} | Create or update a script or search template |
| GET | /_scripts/painless/_execute | Run a script |
| POST | /_scripts/painless/_execute | Run a script |

### _enrich
| Method | Path | Description |
|--------|------|-------------|
| GET | /_enrich/policy/{name} | Get an enrich policy |
| PUT | /_enrich/policy/{name} | Create an enrich policy |
| DELETE | /_enrich/policy/{name} | Delete an enrich policy |
| PUT | /_enrich/policy/{name}/_execute | Run an enrich policy |
| GET | /_enrich/policy | Get an enrich policy |
| GET | /_enrich/_stats | Get enrich stats |

### _eql
| Method | Path | Description |
|--------|------|-------------|
| GET | /_eql/search/{id} | Get async EQL search results |
| DELETE | /_eql/search/{id} | Delete an async EQL search |
| GET | /_eql/search/status/{id} | Get the async EQL status |

### _query
| Method | Path | Description |
|--------|------|-------------|
| POST | /_query/async | Run an async ES|QL query |
| GET | /_query/async/{id} | Get async ES|QL query results |
| DELETE | /_query/async/{id} | Delete an async ES|QL query |
| POST | /_query/async/{id}/stop | Stop async ES|QL query |
| GET | /_query/queries/{id} | Get a specific running ES|QL query information |
| GET | /_query/queries | Get running ES|QL queries information |
| POST | /_query | Run an ES|QL query |

### _features
| Method | Path | Description |
|--------|------|-------------|
| GET | /_features | Get the features |
| POST | /_features/_reset | Reset the features |

### _field_caps
| Method | Path | Description |
|--------|------|-------------|
| GET | /_field_caps | Get the field capabilities |
| POST | /_field_caps | Get the field capabilities |

### _fleet
| Method | Path | Description |
|--------|------|-------------|
| GET | /_fleet/_fleet_msearch | Run multiple Fleet searches |
| POST | /_fleet/_fleet_msearch | Run multiple Fleet searches |

### _script_context
| Method | Path | Description |
|--------|------|-------------|
| GET | /_script_context | Get script contexts |

### _script_language
| Method | Path | Description |
|--------|------|-------------|
| GET | /_script_language | Get script languages |

### _health_report
| Method | Path | Description |
|--------|------|-------------|
| GET | /_health_report | Get the cluster health |
| GET | /_health_report/{feature} | Get the cluster health |

### _ilm
| Method | Path | Description |
|--------|------|-------------|
| GET | /_ilm/policy/{policy} | Get lifecycle policies |
| PUT | /_ilm/policy/{policy} | Create or update a lifecycle policy |
| DELETE | /_ilm/policy/{policy} | Delete a lifecycle policy |
| GET | /_ilm/policy | Get lifecycle policies |
| GET | /_ilm/status | Get the ILM status |
| POST | /_ilm/migrate_to_data_tiers | Migrate to data tiers routing |
| POST | /_ilm/move/{index} | Move to a lifecycle step |
| POST | /_ilm/start | Start the ILM plugin |
| POST | /_ilm/stop | Stop the ILM plugin |

### _analyze
| Method | Path | Description |
|--------|------|-------------|
| GET | /_analyze | Get tokens from text analysis |
| POST | /_analyze | Get tokens from text analysis |

### _migration
| Method | Path | Description |
|--------|------|-------------|
| POST | /_migration/reindex/{index}/_cancel | Cancel a migration reindex operation |
| GET | /_migration/reindex/{index}/_status | Get the migration reindexing status |
| POST | /_migration/reindex | Reindex legacy backing indices |
| GET | /_migration/deprecations | Get deprecation information |
| GET | /_migration/system_features | Get feature migration information |
| POST | /_migration/system_features | Start the feature migration |

### _cache
| Method | Path | Description |
|--------|------|-------------|
| POST | /_cache/clear | Clear the cache |

### _data_stream
| Method | Path | Description |
|--------|------|-------------|
| GET | /_data_stream/{name} | Get data streams |
| PUT | /_data_stream/{name} | Create a data stream |
| DELETE | /_data_stream/{name} | Delete data streams |
| GET | /_data_stream/_stats | Get data stream stats |
| GET | /_data_stream/{name}/_stats | Get data stream stats |
| GET | /_data_stream/{name}/_lifecycle | Get data stream lifecycles |
| PUT | /_data_stream/{name}/_lifecycle | Update data stream lifecycles |
| DELETE | /_data_stream/{name}/_lifecycle | Delete data stream lifecycles |
| GET | /_data_stream/{name}/_options | Get data stream options |
| PUT | /_data_stream/{name}/_options | Update data stream options |
| DELETE | /_data_stream/{name}/_options | Delete data stream options |
| GET | /_data_stream | Get data streams |
| GET | /_data_stream/{name}/_mappings | Get data stream mappings |
| PUT | /_data_stream/{name}/_mappings | Update data stream mappings |
| GET | /_data_stream/{name}/_settings | Get data stream settings |
| PUT | /_data_stream/{name}/_settings | Update data stream settings |
| POST | /_data_stream/_migrate/{name} | Convert an index alias to a data stream |
| POST | /_data_stream/_modify | Update data streams |
| POST | /_data_stream/_promote/{name} | Promote a data stream |

### _create_from
| Method | Path | Description |
|--------|------|-------------|
| PUT | /_create_from/{source}/{dest} | Create an index from a source index |
| POST | /_create_from/{source}/{dest} | Create an index from a source index |

### _index_template
| Method | Path | Description |
|--------|------|-------------|
| GET | /_index_template/{name} | Get index templates |
| PUT | /_index_template/{name} | Create or update an index template |
| POST | /_index_template/{name} | Create or update an index template |
| DELETE | /_index_template/{name} | Delete an index template |
| HEAD | /_index_template/{name} | Check index templates |
| GET | /_index_template | Get index templates |
| POST | /_index_template/_simulate_index/{name} | Simulate an index |
| POST | /_index_template/_simulate | Simulate an index template |
| POST | /_index_template/_simulate/{name} | Simulate an index template |

### _template
| Method | Path | Description |
|--------|------|-------------|
| GET | /_template/{name} | Get legacy index templates |
| PUT | /_template/{name} | Create or update a legacy index template |
| POST | /_template/{name} | Create or update a legacy index template |
| DELETE | /_template/{name} | Delete a legacy index template |
| HEAD | /_template/{name} | Check existence of index templates |
| GET | /_template | Get legacy index templates |

### _alias
| Method | Path | Description |
|--------|------|-------------|
| GET | /_alias/{name} | Get aliases |
| HEAD | /_alias/{name} | Check aliases |
| GET | /_alias | Get aliases |

### _flush
| Method | Path | Description |
|--------|------|-------------|
| GET | /_flush | Flush data streams or indices |
| POST | /_flush | Flush data streams or indices |

### _forcemerge
| Method | Path | Description |
|--------|------|-------------|
| POST | /_forcemerge | Force a merge |

### _lifecycle
| Method | Path | Description |
|--------|------|-------------|
| GET | /_lifecycle/stats | Get data stream lifecycle stats |

### _mapping
| Method | Path | Description |
|--------|------|-------------|
| GET | /_mapping/field/{fields} | Get mapping definitions |
| GET | /_mapping | Get mapping definitions |

### _settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /_settings | Get index settings |
| PUT | /_settings | Update index settings |
| GET | /_settings/{name} | Get index settings |

### _recovery
| Method | Path | Description |
|--------|------|-------------|
| GET | /_recovery | Get index recovery information |

### _refresh
| Method | Path | Description |
|--------|------|-------------|
| GET | /_refresh | Refresh an index |
| POST | /_refresh | Refresh an index |

### _resolve
| Method | Path | Description |
|--------|------|-------------|
| GET | /_resolve/cluster | Resolve the cluster |
| GET | /_resolve/cluster/{name} | Resolve the cluster |
| GET | /_resolve/index/{name} | Resolve indices |
| POST | /_resolve/index/{name} | Resolve indices |

### {alias}
| Method | Path | Description |
|--------|------|-------------|
| POST | /{alias}/_rollover | Roll over to a new index |
| POST | /{alias}/_rollover/{new_index} | Roll over to a new index |

### _segments
| Method | Path | Description |
|--------|------|-------------|
| GET | /_segments | Get index segments |

### _shard_stores
| Method | Path | Description |
|--------|------|-------------|
| GET | /_shard_stores | Get index shard stores |

### _stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /_stats | Get index statistics |
| GET | /_stats/{metric} | Get index statistics |

### _aliases
| Method | Path | Description |
|--------|------|-------------|
| POST | /_aliases | Create or update an alias |

### _validate
| Method | Path | Description |
|--------|------|-------------|
| GET | /_validate/query | Validate a query |
| POST | /_validate/query | Validate a query |

### _inference
| Method | Path | Description |
|--------|------|-------------|
| POST | /_inference/chat_completion/{inference_id}/_stream | Perform chat completion inference on the service |
| POST | /_inference/completion/{inference_id} | Perform completion inference on the service |
| GET | /_inference/{inference_id} | Get an inference endpoint |
| PUT | /_inference/{inference_id} | Create an inference endpoint |
| POST | /_inference/{inference_id} | Perform inference on the service |
| DELETE | /_inference/{inference_id} | Delete an inference endpoint |
| GET | /_inference/{task_type}/{inference_id} | Get an inference endpoint |
| PUT | /_inference/{task_type}/{inference_id} | Create an inference endpoint |
| POST | /_inference/{task_type}/{inference_id} | Perform inference on the service |
| DELETE | /_inference/{task_type}/{inference_id} | Delete an inference endpoint |
| POST | /_inference/embedding/{inference_id} | Perform dense embedding inference on the service |
| GET | /_inference | Get an inference endpoint |
| GET | /_inference/{task_type}/_all | Get an inference endpoint |
| PUT | /_inference/{task_type}/{ai21_inference_id} | Create a AI21 inference endpoint |
| PUT | /_inference/{task_type}/{alibabacloud_inference_id} | Create an AlibabaCloud AI Search inference endpoint |
| PUT | /_inference/{task_type}/{amazonbedrock_inference_id} | Create an Amazon Bedrock inference endpoint |
| PUT | /_inference/{task_type}/{amazonsagemaker_inference_id} | Create an Amazon SageMaker inference endpoint |
| PUT | /_inference/{task_type}/{anthropic_inference_id} | Create an Anthropic inference endpoint |
| PUT | /_inference/{task_type}/{azureaistudio_inference_id} | Create an Azure AI studio inference endpoint |
| PUT | /_inference/{task_type}/{azureopenai_inference_id} | Create an Azure OpenAI inference endpoint |
| PUT | /_inference/{task_type}/{cohere_inference_id} | Create a Cohere inference endpoint |
| PUT | /_inference/{task_type}/{contextualai_inference_id} | Create an Contextual AI inference endpoint |
| PUT | /_inference/{task_type}/{custom_inference_id} | Create a custom inference endpoint |
| PUT | /_inference/{task_type}/{deepseek_inference_id} | Create a DeepSeek inference endpoint |
| PUT | /_inference/{task_type}/{elasticsearch_inference_id} | Create an Elasticsearch inference endpoint |
| PUT | /_inference/{task_type}/{elser_inference_id} | Create an ELSER inference endpoint |
| PUT | /_inference/{task_type}/{googleaistudio_inference_id} | Create an Google AI Studio inference endpoint |
| PUT | /_inference/{task_type}/{googlevertexai_inference_id} | Create a Google Vertex AI inference endpoint |
| PUT | /_inference/{task_type}/{groq_inference_id} | Create a Groq inference endpoint |
| PUT | /_inference/{task_type}/{huggingface_inference_id} | Create a Hugging Face inference endpoint |
| PUT | /_inference/{task_type}/{jinaai_inference_id} | Create an JinaAI inference endpoint |
| PUT | /_inference/{task_type}/{llama_inference_id} | Create a Llama inference endpoint |
| PUT | /_inference/{task_type}/{mistral_inference_id} | Create a Mistral inference endpoint |
| PUT | /_inference/{task_type}/{nvidia_inference_id} | Create an Nvidia inference endpoint |
| PUT | /_inference/{task_type}/{openai_inference_id} | Create an OpenAI inference endpoint |
| PUT | /_inference/{task_type}/{openshiftai_inference_id} | Create an OpenShift AI inference endpoint |
| PUT | /_inference/{task_type}/{voyageai_inference_id} | Create a VoyageAI inference endpoint |
| PUT | /_inference/{task_type}/{watsonx_inference_id} | Create a Watsonx inference endpoint |
| POST | /_inference/rerank/{inference_id} | Perform reranking inference on the service |
| POST | /_inference/sparse_embedding/{inference_id} | Perform sparse embedding inference on the service |
| POST | /_inference/completion/{inference_id}/_stream | Perform streaming completion inference on the service |
| POST | /_inference/text_embedding/{inference_id} | Perform text embedding inference on the service |
| PUT | /_inference/{inference_id}/_update | Update an inference endpoint |
| PUT | /_inference/{task_type}/{inference_id}/_update | Update an inference endpoint |

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Get cluster info |
| HEAD | / | Ping the cluster |

### _ingest
| Method | Path | Description |
|--------|------|-------------|
| GET | /_ingest/geoip/database/{id} | Get GeoIP database configurations |
| PUT | /_ingest/geoip/database/{id} | Create or update a GeoIP database configuration |
| DELETE | /_ingest/geoip/database/{id} | Delete GeoIP database configurations |
| GET | /_ingest/ip_location/database/{id} | Get IP geolocation database configurations |
| PUT | /_ingest/ip_location/database/{id} | Create or update an IP geolocation database configuration |
| DELETE | /_ingest/ip_location/database/{id} | Delete IP geolocation database configurations |
| GET | /_ingest/pipeline/{id} | Get pipelines |
| PUT | /_ingest/pipeline/{id} | Create or update a pipeline |
| DELETE | /_ingest/pipeline/{id} | Delete pipelines |
| GET | /_ingest/geoip/stats | Get GeoIP statistics |
| GET | /_ingest/geoip/database | Get GeoIP database configurations |
| GET | /_ingest/ip_location/database | Get IP geolocation database configurations |
| GET | /_ingest/pipeline | Get pipelines |
| GET | /_ingest/processor/grok | Run a grok processor |
| GET | /_ingest/pipeline/_simulate | Simulate a pipeline |
| POST | /_ingest/pipeline/_simulate | Simulate a pipeline |
| GET | /_ingest/pipeline/{id}/_simulate | Simulate a pipeline |
| POST | /_ingest/pipeline/{id}/_simulate | Simulate a pipeline |
| GET | /_ingest/_simulate | Simulate data ingestion |
| POST | /_ingest/_simulate | Simulate data ingestion |
| GET | /_ingest/{index}/_simulate | Simulate data ingestion |
| POST | /_ingest/{index}/_simulate | Simulate data ingestion |

### _license
| Method | Path | Description |
|--------|------|-------------|
| GET | /_license | Get license information |
| PUT | /_license | Update the license |
| POST | /_license | Update the license |
| DELETE | /_license | Delete the license |
| GET | /_license/basic_status | Get the basic license status |
| GET | /_license/trial_status | Get the trial status |
| POST | /_license/start_basic | Start a basic license |
| POST | /_license/start_trial | Start a trial |

### _logstash
| Method | Path | Description |
|--------|------|-------------|
| GET | /_logstash/pipeline/{id} | Get Logstash pipelines |
| PUT | /_logstash/pipeline/{id} | Create or update a Logstash pipeline |
| DELETE | /_logstash/pipeline/{id} | Delete a Logstash pipeline |
| GET | /_logstash/pipeline | Get Logstash pipelines |

### _mget
| Method | Path | Description |
|--------|------|-------------|
| GET | /_mget | Get multiple documents |
| POST | /_mget | Get multiple documents |

### _ml
| Method | Path | Description |
|--------|------|-------------|
| POST | /_ml/trained_models/{model_id}/deployment/cache/_clear | Clear trained model deployment cache |
| POST | /_ml/anomaly_detectors/{job_id}/_close | Close anomaly detection jobs |
| GET | /_ml/calendars/{calendar_id} | Get calendar configuration info |
| PUT | /_ml/calendars/{calendar_id} | Create a calendar |
| POST | /_ml/calendars/{calendar_id} | Get calendar configuration info |
| DELETE | /_ml/calendars/{calendar_id} | Delete a calendar |
| DELETE | /_ml/calendars/{calendar_id}/events/{event_id} | Delete events from a calendar |
| PUT | /_ml/calendars/{calendar_id}/jobs/{job_id} | Add anomaly detection job to calendar |
| DELETE | /_ml/calendars/{calendar_id}/jobs/{job_id} | Delete anomaly jobs from a calendar |
| GET | /_ml/data_frame/analytics/{id} | Get data frame analytics job configuration info |
| PUT | /_ml/data_frame/analytics/{id} | Create a data frame analytics job |
| DELETE | /_ml/data_frame/analytics/{id} | Delete a data frame analytics job |
| GET | /_ml/datafeeds/{datafeed_id} | Get datafeeds configuration info |
| PUT | /_ml/datafeeds/{datafeed_id} | Create a datafeed |
| DELETE | /_ml/datafeeds/{datafeed_id} | Delete a datafeed |
| DELETE | /_ml/_delete_expired_data/{job_id} | Delete expired ML data |
| DELETE | /_ml/_delete_expired_data | Delete expired ML data |
| GET | /_ml/filters/{filter_id} | Get filters |
| PUT | /_ml/filters/{filter_id} | Create a filter |
| DELETE | /_ml/filters/{filter_id} | Delete a filter |
| POST | /_ml/anomaly_detectors/{job_id}/_forecast | Predict future behavior of a time series |
| DELETE | /_ml/anomaly_detectors/{job_id}/_forecast | Delete forecasts from a job |
| DELETE | /_ml/anomaly_detectors/{job_id}/_forecast/{forecast_id} | Delete forecasts from a job |
| GET | /_ml/anomaly_detectors/{job_id} | Get anomaly detection jobs configuration info |
| PUT | /_ml/anomaly_detectors/{job_id} | Create an anomaly detection job |
| DELETE | /_ml/anomaly_detectors/{job_id} | Delete an anomaly detection job |
| GET | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id} | Get model snapshots info |
| POST | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id} | Get model snapshots info |
| DELETE | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id} | Delete a model snapshot |
| GET | /_ml/trained_models/{model_id} | Get trained model configuration info |
| PUT | /_ml/trained_models/{model_id} | Create a trained model |
| DELETE | /_ml/trained_models/{model_id} | Delete an unreferenced trained model |
| PUT | /_ml/trained_models/{model_id}/model_aliases/{model_alias} | Create or update a trained model alias |
| DELETE | /_ml/trained_models/{model_id}/model_aliases/{model_alias} | Delete a trained model alias |
| POST | /_ml/anomaly_detectors/_estimate_model_memory | Estimate job model memory usage |
| POST | /_ml/data_frame/_evaluate | Evaluate data frame analytics |
| GET | /_ml/data_frame/analytics/_explain | Explain data frame analytics config |
| POST | /_ml/data_frame/analytics/_explain | Explain data frame analytics config |
| GET | /_ml/data_frame/analytics/{id}/_explain | Explain data frame analytics config |
| POST | /_ml/data_frame/analytics/{id}/_explain | Explain data frame analytics config |
| POST | /_ml/anomaly_detectors/{job_id}/_flush | Force buffered data to be processed |
| GET | /_ml/anomaly_detectors/{job_id}/results/buckets/{timestamp} | Get anomaly detection job results for buckets |
| POST | /_ml/anomaly_detectors/{job_id}/results/buckets/{timestamp} | Get anomaly detection job results for buckets |
| GET | /_ml/anomaly_detectors/{job_id}/results/buckets | Get anomaly detection job results for buckets |
| POST | /_ml/anomaly_detectors/{job_id}/results/buckets | Get anomaly detection job results for buckets |
| GET | /_ml/calendars/{calendar_id}/events | Get info about events in calendars |
| POST | /_ml/calendars/{calendar_id}/events | Add scheduled events to the calendar |
| GET | /_ml/calendars | Get calendar configuration info |
| POST | /_ml/calendars | Get calendar configuration info |
| GET | /_ml/anomaly_detectors/{job_id}/results/categories/{category_id} | Get anomaly detection job results for categories |
| POST | /_ml/anomaly_detectors/{job_id}/results/categories/{category_id} | Get anomaly detection job results for categories |
| GET | /_ml/anomaly_detectors/{job_id}/results/categories | Get anomaly detection job results for categories |
| POST | /_ml/anomaly_detectors/{job_id}/results/categories | Get anomaly detection job results for categories |
| GET | /_ml/data_frame/analytics | Get data frame analytics job configuration info |
| GET | /_ml/data_frame/analytics/_stats | Get data frame analytics job stats |
| GET | /_ml/data_frame/analytics/{id}/_stats | Get data frame analytics job stats |
| GET | /_ml/datafeeds/{datafeed_id}/_stats | Get datafeed stats |
| GET | /_ml/datafeeds/_stats | Get datafeed stats |
| GET | /_ml/datafeeds | Get datafeeds configuration info |
| GET | /_ml/filters | Get filters |
| GET | /_ml/anomaly_detectors/{job_id}/results/influencers | Get anomaly detection job results for influencers |
| POST | /_ml/anomaly_detectors/{job_id}/results/influencers | Get anomaly detection job results for influencers |
| GET | /_ml/anomaly_detectors/_stats | Get anomaly detection job stats |
| GET | /_ml/anomaly_detectors/{job_id}/_stats | Get anomaly detection job stats |
| GET | /_ml/anomaly_detectors | Get anomaly detection jobs configuration info |
| GET | /_ml/memory/_stats | Get machine learning memory usage info |
| GET | /_ml/memory/{node_id}/_stats | Get machine learning memory usage info |
| GET | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id}/_upgrade/_stats | Get anomaly detection job model snapshot upgrade usage info |
| GET | /_ml/anomaly_detectors/{job_id}/model_snapshots | Get model snapshots info |
| POST | /_ml/anomaly_detectors/{job_id}/model_snapshots | Get model snapshots info |
| GET | /_ml/anomaly_detectors/{job_id}/results/overall_buckets | Get overall bucket results |
| POST | /_ml/anomaly_detectors/{job_id}/results/overall_buckets | Get overall bucket results |
| GET | /_ml/anomaly_detectors/{job_id}/results/records | Get anomaly records for an anomaly detection job |
| POST | /_ml/anomaly_detectors/{job_id}/results/records | Get anomaly records for an anomaly detection job |
| GET | /_ml/trained_models | Get trained model configuration info |
| GET | /_ml/trained_models/{model_id}/_stats | Get trained models usage info |
| GET | /_ml/trained_models/_stats | Get trained models usage info |
| POST | /_ml/trained_models/{model_id}/_infer | Evaluate a trained model |
| GET | /_ml/info | Get machine learning information |
| POST | /_ml/anomaly_detectors/{job_id}/_open | Open anomaly detection jobs |
| POST | /_ml/anomaly_detectors/{job_id}/_data | Send data to an anomaly detection job for analysis |
| GET | /_ml/data_frame/analytics/_preview | Preview features used by data frame analytics |
| POST | /_ml/data_frame/analytics/_preview | Preview features used by data frame analytics |
| GET | /_ml/data_frame/analytics/{id}/_preview | Preview features used by data frame analytics |
| POST | /_ml/data_frame/analytics/{id}/_preview | Preview features used by data frame analytics |
| GET | /_ml/datafeeds/{datafeed_id}/_preview | Preview a datafeed |
| POST | /_ml/datafeeds/{datafeed_id}/_preview | Preview a datafeed |
| GET | /_ml/datafeeds/_preview | Preview a datafeed |
| POST | /_ml/datafeeds/_preview | Preview a datafeed |
| PUT | /_ml/trained_models/{model_id}/definition/{part} | Create part of a trained model definition |
| PUT | /_ml/trained_models/{model_id}/vocabulary | Create a trained model vocabulary |
| POST | /_ml/anomaly_detectors/{job_id}/_reset | Reset an anomaly detection job |
| POST | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id}/_revert | Revert to a snapshot |
| POST | /_ml/set_upgrade_mode | Set upgrade_mode for ML indices |
| POST | /_ml/data_frame/analytics/{id}/_start | Start a data frame analytics job |
| POST | /_ml/datafeeds/{datafeed_id}/_start | Start datafeeds |
| POST | /_ml/trained_models/{model_id}/deployment/_start | Start a trained model deployment |
| POST | /_ml/data_frame/analytics/{id}/_stop | Stop data frame analytics jobs |
| POST | /_ml/datafeeds/{datafeed_id}/_stop | Stop datafeeds |
| POST | /_ml/trained_models/{model_id}/deployment/_stop | Stop a trained model deployment |
| POST | /_ml/data_frame/analytics/{id}/_update | Update a data frame analytics job |
| POST | /_ml/datafeeds/{datafeed_id}/_update | Update a datafeed |
| POST | /_ml/filters/{filter_id}/_update | Update a filter |
| POST | /_ml/anomaly_detectors/{job_id}/_update | Update an anomaly detection job |
| POST | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id}/_update | Update a snapshot |
| POST | /_ml/trained_models/{model_id}/deployment/_update | Update a trained model deployment |
| POST | /_ml/anomaly_detectors/{job_id}/model_snapshots/{snapshot_id}/_upgrade | Upgrade a snapshot |

### _msearch
| Method | Path | Description |
|--------|------|-------------|
| GET | /_msearch | Run multiple searches |
| POST | /_msearch | Run multiple searches |
| GET | /_msearch/template | Run multiple templated searches |
| POST | /_msearch/template | Run multiple templated searches |

### _mtermvectors
| Method | Path | Description |
|--------|------|-------------|
| GET | /_mtermvectors | Get multiple term vectors |
| POST | /_mtermvectors | Get multiple term vectors |

### _nodes
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /_nodes/{node_id}/_repositories_metering/{max_archive_version} | Clear the archived repositories metering |
| GET | /_nodes/{node_id}/_repositories_metering | Get cluster repositories metering |
| GET | /_nodes/hot_threads | Get the hot threads for nodes |
| GET | /_nodes/{node_id}/hot_threads | Get the hot threads for nodes |
| GET | /_nodes | Get node information |
| GET | /_nodes/{node_id} | Get node information |
| GET | /_nodes/{metric} | Get node information |
| GET | /_nodes/{node_id}/{metric} | Get node information |
| POST | /_nodes/reload_secure_settings | Reload the keystore on nodes in the cluster |
| POST | /_nodes/{node_id}/reload_secure_settings | Reload the keystore on nodes in the cluster |
| GET | /_nodes/stats | Get node statistics |
| GET | /_nodes/{node_id}/stats | Get node statistics |
| GET | /_nodes/stats/{metric} | Get node statistics |
| GET | /_nodes/{node_id}/stats/{metric} | Get node statistics |
| GET | /_nodes/stats/{metric}/{index_metric} | Get node statistics |
| GET | /_nodes/{node_id}/stats/{metric}/{index_metric} | Get node statistics |
| GET | /_nodes/usage | Get feature usage information |
| GET | /_nodes/{node_id}/usage | Get feature usage information |
| GET | /_nodes/usage/{metric} | Get feature usage information |
| GET | /_nodes/{node_id}/usage/{metric} | Get feature usage information |

### _query_rules
| Method | Path | Description |
|--------|------|-------------|
| GET | /_query_rules/{ruleset_id}/_rule/{rule_id} | Get a query rule |
| PUT | /_query_rules/{ruleset_id}/_rule/{rule_id} | Create or update a query rule |
| DELETE | /_query_rules/{ruleset_id}/_rule/{rule_id} | Delete a query rule |
| GET | /_query_rules/{ruleset_id} | Get a query ruleset |
| PUT | /_query_rules/{ruleset_id} | Create or update a query ruleset |
| DELETE | /_query_rules/{ruleset_id} | Delete a query ruleset |
| GET | /_query_rules | Get all query rulesets |
| POST | /_query_rules/{ruleset_id}/_test | Test a query ruleset |

### _rank_eval
| Method | Path | Description |
|--------|------|-------------|
| GET | /_rank_eval | Evaluate ranked search results |
| POST | /_rank_eval | Evaluate ranked search results |

### _reindex
| Method | Path | Description |
|--------|------|-------------|
| POST | /_reindex | Reindex documents |
| POST | /_reindex/{task_id}/_rethrottle | Throttle a reindex operation |

### _render
| Method | Path | Description |
|--------|------|-------------|
| GET | /_render/template | Render a search template |
| POST | /_render/template | Render a search template |
| GET | /_render/template/{id} | Render a search template |
| POST | /_render/template/{id} | Render a search template |

### _rollup
| Method | Path | Description |
|--------|------|-------------|
| GET | /_rollup/job/{id} | Get rollup job information |
| PUT | /_rollup/job/{id} | Create a rollup job |
| DELETE | /_rollup/job/{id} | Delete a rollup job |
| GET | /_rollup/job | Get rollup job information |
| GET | /_rollup/data/{id} | Get the rollup job capabilities |
| GET | /_rollup/data | Get the rollup job capabilities |
| POST | /_rollup/job/{id}/_start | Start rollup jobs |
| POST | /_rollup/job/{id}/_stop | Stop rollup jobs |

### _application
| Method | Path | Description |
|--------|------|-------------|
| GET | /_application/search_application/{name} | Get search application details |
| PUT | /_application/search_application/{name} | Create or update a search application |
| DELETE | /_application/search_application/{name} | Delete a search application |
| GET | /_application/analytics/{name} | Get behavioral analytics collections |
| PUT | /_application/analytics/{name} | Create a behavioral analytics collection |
| DELETE | /_application/analytics/{name} | Delete a behavioral analytics collection |
| GET | /_application/analytics | Get behavioral analytics collections |
| GET | /_application/search_application | Get search applications |
| POST | /_application/analytics/{collection_name}/event/{event_type} | Create a behavioral analytics collection event |
| POST | /_application/search_application/{name}/_render_query | Render a search application query |
| GET | /_application/search_application/{name}/_search | Run a search application search |
| POST | /_application/search_application/{name}/_search | Run a search application search |

### _search_shards
| Method | Path | Description |
|--------|------|-------------|
| GET | /_search_shards | Get the search shards |
| POST | /_search_shards | Get the search shards |

### _searchable_snapshots
| Method | Path | Description |
|--------|------|-------------|
| GET | /_searchable_snapshots/cache/stats | Get cache statistics |
| GET | /_searchable_snapshots/{node_id}/cache/stats | Get cache statistics |
| POST | /_searchable_snapshots/cache/clear | Clear the cache |
| GET | /_searchable_snapshots/stats | Get searchable snapshot statistics |

### _snapshot
| Method | Path | Description |
|--------|------|-------------|
| POST | /_snapshot/{repository}/{snapshot}/_mount | Mount a snapshot |
| POST | /_snapshot/{repository}/_cleanup | Clean up the snapshot repository |
| PUT | /_snapshot/{repository}/{snapshot}/_clone/{target_snapshot} | Clone a snapshot |
| GET | /_snapshot/{repository}/{snapshot} | Get snapshot information |
| PUT | /_snapshot/{repository}/{snapshot} | Create a snapshot |
| POST | /_snapshot/{repository}/{snapshot} | Create a snapshot |
| DELETE | /_snapshot/{repository}/{snapshot} | Delete snapshots |
| GET | /_snapshot/{repository} | Get snapshot repository information |
| PUT | /_snapshot/{repository} | Create or update a snapshot repository |
| POST | /_snapshot/{repository} | Create or update a snapshot repository |
| DELETE | /_snapshot/{repository} | Delete snapshot repositories |
| GET | /_snapshot | Get snapshot repository information |
| POST | /_snapshot/{repository}/_analyze | Analyze a snapshot repository |
| POST | /_snapshot/{repository}/_verify_integrity | Verify the repository integrity |
| POST | /_snapshot/{repository}/{snapshot}/_restore | Restore a snapshot |
| GET | /_snapshot/_status | Get the snapshot status |
| GET | /_snapshot/{repository}/_status | Get the snapshot status |
| GET | /_snapshot/{repository}/{snapshot}/_status | Get the snapshot status |
| POST | /_snapshot/{repository}/_verify | Verify a snapshot repository |

### _security
| Method | Path | Description |
|--------|------|-------------|
| POST | /_security/profile/_activate | Activate a user profile |
| GET | /_security/_authenticate | Authenticate a user |
| GET | /_security/role | Get roles |
| POST | /_security/role | Bulk create or update roles |
| DELETE | /_security/role | Bulk delete roles |
| POST | /_security/api_key/_bulk_update | Bulk update API keys |
| PUT | /_security/user/{username}/_password | Change passwords |
| POST | /_security/user/{username}/_password | Change passwords |
| PUT | /_security/user/_password | Change passwords |
| POST | /_security/user/_password | Change passwords |
| POST | /_security/api_key/{ids}/_clear_cache | Clear the API key cache |
| POST | /_security/privilege/{application}/_clear_cache | Clear the privileges cache |
| POST | /_security/realm/{realms}/_clear_cache | Clear the user cache |
| POST | /_security/role/{name}/_clear_cache | Clear the roles cache |
| POST | /_security/service/{namespace}/{service}/credential/token/{name}/_clear_cache | Clear service account token caches |
| GET | /_security/api_key | Get API key information |
| PUT | /_security/api_key | Create an API key |
| POST | /_security/api_key | Create an API key |
| DELETE | /_security/api_key | Invalidate API keys |
| POST | /_security/cross_cluster/api_key | Create a cross-cluster API key |
| PUT | /_security/service/{namespace}/{service}/credential/token/{name} | Create a service account token |
| POST | /_security/service/{namespace}/{service}/credential/token/{name} | Create a service account token |
| DELETE | /_security/service/{namespace}/{service}/credential/token/{name} | Delete service account tokens |
| POST | /_security/service/{namespace}/{service}/credential/token | Create a service account token |
| POST | /_security/delegate_pki | Delegate PKI authentication |
| GET | /_security/privilege/{application}/{name} | Get application privileges |
| DELETE | /_security/privilege/{application}/{name} | Delete application privileges |
| GET | /_security/role/{name} | Get roles |
| PUT | /_security/role/{name} | Create or update roles |
| POST | /_security/role/{name} | Create or update roles |
| DELETE | /_security/role/{name} | Delete roles |
| GET | /_security/role_mapping/{name} | Get role mappings |
| PUT | /_security/role_mapping/{name} | Create or update role mappings |
| POST | /_security/role_mapping/{name} | Create or update role mappings |
| DELETE | /_security/role_mapping/{name} | Delete role mappings |
| GET | /_security/user/{username} | Get users |
| PUT | /_security/user/{username} | Create or update users |
| POST | /_security/user/{username} | Create or update users |
| DELETE | /_security/user/{username} | Delete users |
| PUT | /_security/user/{username}/_disable | Disable users |
| POST | /_security/user/{username}/_disable | Disable users |
| PUT | /_security/profile/{uid}/_disable | Disable a user profile |
| POST | /_security/profile/{uid}/_disable | Disable a user profile |
| PUT | /_security/user/{username}/_enable | Enable users |
| POST | /_security/user/{username}/_enable | Enable users |
| PUT | /_security/profile/{uid}/_enable | Enable a user profile |
| POST | /_security/profile/{uid}/_enable | Enable a user profile |
| GET | /_security/enroll/kibana | Enroll Kibana |
| GET | /_security/enroll/node | Enroll a node |
| GET | /_security/privilege/_builtin | Get builtin privileges |
| GET | /_security/privilege | Get application privileges |
| PUT | /_security/privilege | Create or update application privileges |
| POST | /_security/privilege | Create or update application privileges |
| GET | /_security/privilege/{application} | Get application privileges |
| GET | /_security/role_mapping | Get role mappings |
| GET | /_security/service/{namespace}/{service} | Get service accounts |
| GET | /_security/service/{namespace} | Get service accounts |
| GET | /_security/service | Get service accounts |
| GET | /_security/service/{namespace}/{service}/credential | Get service account credentials |
| GET | /_security/settings | Get security index settings |
| PUT | /_security/settings | Update security index settings |
| GET | /_security/stats | Get security stats |
| POST | /_security/oauth2/token | Get a token |
| DELETE | /_security/oauth2/token | Invalidate a token |
| GET | /_security/user | Get users |
| GET | /_security/user/_privileges | Get user privileges |
| GET | /_security/profile/{uid} | Get a user profile |
| POST | /_security/api_key/grant | Grant an API key |
| GET | /_security/user/_has_privileges | Check user privileges |
| POST | /_security/user/_has_privileges | Check user privileges |
| GET | /_security/user/{user}/_has_privileges | Check user privileges |
| POST | /_security/user/{user}/_has_privileges | Check user privileges |
| GET | /_security/profile/_has_privileges | Check user profile privileges |
| POST | /_security/profile/_has_privileges | Check user profile privileges |
| POST | /_security/oidc/authenticate | Authenticate OpenID Connect |
| POST | /_security/oidc/logout | Logout of OpenID Connect |
| POST | /_security/oidc/prepare | Prepare OpenID connect authentication |
| GET | /_security/_query/api_key | Find API keys with a query |
| POST | /_security/_query/api_key | Find API keys with a query |
| GET | /_security/_query/role | Find roles with a query |
| POST | /_security/_query/role | Find roles with a query |
| GET | /_security/_query/user | Find users with a query |
| POST | /_security/_query/user | Find users with a query |
| POST | /_security/saml/authenticate | Authenticate SAML |
| POST | /_security/saml/complete_logout | Logout of SAML completely |
| POST | /_security/saml/invalidate | Invalidate SAML |
| POST | /_security/saml/logout | Logout of SAML |
| POST | /_security/saml/prepare | Prepare SAML authentication |
| GET | /_security/saml/metadata/{realm_name} | Create SAML service provider metadata |
| GET | /_security/profile/_suggest | Suggest a user profile |
| POST | /_security/profile/_suggest | Suggest a user profile |
| PUT | /_security/api_key/{id} | Update an API key |
| PUT | /_security/cross_cluster/api_key/{id} | Update a cross-cluster API key |
| PUT | /_security/profile/{uid}/_data | Update user profile data |
| POST | /_security/profile/{uid}/_data | Update user profile data |

### _slm
| Method | Path | Description |
|--------|------|-------------|
| GET | /_slm/policy/{policy_id} | Get policy information |
| PUT | /_slm/policy/{policy_id} | Create or update a policy |
| DELETE | /_slm/policy/{policy_id} | Delete a policy |
| PUT | /_slm/policy/{policy_id}/_execute | Run a policy |
| POST | /_slm/_execute_retention | Run a retention policy |
| GET | /_slm/policy | Get policy information |
| GET | /_slm/stats | Get snapshot lifecycle management statistics |
| GET | /_slm/status | Get the snapshot lifecycle management status |
| POST | /_slm/start | Start snapshot lifecycle management |
| POST | /_slm/stop | Stop snapshot lifecycle management |

### _sql
| Method | Path | Description |
|--------|------|-------------|
| POST | /_sql/close | Clear an SQL search cursor |
| DELETE | /_sql/async/delete/{id} | Delete an async SQL search |
| GET | /_sql/async/{id} | Get async SQL search results |
| GET | /_sql/async/status/{id} | Get the async SQL search status |
| GET | /_sql | Get SQL search results |
| POST | /_sql | Get SQL search results |
| GET | /_sql/translate | Translate SQL into Elasticsearch queries |
| POST | /_sql/translate | Translate SQL into Elasticsearch queries |

### _ssl
| Method | Path | Description |
|--------|------|-------------|
| GET | /_ssl/certificates | Get SSL certificates |

### _streams
| Method | Path | Description |
|--------|------|-------------|
| POST | /_streams/{name}/_disable | Disable a named stream |
| POST | /_streams/{name}/_enable | Enable a named stream |
| GET | /_streams/status | Get the status of streams |

### _synonyms
| Method | Path | Description |
|--------|------|-------------|
| GET | /_synonyms/{id} | Get a synonym set |
| PUT | /_synonyms/{id} | Create or update a synonym set |
| DELETE | /_synonyms/{id} | Delete a synonym set |
| GET | /_synonyms/{set_id}/{rule_id} | Get a synonym rule |
| PUT | /_synonyms/{set_id}/{rule_id} | Create or update a synonym rule |
| DELETE | /_synonyms/{set_id}/{rule_id} | Delete a synonym rule |
| GET | /_synonyms | Get all synonym sets |

### _tasks
| Method | Path | Description |
|--------|------|-------------|
| POST | /_tasks/_cancel | Cancel a task |
| POST | /_tasks/{task_id}/_cancel | Cancel a task |
| GET | /_tasks/{task_id} | Get task information |
| GET | /_tasks | Get all tasks |

### _text_structure
| Method | Path | Description |
|--------|------|-------------|
| GET | /_text_structure/find_field_structure | Find the structure of a text field |
| GET | /_text_structure/find_message_structure | Find the structure of text messages |
| POST | /_text_structure/find_message_structure | Find the structure of text messages |
| POST | /_text_structure/find_structure | Find the structure of a text file |
| GET | /_text_structure/test_grok_pattern | Test a Grok pattern |
| POST | /_text_structure/test_grok_pattern | Test a Grok pattern |

### _transform
| Method | Path | Description |
|--------|------|-------------|
| GET | /_transform/{transform_id} | Get transforms |
| PUT | /_transform/{transform_id} | Create a transform |
| DELETE | /_transform/{transform_id} | Delete a transform |
| GET | /_transform/_node_stats | Get node stats |
| GET | /_transform | Get transforms |
| GET | /_transform/{transform_id}/_stats | Get transform stats |
| GET | /_transform/{transform_id}/_preview | Preview a transform |
| POST | /_transform/{transform_id}/_preview | Preview a transform |
| GET | /_transform/_preview | Preview a transform |
| POST | /_transform/_preview | Preview a transform |
| POST | /_transform/{transform_id}/_reset | Reset a transform |
| POST | /_transform/{transform_id}/_schedule_now | Schedule a transform to start now |
| POST | /_transform/set_upgrade_mode | Set upgrade_mode for transform indices |
| POST | /_transform/{transform_id}/_start | Start a transform |
| POST | /_transform/{transform_id}/_stop | Stop transforms |
| POST | /_transform/{transform_id}/_update | Update a transform |
| POST | /_transform/_upgrade | Upgrade all transforms |

### _update_by_query
| Method | Path | Description |
|--------|------|-------------|
| POST | /_update_by_query/{task_id}/_rethrottle | Throttle an update by query operation |

### _watcher
| Method | Path | Description |
|--------|------|-------------|
| PUT | /_watcher/watch/{watch_id}/_ack | Acknowledge a watch |
| POST | /_watcher/watch/{watch_id}/_ack | Acknowledge a watch |
| PUT | /_watcher/watch/{watch_id}/_ack/{action_id} | Acknowledge a watch |
| POST | /_watcher/watch/{watch_id}/_ack/{action_id} | Acknowledge a watch |
| PUT | /_watcher/watch/{watch_id}/_activate | Activate a watch |
| POST | /_watcher/watch/{watch_id}/_activate | Activate a watch |
| PUT | /_watcher/watch/{watch_id}/_deactivate | Deactivate a watch |
| POST | /_watcher/watch/{watch_id}/_deactivate | Deactivate a watch |
| GET | /_watcher/watch/{id} | Get a watch |
| PUT | /_watcher/watch/{id} | Create or update a watch |
| POST | /_watcher/watch/{id} | Create or update a watch |
| DELETE | /_watcher/watch/{id} | Delete a watch |
| PUT | /_watcher/watch/{id}/_execute | Run a watch |
| POST | /_watcher/watch/{id}/_execute | Run a watch |
| PUT | /_watcher/watch/_execute | Run a watch |
| POST | /_watcher/watch/_execute | Run a watch |
| GET | /_watcher/settings | Get Watcher index settings |
| PUT | /_watcher/settings | Update Watcher index settings |
| GET | /_watcher/_query/watches | Query watches |
| POST | /_watcher/_query/watches | Query watches |
| POST | /_watcher/_start | Start the watch service |
| GET | /_watcher/stats | Get Watcher statistics |
| GET | /_watcher/stats/{metric} | Get Watcher statistics |
| POST | /_watcher/_stop | Stop the watch service |

### _xpack
| Method | Path | Description |
|--------|------|-------------|
| GET | /_xpack | Get information |
| GET | /_xpack/usage | Get usage information |

## Enhanced Skill Content
## Question Mapping

- "How do I search for documents in an index?" -> POST /{index}/_search
- "How do I check if my cluster is healthy?" -> GET /_cluster/health
- "How do I index a new document?" -> PUT /{index}/_doc/{id}
- "How do I delete documents matching a query?" -> POST /{index}/_delete_by_query
- "How do I create a new index with mappings?" -> PUT /{index}
- "How do I get the mapping for an index?" -> GET /{index}/_mapping
- "How do I run a bulk insert of documents?" -> POST /_bulk
- "How do I count documents in an index?" -> GET /{index}/_count
- "How do I update a document by ID?" -> POST /{index}/_update/{id}
- "How do I create or manage an ingest pipeline?" -> PUT /_ingest/pipeline/{id}
- "How do I run an async search for large result sets?" -> POST /_async_search
- "How do I manage index lifecycle policies?" -> PUT /_ilm/policy/{policy}
- "How do I reindex data from one index to another?" -> POST /_reindex
- "How do I create an API key for authentication?" -> POST /_security/api_key
- "How do I check which nodes are in my cluster?" -> GET /_cat/nodes

## Response Tips

- **Search responses** (`_search`, `_async_search`): Results are in `hits.hits[]`; total count is in `hits.total.value`. Use `from`/`size` for pagination or `search_after` for deep pagination. Check `timed_out` and `_shards.failed` for partial results.
- **Bulk responses** (`_bulk`): Always check `errors: true` before assuming success; iterate `items[]` for per-document status codes and error details.
- **Cat responses** (`_cat/*`): Return plain text by default; use `?format=json` for structured data. Use `h=` to select columns and `s=` to sort.
- **Cluster/node responses** (`_cluster/*`, `_nodes/*`): Deeply nested by node ID; `status` field uses green/yellow/red. Check `_nodes.failed` for unreachable nodes.
- **Acknowledged responses** (create/delete/update): Check both `acknowledged: true` and `shards_acknowledged: true` for index operations; acknowledged alone does not guarantee all shards are ready.
- **Async responses** (`_async_search`, `_query/async`): Check `is_running` and `is_partial`; poll with the returned `id` until complete.
- **ML responses** (`_ml/*`): Most list endpoints return `count` plus an array (`jobs`, `datafeeds`, `trained_model_configs`); use `from`/`size` for pagination.

## Anomaly Flags

- **Cluster health degraded**: Surface immediately when `GET /_cluster/health` returns `status: yellow` or `status: red`, or when `unassigned_shards > 0`.
- **Shard failures in search**: Flag when `_shards.failed > 0` in any search response, indicating partial or unreliable results.
- **Bulk errors**: Alert when `errors: true` in a `_bulk` response; extract and summarize failing items from `items[]`.
- **Async search timeout**: Warn when `is_partial: true` persists after polling `_async_search/status/{id}`, or when `timed_out: true`.
- **ILM policy errors**: Flag when `GET /{index}/_ilm/explain` shows a managed index stuck in an error step.
- **Deprecated migration warnings**: Surface results from `GET /_migration/deprecations` proactively before version upgrades.
- **Task queue buildup**: Alert when `GET /_cat/pending_tasks` returns a growing list, or when `GET /_cluster/health` shows high `number_of_pending_tasks`.
- **License expiration**: Flag when `GET /_license` shows an approaching `expiry_date_in_millis`.
- **ML job anomalies**: Surface when `GET /_ml/anomaly_detectors/{job_id}/_stats` shows `state: failed` or high `data_counts.out_of_order_timestamp_count`.

## Playbook

### 1. Create an Index, Define Mappings, and Index Documents

1. Create the index with settings and mappings: `PUT /{index}` with `settings` (shards, replicas) and `mappings` (properties with field types).
2. Verify creation: `HEAD /{index}` (expect 200).
3. Index documents individually: `PUT /{index}/_doc/{id}` with the document body, or use `POST /{index}/_doc` for auto-generated IDs.
4. For bulk loading, use `POST /_bulk` with NDJSON body containing `index` actions.
5. Refresh the index to make documents searchable: `POST /{index}/_refresh`.
6. Verify document count: `GET /{index}/_count`.

### 2. Run a Search with Aggregations and Pagination

1. Start with a basic query: `POST /{index}/_search` with a `query` object (e.g., `match`, `bool`, `range`).
2. Add aggregations in the `aggregations` field to compute metrics alongside results.
3. For the first page, use `size: 10, from: 0`. For subsequent pages, increment `from`.
4. For deep pagination (beyond 10,000), switch to `search_after` with a `sort` field and pass the last document's sort values.
5. If the query is long-running, use `POST /{index}/_async_search` with `keep_alive` and `wait_for_completion_timeout`, then poll `GET /_async_search/{id}`.
6. Clean up: `DELETE /_async_search/{id}` when done.

### 3. Set Up an Ingest Pipeline and Reindex Data

1. Create the ingest pipeline: `PUT /_ingest/pipeline/{id}` with `processors` (e.g., `set`, `rename`, `grok`, `date`).
2. Test it: `POST /_ingest/pipeline/{id}/_simulate` with sample `docs`.
3. Reindex existing data through the pipeline: `POST /_reindex` with `source.index`, `dest.index`, and `dest.pipeline`.
4. Monitor the reindex task: `GET /_tasks/{task_id}` (use the task ID from the reindex response).
5. Throttle if needed: `POST /_reindex/{task_id}/_rethrottle` with a lower `requests_per_second`.

### 4. Monitor Cluster Health and Diagnose Issues

1. Check overall health: `GET /_cluster/health`. Note `status`, `unassigned_shards`, and `number_of_pending_tasks`.
2. Drill into index-level health: `GET /_cluster/health/{index}?level=shards`.
3. Identify unassigned shard reasons: `POST /_cluster/allocation/explain` (optionally specify `index` and `shard`).
4. Review node resource usage: `GET /_cat/nodes?h=name,heap.percent,cpu,disk.used_percent&s=cpu:desc`.
5. Check hot threads on busy nodes: `GET /_nodes/{node_id}/hot_threads`.
6. Review pending tasks: `GET /_cat/pending_tasks`.

### 5. Manage Security: Users, Roles, and API Keys

1. Create a role with index privileges: `PUT /_security/role/{name}` with `indices` (names, privileges) and optional `cluster` permissions.
2. Create a user assigned to that role: `PUT /_security/user/{username}` with `password`, `roles`, and optional `metadata`.
3. Verify access: `POST /_security/user/{username}/_has_privileges` with the intended operations.
4. Generate an API key for programmatic access: `POST /_security/api_key` with `name`, `role_descriptors`, and optional `expiration`.
5. List and audit existing keys: `GET /_security/api_key?owner=true`.
6. Revoke a compromised key: `DELETE /_security/api_key` with the key `id`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
