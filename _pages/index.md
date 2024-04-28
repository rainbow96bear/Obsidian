---
layout: page
title: Home
id: home
permalink: /
---

# 🌈 무지개곰의 포트폴리오
<div>
전공 : 전기공학   
공부중인 스택 : Golang, MongoDB, GraphQL   
사용해본 언어 : TypeScript, JavaScript, C++, JAVA   
사용해본 프레임 워크 : Express(Node.js)   
사용해본 DB : MySQL   

<h4>진행중인 목표</h4>

<ul>프로젝트 경험 쌓기
	<ul>Dex 사이트 개발에 참여하여 Golang을 활용한 block scan 작업 진행중 - [[dex 사이트 개발]]</ul>
</ul>

<h4>달성한 목표</h4>

<ul>SQLD에 도전하여 DBMS의 기본기 다지기 - 2023.12 취득</ul>
<ul>기본 영어 회화를 위한 Opic IM2 - 2023.08달성</ul>
<ul>공모전 도전 (컴투스 [[붕빵이 유니버스 공모전]] - 2024.06.12 발표 예정)</ul>

<h4>배우고 싶은 기술스택</h4>

<h5>Golang</h5>
선택 이유 :
<ul><b>스스로 학습할 수 있다는 것을 증명하기 위하여 새로운 언어에 대한 도전</b></ul>
<ul>Docker, Kubernetes, Geth등 다양한 서비스들이 Golang을 활용한다는 점</ul>
<ul>goroutine라는 경량 쓰레드에 대한 관심</ul>

<h5>Docker, Kubernetes</h5>
선택 이유 :
<ul>네트워크에 대한 전반적인 지식을 쌓을 수 있을 것으로 기대</ul>
<ul>프로젝트 배포 및 관리에 유용할 것이라고 생각되어 실무에서 강점을 가질 수 있을 것으로 기대</ul>

<h4> 프로젝트 기록 </h4>
	<ul style="font-weight: bold">
		<span style="font-weight: bold">[[dex 사이트 개발]]</span>
	</ul>
	<ul style="font-weight: bold">
		<span style="font-weight: bold">[[Prism (포트폴리오 공유 SNS)]]</span>
	</ul>
	<ul style="font-weight: bold">
		<span style="font-weight: bold">[[GIF 변환기]]</span>
	</ul>
	<ul style="font-weight: bold">
		<span style="font-weight: bold">[[NFT를 위한 SNS]]</span>
	</ul>
	
<h4> 공모전 </h4>
	<ul>
		<span style="font-weight: bold">
		[[붕빵이 유니버스 공모전]] - 결과 발표 2024.06.12
		</span>
	</ul>
	
<h4> 공부 기록 </h4>
	<ul style="font-weight: bold">기본을 쌓기 위한 CS 공부 : 
		<span style="font-weight: bold">[[CS 6대 과목]]</span>
	</ul>
	<ul style="font-weight: bold">무중단 배포를 위한 쿠버네티스 공부 : 
		<span style="font-weight: bold">[[Kubernetes 공부 기록]]</span>
	</ul>

<h4>활동</h4>
	<ul>
		<span style="font-weight: bold">
		[[10억 줄 처리 챌린지]]
		</span>
	</ul>
	<ul>
		<span style="font-weight: bold">
		[[위퍼블릭 DAO 활동]]
		</span>
	</ul>
	<ul>
		<span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/%EC%B2%B4%ED%97%98%EB%8B%A8-2023-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EB%88%84%EB%A6%AC%EB%8B%A8-%EB%A6%AC%EC%82%AC%EC%9D%B4%ED%81%B4-%EB%A0%9B%EC%A0%80-%EC%B2%B4%ED%97%98-%ED%9B%84%EA%B8%B0">블록체인 누리단</a>
		</span>
	</ul>

<h4> 기록 </h4>
	<ul>
		<span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/">개발 공부 기록 블로그</a></span>
	</ul>
	<ul>
		<span style="font-weight: bold"><a href="https://creal-news.tistory.com/">레거시 블로그</a></span>
	</ul>
	<ul>
		<span style="font-weight: bold"><a href="https://brunch.co.kr/@rainbowbear">리더십 독서 기록</a></span>
	</ul>
<h3>
	<span style="font-weight: bold"><a href="https://github.com/rainbow96bear">Github</a></span>
</h3>
<br>
<br>
</div>


<div class="graph_background">
<div>{% include notes_graph.html %}</div>
</div>

<strong>Recently updated notes</strong>

<ul>
{% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
{% for note in recent_notes limit: 5 %}
<li>
{{ note.last_modified_at | date: "%Y-%m-%d" }} — <a class="internal-link" href="{{ note.url }}">{{ note.title }}</a>
</li>
{% endfor %}
</ul>

<style>
.wrapper {
max-width: 46em;
}
.graph_background {
border: 1px solid black;
}
</style>
