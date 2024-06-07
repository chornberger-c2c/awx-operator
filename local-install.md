```
# for Nodeport
$ kind create cluster --name awx-test --config cluster-with-nodeport.yml
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
$ kubectl config set-context --current --namespace=awx
$ export VERSION=$(curl  "https://api.github.com/repos/ansible/awx-operator/tags" 2>/dev/null | jq -r '.[0].name')
$ kubectl apply -k .
$ kubectl create -f awx-cr.yaml
$ echo $(kubectl -n awx get secret awx-demo-admin-password -o jsonpath='{.data.password}' | base64 -d)

# for Ingress
$ kind create cluster --name awx-test --config cluster-with-ingress.yml
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
$ kubectl config set-context --current --namespace=awx
$ export VERSION=$(curl  "https://api.github.com/repos/ansible/awx-operator/tags" 2>/dev/null | jq -r '.[0].name')
$ kubectl apply -k .
$ kubectl apply -f awx-cr-with-ingress.yml
$ kubectl apply -f awx-ingress.yml
$ echo $(kubectl -n awx get secret awx-demo-admin-password -o jsonpath='{.data.password}' | base64 -d)
```
