# 使用 Google Compute Engine(GCE)

由上角點開 Cloud Shell

查詢專案ID
```bash
$ gcloud projects list
```

進入到該專案中
```bash
$ gcloud config set project quapni-quapni
```

指定 (compute zone)
```bash
$ gcloud config set compute/zone asia-east1-b
```

建立 k8s
```bash
$ gcloud container clusters create test
```
