# codefresh_test

instructions:
1. vagrant up
2. ansible-playbook deploy-prometheus.yml -t prometheus -i $PWD/.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory
3. vagrant ssh k8s-master
4. kubectl port-forward -n monitoring --address 0.0.0.0 svc/prometheus-service 8080:8080
5. http://192.168.50.10:8080

test cases:
1. apt update && apt install stress-ng &&  stress-ng --vm-bytes $(awk '/MemAvailable/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --vm-keep -m 1
2. yes > /dev/null &