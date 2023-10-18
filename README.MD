

# KUBERNETES COMMANDS


# POD
* Generate pod without create - `kubectl run nginx --image nginx --dry-run=client -o yaml`
* Connect to pod - `kubectl exec -it pod-name -- sh`
* Connect to temporary pod - `kubectl run -it --rm --image=busybox:1.28.4 busybox -- sh`
* Replace pod - `kubectl replace -f pod-definition.yaml --force`
* Export logs from pod - `kubectl logs nginx-pod > nginx.log`
* Get logs form previous pod - `kubectl logs nginx -p`
* Create pod with command sleep - `kubectl run busybox --image=busybox --restart=Never -- sleep 1000`
* Create pod with labels - `kubectl run nginx --image=nginx  --labels="app=nginx,env=prod"`
* Create pod and expose port (--expose - craete service) - `kubectl run nginx --image=nginx --port=80 --dry-run=client -o yaml`


# COPY FROM POD 
* Create pod - `kubectl run pod_name --image=busybox --restart=Never -- sleep 3600`
* Copy - `kubectl cp pod_name:/etc/passwd ./passwd # kubectl cp command`


# DEPLOYMENT
* Crate deployment with replicas - `kubectl create deployment nginx-deploy --image=nginx:1.16 --replicas=4 --dry-run=client -o yaml`
* Scale deployment - `kubectl scale deployment nginx-deploy --replicas=4`
* Update image of deployment - `kubectl set image deployment/nginx-deploy nginx-deploy=nginx:1.17`
* Add env from secret - `kubectl set env --from=secret/ldh-secret666 deployment/ldhsecretapp`
* Add env from configmap - `kubectl set env --from=configmap/config-map-1 deployment/ldhsecretapp`
* Add env - `kubectl set env deployment/ldhsecretapp STORAGE_DIR=/data`


# AUTO SCALE (HPA)
* Autoscale the deployment - `kubectl autoscale deploy nginx --min=5 --max=10 --cpu-percent=80`


# ROLLOUT
* Rollout deployment image - `kubectl rollout undo deployment/nginx-deploy`
* Get rollout history - `kubectl rollout history deployment/nginx-deploy --revision=1`
* Rollout to revision - `kubectl rollout undo deployment/nginx-deploy --to-revision=1`

# EVENTS
* Get events - `kubectl get events`


# CONFIGMAP SECRET 
* Create configmap with value from command - `kubectl create configmap my-config-map --from-literal=APP_COLOR=blue --from-literal=APP_MOD=prod`
* Create configmap from file - `kubectl create configmap my-config-map --from-file=app_config.properties`
* Create configmap from file - `kubectl create configmap configmap-web-moon-html --from-file=index.html=/opt/course/15/web-moon.html`  # important to set the index.html key
* Create configmap from env file - `kubectl create configmap test-env --from-env-file=env-file.env`
* Create secret - `kubectl create secret generic my-secret --from-literal=DB_PASSWORD=password`
* Get token value from secret - `kubectl get secret <secret_name> -o jsonpath={.data.token} | base64 -d`


# JOB CRONJOB
* Create job - `kubectl create job busybox --image=busybox --dry-run=client -o yaml `
* Create job from cronjob - `kubectl create job --from=cronjob/sample-cron-job sample-job`
* Create cronjob that run every minute - `kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * *"`
* Create cronjob - `kubectl create cronjob show-data --schedule="*/1 * * * *" --image=busybox  -- /bin/sh -c 'echo "current date: $(date)"'`


# SERVICE
* Create NodePort service for deployment - `kubectl expose deployment nginx-deploy --port=80 --target-port=80 --name=nginx-service --type=NodePort`


# INGRESS
* Create ingress with host - `kubectl create ingress ingress-vh-routing --rule="watch.ecomstore/video=video-service:30093"`


# SERVICE ACCOUNT
* Create service account - `kubectl create serviceaccount dashboard-sa`


# ROLE 
* Create role - `kubectl create role scaler --verb=get --resource=deployments --resource-name=purple`


# CLUSTER ROLE AND CLUSTER ROLE BINDING

* Create clusterrole - `kubectl create clusterrole pvviewer-role --verb=list --resource=PersistentVolumes`
* Crate clusterrolebinding for service - `kubectl create clusterrolebinding pvviewer-role-binding --clusterrole=pvviewer-role --serviceaccount=default:pvviewer`

- role         - List all pods in a namespace
- cluster role - List all pods in all namespaces. Get a list of all nodes and theis public IP.


# TAINT 
* Taint node - `kubectl taint nodes node-name key=value:NoSchedule`
* Untaint node - `kubectl taint node node-name key-`

# NODE LABELS
* Set label to node - `kubectl label nodes node-name key=value`
* Set label to pod - `kubectl label pod type=runner protected=true`
* Get pod with labels - `kubectl get pod --show-labels`
* Get pod with specific label - `kubectl get po -l app=v2` 
* Remove label - `kubectl label po nginx tier-`

# Annotation 
* Add annotation to pod - `kubectl annotate po nginx1 nginx2 nginx3 description='my description'`
* Remove annotation - `kubectl annotate po nginx description-`

# QUOTA
* Create quota - `kubectl create quota my-rq --hard=requests.cpu=1,requests.memory=1Gi,limits.cpu=2,limits.memory=2Gi,pods=10,secrets=10`



# HELM
* Helm chart list in namespace  - `helm -n mercury ls`
* Helm update repo - `helm repo update`

* Create helm chart - `helm create chart`
* Helm install (local) - `helm install myredis ./redis` 


* Helm list repo - `helm repo list`
* Helm search release - `helm search repo nginx`
* Helm add bitnami repo - `helm repo add bitnami https://charts.bitnami.com/bitnami`
* Helm show values - `helm show values bitnami/node`
* Helm install chart from bitnami repo - `helm install mynode bitnami/node  --set replicaCount=5 --version 19.1.6`
* Helm upgrade chart from bitnami repo - `helm upgrade mynode bitnami/node --set replicaCount=5 `
* Helm history - `helm history mynode`
* Helm rollback - `helm rollback mynode 1`
* Helm uninstall - `helm uninstall mynode`


