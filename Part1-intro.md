## 介紹
Kubernetes (k8s) 的出現，讓管理容器更簡潔方便。

## Container
每個 Container(容器) 都是獨立的個體，能夠選定某個執行環境以及版本，是具有高效率(啟動一個容器只需短短幾秒)、可擴充(動態新增或刪除容器)、個別獨立的應用程式(容器間可相互溝通但不會干擾各自的運作)，此外容器可以部署在許多不同的環境中例如：本機、雲端伺服器、虛擬機...等，不但增加便利性也提升開發上的效能，每位開發者不必再為了架設環境或是不相容問題而煩惱此外更能確保跨平台的一致性。

## Container Orchestration
隨著容器的增加面對的是成千上百個容器的維運，要如有效的何管理超大規模容器叢集(Cluster)呢？Container Orchestration 便是能幫助我們解決龐大叢集的問題！ Orchestration 涵蓋了三大功能包括了服務管理機制、排程管理機制和資源管理機制
，常見的兩個 Container Orchestrator 分別為 [Kubernetes (k8s)](https://kubernetes.io/) 與 [docker swarm](https://docs.docker.com/engine/swarm/)。

- 容器的自動化部署
- 自動化擴展或者縮容
- 自動化應用/服務升級
- 容器成組，對外提供服務，支持負載均衡
- 服務的健康檢查，自動重啟

## Kubernetes(k8s) 架構
kubernetes(縮寫成k8s）是google 開源的一套自動化容器管理平台用於容器的部署、自動化調度和集群管理。
![k8s](https://ithelp.ithome.com.tw/upload/images/20171220/20107062oNprEAL4ks.png)

k8s 包含了三個元件 Master Nodes、Worker Nodes、etcd

## 入坑 k8s 
k8s 是 [開源專案](https://github.com/kubernetes)並且開源源於 GitHub，有三種安裝使用方式如下：

- 手動安裝
- 使用雲端平台(GCP、AWS、Azure)
- minikube

三個各有優缺點，其中我將使用 minikube 來做以下教學，原因是 minikube 非常適合對初學者在本機來做測試上手用，然而 minikube 必須運行在虛擬環境下所以在開始前我們需要在本機上安裝虛擬機，這邊我選擇 VirtualBox 優點在於跨平台 Linux
、Mac OS、Windows 皆可使用。

### 1. 安裝 VirtualBox
首先到 [VirtualBox](https://www.virtualbox.org/) 官網下載相對應系統的安裝檔。
### 2. 安裝 kubectl
kubectl 是一個用來與 k8s 叢集溝通的二進位 (binary) 工具。我們可以透過 kubectl 對 minikube 下達命令。

- Linux
收先確認系統內沒有 curl，可透過下列指令安裝:
```bash
$ sudo apt-get install curl
```

使用以下命令下載最新版本:
```bash
$ curl -LO curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

製作kubectl二進制可執行文件:
```bash
chmod +x ./kubectl
```

將二進制移入你的PATH以利執行:
```bash
 sudo mv ./kubectl /usr/local/bin/kubectl
```

- Mac OS
使用 brew 安裝 kubectl：

```bash
$ brew install kubectl
```

- Windows
請至這裡下載 [exe](https://storage.googleapis.com/kubernetes-release/release/v1.10.0/bin/windows/amd64/kubectl.exe) 執行檔。

詳細可參考告版本的[安裝指引](https://kubernetes.io/docs/tasks/tools/install-kubectl/)


安裝完成後，可用下列指令確認 kubectl 版本:
```bash
$ kubectl version
```

### 3. 安裝 minikube
minikube 是由 Google 發布的一個輕量級工具。讓開發者可以在本機上輕易架設一個 Kubernetes Cluster，快速上手 Kubernetes 的指令與環境。
- Linux
使用 curl 安裝 minikube:
```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

- Mac OS
使用 brew 安裝 minikube:
```bash
$ brew cask install minikube
```

- Windows
請至這裡下載 [exe](https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe) 執行檔並將檔案改名為 `minikube.exe`。


安裝完成後，可用下列指令確認 kubectl 版本:
```bash
$ minikube version
```


## 本文回顧
- 在本機中安裝 VirtualBox, kubectl 與 minikube
