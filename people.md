---
layout: default
title: People
permalink: /people/
---

<div>

{% assign people_sorted = site.people | sort: 'joined' %}
{% assign people_sorted_reverse = site.people | sort: 'joined' | reverse %}
{% assign role_array = "faculty|phd|ms|alumni" | split: "|" %}

{% for role in role_array %}

{% assign people_in_role = people_sorted | where: 'position', role %}

<!-- Skip section if there's nobody -->
{% if people_in_role.size == 0 %}
  {% continue %}
{% endif %}

{% if role == 'faculty' %}
<h3>Faculty</h3>
{% elsif role == 'alumni' %}
<h3>Alumni</h3>
{% elsif role == 'phd' %}
<h3>Students</h3>
{% endif %}
<!-- {% if role == 'postdoc' %}
<h4>Postdoctoral Fellows</h4>
 {% elsif role == 'pi' %}
<h4>Principal Investigator</h4>
 {% elsif role == 'gradstudent' %}
<h4>Graduate Students</h4>
 {% elsif role == 'researchstaff' %}
<h4>Research Staff</h4>
 {% elsif role == 'visiting' %}
<h4>Visiting Scholars</h4>
 {% elsif role == 'others' %}
<h4>Honorary Members</h4>
{% endif %} -->

<div class="people">
{% if role == 'faculty' %}
  {% for profile in people_sorted %}
    {% if profile.position contains role %}
        <div class="list-item-people">
          {% if profile.avatar %}
            <a href="{{ profile.page }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/{{profile.avatar}}"></a>
          {% else %}
            <a href="{{ profile.page }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/anonymous.jpg"></a>
          {% endif %}
          <div class="info-block">
            <ul>
              <li>
                <b>
                <a class="name" href="{{ profile.page }}">{{ profile.name }}</a> ({{ profile.name-cn }}), {{ profile.title }}
                </b>
              </li>
              <li>
                {{ profile.degree }}
              </li>
              <li>
                <i>{{ profile.field }}</i>
              </li>
              <li>
                <b>Email: </b><code>{{ profile.email }}</code>
              </li>
            </ul>
          </div>
        </div>
      <br> 
    {% endif %}
    <!-- <br> -->
  {% endfor %}
</div>

{% elsif role == 'phd' or role == 'ms' %}

<div class="people">
  {% for profile in people_sorted %}
    {% if profile.position contains role %}
      {% if profile.blog %}
        <b>
          <a href="{{ profile.blog }}">{{ profile.name }}</a> ({{ profile.name-cn }})
        </b>
      {% elsif profile.page %}
        <b>
          <a href="{{ site.baseurl }}{{ profile.url }}">{{ profile.name }}</a> ({{ profile.name-cn }})
        </b>
      {% else %}
        <b>
          {{ profile.name }}
        </b>
      {% endif %}
      , {{ profile.degree }}, {{ profile.time }}
      {% if profile.where %}
        , {{ profile.where }}
      {% endif %}
      <br>
    {% endif %}
  {% endfor %}
</div>

{% elsif role == 'alumni' %}

<div class="people">
  {% for profile in people_sorted_reverse %}
    {% if profile.position contains role %}
      {% if profile.blog %}
        <b>
          <a href="{{ profile.blog }}">{{ profile.name }}</a> ({{ profile.name-cn }})
        </b>
      {% elsif profile.page %}
        <b>
          <a href="{{ site.baseurl }}{{ profile.url }}">{{ profile.name }}</a> ({{ profile.name-cn }})
        </b>
      {% else %}
        <b>
          {{ profile.name }}
        </b>
      {% endif %}
      , {{ profile.degree }}, {{ profile.time }}
      {% if profile.where %}
        , {{ profile.where }}
      {% endif %}
      <br>
    {% endif %}
  {% endfor %}
</div>

{% endif %}

{% if role != 'phd' %}
<hr>
{% endif %}

{% endfor %}

Information about alumni who graduated before 2022 has not yet been published here, please wait.

</div>