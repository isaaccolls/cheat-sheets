- [kubectl](#kubectl)

# kubectl

- ensure installed version is up-to-date `kubectl version --client`
- list all pods in the namespace: `kubectl get pods`
- show logs: `kubectl logs -f [pod-name]`
- show multiple pods logs: `kubectl logs -f deployment/<app-name> --all-containers=true`
- delete deploy: `kubectl delete deploy [app-name]`
- delete pod: `kubectl delete pod [pod]`
- show secrets: `kubectl get secrets`
- list all services in the namespace: `kubectl get services`
- describe commands with verbose output: `kubectl describe pods my-pod`
- entrar a la Shell de un POD: `kubectl exec -it [POD_NAME] -- sh`
- filtrar variables de entorno del POD (inside Shell): `printenv | grep -i database`
- get all resources: `kubectl get all -n studytonight`

## KONG

- show kongingress: `kubectl get kongingress`
- `kubectl get kongconsumer`
- `kubectl get kongingress set-app -o yaml`
- `kubectl delete kongconsumer push-set-app-consumer`
- `kubectl delete ingress request-to-hermes`
