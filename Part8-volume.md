## 建立有 volume 的 Pod
```bash
# volume-empty.yaml

---
apiVersion: v1
kind: Pod
metadata:
  name: volume-empty-nginx
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - mountPath: /tmp/conf  # 將 empty-volume 掛載到 /tmp/conf 下
      name: empty-volume
  volumes:
  - name: empty-volume
    emptyDir: {}            # 指定為 emptyDir 
``` 

## 部署 Pod 至 k8s

```bash
$ kubectl apply -f volume-empty.yaml
``` 

## 進入 bash 模式
```bash
$ kubectl exec -it volume-empty-nginx bash
root@volume-empty-nginx:/# ls -al /tmp
```
你會發現有個 conf 資料夾
