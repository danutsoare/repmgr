# PLANNING.md

## High-Level Vision
Create an Ansible project to automate the installation and management of multiple PostgreSQL clusters on RedHat-based systems, each managed by repmgr. The solution must support running multiple clusters on the same set of servers, with each cluster using its own data directory, port, and PostgreSQL version. The project should be modular, reusable, and easy to extend for future requirements.

## Architecture
- **Ansible-based automation**: Use Ansible playbooks and roles to orchestrate installation and configuration.
- **Cluster-per-instance**: Each PostgreSQL cluster is defined by its own parameters (version, port, data directory, repmgr settings).
- **Role-driven**: A dedicated Ansible role manages the lifecycle of each cluster and its repmgr configuration.
- **Inventory-driven deployment**: Hosts and cluster definitions are managed via inventory and group/host variables.
- **Templated configuration**: Use Jinja2 templates for PostgreSQL and repmgr configuration files.

## Constraints
- Must support multiple clusters per server, each with unique data directories and ports.
- Must support specifying PostgreSQL version per cluster.
- Target OS: RedHat-based (RHEL, CentOS, Rocky, AlmaLinux, etc.).
- Must use only open-source tools and packages available via standard or PostgreSQL repositories.
- Should not interfere with existing PostgreSQL installations unless explicitly managed.
- Should be idempotent and safe to re-run.

## Tools
- **Ansible**: Main automation tool.
- **Jinja2**: For templating configuration files.
- **YAML**: For configuration and variable files.
- **PostgreSQL official repositories**: For installing specific versions.
- **repmgr**: For cluster management and failover.

## Project Structure
```
repmgr-ansible/
├── inventories/
│   └── hosts
├── roles/
│   └── repmgr_cluster/
│       ├── tasks/
│       ├── templates/
│       └── defaults/
├── playbooks/
│   └── deploy.yml
├── group_vars/
│   └── all.yml
├── PLANNING.md
└── TASK.md
```
