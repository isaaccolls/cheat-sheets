- [kubectl](#kubectl)
  - [KONG](#kong)
- [test pod](#test-pod)

# kubectl

- ensure installed version is up-to-date `kubectl version --client`
- list all pods in the namespace: `kubectl get pods`
- show logs: `kubectl logs -f [pod-name]`
- show multiple pods logs: `kubectl logs -f deployment/<app-name> --all-containers=true`
- show secrets: `kubectl get secrets`
- list all services in the namespace: `kubectl get services`
- describe commands with verbose output: `kubectl describe pods my-pod`
- entrar a la Shell de un POD: `kubectl exec -it [POD_NAME] -- sh`
- filtrar variables de entorno del POD (inside Shell): `printenv | grep -i database`
- get deployments: `kubectl get deployments`
- restart deployment: `kubectl rollout restart deployment [deployment_name]`
- get all resources: `kubectl get all -n studytonight`
- pods memory utilization: `kubectl top pod`
- copy local file to remote pod in namespace: `kubectl cp <file-src> <some-namespace>/<some-pod>:<file-dest>`
- port forward: `kubectl port-forward pods/hermes-redis-865c5c9757-npprf 6378:6379 -n hermes`
- persisten volume claim: `kubectl get pvc`
- delete pods: `kubectl delete pod $(kubectl get pods | grep "\<chatbot-backend\>" | awk '{print $1}')`
  - watch: `watch -n 5 "kubectl delete pod $(kubectl get pods | grep "\<chatbot-backend\>" | awk '{print $1}')"`
- display pod usage: `kubectl top pod [pod_name]`
- delete all pods from deployment:
  - `kubectl delete pods --selector=app=[deployment_name]`
  - `kubectl delete pods -l app=vortex-executor`
- show secret: `kubectl get secret request-to-hermes-inbox-consumer-key-1 -o jsonpath="{.data.key}" | base64 --decode`
- show hpa info `kubectl get hpa vortex-studio-frontend -o yaml`
- port forward: `kubectl port-forward request-to-hermes-inbox-864d9b54b4-pjn6t 8082:3000`

## consumo de pods individuales

- Ver métricas de todos los pods en el namespace actual: `kubectl top pods`
- Ver métricas de pods específicos del deployment: `kubectl top pods -l app=request-to-hermes-inbox`
- Ver métricas con más detalles (incluyendo límites y requests): `kubectl top pods --containers`
- Ver métricas de un pod específico: `kubectl top pod <nombre-del-pod>`

## Para ver el consumo promedio del deployment

- Ver métricas de todos los pods del deployment con labels específicos: `kubectl top pods -l app=request-to-hermes-inbox --no-headers | awk '{cpu+=$2; mem+=$3; count++} END {print "Promedio CPU: " cpu/count "m", "Promedio Memoria: " mem/count "Mi"}'`
- Ver métricas de todos los pods y calcular promedio manualmente: `kubectl top pods -l app=request-to-hermes-inbox`
- Ver métricas de nodos: `kubectl top nodes`

## información detallada de recursos:

- Ver requests y limits configurados: `kubectl describe deployment request-to-hermes-inbox`
- Ver información detallada de los pods: `kubectl describe pods -l app=request-to-hermes-inbox`

### deletes

```sh
kubectl delete deploy [deploy-name]
kubectl delete service [service-name]
kubectl delete secret [secret-name]
kubectl delete ingress [ingress-name]
kubectl delete hpa [hpa-name]
kubectl delete cronjob [cronjob-name]
kubectl get all | grep [app-name] # and delete all that 💩
# check for kong and delete...
kubectl get kongingress
kubectl get kongconsumer
kubectl get kongplugin
```

## KONG

- show kongingress: `kubectl get kongingress`
- `kubectl get kongconsumer`
- `kubectl get kongingress set-app -o yaml`
- `kubectl delete kongconsumer push-set-app-consumer`
- `kubectl delete ingress request-to-hermes`
- `kubectl get kongplugin`

# test pod

- create debug pod: `kubectl run -i --rm --tty ic-test --image=ubuntu:20.04 --restart=Never --env="NODE_OPTIONS=--max-old-space-size=2048" --limits=memory=4G -- sh`
  <!-- - `kubectl create deployment ic-test --image=ubuntu:20.04 --replicas=1` -->
  <!-- - create debug pod: `kubectl run -i --rm --tty ic-test --image=ubuntu:20.04 --restart=Never -- sh` -->
- update and install all required packages: `apt-get update -yq && apt-get install -yq curl git vim`
- install node: `curl -sL https://deb.nodesource.com/setup_16.x | bash - && apt-get install -yq nodejs build-essential`
- `export NODE_OPTIONS="--max-old-space-size=2048"`
  - check it: `node -e 'console.log(v8.getHeapStatistics().heap_size_limit/(1024*1024))'`
- `kubectl apply -f ubuntu-as-pod.yaml`
