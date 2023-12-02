---
layout: default
title: Deepak Yadav
---

<div class="projets" id="projects">
	<h3 class="pageTitle">Recent Projects</h3>
	<div class="posts noList">
		<table>
			<thead>
				<tr>
					<th>Project</th>
					<th>Description</th>
					<th>GitHub Link</th>
				</tr>
			</thead>
			<tbody>
				{% for project in site.data.projects %}
				<tr>
					<td><h4>{{ project.name }}</h4></td>
					<td>{{ project.description }}</td>
					<td><a href="{{ project.link }}">GitHub link</a></td>
				</tr>
				{% endfor %}
			</tbody>
		</table>
	</div>
</div>
