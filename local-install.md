```
$ kind create cluster --name awx-test --config cluster-with-nodeport.yaml
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
$ kubectl config set-context --current --namespace=awx
$ export VERSION=2.17.0
$ kubectl apply -k .
$ kubectl create -f awx-cr.yaml
$ echo $(kubectl -n awx get secret awx-demo-admin-password -o jsonpath='{.data.password}' | base64 -d)
```
