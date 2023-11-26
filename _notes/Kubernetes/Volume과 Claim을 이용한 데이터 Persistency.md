# **1. 볼륨**
볼륨은 Pod의 컨테이너들이 데이터를 공유하고 데이터를 보존하는 데 사용되는 저장소

## 볼륨의 종류
- emptyDir
- hostPath
- PersistentVolume / PersistentVolumeClaim

## emptyDir (공디렉터리)
데이터를 파드에 저장하는 볼륨으로, 생애 주기가 파드와 같아 컨테이너가 재 시작하는 경우 데이터를 잃지 않고 파드가 삭제되면 데이터를 잃는다.


<img src="Pasted image 20231126193347.png">

**매니페스트 예시**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sleep
spec:
  selector:
    matchLabels:
      app: sleep
  template:
    metadata:
      labels:
        app: sleep
    spec:
      containers:
        - name: sleep
          image: kiamol/ch03-sleep
          volumeMounts:
            - name: data
              mountPath: /data
      volumes:
        - name: data
          emptyDir: {}
```

## hostPath (호스트 경로)
데이터를 노드에 저장하는 볼륨으로, 파드가 재 시작되어도 데이터를 잃지 않는다.   

<img src="Pasted image 20231126193451.png">

**매니페스트 예시**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sleep
spec:
  selector:
    matchLabels:
      app: sleep
  template:
    metadata:
      labels:
        app: sleep
    spec:
      containers:
        - name: sleep
          image: kiamol/ch03-sleep
          volumeMounts:
            - name: node-root
              mountPath: /node-root
      volumes:
        - name: node-root
          hostPath:
            path: /
            type: Directory
```

## PV와 PVC
클러스터 수준에서 영구적인 스토리지를 관리하는데 사용되는 리소스

<img src="Pasted image 20231126212934.png">

### PV 생성
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/persistentVolume.yaml</code>

**persistentVolume.yaml**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv01
spec:
  capacity:
    storage: 50Mi
  accessModes:
    - ReadWriteOnce
  local:
    path: /volumes/pv01 
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
          - key: kiamol
            operator: In
            values:
              - ch05
```

### PVC 생성
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/postgres-persistentVolumeClaim.yaml</code>

**postgres-persistentVolumeClaim.yaml**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 40Mi
  storageClassName: ""
```
### 실습
#### sleep 파드 생성 (hostPath 볼륨)
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/sleep/sleep-with-hostPath.yaml</code>

#### local에 폴더 생성
<code>kubectl exec deploy/sleep -- mkdir -p /node-root/volumes/pv01</code>

#### local 폴더 속 자료 확인
<code>kubectl exec deploy/sleep -- ls -l /node-root/volumes/pv01/pg_wal</code>

#### 데이터베이스 파드 생성
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/postgres/todo-db-secret.yaml -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/postgres/todo-db.yaml</code>

#### 연결 로그 확인
<code>kubectl logs -l app=todo-db --tail 1</code>

#### pv01 속 파일 확인
<code>kubectl exec deploy/sleep -- sh -c 'ls -l /node-root/volumes/pv01| grep wal'</code>

#### to-do 웹 파드 생성
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/web/todo-web-configMap.yaml -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/web/todo-web-secret.yaml -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch05/todo-list/web/todo-web.yaml</code>


## mountPath와 subPath

mountPath : 컨테이너 내에 볼륨을 mount 할 경로를 지정
subPath : 볼륨 내의 특정 디렉터리나 파일을 지정

**예시**
```yaml
spec:
  containers:
  - name: my-container
    volumeMounts:
    - name: my-volume
      mountPath: /target/data
      subPath: source/data
```
my-volume의 /source/data의 내용을 my-container의 /target/data에 mount

# **2. 5장 리뷰**
지금까지의 내용 중 가장 어렵게 느껴졌습니다.
뒤로 갈수록 난이도가 오르겠지만 실습용 to-do web에서 오류가 발생하여 더욱 어렵게 느껴졌습니다.   
공부는 단순히 실습만 따라하는게 아니라 직접 활용하며 익혀가는 것이기에 기본 개념을 잡는다는 관점에서는 충분히 괜찮은 내용이기에 입문자에게는 좋은 책이라는 생각은 변하지 않습니다.   
앞으로 프로젝트를 준비하고 배포할 때 활용하며 온전한 제 것으로 만들겠습니다.   