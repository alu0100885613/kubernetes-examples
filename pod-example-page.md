
```YAML
apiVersion: v1
kind: Pod
metadata:
  name: nodehelloworld.example.com
  labels:
    app: helloworld
spec:
  containers:
  - name: k8s-demo
    image: wardviaene/k8s-demo
    ports:
    - name: nodejs-port
containerPort: 3000
```
[Descargar pod-yaml.yml](https://github.com/alu0100885613/kubernetes-examples/blob/master/pod-yaml.yml)

[<< Atrás](README.md)
