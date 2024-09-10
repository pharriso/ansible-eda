Setup Prometheus alertmanager demo
=========

For this demo, we use prometheus and alertmanager to send events to EDA. The playbook will run prometheus and alertmanager as podman quadlets and node_exporter as a systemd process on the host. All services are installed on the same host.

It is configured to use the alertmanager webhook to send events to eda (could also look at the alertmanager plugin I guess). 

Install prometheus, alertmanager and node_exporter
------------

```bash
cd playbooks/
ansible-playbook prometheus-setup.yml -i <fqdn>, -e eda_webhook_url=<eda webhook url>
```

Example:

```bash
ansible-playbook prometheus-setup.yml -i demovm.example.com, -e eda_webhook_url=http://eda.example.com:3000/endpoint
```


Quick and easy testing of alertmanager webhook.
------------

SSH to your EDA controller and install netcat:

```bash
sudo dnf install nc -y
```

Start listening on port 3000

```bash
nc -l 3000
```

Generate an alert and ensure that you recieve the payload.

Rulebooks and playbooks
------------

Rulebooks and playbooks are in the root of this repo in the respective directories.

* rulebooks/prometheus.yml
*prometheus-systemd.yml
*prometheus-security.yml

ToDo
------------

Add config as code for AAP.
