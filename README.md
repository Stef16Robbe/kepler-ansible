# kepler-ansible

## The idea

Kepler has a great operator for Kubernetes/OpenShift environments. It has Grafana integration, for these environments it looks pretty complete.
It's also runnable on bare Linux hosts. This is where it's missing features at the moment.

We're going to make ansible playbooks for getting insight into energy consumption of a wide range of hosts. For environments that are not containerized, but still run on just Linux systems, whether VM's or BM's (spoiler alert, a lot of companies still rely on this).

## Known limitations

- Currently not running in container which is possible
- This means only RHEL based hosts are supported since only .rpm is given

## Usage

`ansible-navigator run kepler-install.yml -m stdout --enable-prompts`

This will install Kepler on selected systems

These can be scraped using various methods, one of which is Prometheus agent.

Install Prometheus, for example with Ansible: <https://github.com/prometheus-community/ansible/tree/main/roles/prometheus>

The following example config can be used to collect log data on a central host:

```yaml
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.

scrape_configs:
  - job_name: dc_prometheus
    honor_labels: true
    metrics_path: /metrics
    params:
      match[]:
        - '{__name__=~"^job:.*"}' # Request all job-level time series
    static_configs:
      - targets:
        # YOUR TARGETS GO HERE:
        - <ip or hostname>
```

## TODO

We now have a very simple install setup but it can be improved upon

- Run kepler in container instead of directly on host
- Add log centralization?
- ...
