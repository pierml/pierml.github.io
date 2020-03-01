---
layout: page
title: Tags

---

<div class="page-content wc-container">
	<div class="post">
		<h1>Tags</h1>
{% for tag in site.tags %}
	<h4 id="">{{ tag[0] }}</h4>
	<ul>
	 {% for post in site.posts %}
		 {% if post.tags contains tag[0] %}
		 <li>
		 <small>{{ post.date | date_to_string }}</small>
		 <a href="{{ post.url }}">
		 {{ post.title }}
		 </a>
		 {% for tag in post.tags %}
			 <a class="tag" href="">{{ tag[0] }}</a>
		 {% endfor %}
		 </li>
		 {% endif %}
	 {% endfor %}
	</ul>
{% endfor %}
	</div>
</div>
