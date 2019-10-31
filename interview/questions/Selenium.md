```
java -Dwebdriver.chrome.driver="/Users/jizheng/workspace/code/java/test/selenium-grid/chromedriver" -jar selenium-server-standalone-3.141.59.jar -role node -hub http://10.0.0.16:4444/grid/register/
```

```
export NODEPORT=`kubectl get svc --selector='app=selenium-hub' --output=template --template="{{ with index .items 0}}{{with index .spec.ports 0 }}{{.nodePort}}{{end}}{{end}}"`
export NODE=`kubectl get nodes --output=template --template="{{with index .items 0 }}{{.metadata.name}}{{end}}"`

curl http://$NODE:$NODEPORT
```

vi /etc/docker/daemon.json

```
{
  "registry-mirrors": ["https://gvoc8wgu.mirror.aliyuncs.com"]
}
```

```text
sudo systemctl daemon-reload
sudo systemctl restart docker
```

https://github.com/kubernetes/examples/tree/master/staging/selenium

http://k-master:32441/grid/console