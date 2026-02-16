---
# layout: page
# title: About
# permalink: /about/
---

<div class="about-content">
    <div class="about-section">
        <h3>Current Work</h3>
        <p>I co-lead <strong><a href="https://matsprogram.org">MATS Research</a></strong>, a research nonprofit that aims to solve the talent bottleneck in AI alignment, transparency, and security. We run fellowship programs that have supported 530+ researchers and output <a href="https://www.matsprogram.org/research">160+ research publications</a>, with offices in Berkeley and London. Our alumni have founded 30+ AI safety & security organizations and teams, including <a href="https://www.apolloresearch.ai">Apollo Research</a>, <a href="https://timaeus.co">Timaeus</a>, and <a href="https://atla-ai.com">Atla</a>.</p>
	<p>I co-founded the <a href="https://safeai.org.uk">London Initiative for Safe AI (LISA)</a>, the largest AI safety hub in Europe, and advise <a href="https://halcyonfutures.org">Halcyon Futures</a>, <a href="https://catalyze-impact.org">Catalyze Impact</a>, <a href="https://www.pivotal-research.org">Pivotal Research</a>, <a href="https://www.aisafetyanz.com.au">AI Safety ANZ</a>, <a href="https://www.baseresearch.org">Black in AI Safety and Ethics (BASE)</a>, and more. As a <a href="https://manifund.org/RyanKidd">Manifund Regrantor</a>, I have awarded $400,000 to AI safety start-ups and projects and helped seed <a href="https://catalyze-impact.org/">Catalyze Impact</a>, <a href="https://timaeus.co/">Timaeus</a>, <a href="https://ai-safety-atlas.com/">AI Safety Atlas</a>, <a href="https://sydneyaisafetyspace.org/">Sydney AI Safety Space</a>, and many more.</p>
        <p>My focus is on scaling AI safety through building the organizations, talent pipelines, and infrastructure needed to ensure advanced AI systems are developed safely and for the benefit of all.</p>
    </div>

    <div class="about-section">
        <h3>Mission</h3>
        <p>I believe the development of transformative AI is one of the most important events in human history, and that we have a narrow window to get the foundations right. Transformative AI, which can perform most human tasks and thus (in theory) ~10x world economic growth rates, will likely be realized <a href="https://agi.goodheartlabs.com">within the next 2-15 years</a>.</p>

	<p>It seems extremely difficult to guarantee that powerful and by-default-uninterpretable AI systems will act in ways that are <a href="https://agi.goodheartlabs.com/">safe or aligned</a> with the best interests of humans and their institutions. There are enormous incentives to deploy economically and militarily advantageous AI systems, and I think current international governance practices might fail to curtail the deployment of unsafe technology. In short, I believe humanity's power may soon dangerously outstrip its wisdom.</p>

	<p>I am interested in solving problems related to "value-loading" and "corrigibility," building institutions for AI alignment/governance research, forecasting transformative AI, and developing robust governance norms for "black-ball" technology. I support Effective Altruism, a movement for solving the world's most impactful, neglected, and tractable problems.</p>
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
        <p>Before MATS, I completed a PhD in physics at the University of Queensland.
    </div>
</div>
