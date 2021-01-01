---
# Add new glossary terms by editing _data/glossary_terms.yml
sort: 12 # Order in the sidebar
# permalink: /tutorials/glossary
# published: false
---

# Glossary

This page is a list of terms and their definitions in the context of the BoGL language.

<!-- Sort the glossary terms alphabetically -->
{% assign sorted-terms = site.data.glossary_terms | sort_natural: 'term' %}

<!-- Set prev letter var to something that is not the first letter of any term -->
{% assign prev-letter = '?' %}

<!-- Create letter nav -->
<nav>
{% for term in sorted-terms %}
	{% assign first-letter = term.term | slice: 0 | capitalize %}
	{% if first-letter != prev-letter %}  
		<a class="anchor" href="{{ first-letter | capitalize | prepend: "#" }}"> {{ first-letter | capitalize }} </a>
		{% assign prev-letter = first-letter | capitalize %}
	{% endif %}
{% endfor %}
</nav>

<!-- Set prev letter var to something that is not the first letter of any term -->
{% assign prev-letter = '?' %}

<!-- Create list of terms -->
<ul style="list-style: none;">
{% for term in sorted-terms %}
	
	<!-- If this is a term with a new starting letter create a header -->
	{% assign first-letter = term.term | slice: 0 | capitalize %}
	{% if first-letter != prev-letter %}  
		<h2 id={{ first-letter | capitalize }}>{{ first-letter | capitalize }}</h2>
		{% assign prev-letter = first-letter | capitalize %}
	{% endif %}

	<li>
		<b>{{ term.term }}</b>
		<br/>
		{{ term.definition }}
		<br/>
		<br/>
	</li>
{% endfor %}
</ul>

