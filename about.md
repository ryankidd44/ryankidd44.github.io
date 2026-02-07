---
layout: page
title: About
permalink: /about/
---

<div class="about-content">
    <div class="about-section">
        <h3>Current Work</h3>
        <p>I co-lead <strong>MATS Research</strong>, a research nonprofit that trains talented researchers to work on AI alignment, transparency, and security. We run fellowship programs that have supported 446 researchers, with offices in Berkeley and London.</p>
        <p>My focus is on scaling AI safety through field—building the organizations, talent pipelines, and infrastructure needed to ensure advanced AI systems are developed safely. I think about organizational design, talent development, and field-wide coordination.</p>
    </div>

    <div class="about-section">
        <h3>Mission</h3>
        <p>I believe the development of transformative AI is one of the most important events in human history, and that we have a narrow window to get the foundations right. My work is oriented toward building the human capital and institutional capacity the field needs to succeed.</p>
    </div>

    <div class="about-section">
        <h3>Board & Advisory Positions</h3>
        <ul>
            {% for position in site.data.positions %}
            <li>
                <span class="position-title">{{ position.role }}</span>
                <span class="position-org">— {{ position.organization }}</span>
            </li>
            {% endfor %}
        </ul>
    </div>

    <div class="about-section">
        <h3>Background</h3>
        <p>Before MATS, I completed a PhD in physics. I've been working in AI safety for four years, and have been fortunate to contribute to the field's growth during a critical period.</p>
    </div>
</div>
