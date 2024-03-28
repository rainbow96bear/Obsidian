---
layout: page
title: Home
id: home
permalink: /
---

# 🌈 무지개곰의 포트폴리오
<div>
  <ul style="font-weight: bold">목표 설정의 첫 단계 자기 분석 : 
    <span style="font-weight: bold">[[자기 분석]]</span>
  </ul>
  
  <h3> 프로젝트 기록 </h3>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[Prism (포트폴리오 공유 SNS)]]</span>
    </ul>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[GIF 변환기]]</span>
    </ul>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[OpenGSN 와 DefiScan 프로젝트 기록]]</span>
    </ul>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[NFT를 위한 SNS]]</span>
    </ul>
<h3> 공부 기록 </h3>
	   <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[ICP (Internet Computer Protocol)]]</span>
    </ul>
	  <ul>
		  <span style="font-weight: bold"><a href="https://www.youtube.com/channel/UCz7xhiKgrdhwFRxfvpnUriw">혼자하는 우테코</a></span>
	  </ul>
	  <ul>
		  <span style="font-weight: bold">[[아키텍처 공부]]</span>
	  </ul>
	  <ul style="font-weight: bold">기본을 쌓기 위한 CS 공부 : 
	    <span style="font-weight: bold">[[CS 6대 과목]]</span>
	  </ul>
	  <ul style="font-weight: bold">무중단 배포를 위한 쿠버네티스 공부 : 
	    <span style="font-weight: bold">[[Kubernetes 공부 기록]]</span>
	  </ul>
	  
  <h3>수상</h3>
	  <ul>블록체인 누리단 혁신 우수상</ul>
	  
  <h3>활동</h3>
	  <ul>
		  <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/%EC%84%9C%ED%8F%AC%ED%84%B0%EC%A6%88-%EC%9C%84%ED%8D%BC%EB%B8%94%EB%A6%AD-%EC%84%9C%ED%8F%AC%ED%84%B0%EC%A6%88-%EB%B0%9C%EB%8C%80%EC%8B%9D">위퍼블릭(DAO) 서포터즈</a></span>
	  </ul>
	  <ul>
		  <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/ICP-ICP-Hacker-House-%EC%B0%B8%EA%B0%80-%ED%9B%84%EA%B8%B0">ICP Hacker House 참가 후기</a></span>
	  </ul>
	  <ul>
		  <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/%EC%B2%B4%ED%97%98%EB%8B%A8-2023-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EB%88%84%EB%A6%AC%EB%8B%A8-%EB%A6%AC%EC%82%AC%EC%9D%B4%ED%81%B4-%EB%A0%9B%EC%A0%80-%EC%B2%B4%ED%97%98-%ED%9B%84%EA%B8%B0">블록체인 누리단</a></span></ul>
	  <ul>
		  <span style="font-weight: bold">[[ICT BC 고급 미니 프로젝트]]</span>
	  </ul>
	  <ul>길벗 리뷰어 : <span style="font-weight: bold">[[Kubernetes 공부 기록]]</span></ul>
	  <ul>
		  <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/%EA%B2%BD%EC%A7%84-%EB%8C%80%ED%9A%8C-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EB%82%9C%EC%A0%9C%ED%95%B4%EA%B2%B0-%EC%B1%8C%EB%A6%B0%EC%A7%80-%EC%A7%80%EC%9B%90">블록체인 난제해결 첼린지</a></span>
	  </ul>
	  <ul>
		  <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/entry/%ED%9B%84%EA%B8%B0-%EB%AF%B9%EC%8A%A4%EB%A7%88%EB%B8%94-%EB%B0%8B%EC%97%85-%ED%9B%84%EA%B8%B0-mixmarvel-meet-up">믹스마블 밋업</a></span>
	  </ul>
	  
  <h3> 블로그 </h3>
	   <ul>
		   <span style="font-weight: bold"><a href="https://rainbow96bear.tistory.com/">개발 공부 기록 블로그</a></span>
	   </ul>
	   <ul>
		   <span style="font-weight: bold"><a href="https://creal-news.tistory.com/">레거시 블로그</a></span>
	   </ul>
   <h3><span style="font-weight: bold"><a href="https://github.com/rainbow96bear">Github</a></span></h3>
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
