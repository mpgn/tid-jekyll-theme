---
layout: default
---

<!-- Get the tag name for every tag on the site and set them to the `site_tags` variable. -->
{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}

<!-- `tag_words` is a sorted array of the tag names. -->
{% assign tag_words = site_tags | split:',' | sort %}

<!-- List of all tags -->
<div style="margin-bottom: 30px;">
	{% for item in (0..site.tags.size) %}
		{% unless forloop.last %}
			{% capture tag %}{{ tag_words[item] }}{% endcapture %}
				<span class="label" style="background-color:{{ site.data.categories[tag] }}"><a href="#{{ tag | cgi_escape }}">{{ tag }} <span class="sub-label">{{ site.tags[tag].size }}</span></a></span>
		{% endunless %}
	{% endfor %}
</div>


<!-- Posts by Tag -->
<div>
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture tag %}{{ tag_words[item] }}{% endcapture %}
    <h3 id="{{ tag | cgi_escape }}">{{ tag }}</h3>
    {% for post in site.tags[tag] %}{% if post.title != null %}
      <div>
        <span style="float: left;">
          <a href="{{ site.baseurl}}{{ post.url }}">{{ post.title }}</a>{% if post.stared %} <i style="font-size: 12px;" class="fa fa-star"></i> {% endif %}
        </span>
        <span style="float: right;">
          {{ post.date | date_to_string }}
        </span>
      </div>
      <div style="clear: both;"></div>
    {% endif %}{% endfor %}
  {% endunless %}{% endfor %}
</div>
