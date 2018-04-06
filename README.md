

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
    app: database
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

```YAML
apiVersion: v1
kind: Service
metadata:
  name: database-service
spec:
  ports:
  - port: 3306
    protocol: TCP
  selector:
    app: database
  type: NodePort

```

```YAML
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: helloworld-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: helloworld-db
    spec:
      containers:
      - name: k8s-demo
        image: wardviaene/k8s-demo
        command: ["node", "index-db.js"]
        ports:
        - name: nodejs-port
          containerPort: 3000
        env:
          - name: MYSQL_HOST
            value: database-service
          - name: MYSQL_USER
            value: root
          - name: MYSQL_PASSWORD
            valueFrom:
              secretKeyRef:
                name: helloworld-secrets
                key: rootPassword
          - name: MYSQL_DATABASE
            valueFrom:
              secretKeyRef:
                name: helloworld-secrets
                key: database

```

```YAML
apiVersion: v1
kind: Service
metadata:
  name: helloworld-db-service
spec:
  ports:
  - port: 3000
    protocol: TCP
  selector:
    app: helloworld-db
  type: NodePort

```

**Volumes**:

Permite que los datos persitan.

**Pet Set**:

Permite establecer un nombre fijo para un pod a la hora de acceder a recursos de manera estática.

**Daemon Sets**:

Definir el pod que se va a ejecutar en todos los nodos. (cAdvisor)

**Autoscaler**:

[https://github.com/kubernetes/heapster/archive/master.zip](https://github.com/kubernetes/heapster/archive/master.zip)

https://github.com/kubernetes-incubator/metrics-server/archive/master.zip(https://github.com/kubernetes-incubator/metrics-server/archive/master.zip)



