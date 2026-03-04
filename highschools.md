---
layout: default
role: notes
title: Local Arts High Schools
---
<p>
	These are arts high schools to approach. They all participate in the SHSM Program. This is a preliminary list that can be built upon with time. <a href="https://www.ontario.ca/document/specialist-high-skills-major-policy-and-implementation-guide/arts-and-culture" target="_target">Read more about the SHSM program here</a>.
</p>

<div class="schools-search">
	<input type="text" id="schoolFilter" placeholder="Search schools by name..." class="search-input">
</div>

<div class="table-wrapper">
	<table class="schools-table" id="schoolsTable">
		<thead>
			<tr>
				<th>School Name</th>
				<th>Contact</th>
				<th>Status</th>
				<th>Last Contact</th>
				<th>Communications</th>
			</tr>
		</thead>
		<tbody>
			{% assign sorted-schools = site.data.schools.schools | sort: "name" %}
			{% for school in sorted-schools %}
			<tr class="school-row" data-school="{{ school.name | downcase }}">
				<td data-label="School Name" class="school-name">
					<strong>{{ school.name }}</strong>
					{% if school.contact.email or school.contact.phone %}
					<div class="contact-quick">
						{% if school.contact.email %}<a href="mailto:{{ school.contact.email }}">{{ school.contact.email }}</a>{% endif %}
						{% if school.contact.phone %}<span class="divider">•</span> <a href="tel:{{ school.contact.phone }}">{{ school.contact.phone }}</a>{% endif %}
					</div>
					{% endif %}
				</td>
				<td data-label="Contact">
					{% if school.contact.name or school.contact.title %}
						{% if school.contact.name %}<strong>{{ school.contact.name }}</strong>{% endif %}
						{% if school.contact.title %}<div class="subtitle">{{ school.contact.title }}</div>{% endif %}
					{% else %}
						<span class="empty">No contact assigned</span>
					{% endif %}
				</td>
				<td data-label="Status">
					<span class="status-badge status-{{ school.status }}">{{ school.status }}</span>
				</td>
				<td data-label="Last Contact">
					{% if school.communications.size > 0 %}
						{% assign last_comm = school.communications | last %}
						<span class="last-contact">{{ last_comm.date }}</span>
						<div class="method-badge">{{ last_comm.method }}</div>
					{% else %}
						<span class="empty">No contact yet</span>
					{% endif %}
				</td>
				<td data-label="Communications">
					{% if school.communications.size > 0 %}
						<div class="communications-log">
							{% for comm in school.communications %}
								<div class="communication-entry">
									<span class="comm-date">{{ comm.date }}</span>
									<span class="comm-method">{{ comm.method }}</span>
									<span class="comm-note">{{ comm.note }}</span>
								</div>
							{% endfor %}
						</div>
					{% else %}
						<span class="empty">No communications logged</span>
					{% endif %}
				</td>
			</tr>
			{% endfor %}
		</tbody>
	</table>
</div>

<script>
document.getElementById('schoolFilter').addEventListener('keyup', function(e) {
	const searchTerm = e.target.value.toLowerCase();
	const rows = document.querySelectorAll('.school-row');
	
	rows.forEach(row => {
		const schoolName = row.getAttribute('data-school');
		if (schoolName.includes(searchTerm)) {
			row.style.display = '';
		} else {
			row.style.display = 'none';
		}
	});
});
</script>