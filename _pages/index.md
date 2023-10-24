---
layout: page
title: Home
id: home
permalink: /
---

# 무지개곰의 개발자 공부 기록! 🌱

<p style="padding: 3em 1em; background: #f5f7ff; border-radius: 4px;">
  <div>
    당당한 개발자가 되기 위한 자기 분석
    <span style="font-weight: bold">[[자기 소개]]</span>
  </div>
  <div>
    기본을 쌓기 위한 기초공부 계획
    <span style="font-weight: bold">[[CS 6대 과목 공부 계획]]</span>
  </div>
</p>

<div>
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
</style>
