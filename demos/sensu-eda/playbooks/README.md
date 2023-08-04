Setup Sensu Demo
=========

* Runs sensu-server in container
* Configures sensu server
* Deploy sensu agent

Requirements
------------

* Install the collection sensu.sensu_go
* Have a RHEL server running somewhere with ports 3000, 8080 and 8081 open.
* Have ansible-core installed

Required Variables
------------

These variables are needed to deploy and configure sensu

| Name                      | Default value         |                                                                                  |
|---------------------------|-----------------------|----------------------------------------------------------------------------------|
| sensu_server              |                       | sensu server fqdn                                                                |
| sensu_admin_password      |                       | sensu admin password                                                             |

These variables are needed to configure sensu server to send webhooks to EDA.

| Name                      | Default value         |                                                                                  |
|---------------------------|-----------------------|----------------------------------------------------------------------------------|
| eda_server_url            | http://edaserver.example.com:5000/endpoint                      | URL for eda server                                                               |


Deploying sensu server
------------

1. Clone this repo

2. Run the playbook.

```bash
ansible-playbook deploy_sensu_server.yml -i sensu.example.com, -e sensu_admin_password=somepassword
```

4. Check you can login to sensu on http://sensu.example.com:3000 with the admin password you set.

Configuring sensu server
------------

After deploying sensu you can populate it with checks and handlers.

```bash
ansible-playbook configure_sensu_server.yml -e sensu_admin_password=somepassword -e sensu_server=sensu.example.com
```

Deploying agents
------------

Deploy sensu agent to a server as follows:

1. Ensure the server has access to the sensu server on port 8081.

2. Ensure server has internet access to get to sensu yum repos.

3. Run playbook:

```bash
ansible-playbook deploy_sensu_agent.yml -i someclient.example.com, -e sensu_server=sensu.example.com
```

4. Log into sensu UI http://sensu.example.com:3000 and check the client is reporting in.
