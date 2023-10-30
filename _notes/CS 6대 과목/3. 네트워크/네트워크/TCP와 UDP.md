# **1. TCP란?**

정보 유실이 없는 통신을 보장하기 위하여 패킷에 번호를 부여하고 잘 전송되었는지 응답 번호로 확인하는 방식
SYN, ACK 활용

## 3방향 핸드셰이크

정보 유실을 방지하기 위한 사전 연결 작업
3번의 패킷을 주고 받으며 통신을 준비하여 3방향 핸드셰이크

<img src="/assets/Pasted image 20231030171039.png">
   
   
## 윈도 사이즈, 슬라이딩 윈도

패킷을 보내고 응답을 확인하는 과정에서 왕복 지연 시간이 발생
이를 줄이기 위하여 한 번에 많은 패킷을 전달하는 방식이 존재

- **윈도 사이즈** : 한 번에 받을 수 있는 데이터 크기
- **슬라이딩 윈도** : 네트워크 상황에 따라 윈도 사이즈를 조절하는 것

<img src="/assets/Pasted image 20231030171109.png">

# **2. UDP란?**

TCP의 3방향 핸드셰이크를 사용하지 않는다.
멀티캐스트처럼 단방향으로 다수의 단말과 통신하여 응답받기 어려운 환경에서 주로 사용

# 비교

<table style="border-collapse: collapse; width: 100%;">
  <tr>
    <th style="padding: 10px; border: 1px solid black;">TCP</th>
    <th style="padding: 10px; border: 1px solid black;">UDP</th>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">연결지향</td>
    <td style="padding: 10px; border: 1px solid black;">비연결형</td>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">오류 제어 수행</td>
    <td style="padding: 10px; border: 1px solid black;">오류 제어 수행 X</td>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">흐름 제어 수행</td>
    <td style="padding: 10px; border: 1px solid black;">흐름 제어 수행 X</td>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">유니캐스트</td>
    <td style="padding: 10px; border: 1px solid black;">유니캐스트, 멀티캐스트, 브로드캐스트</td>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">전이중(Full Duplex)</td>
    <td style="padding: 10px; border: 1px solid black;">반이중(Half Duplex)</td>
  </tr>
  <tr>
    <td style="padding: 10px; border: 1px solid black;">데이터 전송</td>
    <td style="padding: 10px; border: 1px solid black;">실시간 트래픽 전송</td>
  </tr>
</table>
