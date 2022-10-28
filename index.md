---
title:
layout: default
permalink: /index.html
---

<br/>

<ul class="actions">
<center>
    <li><a href="{{site.url}}{{site.baseurl}}/events" class="button medium">Previous events</a></li>
    <li><a href="{{site.url}}{{site.baseurl}}/participating" class="button medium">Participating</a></li>
    <li><a href="{{site.url}}{{site.baseurl}}/contacts" class="button medium">Contact</a></li>
</center>
</ul>

{% assign today = site.time | date: '%s' %}
{% assign events_sorted = site.events | sort: 'date' | reverse  %}
{% assign next_days = -1000 %}
{% assign next_date = 'not meeting planed' %}
{% for item in events_sorted %}
    {% assign start = item.date | date: '%s' %}
    {% assign seconds_since = today | minus: start %}
    {% assign hours_since = seconds_since | divided_by: 60 | divided_by: 60 %}
    {% assign days_since = hours_since | divided_by: 24 %}
    {% if days_since <= 0 and next_days < days_since %}
        {% assign next_days = days_since %}
        {% assign next_date = item.date | date: '%-d %B %Y' %}
    {% endif %}
{% endfor %}
    

<header class="major">
  <h2>Next Meeting</h2>
</header>

<span style="background-color: #FFFF00;font-size: larger">{{next_date}}</span> at NeuroSpin in the ShowRoom from 2 to 3pm.


<!-- Section -->
<section>
    <header class="major">
      <h2>Lightning Talks</h2>
    </header>
    {% if next_date != 'not meeting planed' %}
        <div class="posts">
        {% for item in events_sorted %}
            {% assign start = item.date | date: '%s' %}
            {% assign seconds_since = today | minus: start %}
            {% assign hours_since = seconds_since | divided_by: 60 | divided_by: 60 %}
            {% assign days_since = hours_since | divided_by: 24 %}
            {% if next_days == days_since %}
                <article>
                <section style="width: 100%; float: left">
                  <div style=" width: 30%; height: 150px; float: right">
                    <a class="image"><img src="{{site.url}}{{site.baseurl}}/images/resources/{{item.icon}}" alt="" /></a>
                  </div>
                  <p><b>{{item.author}}</b>: {{ item.title }}
                  {{ item.teasing }}</p>
                </section>
                </article>
            {% endif %}
        {% endfor %}
        </div>
    {% endif %}
</section>

