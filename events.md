---
layout: page_select
entry: events
permalink: events.html
---


<header class="major">
  <h2> Upcoming and previous events </h2>
</header>

{% assign today = site.time | date: '%s' %}
{% assign events_sorted = site.events | sort: 'date' | reverse %}


<div class="bibliography">
  {% for entry in events_sorted %}
    {% assign start = entry.date | date: '%s' %}
    {% assign seconds_since = today | minus: start %}
    {% assign hours_since = seconds_since | divided_by: 60 | divided_by: 60 %}
    {% assign days_since = hours_since | divided_by: 24 %}
    {% if days_since < site.expiration_events %}
        <li>
          <div class="text-justify  {{entry.cat | replace: " ", "-" | downcase}}">
            <b>{{entry.date | date: '%-d %B %Y' }}</b>
            {% if entry.presentation_url %}
              <a href="{{entry.presentation_url}}" class="icon fa-download" target="_blank"><span class="label">URL</span></a>
            {% endif %}
            <br/>
            {{entry.author}}: {{entry.title}}
            <p> {{entry.teasing}} </p>
          </div>
        </li>
    {% endif %}
  {% endfor %}
</div>
<hr>


