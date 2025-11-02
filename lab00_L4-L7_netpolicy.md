kubectl create -f https://raw.githubusercontent.com/cilium/cilium/HEAD/examples/minikube/http-sw-app.yaml
kubectl get svc
kubectl get pods,CiliumEndpoints
kubectl exec xwing -- curl -s -XPOST deathstar.default.svc.cluster.local/v1/request-landing
kubectl exec tiefighter -- curl -s -XPOST deathstar.default.svc.cluster.local/v1/request-landing
kubectl describe pod/xwing

#create l4 policy file and apply

kubectl apply -f allow-empire-in-namespace.yaml
kubectl get ciliumnetworkpolicies -A


#test policy

kubectl exec xwing -- curl --connect-timeout 10 -s -XPOST deathstar.default.svc.cluster.local/v1/request-landing
kubectl exec tiefighter -- curl --connect-timeout 10 -s -XPOST deathstar.default.svc.cluster.local/v1/request-landing
kubectl exec tiefighter -- curl -s -XPUT deathstar.default.svc.cluster.local/v1/exhaust-port

