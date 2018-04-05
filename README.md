

## Kubernetes:

[pods](pod-example-page.md)

`kubectl port-forward grafanademo 8081:3000`

[services](services-example-page.md)

[replicaset](rs-example-page.md)

`cambia la imagen de un pod ;) y curl script`

#IMAGEN : wardviaene/k8s-demo

`kubectl delete pod`

`kubectl delete rs`

[deployment](deployment-example-page.md)


Labels:

`kubectl get nodes --show-labels`

Healthchecks:

```YAML  livenessProbe:
          httpGet:
            path: /
            port: grafana-port
          initialDelaySeconds: 15
          timeoutSeconds: 30```





