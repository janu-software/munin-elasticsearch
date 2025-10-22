## Elasticsearch Munin Plugin

An Elasticsearch Munin Plugin for monitoring Elasticsearch nodes. Written in Ruby, depends on JSON gem. Compatible with Elasticsearch 5.x–9.x.

### Features
- Monitors key Elasticsearch metrics: JVM heap usage, garbage collection stats, cache usage, document counts, operation rates, and store size.
- Supports multiple Elasticsearch nodes.
- Configurable via environment variables.

### Installation
1. Ensure you have Ruby and the JSON gem installed:
   ```bash
   gem install json
   ```
2. Download the plugin script and place it in your Munin plugins directory (e.g., `/etc/munin/plugins/`):
   ```bash
   wget https://raw.githubusercontent.com/janu-software/munin-elasticsearch/refs/heads/master/elasticsearch_ -O /etc/munin/plugins/elasticsearch_
   chmod +x /etc/munin/plugins/elasticsearch_
   ```
3. Create symlinks for each Elasticsearch node you want to monitor:
   ```bash
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_jvm
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_docs
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_ops
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_cache
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_store
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_gc
   ln -s /etc/munin/plugins/elasticsearch_ /etc/munin/plugins/elasticsearch_gc_time
   ```
4. Restart the Munin node to apply changes:
   ```bash
    service munin-node restart
    ```
### Configuration
Create configuration files in `/etc/munin/plugin-conf.d/` to specify the Elasticsearch nodes to monitor. Example configuration:

#### File: /etc/munin/plugin-conf.d/elasticsearch
```ini
[elasticsearch*]
env.host localhost
env.port 9200
env.node es01,es02,es03
env.user munin
env.pass SecurePass123
env.scheme https
env.verify_ssl false
```
