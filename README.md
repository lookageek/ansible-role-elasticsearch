# Ansible Role: Elasticsearch

An Ansible Role that installs Elasticsearch on Debian/Ubuntu with systemd.

## Requirements

Requires at least Java 7 (Java 8+ preferred). Install OpenJDK or Oracle JDK using any galaxy role.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticstack_deb_repo: "5.x"

The elasticstack debian repo version

    elasticsearch_version: "5.3.2"

Specific elasticsearch version to install

    elasticsearch_enabled_on_boot: yes

Set this to `no` if you don't want elasticsearch to run on system startup.

    elasticsearch_network_host: localhost

Network host to listen for incoming connections on. By default we only listen on the localhost interface. Change this to the IP address to listen on a specific interface, or `0.0.0.0` to listen on all interfaces.

    elasticsearch_http_port: 9200

The port to listen for HTTP connections on.

    elasticsearch_script_inline: "true"

Whether to allow inline scripting against ElasticSearch. You should read the following link as there are possible security implications for enabling these options: [Enable Dynamic Scripting](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-security.html). Available options include: `true` and `false`.

    elasticsearch_custom_storage_enabled: false

Whether indexes need to stored into a separate path, like an EBS volume.

    elasticsearch_custom_storage_path: "/data/es-indexes"

Path where indexes have to be stored, if `yes` for previous variable

    elasticsearch_lock_heap: "false"

Whether locking heap memory allocated on JVM before starting Elasticsearch

    environment:
      ES_JAVA_OPTS: "-Xms2g -Xmx2g"

Set `ES_JAVA_OPTS` environment variable in the play before starting Elasticsearch to specify how much heap memory you need Elasticsearch to have. It should not be more than half of machine's total memory.

## Removing or Closing logstash indexes

If you are using elasticsearch for logstash, you may need to remove indexes older than some X days

    elasticsearch_user: ubuntu

Set the `machine_user`, cron jobs are created on this user

    elasticsearch_delete_logstash_indexes: false
    elasticsearch_delete_logstash_indexes_older_than: 15

If you want to delete the indexes older than days mentioned, a cron job is created which runs once a day

    elasticsearch_close_logstash_indexes: false
    elasticsearch_close_logstash_indexes_older_than: 15

If you want to keep the older data, and just remove it from being active, a cron job is created which runs once a day. [More info](https://www.elastic.co/guide/en/elasticsearch/guide/current/retiring-data.html)

    elasticsearch_log_level: info
    elasticsearch_slow_search_log_level: info
    elasticsearch_slow_index_log_level: info

Three log events that can be set with different levels. Available levels `trace`, `debug`, `info`, `warn`, `error`, and `fatal`.

## License

MIT / BSD

## Author Information

This role was created in 2017 by Jayanth Manklu cloning from [geerlingguy/ansible-role-elasticsearch](https://github.com/geerlingguy/ansible-role-elasticsearch).
