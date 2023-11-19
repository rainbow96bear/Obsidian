---
layout: page
title: Home
id: home
permalink: /
---

# 🌈 무지개곰의 개발자 공부 기록!

<div>
  <h3> 목차 </h3>
  <ul style="font-weight: bold">목표 설정의 첫 단계 자기 분석 : 
    <span style="font-weight: bold">[[자기 소개]]</span>
  </ul>
  <ul style="font-weight: bold">기본을 쌓기 위한 기초공부 계획 : 
    <span style="font-weight: bold">[[CS 6대 과목 공부 계획]]</span>
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
