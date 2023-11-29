---
layout: page
title: Home
id: home
permalink: /
---

# 🌈 무지개곰의 포트폴리오

<div>
  <h3> 목차 </h3>
  <ul style="font-weight: bold">목표 설정의 첫 단계 자기 분석 : 
    <span style="font-weight: bold">[[자기 분석]]</span>
  </ul>
    <h3> 프로젝트 기록 </h3>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[OpenGSN 구축]]</span>
    </ul>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[Defi Scan 사이트]]</span>
    </ul>
    <ul style="font-weight: bold">
	    <span style="font-weight: bold">[[NFT를 위한 SNS]]</span>
    </ul>
  <h3> 공부 기록 </h3>
  <ul style="font-weight: bold">기본을 쌓기 위한 CS 공부 : 
    <span style="font-weight: bold">[[CS 6대 과목]]</span>
  </ul>
  <ul style="font-weight: bold">무중단 배포를 위한 쿠버네티스 공부 : 
    <span style="font-weight: bold">[[Kubernetes 공부 기록]]</span>
  </ul>
  <ul>
    [혼자하는 우테코](https://www.youtube.com/channel/UCz7xhiKgrdhwFRxfvpnUriw)
  </ul>
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
