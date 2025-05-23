# TASK.md

## Purpose
Tracks current tasks, backlog, and sub-tasks for the repmgr-ansible project.

---

## Active Work
- [x] Planning phase: Define high-level vision, architecture, constraints, tools, and project structure (see PLANNING.md)
- [x] Set up initial project directory structure
- [x] Create data-driven approach for cluster configuration (avoiding code duplication)
- [x] Implement role task files (preflight, repositories, postgresql, etc.)
- [x] Add FQCN requirements to cursor rules
- [x] Create Jinja2 templates for configuration files
- [ ] Research best practices for running multiple PostgreSQL clusters with repmgr on RedHat
- [ ] Test basic deployment on test VMs

## Backlog
- [x] Create Ansible inventory and variable files for multi-cluster support
- [x] Develop Ansible role for PostgreSQL + repmgr cluster management
- [x] Implement templated configuration for postgresql.conf and repmgr.conf
- [ ] Add tasks for user, database, and systemd service management per cluster
- [ ] Add repmgr cluster registration and failover setup
- [ ] Test on multiple RedHat-based VMs/containers
- [ ] Document usage and customization

## Milestones
- Project structure and planning complete
- Basic Ansible playbook and role skeleton in place
- Single cluster deployment working
- Multi-cluster deployment working
- repmgr integration and failover tested
- Documentation finalized

## Notes / Discoveries
- Need to ensure systemd service naming does not conflict between clusters
- SELinux and firewall configuration may require special handling
- Official PostgreSQL and repmgr repositories support multiple versions
- Implemented data-driven cluster configuration to avoid code duplication
- Using postgresql_clusters dictionary in all.yml for scalable cluster definitions
- Current cluster detection uses group_names to dynamically set cluster-specific variables
- All Ansible modules now use FQCN (Fully Qualified Collection Names) for best practices
- Role task files implemented: preflight, repositories, postgresql, repmgr, configuration, services, cluster_init, standby
- Template files created: postgresql.conf, pg_hba.conf, repmgr.conf, systemd services, monitoring scripts
- Complete role structure with handlers, defaults, and documentation
