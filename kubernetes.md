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

### deletes

```sh
kubectl delete deploy [deploy-name]
kubectl delete service [service-name]
kubectl delete secret [secret-name]
kubectl delete ingress [ingress-name]
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
