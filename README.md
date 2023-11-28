# Multi-Node Application Cluster Configuration

## Task Description

    This project involves deploying a multi-node application cluster, where each node requires a configuration file.
    The configuration file content varies based on the node's role, position in the cluster, and its name.

## Requirements
## Roles and Node Names

- Three roles: `leader`, `worker`, and `backup`.
- Nodes named in the format: `nodeX`, where `X` is a number (e.g., `node1`, `node2`, etc.).
- `leader` node requires additional configuration directives.
- `worker` nodes have common directives and a unique identifier based on their node name.
- `backup` node requires directives to know which node it backs up.

## Configuration Directives & Jinja2 template with Ansible Playbook

All nodes need common directives:

```yaml
cluster_name: "my_cluster"
log_level: "info"

- role: "leader"
    Each worker node requires common directives plus:

- role: "worker"
    worker_id: [unique_id]
    Where [unique_id] is calculated as 1000 + X (from the node name nodeX).

- backup node requires:
    role: "backup"
    backup_for: [node_name]
    Where [node_name] is the name of the node it backs up (could be leader or any worker).

## Jinja2 Template
  Create a Jinja2 template (config_template.j2) that generates the appropriate configuration for any node type. Utilize advanced Jinja2 features like conditional statements, loops, filters, and string manipulations.

## Ansible Playbook
    Write an Ansible playbook (generate_configs.yaml) that uses the Jinja2 template to generate configuration files for a sample cluster setup:
    
    1 leader node named node1
    3 worker nodes named node2, node3, and node4
    1 backup node named node5 (backing up node1)
    The playbook should place these configuration files in a directory named configs on the Ansible control node, with each file named config_[node_name].conf.

## How to Run:

Clone this repository:
    git clone https://github.com/AdnanRafique27/dynamic-conf-jinja-ansible
    cd dynamic-conf-jinja-ansible

## Run the Ansible playbook:
    ansible-playbook generate_configs.yaml
    //Check the configs directory for generated configuration files.

Author
Adnan Rafique
