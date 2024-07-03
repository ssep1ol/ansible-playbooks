# ansible-playbooks
This repository contains a collection of useful Ansible playbooks for various tasks, which are described below:

- **cve-2024-6387-mitigation.yaml**:
  - This is a simple Ansible playbook for mitigation of CVE-2024-6387 vulnerability on OpenSSH on an inventory of machines of your choice.
  - Your Ansible user needs to have the necessary grants for sudoing on remote machines.
  - There is also a basic Jenkinsfile in case you want to launch the Ansible playbook through a Jenkins instance.
