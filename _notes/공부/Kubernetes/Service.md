# **서비스(Service)란?**
파드에서 발생되는 통신 트래픽의 라우팅을 맡는 리소스   
여러 Pod를 그룹화 하여 하나의 가상 주소 IP로 통신

## 내부 파드(Pod)간 통신

<img src="/assets/Pasted image 20231121215555.png">

### 실습 환경   
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch03/numbers/api.yaml -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch03/numbers/web.yaml
</code>

- api.yaml   
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: numbers-api
spec:
  selector:
    matchLabels:
      app: numbers-api
  template:
    metadata:
      labels:
        app: numbers-api
    spec:
      containers:
        - name: api
          image: kiamol/ch03-numbers-api
```

- web.yaml   
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: numbers-web
spec:
  selector:
    matchLabels:
      app: numbers-web
  template:
    metadata:
      labels:
        app: numbers-web
    spec:
      containers:
        - name: web
          image: kiamol/ch03-numbers-web
```

### 서비스 구축   
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch03/numbers/api-service.yaml
</code>


```yaml
apiVersion: v1
kind: Service
metadata:
  name: numbers-api
spec:
  ports:
    - port: 80
  selector:
    app: numbers-api
  type: ClusterIP
```
### 포트포워딩   
<code>kubectl port-forward deploy/numbers-web 8080:80</code>


## 외부 트래픽을 파드로 전달

<img src="/assets/Pasted image 20231121220827.png">

### LoadBalancer 서비스
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch03/numbers/web-service.yaml</code>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: numbers-web
spec:
  ports:
    - port: 8080
      targetPort: 80
  selector:
    app: numbers-web
  type: LoadBalancer
```


## 외부로 트래픽 전달

<img src="/assets/Pasted image 20231121221023.png">

### ExternalName 서비스

<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch03/numbers-services/api-service-externalName.yaml</code>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: numbers-api
spec:
  type: ExternalName
  externalName: raw.githubusercontent.com
```

# **3장 리뷰**
실습 자료가 제공되어 자칫하면 복잡하고 어려울 내용들을 실습을 통하여 직접 서비스를 생성해 보며 배울 수 있어서 좋았습니다.
각 서비스마다 용도는 무엇인지 어떠한 상황에서 사용되는지에 대한 짧은 설명이 있었던 점도 좋았습니다.
단순히 외부로 트래픽을 보내는 서비스만 설명한다면 종종 '그래서 이걸 어떠한 상황에 쓰지?, 중요한 내용인가?' 등의 의문을 가질 수 있는데 짧은 설명들이 중간 중간 들어있어 이해하는데 더 도움이 되었습니다.