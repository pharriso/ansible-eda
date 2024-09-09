Setup Prometheus alertmanager demo
=========

For this demo, we use prometheus and alertmanager to send events to EDA.

Run the playbook
------------

```bash
cd playbooks/
ansible-playbook prometheus-setup.yml -i <fqdn>, -e eda_webhook_url=<eda webhook url>
```

Example:




Quick and easy test
------------

SSH to your EDA controller and install netcat:

```bash
sudo dnf install nc -y
```

Start listening on port 5000

```bash
nc -l 5000
```

