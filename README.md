Ansible-4-Openshift-on-Proxmox

Playbook in action https://youtu.be/TBtNi4pi9pU

Commands post Ansible playbooks

# openshift-install --dir=/root/os4_installer wait-for bootstrap-complete --log-level=debug

Remove bootstrap node from loadbalancer 
# ansible-playbook tasks/cluster-after-bootstrap.yml


Login into OC, verify installation and set persistent storage for the registry

# export KUBECONFIG=/root/os4_installer/auth/kubeconfig
# oc whoami
# oc get nodes
# oc get csr
# oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"managementState":"Managed"}}'
# oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"storage":{"emptyDir":{}}}}'

# Monitor Operator Setup and wait for admin password 

# watch -n5 oc get clusteroperators 
# openshift-install --dir=/root/os4_installer wait-for install-complete --log-level=debug

