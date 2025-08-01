Start the main site.yml playbook using:
`ansible-playbook -i inventory.ini site.yml --ask-vault-password`

Our project's architecture could go cleaner by separating roles in different directories such as `roles/tests`, `roles/system`, etc. 
We would then have to call the playbooks in `site.yml` using `tests/role_1`, `system/role_2`...

---

Roles checklist:  
DONE - check_services – Checks the status of essential system services like sshd

DONE - copy_file – Copies a file from the controller to the target machines

DONE - update_packages – Updates all packages depending on the distro

DONE - create_admin – Creates ansible_admin sudo user with a hashed password

DONE - configure_firewall – Installs UFW and sets rules for 2002, 80 and 443 ports

DONE - filebeat_snort – Installs Filebeat using a template and enables system and auditd modules, installs Snort with minimal configuration for network monitoring

DONE - compliance_check – Checks permissions, users without passwords, and permissive directories

DONE - system_hardening – Applies settings in sysctl.conf, strengthens PAM, hardens SSH, removes useless users, hardens system globally (disables avahi, cups)

DONE - incident_response – Simulates incident response

DONE - vault_example – Testing ansible vault

DONE - collect_facts – Gathers system facts and displays OS and RAM
