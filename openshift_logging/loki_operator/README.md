This is a manual to install OpenShift Logging using OpenShift Logging, Loki Operator and Cluster Observability Operator
OpenShift Logging version: 6.1.0
Loki Operator version: 6.1.0
Cluster Observability Operator: 0.4.1

- Install Operators from Operator Hub
- Create secret for LokiStack instance
oc apply -f logging-loki-s3
- Deploy a LokiStack instance
oc apply -f loki-stack.yaml
- Create service account
oc create sa collector -n openshift-logging
- Bind the ClusterRole to the service account
oc adm policy add-cluster-role-to-user logging-collector-logs-writer -z collector
- Create a UIPlugin to enable the Log section in Web Console
oc apply -f uiplugin.yaml
- Add additional roles to the service account
oc project openshift-logging
oc adm policy add-cluster-role-to-user collect-application-logs -z collector
oc adm policy add-cluster-role-to-user collect-audit-logs -z collector
oc adm policy add-cluster-role-to-user collect-infrastructure-logs -z collector
- Create a ClusterLogForwarder
oc apply -f cluster_log_forwarder.yaml
