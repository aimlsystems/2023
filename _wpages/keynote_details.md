---
layout: other
title: Keynote Speakers
---

{% for cat in site.data.keynote_speakers %}
{% assign catId = forloop.index %}
<!-- {{ cat  }} -->
{% assign talks = cat[1] %}
{% if forloop.first == false %} 
<br>
<hr>
<br>
{% endif %}
<!--<h3 class="nt-panel-title">{{ cat[0] }} Keynotes </h3>-->

<div class="row oc_cntr">
<div class="col-12">

{% for talk in talks %}
{% assign talkId = forloop.index %}
{% assign detail = talk %}
{% if detail['title'] == nil %}
{% continue %}
{% endif %}
<!-- {{ talk }} -->
<!-- {{ forloop.index }}{{ catId }} -->
<a id="keynote_{{ forloop.index }}_{{ catId }}"></a>
<div class="row">
    <div class="col-3 col-12-medium">
        <div class="row text-center">
        {% for speaker in talk.speakers %}
        {% assign mem = speaker %}
            <div class="col-12">
                <img class="img-fuild" style="max-width: 120px; max-height: auto;" src="{{ site.baseurl }}/images/people/{{ site.data.people[mem][3] | default: "avtar.png" }}?{{ site.time | date: "%s" }}">
            </div>
            <div class="col-12">
                <div class="nt-feature-pad">
                    <h3><a href="{{ site.data.people[mem][2] | default: "#" }}" target="_blank">{{ site.data.people[mem][0] | default: mem }}</a></h3>
                    <p>{{ site.data.people[mem][1] | default: ""}}</p>
                </div>
            </div>
        {% endfor %}
        </div>
    </div>
    <div class="col-9 col-12-medium">
        <h2>{{ detail['title'] }}</h2>
        {% if detail['video'] %}
<!--         <a href="{{ detail['video'] }}" class="btn"> Video </a> -->
        {% endif %}
        {% if detail['abstract'] %}
        {% for d in detail['abstract'] %}
        <div class="text-justify">
            {% if forloop.first %}
            <b>Abstract: </b> <br/>
            {% else %}
                &nbsp;&nbsp;&nbsp;&nbsp;
            {% endif %}
            {{ d }}
        </div>
        <br/>
        {% endfor %}
        {% endif %}
        {% for speaker in talk.speakers %}
        {% assign mem = speaker %}
        {% if site.data.bio[mem] %}
        {% for b in site.data.bio[mem] %}
        <div class="text-justify">
            {% if forloop.first %}
            <b>Bio: </b><br/>
                {% if talk.speakers.size > 1 %}
                ({{ mem }})
                {% endif %}
            {% else %}
                &nbsp;&nbsp;&nbsp;&nbsp;
            {% endif %}
            {{ b }}
        </div>
        {% endfor %}
        {% endif %}
        {% endfor %}
    </div>
</div>
<br>
<br>
{% endfor %}
</div>
</div>
{% endfor %}