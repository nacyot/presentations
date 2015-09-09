footer: Kubernetes 101 © nacyot 2014 -
slidenumbers: true

# [fit] Kubernetes
# [fit] 101

---

# [fit] GDG Devfair 2014
### 2014. 11. 29.
### 2015. 09. 09. update

---

![fit](http://i.imgur.com/BVz3cIx.png)

---

# ![inline 350%](http://www.smartstudy.co.kr/static/image/icon/company.png)

## Daekwon Kim
### SMARTSTUDY Software & System Engineer

---
 ![fit](https://qiita-image-store.s3.amazonaws.com/0/27361/9f2c228d-75bf-ce84-09fc-0ff1f565acea.png)

---

# Node

* Host Machine
  * 가상 머신
  * 물리 머신
* 컴퓨터 단위
* etcd로 클러스터링

---

# Conatainer

* Host 위에서 실행되는 격리된 프로세스
  * LXC(LinuX Container)
  * Docker Container
  * ...

---

# Pod

* Kubernetes에서 사용하는 배포단위
  * 하나의 서비스를 구성하는 Container들
  * Kubelet 형식으로 선언

---

# Kubelet

* Pod 선언 파일
* https://cloud.google.com/compute/docs/containers/container_vms#container_manifest

```
version: v1beta2      // Required.
containers:           // Required.
  - name: string        // Required.
    image: string       // Required.
```

---

# 기타

* Label
* Proxy
* Kubernetes API Server
* etcd

---

# END

---

# Kubernetes on CoreOS Example

https://gist.github.com/YungSang/6177b69f1754f0590dbe

---

# vagrant up

$ vagrant status
discovery                 running (virtualbox)
master                    running (virtualbox)
minion-1                  running (virtualbox)
minion-2                  running (virtualbox)

---

# Servers

* discovery - etcd Server
* master - kubernetes API server
* minion-1 - CoreOS Node1
* minion-2 - CoreOS Node2

---

# Install kubecfg

$ curl -OL http://storage.googleapis.com/kubernetes/darwin/kubecfg
$ chmod +x kubecfg
$ sudo mv kubecfg /usr/local/bin
$ kubecfg --version
Kubernetes v0.3-dev

---

# Set kubernetes API server

$ vagrant ssh-config master > ssh.config
$ ssh -f -nNT -L 8080:127.0.0.1:8080 -F ssh.config master
$ kubecfg list pods
ID                  Image(s)            Host                Label               Status
----------          ----------          ----------          ----------          ----------

# redis-master.json

{
  "id": "redis-master-2",
  "kind": "Pod",
  "apiVersion": "v1beta1",
  "desiredState": {
    "manifest": {
      "version": "v1beta1",
      "id": "redis-master-2",
      "containers": [{
        "name": "master",
        "image": "dockerfile/redis",
        "ports": [{
          "containerPort": 6379,
          "hostPort": 6379
        }]
      }]
    }
  },
  "labels": {
    "name": "redis-master"
  }
}

---

# Run redis-master

$ kubecfg -c redis-master.json create pods
$ kubecfg list pods
ID                  Image(s)            Host                Labels              Status
----------          ----------          ----------          ----------          ----------
redis-master-2      dockerfile/redis    192.168.12.11/      name=redis-master   Waiting

---

# 이하 생략

---

# 참조
* https://github.com/GoogleCloudPlatform/kubernetes/blob/master/DESIGN.md
* https://gist.github.com/YungSang/6177b69f1754f0590dbe
* https://coreos.com/blog/running-kubernetes-example-on-CoreOS-part-1
* https://coreos.com/blog/running-kubernetes-example-on-CoreOS-part-2
   
