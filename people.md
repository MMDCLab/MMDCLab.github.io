---
title: People
permalink: /people/
---

{% assign people_sorted = site.people | sort: 'joined' %}
{% assign role_array = "faculty|phd|ms|alumni" | split: "|" %}

{% for role in role_array %}

{% assign people_in_role = people_sorted | where: 'position', role %}

<!-- Skip section if there's nobody -->
{% if people_in_role.size == 0 %}
  {% continue %}
{% endif %}

<div class="pos_header">
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
</div>

{% if role == 'faculty' %}
<div class="people">
  {% for profile in people_sorted %}
    {% if profile.position contains role %}
      <div class="list-item-people">
        <div class="list-post-title">
          {% if profile.avatar %}
            <a href="{{ profile.page }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/{{profile.avatar}}"></a>
          {% else %}
            <a href="{{ profile.page }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/anonymous.jpg"></a>
          {% endif %}
          <div class="info-block">
          <div class="info">
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
                <b>Email: </b><a href="mailto:{{ profile.email }}">{{ profile.email }}</a>
              </li>
            </ul>
          </div>
          </div>
        </div>
      </div>    
    {% endif %}
    <!-- <br> -->
  {% endfor %}
</div>
<hr>

{% elsif role == 'phd' or role == 'ms' or role == 'alumni' %}

<div class='people'>
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
      <br>
    {% endif %}
  {% endfor %}
</div>

<hr>

{% endif %}
{% endfor %}

Information about alumni who graduated before 2023 has not yet been published here, please wait.
