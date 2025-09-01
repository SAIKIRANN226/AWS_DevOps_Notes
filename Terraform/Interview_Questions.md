### What is terraform and why we use it ?
Terraform is popular IaC. It is best in the market because of its advantages like V,C,A,I,C,A,M,H

### Ansible vs Terraform when to use ? What is the purpose ?
Ansible is a popular configuration management tool. We can automate the configuration inside the servers using ansible. We write playbooks for that and these playbooks are version controlled in Git, since our source code is also Git. Ansible can also create infrastructure but it is very poor in updating infra or deleting infra because state is not available in ansible while terraform does. So thats why terraform is best for creating infra and ansible is best in configuring the servers, so we integrate this terraform with ansible. Once terraform create servers, it can handover for configuration to ansible.

### 
