

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

```YAML  
livenessProbe:
     httpGet:
     path: /
     port: grafana-port
     initialDelaySeconds: 15
     timeoutSeconds: 30
```

Secrets:

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: helloworld-secrets
type: Opaque
data:
  username: aGVsbG93b3JsZA==
  password: cGFzc3dvcmQ=
  rootPassword: cm9vdHBhc3N3b3Jk
  database: aGVsbG93b3JsZA==
```

Service Discovery:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: database
  labels:
    *app: database*
spec:
  containers:
  - name: mysql
    image: mysql:5.7
    ports:
    - name: mysql-port
      containerPort: 3306
    env:
      - name: MYSQL_ROOT_PASSWORD
        valueFrom:
          secretKeyRef:
            name: helloworld-secrets
            key: rootPassword
      - name: MYSQL_USER
        valueFrom:
          secretKeyRef:
            name: helloworld-secrets
            key: username
      - name: MYSQL_PASSWORD
        valueFrom:
          secretKeyRef:
            name: helloworld-secrets
            key: password
      - name: MYSQL_DATABASE
        valueFrom:
          secretKeyRef:
            name: helloworld-secrets
            key: database
```



