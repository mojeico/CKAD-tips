

# PODS 

* Create pod - `kubectl run nginx --image nginx`
* Create pod with port + create service - `kubectl run nginx --image nginx --port=80 --expose`



# CONFIG MAP 

* Create configmap - `kubectl create configmap my-config-map --from-literal=APP_COLOR=blue --from-literal=APP_MOD=prod`




# SECRETS 

* Create secret - `kubectl create secret generic my-secret --from-literal=DB_PASSWORD=password --from-literal=DB_USER=user`


# SERVICE ACCOUNT 

* Create service account - `kubectl create serviceaccount my-service-account`


# TAINT TOLERATION 

* taint - mark node with label  - taint=blue    - `kubectl taint nodes node-name key=value:taint-effect`  - `kubectl taint nodes node01 spray=mortein:NoSchedule`
* toleration - allow (not make) scheduler schedule pod to node with taint 

# LABEL NODE

* create label for node - `kubectl label nodes node1 label-key=label-value` 


# AFFINITY

* affinity - schedule pod to node with some label 


#  Readiness and Liveness Probes

* Readiness - will stop our application from serving traffic
* Liveness  - will restart the container


# Selectors (search by label)

* Get with labels - `kubectl get all --selector env=prod,bu=finance,tier=frontend`

# Deployment rollout and update 

* Rollback to previous revision - `kubectl rollout undo deployment deployment-a`
* Update image - `kubectl set image deployment deployment-name container-name=nginx:1.9.1` - `kubectl set image deployment.apps/deployment-a deployment-a=nginx:1.9.1`


# Service 

* NodePort  - open port on all nodes - it needs - nodePort, targetPort and port 
* ClusterIP - service get virtual ip inside cluster 
* LoadBalancer - public ip for service 


# Ingress

* Ingress - is a collection of rules that allow inbound connections to reach the cluster services

# Egress

* Egress - is a collection of rules that allow outbound connections from the cluster


# Network Policy

* Network Policy - is a specification of how groups of pods are allowed to communicate with each other and other network endpoints



# Volumes

* Persistent Volume - is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes
* Persistent Volume Claim - is a request for storage by a user


# Role for user 

* Create role - `kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods`
* Create role binding - `kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user`

# Role for service account

* Create role - `kubectl create role service-account-role --namespace=default --verb=list,create,delete --resource=pods`
* Create role binding - `kubectl create rolebinding dev-user-binding --namespace=default --role=service-account-role --serviceaccount=default:dev-user`
* Create service account - `kubectl create serviceaccount dev-user`






















