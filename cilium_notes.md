#get status

cilium status --wait
cilium status

#enable hubble

cilium hubble enable --ui
cilium status --wait 

#conectivity test

cilium connectivity test --request-timeout 30s --connect-timeout 10s

#examine cluster with kubectl

kubectl get nodes
kubectl get daemonsets --all-namespaces
kubectl get deployments --all-namespaces

#connect to cilium
#start tunnel in host
kubectl -n kube-system port-forward svc/hubble-ui 12000:80
#connect via ssh from remote host
ssh -L 12000:127.0.0.1:12000 user@cilium-host


#gateway api, checar microcurso;

kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/latest/download/standard-install.yaml
kubectl get crds | grep gateway
istioctl install –set profile=default
kubectl apply -f https://github.com/istio/istio/releases/latest/download/gateway.yaml
