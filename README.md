
###Create Namespace
`kubectl apply -f ./michelle-helm-chart/namespace.yml`

###helm install
The following command deploys the application. To see the actual kubernetes
specification ouput add `--dry-run`.
`helm install michelle-test ./michelle-helm-chart`

Once the helm chart is successfully deployed, it should say
```
Get the application URL by running these commands:
http://test.michelleheh.com/
```
However, that URL won't work until the [DNS is setup for the load balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/using-domain-names-with-elb.html).

You can see the load balancer's external IP with:
`kubectl get services`

###helm uninstall
`helm uninstall michelle-test` destroys the deployment.
`kubectl get pods` should show that the pod is getting terminated.
`kubectl delete -f ./michelle-helm-chart/namespace.yaml` deletes the namespace.

###ckr iie deploy
`ckr iie deploy` looks at the `.gitops` directory and uses `helmfile.yaml` as an entry
point. Once the service is up and running, you can port forward to localhost
with the following command:
```
kubectl port-forward service/reserved-8-michelle-node-app-michelle-helm-chart 4200:80 -n <my-namespace>
```
You should see `Hello Michelle!` with `curl localhost:4200`


###ckr iie destroy
Cleans up the deployment.