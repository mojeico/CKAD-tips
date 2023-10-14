

# KUBERNETES COMMANDS


# POD
* Generate pod without create - `kubectl run nginx --image nginx --dry-run=client -o yaml`
* Connect to pod - `kubectl exec -it pod-name -- sh`
* Connect to temporary pod - `kubectl run -it --rm --image=busybox:1.28.4 busybox -- sh`
* Replace pod - `kubectl replace -f pod-definition.yaml --force`
* Export logs from pod - `kubectl logs nginx-pod > nginx.log`
* Create pod with command sleep - `kubectl run busybox --image=busybox --restart=Never --command -- sleep 1000`
* Create pod with labels - `kubectl run nginx --image=nginx  --labels="app=nginx,env=prod"`
* Create pod and expose port (--expose - craete service) - `kubectl run nginx --image=nginx --port=80 --dry-run=client -o yaml`

# DEPLOYMENT
* Crate deployment with replicas - `kubectl create deployment nginx-deploy --image=nginx:1.16 --replicas=4 --dry-run=client -o yaml`
* Scale deployment - `kubectl scale deployment nginx-deploy --replicas=4`
* Update image of deployment - `kubectl set image deployment/nginx-deploy nginx-deploy=nginx:1.17`
* Add env from secret - `kubectl set env --from=secret/ldh-secret666 deployment/ldhsecretapp`
* Add env from configmap - `kubectl set env --from=secret/ldh-secret666 deployment/ldhsecretapp`
* Add env - `kubectl set env deployment/ldhsecretapp STORAGE_DIR=/data`


# ROLLOUT
* Rollout deployment image - `kubectl rollout undo deployment/nginx-deploy`
* Get rollout history - `kubectl rollout history deployment/nginx-deploy --revision=1`
* Rollout to revision - `kubectl rollout undo deployment/nginx-deploy --to-revision=1`


# CONFIGMAP SECRET 
* Create configmap with value from command - `kubectl create configmap my-config-map --from-literal=APP_COLOR=blue --from-literal=APP_MOD=prod`
* Create configmap from file - `kubectl create configmap my-config-map --from-file=app_config.properties`
* Create configmap from file - kubectl create configmap configmap-web-moon-html --from-file=index.html=/opt/course/15/web-moon.html  # important to set the index.html key
* Create secret - `kubectl create secret generic my-secret --from-literal=DB_PASSWORD=password`
* Get token value from secret - `kubectl get secret <secret_name> -o jsonpath={.data.token} | base64 -d`

# CRONJOB JOB
* Create cronjob that run every minute - `kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * *" `
* Create cronjob - `kubectl create cronjob show-data --schedule="*/1 * * * *" --image=busybox  -- /bin/sh -c 'echo "current date: $(date)"'`
* Create job - `kubectl create job busybox --image=busybox --dry-run=client -o yaml --`


# SERVICE
* Create service for deployment - `kubectl expose deployment nginx-deploy --port=80 --target-port=80 --name=nginx-service --type=NodePort`



# INGRESS
* Create ingress with host - `kubectl create ingress ingress-vh-routing --rule="watch.ecomstore/video=video-service:30093"`


# SERVICE ACCOUNT
* Create service account - `kubectl create serviceaccount dashboard-sa`


# ROLE 
* Create role - kubectl create role scaler --verb=get --resource=deployments --resource-name=purple 


# CLUSTER ROLE AND CLUSTER ROLE BINDING

* Create clusterrole - `kubectl create clusterrole pvviewer-role --verb=list --resource=PersistentVolumes`
* Crate clusterrolebinding for service - `kubectl create clusterrolebinding pvviewer-role-binding --clusterrole=pvviewer-role --serviceaccount=default:pvviewer`




# NODE LABELS
* Taint node - `kubectl taint nodes node-name key=value:NoSchedule`
* Set label to node - `kubectl label nodes node-name key=value`
* Set label to pod - `kubectl label pod -l type=runner protected=true`
* Get pod with labels - `kubectl get pod --show-labels`


# QUOTA
* Create quota - `kubectl create quota my-quota --hard=cpu=1,memory=1G,pods=2,services=2,replicationcontrollers=2,resourcequotas=1,secrets=1,persistentvolumeclaims=1`

# HELM
* Helm chart list in namespace  - `helm -n mercury ls`
* Helm update repo - `helm repo update`


* Helm list repo - `helm repo list`
* Helm search release - `helm search repo nginx`
* Helm add bitnami repo - `helm repo add bitnami https://charts.bitnami.com/bitnami`
* Helm install chart from bitnami repo - `helm install mynode bitnami/node  --set replicaCount=5 --version 19.1.6`
* Helm upgrade chart from bitnami repo - `helm upgrade mynode bitnami/node --set replicaCount=5 `
* Helm history - `helm history mynode`
* Helm rollback - `helm rollback mynode 1`
* Helm uninstall - `helm uninstall mynode`

