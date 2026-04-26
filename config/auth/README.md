### Requirements
- htpasswd file
#### Get htpasswd binary
Based on RHEL
dnf install -y httpd-tools

#### Create a htpasswd file
htpasswd -c -B -b htpasswd <user> <password>

- kustomization
#### Apply manifests
Create secret using secret generator
```
oc apply -k .
```
 Get secret name
 ```
 oc get secret -n openshift-config | grep htpass
 ```
 Complete oauth.yaml file with secret name and apply manifest
 ```
 oc apply -f oauth.yaml
 ```
 Verify changes
```
watch oc get pods -n openshift-authentication
```
