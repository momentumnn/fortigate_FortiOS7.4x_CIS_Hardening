# FortiGate FortiOS7.4x CIS Hardening

Automated CIS Hardening solution for FortiGate firewalls using Ansible.

## Features

- ✅ Automated configuration backups
- ✅ Device information documentation
- ✅ Audit logging

## Quick Start

### 1. Install Prerequisites
```bash
pip3 install ansible fortiosapi
ansible-galaxy collection install -r requirements.yaml
```

### 2. Configure Credentials
```bash
export FORTIGATE_USER="admin"
export FORTIGATE_PASSWORD="YourPassword"
```

### 3. Update Inventory

Edit `hosts.yaml` and update IP addresses for your FortiGate devices.

### 4. Run Audit
```bash
# Audit all devices
ansible-playbook playbooks/forti_audit.yaml

# Audit specific group
ansible-playbook playbooks/forti_audit.yaml --limit production_fortigates

# Audit single device
ansible-playbook playbooks/forti_audit.yaml --limit fw-prod-01
```

### 5. Run Hardening
```bash
# Harden all devices
ansible-playbook playbooks/forti_general_settings.yaml

# Harden specific group
ansible-playbook playbooks/forti_general_settings.yaml --limit production_fortigates

# Harden single device
ansible-playbook playbooks/forti_general_settings.yaml --limit fw-prod-01
```


## Directory Structure
```
fortigate-backup/
├── ansible.cfg
├── backup_fortigate.yaml
├── hosts.yaml
├── requirements.yaml
├── group_vars/
│   ├── all.yaml
│   └── fortigates/
│       ├── vars.yaml
│       └── vault.yaml
├── host_vars/
│   ├── fw-prod-01.yaml
│   ├── fw-prod-02.yaml
│   ├── fw-branch-01.yaml
│   ├── fw-branch-02.yaml
│   └── fw-dmz-01.yaml
├── playbooks/
│   ├── backups/
│   ├── forti_add_trust_host.yaml
│   ├── forti_audit.yaml
│   ├── forti_backup.yaml
│   ├── forti_general_settings.yaml
│   ├── forti_logging.yaml
│   ├── forti_security_profiles.yaml
│   └── get.yaml
```

## Configuration

### Global Settings (group_vars/all.yaml)

- `backup_dir`: Backup storage location
- `retention_days`: Default retention period
- `backup_timestamp`: Timestamp format

### FortiGate Settings (group_vars/fortigates/vars.yaml)

- Connection parameters (HTTPS, SSL, timeouts)
- Authentication configuration
- FortiGate-specific settings

### Per-Device Settings (host_vars/)

- Device metadata (site, location, role)
- Custom retention periods
- Device-specific overrides

## Security

- Use Ansible Vault for credential storage
- Set appropriate file permissions
- Secure backup directory
- Use dedicated API user with read-only access

## Troubleshooting

### Test Connectivity
```bash
ansible fortigates -m fortinet.fortios.fortios_monitor_fact -a "selector=system_status"
```

### Check Variables
```bash
ansible-inventory --host fw-prod-01
```

### Verbose Output
```bash
ansible-playbook forti_xxx.yaml -vvv
```

## License

MIT

## Author

Ehsan Momeni Bashusqeh, Network Automation Engineer