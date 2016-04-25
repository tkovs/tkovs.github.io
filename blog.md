---
layout: default
title: Arquivos
---

<div class="page-content wc-container">
    {% assign rawtags = "" %}
    {% for post in site.posts %}
	{% assign ttags = post.tags | join:'|' | append:'|' %}
	{% assign rawtags = rawtags | append:ttags %}
    {% endfor %}
    {% assign rawtags = rawtags | split:'|' | sort %}

    {% assign tags = "" %}
    {% for tag in rawtags %}
	{% if tag != "" %}
	    {% if tags == "" %}
		{% assign tags = tag | split:'|' %}
	    {% endif %}

	    {% unless tags contains tag %}
		{% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
	    {% endunless %}
	{% endif %}
    {% endfor %}

    <h1>Arquivos do blog</h1>    
    {% for tag in tags %}
	<h5>{{ tag }}</h5>
	<ul>
            {% for post in site.posts %}
                {% if post.tags contains tag %}
                    <li>
                        <span style="float: left;">
                            <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
                        </span>
                        <span style="float: right;">
                            {{ post.date | date_to_string }}
                        </span>
                        <div style="clear: both;"></div>
                    </li>
		{% endif %}
	    {% endfor %}
	</ul>
    {% endfor %}
</div>
