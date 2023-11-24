# **1. Config Map이란?**
설정 데이터를 저장하고 관리하기 위한 리소스

<img src="/assets/Pasted image 20231123034254.png">

### 리터럴 값으로 Config Map 생성
<code>kubectl create configmap sleep-config-literal --from-literal=kiamol.section='4.1'</code>   
키 : kiamol.section   
값 : 4.1

### 파일을 통한 Config Map 생성
<code>kubectl create configmap sleep-config-env-file --from-env-file-sleep/ch04.env
</code>
```env
KIAMOL_CHAPTER=ch04
KIAMOL_SECTION=ch04-4.1
KIAMOL_EXERCISE=try it now
```

### 파드 생성과 함께 Config Map 읽기 & 생성
<code>kubectl apply -f https://raw.githubusercontent.com/gilbutITbook/kiamol/main/ch04/sleep/sleep-with-configMap-env-file.yaml
</code>

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
          envFrom:
          - configMapRef:
              name: sleep-config-env-file
          env:
          - name: KIAMOL_CHAPTER
            value: "04"
          - name: KIAMOL_SECTION
            valueFrom:
              configMapKeyRef:              
                name: sleep-config-literal
                key: kiamol.section
```

### env 출력
<code>kubectl exec deploy/sleep -- sh -c 'printenv | grep "^KIAMOL"'</code>
<img src="/assets/KakaoTalk_20231124_222216874.jpg">

# **2. Secret이란?**
주로 민감한 정보를 컨피그맵보다 안전하게 노출을 최소화 시키는 방법입니다.

### 리터럴로 Secret 생성
<code>kubectl create secret generic sleep-secret-literal --from-literal=secret=rainbowbear</code>

### Secret 출력
- 단순 출력
<code>kubectl get secret sleep-secret-literal -o jsonpath="{.data.secret}"</code>
- base64 디코딩
<code>kubectl get secret sleep-secret-literal -o jsonpath="{.data.secret}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }
</code>

<code>kubectl get secret sleep-secret-literal -o jsonpath="{.data.secret}" | base64 -d</code>

<img src="/assets/스크린샷 2023-11-24 220129.png">
# **3. 4장 리뷰**
쿠버네티스에서 컨피그맵과 Secret을 생성하여 환경변수를 다루는 방법에 대한 내용이었습니다.
컨피그맵과 Secret을 생성하는 다양한 예시가 있었고 이에 따라 적용되는 우선 순위가 다르다는 것을 확인할 수 있는 예시까지 있었습니다.
입문하는 입장에서 다소 어려울 수 있는 내용들을 가볍게 이해하고 넘어가기에 부족함 없는 내용인 점에서 좋았습니다.
