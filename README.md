# KUBE PROMETHEUS

Install all dependencies:
```
%> go get github.com/google/go-jsonnet/cmd/jsonnet
%> go get github.com/jsonnet-bundler/jsonnet-bundler/cmd/jb
%> go get github.com/brancz/gojsontoyaml
```
Get the kube prometheus jsonnet files:
```
%> jb install github.com/coreos/kube-prometheus/jsonnet/kube-prometheus@release-0.4
```
Get the example scripts:
```
%> wget https://raw.githubusercontent.com/coreos/kube-prometheus/master/build.sh
%> wget https://raw.githubusercontent.com/coreos/kube-prometheus/master/example.jsonnet
```
Build the manifests:
```
%> ./build.sh example.jsonnet
```
Edit `manifests/prometheus-prometheus.yaml` to add remote write:
```yaml
spec:
  remoteWrite:
    - url: "http://vminsert:8428/api/v1/write"
```
Apply the manifests:
```
%> apply -f manifests/setup
%> apply -f manifests
```