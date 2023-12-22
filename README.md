# kepler-ansible

## The idea

Kepler has a great operator for Kubernetes/OpenShift environments. It has Grafana integration, for these environments it looks pretty complete.
It's also runnable on bare Linux hosts. This is where it's missing features at the moment.

We're going to make ansible playbooks for getting insight into energy consumption of a wide range of hosts. For environments that are not containerized, but still run on just Linux systems, whether VM's or BM's (spoiler alert, a lot of companies still rely on this).

## Tech

- ansible + <https://prometheus.io/docs/prometheus/latest/federation/>

## Known limitations

- Currently not running in container which is possible
- This means only RHEL based hosts are supported since only .rpm is given

## Usage

ansible-navigator run kepler-install.yml -m stdout --enable-prompts
