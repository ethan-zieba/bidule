Roles checklist:  
check_services – Checks the status of essential system services like sshd

copy_file – Copies a file from the controller to the target machines

update_packages – Updates all packages depending on the distro

create_admin_user – Creates ansible_admin sudo user with a hashed password

configure_firewall – Installs UFW and sets rules for 2002, 80 and 443 ports

install_filebeat – Installs Filebeat using a template and enables system and auditd modules

compliance_check – Checks permissions, users without passwords, and permissive directories

DONE - system_hardening – Applies settings in sysctl.conf, strengthens PAM, hardens SSH, removes useless users, hardens system globally (disables avahi, cups)

install_snort – Installs Snort with minimal configuration for network monitoring

incident_response – Simulates incident response

vault_example – Testing ansible vault

DONE - collect_facts – Gathers system facts and displays OS and RAM
