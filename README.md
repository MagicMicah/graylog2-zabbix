# graylog2-zabbix
Basic Zabbix monitoring for Graylog2

Mainly written for my own use, please feel to fork/use and give feedback.

- Branch pre-2.1
Written using Zabbix 2.4 and Graylog 1.3. Lightly tested, but does no harm anyway.
Confirmed to work on Zabbix 3.0 and Graylog 2.0.3 as well.

- Master branch 2.1 and up (for now)
Tested using Zabbix 3.2 and Graylog 2.1.1

For specific Elasticsearch monitoring, please head over to Elastizabbix (https://github.com/mkhpalm/elastizabbix)

## Requirements
  * jq (https://github.com/stedolan/jq) 1.4+
  * curl

This doesn't require anything on the agent. It is an external script curl'ing to the Graylog2 API.

## How to install
  * Create a Graylog2 user with the "reader" role
  * Enter the credentials in the check_graylog_node_creds.txt file.
  * Copy the 2 files to your zabbix's externalscripts directory.
  * Make sure your files permissions are adequate.
  * Import the XML template in Zabbix.
  * Add template to graylog server and subscribe your graylog server hosts to it.

## Usage

Note: As of 2.1, the default API port is 9000. It used to be 12900. You change it back to the old behavior with ```rest_listen_uri```.

```
check_graylog_node -H <HOSTNAME> -a <ATTRIBUTE> [-p <GRAYLOG_API_PORT>] [-h] [-d]

Args:
    -H : Hostname or IP address of graylog server
    -a : Attribute to monitor. See list below.
    -p : Graylog API port (default: 12900)
    -d : Debug message to log file (default: false)
    -h : Displays help

List of attributes:
    - node_id : returns graylog node_id
    - node_transport
    - node_is_master
    - node_cluster
    - node_type
    - node_throughput
    - lb_status
    - total_message_count
    - es_cluster_health
    - journal_size
    - journal_num_segments
    - journal_uncommitted_entries
    - journal_events_read
    - journal_events_append
    - buffer_input_utilization
    - buffer_output_utilization
    - buffer_input_utilization_percent
    - buffer_output_utilization_percent
    - poll_data
    - current_deflector (not yet supported, because not accessible via regular user)
    - system_lifecycle
    - system_isprocessing
    - system_tz
    - system_version
    - system_startedat
    - cluster_stream_count
    - cluster_stream_rule_count
    - cluster_user_count
    - cluster_output_count
    - cluster_dashboard_count
    - cluster_input_count
    - cluster_global_input_count
    - cluster_extractor_count
    - cluster_contentpack_count
    - cluster_alerts_count
```
