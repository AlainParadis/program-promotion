---
layout: default
title: "Schools Directory"
role: nav
order: 1
---

<div class="schools-directory">
	<p>
		These are arts high schools to approach. They all participate in the SHSM Program. This is a preliminary list that can be built upon with time. <a href="https://www.ontario.ca/document/specialist-high-skills-major-policy-and-implementation-guide/arts-and-culture" target="_blank">Read more about the SHSM program here</a>.
	</p>

	<div class="schools-search">
		<input type="text" id="schoolFilter" placeholder="Search schools by name..." class="search-input">
	</div>

	<div class="schools-list">
		{% assign sorted_schools = site.schools | sort: "title" %}
		{% for school in sorted_schools %}
		<article class="school-card" data-school="{{ school.title | downcase }}">
			<div class="school-card-header">
				<h3><a href="{{ site.baseurl }}{{ school.url }}">{{ school.title }}</a></h3>
				<div class="badge-container">
					<span class="status-badge status-{{ school.status }}">{{ school.status }}</span>
				</div>
			</div>

			<div class="school-card-body">
				{% if school.contact.name or school.contact.title %}
				<div class="contact-info">
					{% if school.contact.name %}<strong>{{ school.contact.name }}</strong>{% endif %}
					{% if school.contact.title %}<div class="subtitle">{{ school.contact.title }}</div>{% endif %}
				</div>
				{% endif %}

				{% if school.contact.email or school.contact.phone %}
				<div class="quick-contact">
					{% if school.contact.email %}<a href="mailto:{{ school.contact.email }}">{{ school.contact.email }}</a>{% endif %}
					{% if school.contact.phone %}<span class="divider">•</span> <a href="tel:{{ school.contact.phone }}">{{ school.contact.phone }}</a>{% endif %}
				</div>
				{% endif %}

				{% if school.communications.size > 0 %}
				<div class="last-contact">
					{% assign last_comm = school.communications | last %}
					<small>Last contact: {{ last_comm.date }} via <strong>{{ last_comm.method }}</strong></small>
				</div>
				{% endif %}
			</div>

			<div class="school-card-footer">
				<a href="{{ site.baseurl }}{{ school.url }}" class="view-button">View Details →</a>
			</div>
		</article>
		{% endfor %}
	</div>
</div>

<style>
	.schools-directory {
		max-width: 1200px;
		margin: 0 auto;
	}

	.schools-search {
		margin: 2rem 0 1.5rem 0;
	}

	.search-input {
		width: 100%;
		max-width: 400px;
		padding: 0.75rem;
		border: 1px solid #ddd;
		border-radius: 4px;
		font-size: 1rem;
	}

	.schools-list {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
		gap: 1.5rem;
		margin-top: 2rem;
	}

	.school-card {
		border: 1px solid #ddd;
		border-radius: 6px;
		overflow: hidden;
		background: white;
		transition: box-shadow 0.2s ease;
	}

	.school-card:hover {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
	}

	.school-card-header {
		padding: 1.5rem;
		border-bottom: 1px solid #eee;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		gap: 0.75rem;
	}

	.school-card-header h3 {
		margin: 0;
		font-size: 1.15rem;
	}

	.badge-container {
		width: 100%;
	}

	.school-card-header a {
		color: #0066cc;
		text-decoration: none;
	}

	.school-card-header a:hover {
		text-decoration: underline;
	}

	.status-badge {
		display: inline-block;
		padding: 0.35rem 0.75rem;
		border-radius: 4px;
		font-size: 0.85rem;
		font-weight: 600;
		text-transform: capitalize;
		white-space: nowrap;
	}

	.status-contacted {
		background: #d4f1d4;
		color: #186618;
	}

	.status-not-contacted {
		background: #f0f0f0;
		color: #666;
	}

	.school-card-body {
		padding: 1.5rem;
	}

	.contact-info {
		margin-bottom: 0.75rem;
	}

	.contact-info strong {
		display: block;
		color: #333;
	}

	.contact-info .subtitle {
		font-size: 0.9rem;
		color: #666;
		font-weight: normal;
		margin-top: 0.25rem;
	}

	.quick-contact {
		margin-bottom: 0.75rem;
		font-size: 0.9rem;
	}

	.quick-contact a {
		color: #0066cc;
		text-decoration: none;
	}

	.quick-contact a:hover {
		text-decoration: underline;
	}

	.quick-contact .divider {
		margin: 0 0.5rem;
		color: #ccc;
	}

	.last-contact {
		display: block;
		margin-top: 0.75rem;
		padding-top: 0.75rem;
		border-top: 1px solid #eee;
		color: #666;
	}

	.school-card-footer {
		padding: 1rem 1.5rem;
		background: #f9f9f9;
		border-top: 1px solid #eee;
	}

	.view-button {
		color: #0066cc;
		text-decoration: none;
		font-weight: 500;
		transition: color 0.2s ease;
	}

	.view-button:hover {
		color: #0052a3;
	}

	.hidden {
		display: none;
	}
</style>

<script>
	document.getElementById('schoolFilter').addEventListener('keyup', function(e) {
		const searchTerm = e.target.value.toLowerCase();
		const cards = document.querySelectorAll('.school-card');
		
		cards.forEach(card => {
			const schoolName = card.getAttribute('data-school');
			if (schoolName.includes(searchTerm)) {
				card.classList.remove('hidden');
			} else {
				card.classList.add('hidden');
			}
		});
	});
</script>
