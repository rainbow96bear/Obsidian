# **1. 파드(Pod)란?**

- 쿠버네티스가 하나 또는 그 이상의 컨테이너를 관리하는 데 사용하는 단위
- 다른 리소스를 관리하고, 고 수준의 리소스는 컨테이너의 세부 사항을 추상화시킨다.
- 쿠버네티스로 관리되는 가상 IP로 가상 네트워크에 접속된 다른 파드와 통신 가능

쿠버네티스 구성 예시
<img src="/assets/Pasted image 20231120115928.png">

- **컨테이너 하나를 담은 파드 생성**   
<code>kubectl run 파드 이름 --image = 이미지 이름
</code>

- **클러스터에 있는 모든 파드의 목록 출력**   
<code>kubectl get pods
</code>

- **파드의 상세 정보 출력**   
<code>kubectl describe pod 파드 이름
</code>

- **포트 포워딩**   
<code>kubectl port-forward pod/파드이름 8080:80
</code>

- **파드 삭제**   
<code>kubectl delete pod 파드 이름
</code>

### CRI(Container Runtime Interface)
컨테이너 런타임과 통신하여 노드가 파드에 포함된 컨테이너를 관리하기 위한 인터페이스

# **2. 디플로이먼트(Deployment)란?**
파드를 주로 관리하는 컨트롤러 객체로 쿠버네티스 API를 사용하여 파드를 관리

- **디플로이먼트 생성 방법**   
<code>kubectl create deployment 디플로이먼트 이름 --image = 이미지 이름
</code>

- **포트 포워딩**   
<code>kubectl port-forward deploy/디플로이먼트이름 8080:80
</code>

- **디플로이먼트 삭제**   
<code>kubectl delete deploy 디플로이먼트 이름
</code>


# **3. 매니페스트**
JSON 또는 YAML 포맷으로 작성된 쿠버네티스의 오브젝트 정의를 담은 선언적 스크립트

- **매니페스트 파일로 애플리케이션 배포**   
<code>kubectl apply -f 매니페스트 파일명.포멧명
</code>
- **원격 URL에서 제공되는 매니페스트 파일로 애플리케이션 배포**   
<code>kubectl apply -f https://raw.githubusercontent.com/sixeyed/kiamol/master/ch02/pod.yaml
</code>   
   
위 주소의 파일 매니페스트 내용
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-kiamol-3
spec:
  containers:
    - name: web
      image: kiamol/ch02-hello-kiamol
```


## 파드와 컨테이너 부가 기능
- **파드 내부에 접근하기**   
<code>kubectl exec -it 파드 명 sh
</code>
- **파드의 로그 확인하기**   
<code>kubectl logs --tail=2 파드명
</code>
- **파드 속의 파일을 로컬 영역으로 복사**   
<code>kubectl cp 파드명:/복사할 파일경로/파일명 /저장할 로컬 경로/파일명
</code>


# 2장 리뷰
1장은 설치 방법과 책의 간략한 소개로 크게 리뷰로 남길게 없어 2장을 공부하며 리뷰를 남깁니다.

쿠버네티스의 가장 기본이라고 할 수 있는 파드와 디플로이먼트에 대한 설명과 함께 아래와 같은 시각적인 자료를 많이 제공한다는 점이 좋았습니다.

<img src="/assets/KakaoTalk_20231119_223947278.jpg">

명령어를 보여주고 설명만 존재하는 것이 아닌 아래와 같이 전체적인 내용을 보여주기에 이해하기도 편하고 각각의 결과마다 추가적인 설명을 통하여 이해를 도와준다는 점도 좋았습니다.

<img src="/assets/KakaoTalk_20231119_231811396.jpg">

2장까지의 내용에서는 아쉬운 점이 딱히 없었습니다.   
21장까지의 구성으로 이루어진 길벗의 **쿠버네티스 교과서**를 참고하여 매일 1장씩 공부하고 기록하며 리뷰하도록 하겠습니다.