# tst-argo-config

## Initial Start Notes
(1) Create namespace to contain Argo CD then (2) install into cluster:
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.14.10/manifests/install.yaml
```

Service starts only exposed to the cluster so you have to port forward to your local machine to be able to access the Web UI of the Argo Service.

Port forward with:
`kubectl port-forward svc/argocd-server -n argocd 8080:443`

Access from your browser:
http://localhost:8080

Default username is `admin` and password is from the Kubernetes service:
Linux and Mac:
`kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode; echo`
Windows:
`kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }`

