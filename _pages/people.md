---
layout: page
permalink: /people/
title: People
# description: 
nav: true
nav_order: 3
---

<style>
/* Container for the entire member entry */
.member-entry {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-bottom: 3rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid var(--global-divider-color);
}

/* On wider screens, place image on left and text on right */
@media (min-width: 768px) {
  .member-entry {
    flex-direction: row;
    align-items: flex-start;
  }
}

/* Sidebar with image and social links */
.member-sidebar {
  flex: 0 0 200px;
  text-align: center;
}

.member-photo {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1rem;
  box-shadow: 0 4px 14px rgba(0,0,0,0.1);
}

.member-links {
  display: flex;
  justify-content: center;
  gap: 0.8rem;
  flex-wrap: wrap;
}

.member-links a {
  color: var(--global-text-color-light);
  font-size: 1.2rem;
  transition: color 0.2s;
}

.member-links a:hover {
  color: var(--global-theme-color);
}

/* Main content area (name, role, bio) */
.member-content {
  flex: 1;
}

.member-name {
  font-weight: 600;
  font-size: 1.6rem;
  margin-bottom: 0.2rem;
  margin-top: 0;
}

.member-name a {
  color: var(--global-text-color);
  text-decoration: none;
}

.member-name a:hover {
  color: var(--global-theme-color);
}

.member-role {
  font-size: 1.1rem;
  color: var(--global-text-color-light);
  margin-bottom: 0.2rem;
  font-style: italic;
}

.member-degree {
  font-size: 1rem;
  color: var(--global-theme-color);
  margin-bottom: 1rem;
  font-weight: 500;
}

/* Styling the markdown content */
.member-bio {
  margin-top: 1rem;
  font-size: 1rem;
  line-height: 1.6;
}

.member-bio p {
  margin-bottom: 1rem;
}

.category-title {
  border-bottom: 2px solid var(--global-theme-color); /* Emphasize category headers */
  padding-bottom: 0.5rem;
  margin-top: 3rem;
  margin-bottom: 2rem;
  font-weight: bold;
}
</style>

<!-- Define the order of the categories here -->
{% assign categories = "Principal Investigator,Postdocs,Current PhD Students,Current Masters Students,Undergraduates,Alumni" | split: "," %}

{% for category in categories %}
{% assign category_members = site.members | where: "category", category %}

{% if category_members.size > 0 %}
<h2 class="category-title">{{ category }}</h2>

<div class="member-list">
{% for member in category_members %}
<div class="member-entry">

<!-- Left Sidebar: Image and Social Links -->
<div class="member-sidebar">
{% if member.image %}
<img src="{{ member.image | prepend: '/assets/img/members/' | relative_url }}" alt="{{ member.name }}" class="member-photo">
{% else %}
<img src="{{ '/assets/img/prof_pic.jpg' | relative_url }}" alt="{{ member.name }}" class="member-photo">
{% endif %}

<div class="member-links">
{% if member.email %}
<a href="mailto:{{ member.email }}" title="Email"><i class="fas fa-envelope"></i></a>
{% endif %}
{% if member.linkedin %}
<a href="https://www.linkedin.com/in/{{ member.linkedin }}" title="LinkedIn" target="_blank" rel="noopener noreferrer"><i class="fab fa-linkedin"></i></a>
{% endif %}
{% if member.github %}
<a href="https://github.com/{{ member.github }}" title="GitHub" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i></a>
{% endif %}
{% if member.twitter %}
<a href="https://twitter.com/{{ member.twitter }}" title="Twitter" target="_blank" rel="noopener noreferrer"><i class="fab fa-twitter"></i></a>
{% endif %}
{% if member.scholar %}
<a href="https://scholar.google.com/citations?user={{ member.scholar }}" title="Google Scholar" target="_blank" rel="noopener noreferrer"><i class="ai ai-google-scholar"></i></a>
{% endif %}
</div>
</div>

<!-- Right Area: Name, Role, and Bio -->
<div class="member-content">
<h3 class="member-name">
{% if member.website %}
<a href="{{ member.website }}" target="_blank" rel="noopener noreferrer">{{ member.name }}</a>
{% else %}
{{ member.name }}
{% endif %}
</h3>

{% if member.position %}
<div class="member-role">{{ member.position }}</div>
{% endif %}

{% if category == "Alumni" and member.degree %}
<div class="member-degree">{{ member.degree }}</div>
{% endif %}

{% if member.content != "" %}
<div class="member-bio">
{{ member.content | markdownify }}
</div>
{% endif %}
</div>

</div>
{% endfor %}
</div>
{% endif %}
{% endfor %}