
```YAML
apiVersion: v1
kind: Pod
metadata:
  name: grafanademo
  labels:
    app: hellografana
spec:
  containers:
  - name: k8s-demo
    image: grafana/grafana:4.6.3
    ports:
    - name: grafana-port
      containerPort: 3000
```
[Descargar pod-yaml.yml](https://github.com/alu0100885613/kubernetes-examples/blob/master/pod-yaml.yml)

[<< Atrás](README.md)
