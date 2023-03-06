# kubernetes-playground

*DEPLOYMENT - KUBERNETES*

kubectl get deploy -n [namespace] -> los deploy que hay en el namespace
kubectl create -f [fiile-name.yml] -> crea a partir de archivo
kubectl apply -f [deploy-definition.yml] -> crea a partir de archivo
kubectl delete deployment [deploymentname] -> (in yml file > metadata: name: deploymentname)
kubectl delete deployment [deploymentname] -n [namespace] -> (in yml file > metadata: name: deploymentname)
kubectl delete deploy [deploymentname] -> shortcut
kubectl describe deployment -n [namespace] [deploymentname]
kubectl edit deployment [deploymentname] -n [namespace]
kubectl get rs -> lista los replicasets

*NODES - KUBERNETES*

kubectl get nodes
kubectl describe node
kubectl label nodes [node-name>]  [label-key]=[label-value] -> agrega labels a nodos
kubectl get nodes --show-labels -> muestra los nodos con sus labels

*LOGS - KUBERNETES*

kubectl logs [nombre-pod] -n [namespace] -> obtener logs
kubectl logs [podname] -c [container-name] -> obtiene logs de un container en particular que esta en un pod con mas de un container

*PODS - KUBERNETES*

kubectl get pods (de donde estoy parado)
kubectl get pods --namespace=kube-system
kubectl get pods -n kube-system -> shortcut
kubectl get pods --all-namespaces
kubectl get pods -o wide -> mas info
kubectl describe pod [pod- name]
kubectl run [pod-name] --image=[image-name:tag]
kubectl create -f [pod-definition.yml] -> crea pod a partir de yml
kubectl exec -it [pod-name] -- sh -> abre una consola contextualizada en el pod
kubectl delete -f [pod-definition.yml]
kubectl delete pod [pod-name]
kubectl delete pod [pod-name] --wait=false -> te da la consola sin esperar a que termine de borrar
kubectl delete pod [pod-name] --grace-period=0 --force -> le rompe toda la gorra al pod al toque
kubectl get pods --selector=[key]=[value] -o wide -> obtiene los pods que tienen esa label
kubectl exec -it [podname] -c [container-name] -- sh -> para acceder a la consola de un container (en un pod con mas de 1 container)

*DEAMONSET - KUBERNETES*

kubectl apply -f [deamonset-definition.yml]
kubectl get ds
kubectl describe ds
kubectl delete -f [deamonset-definition.yml]
kubectl delete ds [ds-name]

*JOB - KUBERNETES*

kubectl create job [jobName] --image=busybox -> The imperative way
kubectl apply -f [definition.yaml] -> Create a Job
kubectl get job -> List jobs
kubectl describe job [jobName] -> Get info
kubectl delete -f [definition.yaml] -> Delete a job
kubectl delete job [jobName] -> Delete using the Job name

*CRONJOB - KUBERNETES*

kubectl create cronjob [jobName]--image=busybox --schedule="*/1 * * * *" bin/sh -c "date;" -> The imperative way
kubectl apply -f [definition.yaml] -> Create a CronJob
kubectl get cj -> List CronJobs
kubectl describe cj [jobName] -> Get info 
kubectl delete -f [definition.yaml] -> Delete a CronJob
kubectl delete cj [jobName] -> Same but using the CronJob name

*ROLLOUT -KUBERNETES*

kubectl apply -f [definition.yaml] -> Update a deployment
kubectl rollout status -> Get the progress of the update
kubectl rollout status deployment/[deployment-name] -> status del rollout del deployment
kubectl rollout history deployment [deploymentname] -> Get the history of the deployment
kubectl rollout undo [deploymentname] -> Rollback a deployment
kubectl rollout undo [deploymentname]-to-revision=[revision#] -> Rollback to a revision number

*PERSISTENT VOLUME - KUBERNETES*

kubectl get pv
kubectl delete pv --all

*SERVICE - KUBERNETES*

kubectl get ep myservice -> endpoint del service

ClusterIP
kubectl expose po [pod-name] --port=80 --target-port=8080 --name=[service-name] -> create service
kubectl expose deploy [deploy-name] --port=80 --target-port=8080 --name=[service-name] -> service expose a deployment
kubectl  apply -f [service-def.yml] -> deploy service from file
kubectl get svc -> get service list
kubectl get svc -o wide -> mucha info
kubectl describe svc [service-name] -> describe service
kubectl delete -f [service-def.yml] -> delete service
kubectl delete svc [service-name] -> delete the service using name
NodePort (30000-32767)
kubectl expose po [podName] --port=80--target-port=8080 --type=NodePort -> Create a service to expose a pod
kubectl expose deploy [deployName] -- port=80 --target -port =8080 --type=NodePort --name=frontend  -> Create a service to expose a deployment
