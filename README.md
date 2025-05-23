# repmgr_cluster Role

This Ansible role automates the installation and configuration of PostgreSQL clusters with repmgr for high availability and automatic failover on RedHat-based systems.

## Features

- **Multi-cluster support**: Deploy multiple PostgreSQL clusters on the same hosts
- **Version flexibility**: Support for PostgreSQL versions 12-17
- **Automatic failover**: repmgr integration for cluster management
- **Data-driven configuration**: Easy cluster management through variables
- **FQCN compliance**: Uses fully qualified collection names for all modules

## Requirements

- RedHat-based operating system (RHEL, CentOS, Rocky, AlmaLinux)
- Ansible 2.9 or higher
- Sudo access on target hosts
- Network connectivity between cluster nodes

## Role Variables

### Cluster Configuration

Clusters are defined in `group_vars/all.yml` using the `postgresql_clusters` dictionary:

```yaml
postgresql_clusters:
  cluster1:
    cluster_name: cluster1
    cluster_id: 1
    postgresql_version: "15"
    postgresql_port: 5432
    repmgr_node_id_start: 1
    postgresql_max_connections: 100
```

### Default Variables

See `defaults/main.yml` for all available variables including:
- Security settings
- Performance tuning options
- Monitoring configuration
- Service settings

## Inventory Structure

```ini
[cluster1_primary]
pg1.example.com

[cluster1_standby]
pg2.example.com
pg3.example.com

[cluster1:children]
cluster1_primary
cluster1_standby
```

## Usage

1. Configure your inventory with primary and standby groups
2. Define cluster parameters in `group_vars/all.yml`
3. Run the playbook:

```bash
ansible-playbook -i inventories/hosts playbooks/deploy.yml
```

## Task Flow

1. **Preflight checks**: Validates configuration and system requirements
2. **Repositories**: Sets up PostgreSQL and EPEL repositories
3. **PostgreSQL installation**: Installs packages and initializes database
4. **repmgr setup**: Installs repmgr and configures SSH keys
5. **Configuration**: Generates all configuration files
6. **Services**: Manages systemd services
7. **Cluster initialization**: Sets up primary node (primary nodes only)
8. **Standby setup**: Clones data and registers standby (standby nodes only)

## Monitoring Scripts

The role creates monitoring scripts:
- `/usr/local/bin/check_postgresql_<version>.sh`
- `/usr/local/bin/check_repmgr_<version>.sh`

## Service Management

Services created:
- `postgresql-<version>`: PostgreSQL database service
- `repmgrd-<version>`: repmgr daemon service

## Files and Directories

- Configuration: `/etc/repmgr/<version>/repmgr.conf`
- Data: `/var/lib/pgsql/<version>/data`
- Logs: `/var/log/postgresql/<version>/` and `/var/log/repmgr/<version>/`
- Archives: `/var/lib/pgsql/archive`

## Troubleshooting

1. Check service status: `systemctl status postgresql-<version>`
2. Run monitoring scripts: `/usr/local/bin/check_postgresql_<version>.sh`
3. View logs: `journalctl -u postgresql-<version> -f`
4. Check cluster status: `repmgr cluster show`

## License

MIT

## Author

Vibe coding with Cursor.