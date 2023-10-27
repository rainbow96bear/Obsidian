# **1. MAC 주소란?**

MAC은 Media Access Control의 약자  
2계층 통신을 위해 네트워크 인터페이스에 할당된 고유 식별자  
네트워크에 접속하는 모든 장비는 MAC주소가 있어야 한다.

## 표현 방법

48비트를 사용하며 16진수를 활용하여 총 12자리로 표현
ex) AB . 5C . 19 . AA . BB . 77

OUI - 앞의 24비트 즉 앞의 6자리 -> IEEE에서 제조사에 할당  
UAA - 뒤의 24비트 즉 뒤의 6자리 -> 제조사에서 할당

NIC는 전송받은 정보의 MAC주소를 해석하여 목적지 MAC주소가 자기자신인 경우, 브로드 캐스트, 멀티 캐스트 등의 경우만 정보를 상위 계층으로 전달

# **2. IP 주소란?**

IP는 Internet Protocol의 약자  
ex) 192.168.0.1 -> 1100 0000 . 1010 1000 . 0000 0000 . 0000 0001

## 특징

사용자가 변경 가능한 논리 구조
그룹을 의미하는 네트워크 주소와 호스트 주소가 존재

## 클래스 개념

A클래스, B클래스, C클래스 등으로 호스트의 IP 개수에 따라 크기를 다르게 할당하는 개념

## 클래스 리스 개념 (서브네팅)

서브넷 마스크를 사용하여 네트워크 주소와 호스트 주소를 구별

### ex

IP 주소 : 135 . 135 . 135 . 135  
서브넷 마스크 :

- 1111 1111 . 1111 1111 . 1111 1111 . 1100 0000 <=> 255.255.255.192
- 135.135.135.135/26

## 서브넷 마스크로 네트워크 주소와 호스트 주소 확인

<table border="1">
<thead>
<tr>
<th align="left"></th>
<th align="center" style="padding: 10px;">2진법</th>
<th align="center" style="padding: 10px;">10진법</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left" style="padding: 10px;">IP 주소</td>
<td align="center" style="padding: 10px;">1000 0111 . 1000 0111 . 1000 0111 . 1000 0111</td>
<td align="center" style="padding: 10px;">135.135.135.135</td>
</tr>
<tr>
<td align="left" style="padding: 10px;">서브넷 마스크</td>
<td align="center" style="padding: 10px;">1111 1111 . 1111 1111 . 1111 1111 . 1100 0000</td>
<td align="center" style="padding: 10px;">255.255.255.192</td>
</tr>
<tr>
<td align="left" style="padding: 10px;">네트워크 주소</td>
<td align="center" style="padding: 10px;">1000 0111 . 1000 0111 . 1000 0111 . 1000 0000</td>
<td align="center" style="padding: 10px;">135.135.135.128</td>
</tr>
<tr>
<td align="left" style="padding: 10px;">브로드캐스트 주소</td>
<td align="center" style="padding: 10px;">1000 0111 . 1000 0111 . 1000 0111 . 1011 1111</td>
<td align="center" style="padding: 10px;">135.135.135.191</td>
</tr>
</tbody>
</table>

사용 가능한 호스트 IP는 네트워크 주소보다 크고 브로드 캐스트 주소보다 작은 IP  
ex) 호스트 IP : 135.135.135.129 ~ 135.135.135.190

## IP 주소를 통하여 통신하는 방법

- **유니 캐스트** - 1:1로 통신, 출발지와 도착지가 정해져있다.
- **애니 캐스트** - 1:1로 통신, 동일 그룹(네트워크 주소 동일) 중 가장 가까운 호스트에서 응답
- **브로드 캐스트** - 1:모두로 통신, 동일 그룹내의 모든 호스트가 목적지
- **멀티 캐스트** - 1:그룹으로 통신, 다수의 특정 목적지로 데이터 전송
