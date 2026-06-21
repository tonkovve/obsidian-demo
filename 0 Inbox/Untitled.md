
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>your-name — DevOps Learning Portfolio</title>
<style>
  /* ============ Design tokens ============ */
  :root{
    --bg: #0a0d0c;
    --surface: #111513;
    --surface-2: #161c19;
    --border: #232a26;
    --ink: #e6ece8;
    --muted: #7d8b86;
    --accent: #46e08a;
    --accent-soft: rgba(70,224,138,0.14);
    --glow-accent: 0 0 8px rgba(70,224,138,0.55);
    --status-ok: #54c7d6;
    --status-ok-soft: rgba(84,199,214,0.16);
    --glow-cyan: 0 0 8px rgba(84,199,214,0.5);
    --radius: 6px;
    --maxw: 880px;
    --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", "IBM Plex Sans", Roboto, Helvetica, Arial, sans-serif;
    --font-mono: ui-monospace, SFMono-Regular, "JetBrains Mono", "IBM Plex Mono", Menlo, Consolas, monospace;
  }

  /* ============ Reset / base ============ */
  *,*::before,*::after{ box-sizing: border-box; }
  html{ scroll-behavior: smooth; }
  body{
    margin:0;
    background: radial-gradient(ellipse 1100px 560px at 50% -8%, rgba(70,224,138,0.07), transparent 60%), var(--bg);
    color: var(--ink);
    font-family: var(--font-sans);
    font-size: 16px;
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    position: relative;
  }
  /* faint ambient grid + scanline texture, restrained */
  body::before{
    content:"";
    position: fixed; inset:0;
    background-image: radial-gradient(circle, var(--border) 1px, transparent 1px);
    background-size: 26px 26px;
    opacity: .35;
    pointer-events: none;
    z-index: 0;
  }
  body::after{
    content:"";
    position: fixed; inset:0;
    background-image: repeating-linear-gradient(to bottom, rgba(230,236,232,0.025) 0px, rgba(230,236,232,0.025) 1px, transparent 1px, transparent 3px);
    pointer-events: none;
    z-index: 0;
  }
  h1,h2,h3,h4{ margin: 0; font-weight: 600; letter-spacing: -0.01em; }
  p{ margin: 0; }
  ul{ margin:0; padding:0; list-style:none; }
  a{ color: var(--ink); text-decoration: none; }
  a:hover{ color: var(--accent); }
  *:focus-visible{ outline: 2px solid var(--accent); outline-offset: 3px; border-radius: 4px; }

  .skip-link{
    position:absolute; left:-9999px; top:0; z-index: 100;
    background: var(--accent); color:#06140d; padding:10px 16px; border-radius: 6px;
  }
  .skip-link:focus{ left: 16px; top: 16px; }

  .wrap{ max-width: var(--maxw); margin: 0 auto; padding: 0 24px; position: relative; z-index:1; }
  .section{ padding: 72px 0; border-top: 1px solid var(--border); }
  section#top.section, .hero.section{ border-top: none; }
  @media (max-width: 720px){ .section{ padding: 48px 0; } }

  .eyebrow{
    font-family: var(--font-mono);
    font-size: .78rem;
    letter-spacing: .04em;
    color: var(--accent);
    text-transform: lowercase;
    margin-bottom: 14px;
  }
  .eyebrow::before{ content:"[ "; }
  .eyebrow::after{ content:" ]"; }

  /* ============ Header ============ */
  .site-header{
    position: sticky; top:0; z-index: 50;
    background: rgba(10,13,12,0.82);
    backdrop-filter: blur(8px);
    border-bottom: 1px solid var(--border);
  }
  .header-inner{
    max-width: var(--maxw); margin:0 auto; padding: 16px 24px;
    display:flex; align-items:center; justify-content: space-between; gap: 16px;
  }
  .brand{ display:flex; align-items:center; gap:8px; font-family: var(--font-mono); font-size: .92rem; color: var(--ink); }
  .brand-mark{ color: var(--status-ok); font-size: .7rem; text-shadow: var(--glow-cyan); }
  .header-nav{ display:flex; gap: 24px; font-size: .92rem; }
  .header-nav a{ color: var(--muted); }
  .header-nav a:hover{ color: var(--ink); }
  .lang-toggle{ display:flex; border:1px solid var(--border); border-radius: 6px; overflow:hidden; font-family: var(--font-mono); font-size:.78rem; }
  .lang-btn{
    background:none; border:none; color: var(--muted); padding: 6px 12px; cursor:pointer;
  }
  .lang-btn.active{ background: var(--accent-soft); color: var(--accent); }
  @media (max-width: 600px){ .header-nav{ display:none; } }

  /* ============ Hero ============ */
  .hero-inner{ display:grid; grid-template-columns: 1fr 280px; gap: 48px; padding-top: 64px; align-items: start; }
  @media (max-width: 760px){ .hero-inner{ grid-template-columns: 1fr; } }
  .hero h1{ font-size: clamp(1.6rem, 3.4vw, 2.3rem); line-height:1.25; margin-bottom: 18px; max-width: 22ch; }
  .hero-lead{ color: var(--muted); font-size: 1.02rem; max-width: 52ch; margin-bottom: 26px; }
  .hero-links{ display:flex; gap: 22px; font-family: var(--font-mono); font-size: .88rem; }
  .hero-links a{ border-bottom: 1px solid var(--border); padding-bottom: 2px; }
  .hero-links a:hover{ border-color: var(--accent); }

  .status-panel{
    background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius);
    padding: 20px; font-family: var(--font-mono); font-size: .84rem;
  }
  .status-panel-head{ display:flex; align-items:center; gap:8px; margin-bottom: 16px; color: var(--muted); }
  .status-panel-head strong{ color: var(--ink); font-weight: 600; }
  .status-dot{ width:7px; height:7px; border-radius:50%; display:inline-block; flex-shrink:0; }
  .status-dot--ok{ background: var(--status-ok); box-shadow: var(--glow-cyan), 0 0 0 3px var(--status-ok-soft); }
  .status-dot--progress{ background: var(--accent); box-shadow: var(--glow-accent), 0 0 0 3px var(--accent-soft); }
  .status-rows{ margin:0; display:flex; flex-direction:column; gap:10px; }
  .status-row{ display:flex; justify-content: space-between; gap: 10px; border-top: 1px dashed var(--border); padding-top: 10px; }
  .status-row:first-child{ border-top:none; padding-top:0; }
  .status-row dt{ color: var(--muted); }
  .status-row dd{ margin:0; color: var(--ink); text-align:right; }
  .status-value .cursor{ display:inline-block; animation: blink 1.1s steps(1) infinite; color: var(--accent); text-shadow: var(--glow-accent); }
  @keyframes blink{ 50%{ opacity:0; } }
  @media (prefers-reduced-motion: reduce){ .status-value .cursor{ animation: none; } html{ scroll-behavior:auto; } }
  .stack-row{ flex-direction: column; align-items: flex-start; }
  .stack-chips{ display:flex; flex-wrap:wrap; gap:6px; margin-top:6px; }
  .chip{
    font-family: var(--font-mono); font-size:.72rem; color: var(--muted);
    border:1px solid var(--border); background: var(--surface-2);
    padding: 2px 8px; border-radius: 4px;
  }

  /* ============ Working style ============ */
  .ws-list{ display:flex; flex-direction:column; gap:14px; margin-top: 22px; max-width: 64ch; }
  .ws-list li{
    position:relative; padding-left: 22px; color: var(--ink); font-size: .98rem;
  }
  .ws-list li::before{ content:"–"; position:absolute; left:0; color: var(--accent); font-family: var(--font-mono); }

  /* ============ Reviewer guide ============ */
  .guide-intro{ color: var(--muted); margin-top: 10px; max-width: 60ch; }
  .role-tabs{ display:flex; flex-wrap:wrap; gap:8px; margin-top: 22px; }
  .role-tab{
    font-family: var(--font-mono); font-size: .82rem; color: var(--muted);
    background: var(--surface); border:1px solid var(--border); border-radius: 6px;
    padding: 8px 14px; cursor: pointer;
  }
  .role-tab.active{ color: var(--accent); border-color: var(--accent); background: var(--accent-soft); }
  .role-panel{
    margin-top: 18px; background: var(--surface); border:1px solid var(--border); border-radius: var(--radius);
    padding: 20px 22px; color: var(--ink); max-width: 64ch; font-size: .98rem;
  }

  /* ============ Sessions feed ============ */
  .sessions-head p{ color: var(--muted); margin-top: 8px; }
  .sessions-feed{ margin-top: 30px; display:flex; flex-direction:column; gap: 14px; }
  .entry{
    background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius);
    overflow:hidden;
  }
  .entry summary{ list-style:none; cursor:pointer; padding: 20px 22px; }
  .entry summary::-webkit-details-marker{ display:none; }
  .entry summary::marker{ content:""; }
  .entry-meta{ display:flex; align-items:center; gap: 10px; font-family: var(--font-mono); font-size: .78rem; color: var(--muted); margin-bottom: 10px; }
  .entry-hash{ color: var(--muted); }
  .entry-status-label{ text-transform: lowercase; }
  .entry-title{ font-size: 1.12rem; margin-bottom: 8px; }
  .entry-lead{ color: var(--muted); font-size: .96rem; max-width: 64ch; }
  .entry-tags{ display:flex; flex-wrap:wrap; gap:6px; margin-top: 14px; }
  .entry-toggle{
    display:inline-flex; align-items:center; gap:6px; margin-top: 16px;
    font-family: var(--font-mono); font-size: .8rem; color: var(--accent);
  }
  .chevron{ display:inline-block; transition: transform .15s ease; }
  .entry[open] .chevron{ transform: rotate(90deg); }
  @media (prefers-reduced-motion: reduce){ .chevron{ transition:none; } }

  .entry-body{ padding: 0 22px 26px; border-top: 1px solid var(--border); }
  .entry-field{ padding-top: 20px; }
  .entry-field h4{
    font-family: var(--font-mono); font-size: .76rem; text-transform: uppercase; letter-spacing: .04em;
    color: var(--accent); margin-bottom: 10px; font-weight: 600;
  }
  .entry-field ul{ display:flex; flex-direction:column; gap:8px; }
  .entry-field li{ position:relative; padding-left:16px; color: var(--ink); font-size: .94rem; }
  .entry-field li::before{ content:"·"; position:absolute; left:0; color: var(--muted); }
  .entry-evidence pre{
    background: var(--surface-2); border:1px solid var(--border); border-radius: 6px;
    padding: 14px 16px; overflow-x:auto; margin:0;
  }
  .entry-evidence code{ font-family: var(--font-mono); font-size: .82rem; color: var(--ink); white-space: pre; }

  /* ============ Footer ============ */
  .site-footer{ border-top: 1px solid var(--border); padding: 32px 0 48px; }
  .site-footer p{ color: var(--muted); font-family: var(--font-mono); font-size: .8rem; text-align:center; }
</style>
</head>
<body>
<a class="skip-link" href="#sessions">Skip to Working Sessions</a>

<header class="site-header">
  <div class="header-inner">
    <a class="brand" href="#top"><span class="brand-mark">●</span><span data-i18n="brand_name">your-name</span></a>
    <nav class="header-nav">
      <a href="#about" data-i18n="nav_about">About</a>
      <a href="#guide" data-i18n="nav_guide">For Reviewers</a>
      <a href="#sessions" data-i18n="nav_sessions">Working Sessions</a>
    </nav>
    <div class="lang-toggle" role="group" aria-label="Language">
      <button class="lang-btn active" data-lang="en" aria-pressed="true">EN</button>
      <button class="lang-btn" data-lang="de" aria-pressed="false">DE</button>
    </div>
  </div>
</header>

<main id="top">

  <section class="hero section" id="about">
    <div class="wrap hero-inner">
      <div class="hero-text">
        <p class="eyebrow" data-i18n="hero_eyebrow">systems engineering — learning devops in public</p>
        <h1 data-i18n="hero_title">From basic IT knowledge to running real infrastructure — documented step by step.</h1>
        <p class="hero-lead" data-i18n="hero_lead">I'm building toward a DevOps role with a focus on Kubernetes, starting from the fundamentals. This is the working log: what I built, what broke, and what I learned fixing it — fully transparent.</p>
        <div class="hero-links">
          <a href="#" data-i18n="link_cv">CV</a>
          <a href="#" data-i18n="link_linkedin">LinkedIn</a>
          <a href="#" data-i18n="link_github">GitHub</a>
        </div>
      </div>
      <aside class="status-panel" aria-label="Status">
        <div class="status-panel-head">
          <span class="status-dot status-dot--ok"></span>
          <span>whoami → <strong>your-name</strong></span>
        </div>
        <dl class="status-rows">
          <div class="status-row"><dt data-i18n="status_label">status</dt><dd class="status-value"><span data-i18n="status_value">actively building</span><span class="cursor">_</span></dd></div>
          <div class="status-row"><dt data-i18n="started_label">started</dt><dd id="started-value">—</dd></div>
          <div class="status-row"><dt data-i18n="uptime_label">uptime</dt><dd id="uptime-value">—</dd></div>
          <div class="status-row"><dt data-i18n="focus_label">focus</dt><dd>Kubernetes &amp; Platform Engineering</dd></div>
          <div class="status-row stack-row"><dt data-i18n="stack_label">stack</dt>
            <dd class="stack-chips">
              <span class="chip">linux</span><span class="chip">docker</span><span class="chip">kubernetes</span><span class="chip">ci/cd</span>
            </dd>
          </div>
        </dl>
      </aside>
    </div>
  </section>

  <section class="section" id="working-style">
    <div class="wrap">
      <h2 data-i18n="ws_title">How I work</h2>
      <ul class="ws-list">
        <li data-i18n="ws_item1">I default to writing things down and trying first — but once I'm stuck, I ask early rather than burning hours alone.</li>
        <li data-i18n="ws_item2">Every entry includes what went wrong, not just the final working state — that's usually where the real learning happened.</li>
        <li data-i18n="ws_item3">I treat documentation as part of the work, not an afterthought — teammates shouldn't have to reverse-engineer what I did.</li>
      </ul>
    </div>
  </section>

  <section class="section" id="guide">
    <div class="wrap">
      <h2 data-i18n="guide_title">Quick guide for reviewers</h2>
      <p class="guide-intro" data-i18n="guide_intro">Short on time? Pick the role closest to yours — it'll point you to what's most relevant below.</p>
      <div class="role-tabs" role="tablist" aria-label="Reviewer role">
        <button class="role-tab active" role="tab" aria-selected="true" data-role="recruiter" data-i18n="role_recruiter_label">Recruiter</button>
        <button class="role-tab" role="tab" aria-selected="false" data-role="lead" data-i18n="role_lead_label">Team Lead</button>
        <button class="role-tab" role="tab" aria-selected="false" data-role="cto" data-i18n="role_cto_label">CTO / Director</button>
        <button class="role-tab" role="tab" aria-selected="false" data-role="exec" data-i18n="role_exec_label">Exec / CEO</button>
      </div>
      <div class="role-panel" id="role-panel"></div>
    </div>
  </section>

  <section class="section" id="sessions">
    <div class="wrap">
      <div class="sessions-head">
        <h2 data-i18n="sessions_title">Working Sessions</h2>
        <p data-i18n="sessions_sub">Newest first — a running log of what I've built, broken, and learned.</p>
      </div>
      <div class="sessions-feed" id="sessions-feed"></div>
    </div>
  </section>

</main>

<footer class="site-footer">
  <p data-i18n="footer_text">Written in Obsidian, version-controlled in Git, deployed automatically on every push.</p>
</footer>

<script>
/* =========================================================
   PROTOTYPE — replace placeholder name/links/dates/entries
   with your real content. Dates are kept in ISO format on
   purpose (log/commit convention) so no date-locale code is
   needed.
   ========================================================= */

const ui = {
  en: {
    page_title: "your-name — DevOps Learning Portfolio",
    brand_name: "your-name",
    nav_about: "About",
    nav_guide: "For Reviewers",
    nav_sessions: "Working Sessions",
    hero_eyebrow: "systems engineering — learning devops in public",
    hero_title: "From basic IT knowledge to running real infrastructure — documented step by step.",
    hero_lead: "I'm building toward a DevOps role with a focus on Kubernetes, starting from the fundamentals. This is the working log: what I built, what broke, and what I learned fixing it — fully transparent.",
    link_cv: "CV", link_linkedin: "LinkedIn", link_github: "GitHub",
    status_label: "status", status_value: "actively building",
    started_label: "started", uptime_label: "uptime",
    focus_label: "focus", stack_label: "stack",
    day_word: "Day",
    ws_title: "How I work",
    ws_item1: "I default to writing things down and trying first — but once I'm stuck, I ask early rather than burning hours alone.",
    ws_item2: "Every entry includes what went wrong, not just the final working state — that's usually where the real learning happened.",
    ws_item3: "I treat documentation as part of the work, not an afterthought — teammates shouldn't have to reverse-engineer what I did.",
    guide_title: "Quick guide for reviewers",
    guide_intro: "Short on time? Pick the role closest to yours — it'll point you to what's most relevant below.",
    role_recruiter_label: "Recruiter", role_lead_label: "Team Lead",
    role_cto_label: "CTO / Director", role_exec_label: "Exec / CEO",
    role_recruiter_text: "Start with the intro above, then skim the title and summary of the two most recent entries below — that's enough to see the trajectory and how clearly I document my work.",
    role_lead_text: "Open an entry that matches your stack and read the “Challenges” section first — that's where the real troubleshooting shows, not just the polished result.",
    role_cto_text: "Compare the oldest entry with the newest one to see how depth and reasoning have developed. The intro above explains the approach and why this learning path was chosen.",
    role_exec_text: "The intro above plus the title of the latest entry give you the headline: someone building production-relevant infrastructure skills methodically, and documenting it clearly enough for anyone to follow.",
    sessions_title: "Working Sessions",
    sessions_sub: "Newest first — a running log of what I've built, broken, and learned.",
    did_label: "What I did", learned_label: "What I learned",
    challenges_label: "Challenges & how I solved them", evidence_label: "Evidence",
    read_more: "View full entry",
    status_done: "done", status_progress: "in progress",
    footer_text: "Written in Obsidian, version-controlled in Git, deployed automatically on every push."
  },
  de: {
    page_title: "your-name — DevOps-Lernportfolio",
    brand_name: "your-name",
    nav_about: "Über mich",
    nav_guide: "Für Leser:innen",
    nav_sessions: "Arbeitsprotokoll",
    hero_eyebrow: "systemtechnik — devops lernen, öffentlich dokumentiert",
    hero_title: "Von grundlegenden IT-Kenntnissen zu echter Infrastruktur — Schritt für Schritt dokumentiert.",
    hero_lead: "Ich arbeite gezielt auf eine DevOps-Rolle mit Kubernetes-Schwerpunkt hin, beginnend bei den Grundlagen. Dies ist mein Arbeitslog: was ich gebaut habe, was kaputtging und was ich beim Beheben gelernt habe — vollständig transparent.",
    link_cv: "Lebenslauf", link_linkedin: "LinkedIn", link_github: "GitHub",
    status_label: "status", status_value: "aktiv am Aufbauen",
    started_label: "gestartet", uptime_label: "uptime",
    focus_label: "fokus", stack_label: "stack",
    day_word: "Tag",
    ws_title: "Wie ich arbeite",
    ws_item1: "Ich versuche Dinge zunächst selbst zu lösen und dokumentiere währenddessen — stecke ich fest, frage ich frühzeitig nach, statt stundenlang allein zu suchen.",
    ws_item2: "Jeder Eintrag zeigt auch, was nicht funktioniert hat — nicht nur das Endergebnis. Genau dort fand das eigentliche Lernen statt.",
    ws_item3: "Dokumentation ist für mich Teil der Arbeit, kein nachträglicher Schritt — Teamkolleg:innen sollten nicht rekonstruieren müssen, was ich getan habe.",
    guide_title: "Kurzleitfaden für Leser:innen",
    guide_intro: "Wenig Zeit? Wählen Sie die passende Rolle — Sie erhalten direkt einen Hinweis, was am relevantesten ist.",
    role_recruiter_label: "Recruiter", role_lead_label: "Team-/Bereichsleitung",
    role_cto_label: "CTO / Direktion", role_exec_label: "Geschäftsführung",
    role_recruiter_text: "Beginnen Sie mit der Einleitung oben und überfliegen Sie dann Titel und Zusammenfassung der beiden neuesten Einträge unten — das reicht, um Entwicklung und Dokumentationsqualität einzuschätzen.",
    role_lead_text: "Öffnen Sie einen Eintrag aus Ihrem Themenbereich und lesen Sie zuerst den Abschnitt „Herausforderungen“ — dort zeigt sich die tatsächliche Problemlösungskompetenz, nicht nur das fertige Ergebnis.",
    role_cto_text: "Vergleichen Sie den ältesten mit dem neuesten Eintrag, um die Entwicklung in Tiefe und Argumentation zu sehen. Die Einleitung oben erläutert Ansatz und Beweggründe für diesen Lernweg.",
    role_exec_text: "Die Einleitung oben sowie der Titel des neuesten Eintrags geben Ihnen die Kernaussage: jemand, der praxisrelevante Infrastruktur-Kompetenzen methodisch aufbaut und klar genug dokumentiert, dass jeder den Fortschritt nachvollziehen kann.",
    sessions_title: "Arbeitsprotokoll",
    sessions_sub: "Neueste zuerst — ein laufendes Protokoll dessen, was ich gebaut, kaputt gemacht und gelernt habe.",
    did_label: "Was ich gemacht habe", learned_label: "Was ich gelernt habe",
    challenges_label: "Herausforderungen & Lösungen", evidence_label: "Belege",
    read_more: "Eintrag öffnen",
    status_done: "abgeschlossen", status_progress: "in Arbeit",
    footer_text: "Geschrieben in Obsidian, versioniert in Git, automatisch bei jedem Push deployed."
  }
};

const sessions = [
  {
    id: "k8s-pi-cluster", date: "2026-06-18", hash: "f0c3a1", status: "progress",
    tags: ["topic=kubernetes","level=intermediate","env=homelab"],
    en: {
      title: "Building a 3-Node Kubernetes Cluster on Raspberry Pi",
      summary: "Moved from a single Minikube cluster to three real Raspberry Pi nodes — hands-on with kubeadm, networking, and the things that only break on real hardware.",
      did: [
        "Flashed Raspberry Pi OS Lite on three Pi 4s and configured static IPs",
        "Bootstrapped the cluster with kubeadm init / kubeadm join",
        "Installed Calico as the CNI and verified pod-to-pod networking across nodes",
        "Deployed a small test app behind a NodePort service to confirm it routes correctly"
      ],
      learned: [
        "The difference between a CNI plugin's job and kube-proxy's job — and why pods couldn't reach each other until I fixed a CIDR mismatch",
        "How kubeadm actually bootstraps a control plane vs. what Minikube was hiding from me",
        "Why a cgroup driver mismatch between kubelet and the container runtime causes nodes to silently fail to join"
      ],
      challenges: [
        "Worker nodes joined but stayed NotReady — caused by a cgroup driver mismatch between containerd and kubelet, fixed by aligning both to systemd",
        "Pod-to-pod traffic was dropped across nodes until I corrected an overlapping CIDR range between the pod network and my home LAN"
      ],
      evidence: "$ kubectl get nodes\nNAME      STATUS   ROLES           VERSION\npi-node1  Ready    control-plane   v1.30.2\npi-node2  Ready    <none>          v1.30.2\npi-node3  Ready    <none>          v1.30.2"
    },
    de: {
      title: "Aufbau eines 3-Knoten-Kubernetes-Clusters auf Raspberry Pi",
      summary: "Vom einzelnen Minikube-Cluster zu drei echten Raspberry-Pi-Knoten — praktische Erfahrung mit kubeadm, Netzwerk und allem, was erst auf echter Hardware kaputtgeht.",
      did: [
        "Raspberry Pi OS Lite auf drei Pi 4 geflasht und statische IPs konfiguriert",
        "Cluster mit kubeadm init / kubeadm join aufgesetzt",
        "Calico als CNI installiert und Pod-zu-Pod-Netzwerk über Knoten hinweg geprüft",
        "Kleine Testanwendung hinter einem NodePort-Service bereitgestellt, um das Routing zu prüfen"
      ],
      learned: [
        "Der Unterschied zwischen der Aufgabe eines CNI-Plugins und der von kube-proxy — und warum Pods sich erst nach Behebung eines CIDR-Konflikts erreichen konnten",
        "Wie kubeadm eine Control Plane tatsächlich bootstrapped — im Gegensatz zu dem, was Minikube verborgen hat",
        "Warum unterschiedliche cgroup-Treiber zwischen kubelet und Container-Runtime dazu führen, dass Knoten dem Cluster nicht beitreten"
      ],
      challenges: [
        "Worker-Knoten sind beigetreten, blieben aber NotReady — Ursache war ein cgroup-Treiber-Konflikt zwischen containerd und kubelet, behoben durch Angleichung auf systemd",
        "Pod-zu-Pod-Traffic wurde knotenübergreifend verworfen, bis ich eine Überlappung zwischen Pod-Netzwerk und Heimnetzwerk-CIDR korrigiert habe"
      ],
      evidence: "$ kubectl get nodes\nNAME      STATUS   ROLES           VERSION\npi-node1  Ready    control-plane   v1.30.2\npi-node2  Ready    <none>          v1.30.2\npi-node3  Ready    <none>          v1.30.2"
    }
  },
  {
    id: "docker-first-steps", date: "2026-05-30", hash: "9b21e7", status: "done",
    tags: ["topic=docker","level=beginner","env=local"],
    en: {
      title: "First Steps with Docker: Containerizing a Small App",
      summary: "Took a small Python script and turned it into a portable, reproducible container — and understood what “it works on my machine” was actually hiding.",
      did: [
        "Wrote a Dockerfile for a small Flask app, starting from python:slim",
        "Used multi-stage builds to keep the final image small",
        "Set up .dockerignore and passed environment variables via docker run --env-file",
        "Pushed the image to a private registry and pulled it on a second machine to confirm portability"
      ],
      learned: [
        "Why image layer order matters for build cache and final image size",
        "The difference between CMD and ENTRYPOINT, and when to use each",
        "That “works on my machine” usually means “works with dependencies I forgot I installed”"
      ],
      challenges: [
        "Initial image was 1.2GB — reduced to 184MB by switching the base image and using multi-stage builds",
        "Environment variables worked locally but not after pushing to the registry — I had hardcoded a path instead of using the env var"
      ],
      evidence: "$ docker images\nREPOSITORY     TAG       SIZE\nmy-flask-app   v1        184MB"
    },
    de: {
      title: "Erste Schritte mit Docker: Eine kleine App containerisieren",
      summary: "Ein kleines Python-Skript in einen portablen, reproduzierbaren Container verwandelt — und verstanden, was sich hinter „läuft bei mir“ wirklich verbirgt.",
      did: [
        "Dockerfile für eine kleine Flask-App geschrieben, ausgehend von python:slim",
        "Multi-Stage-Builds genutzt, um das finale Image klein zu halten",
        ".dockerignore eingerichtet und Umgebungsvariablen über docker run --env-file gesetzt",
        "Image in eine private Registry gepusht und auf einer zweiten Maschine gepullt, um Portabilität zu prüfen"
      ],
      learned: [
        "Warum die Reihenfolge der Image-Layer für Build-Cache und Image-Größe entscheidend ist",
        "Der Unterschied zwischen CMD und ENTRYPOINT — und wann man was nutzt",
        "Dass „läuft bei mir“ meist bedeutet: „läuft mit Abhängigkeiten, die ich vergessen habe zu erwähnen“"
      ],
      challenges: [
        "Erstes Image war 1,2GB groß — durch ein anderes Basis-Image und Multi-Stage-Builds auf 184MB reduziert",
        "Umgebungsvariablen funktionierten lokal, aber nicht nach dem Push in die Registry — Ursache war ein hartcodierter Pfad statt der Umgebungsvariable"
      ],
      evidence: "$ docker images\nREPOSITORY     TAG       SIZE\nmy-flask-app   v1        184MB"
    }
  },
  {
    id: "linux-fundamentals", date: "2026-05-10", hash: "3d77a4", status: "done",
    tags: ["topic=linux","level=fundamentals","env=homelab"],
    en: {
      title: "Linux Fundamentals on My Homelab",
      summary: "Set up a dedicated homelab box and went back to basics: filesystem hierarchy, permissions, systemd, and actually reading logs instead of guessing.",
      did: [
        "Installed Debian on a spare mini PC and set up SSH key-based access",
        "Practiced user/group permissions, chmod/chown, and sudoers configuration",
        "Set up and debugged a systemd service for a small script that runs on boot",
        "Got comfortable navigating journalctl and /var/log instead of restarting things blindly"
      ],
      learned: [
        "How the Linux filesystem hierarchy is organized and why it matters for troubleshooting",
        "The actual difference between a process owner, a file owner, and group permissions",
        "That systemd unit files are easier to debug with journalctl -u <service> than I expected"
      ],
      challenges: [
        "My systemd service failed silently on boot — journalctl showed a PATH issue inside the unit file, not the script itself",
        "Locked myself out of sudo briefly by misconfiguring /etc/sudoers — fixed via recovery mode, learned to always use visudo"
      ],
      evidence: "$ systemctl status homelab-sync.service\n● homelab-sync.service - Homelab sync job\n   Active: active (running) since Sat 2026-05-09 21:14:02"
    },
    de: {
      title: "Linux-Grundlagen auf meiner Homelab-Maschine",
      summary: "Eine eigene Homelab-Maschine aufgesetzt und zurück zu den Grundlagen: Dateisystemhierarchie, Berechtigungen, systemd — und Logs tatsächlich lesen statt raten.",
      did: [
        "Debian auf einem Mini-PC installiert und SSH-Zugang per Key eingerichtet",
        "Benutzer-/Gruppenberechtigungen, chmod/chown und sudoers-Konfiguration geübt",
        "Einen systemd-Service für ein Boot-Skript eingerichtet und debuggt",
        "Sicheren Umgang mit journalctl und /var/log statt blindem Neustarten geübt"
      ],
      learned: [
        "Wie die Linux-Dateisystemhierarchie aufgebaut ist und warum das für die Fehlersuche wichtig ist",
        "Der tatsächliche Unterschied zwischen Prozessbesitzer, Dateibesitzer und Gruppenberechtigungen",
        "Dass sich systemd-Unit-Dateien mit journalctl -u <service> einfacher debuggen lassen als gedacht"
      ],
      challenges: [
        "Mein systemd-Service scheiterte beim Boot lautlos — journalctl zeigte ein PATH-Problem in der Unit-Datei, nicht im Skript selbst",
        "Mich kurzzeitig aus sudo ausgesperrt durch eine falsche /etc/sudoers-Konfiguration — per Recovery-Modus behoben, seitdem immer visudo verwendet"
      ],
      evidence: "$ systemctl status homelab-sync.service\n● homelab-sync.service - Homelab sync job\n   Active: active (running) since Sat 2026-05-09 21:14:02"
    }
  }
];

// Newest first, always — based on date, not array order.
// You can add a new entry anywhere in the array above; it will
// still land in the right place.
sessions.sort((a, b) => b.date.localeCompare(a.date));

let currentLang = "en";
let currentRole = "recruiter";

function applyI18n(lang){
  document.querySelectorAll("[data-i18n]").forEach(el => {
    const key = el.getAttribute("data-i18n");
    if (ui[lang][key] !== undefined) el.textContent = ui[lang][key];
  });
  document.documentElement.lang = lang;
  document.title = ui[lang].page_title;
}

function renderRolePanel(role, lang){
  document.getElementById("role-panel").innerHTML =
    `<p>${ui[lang]["role_" + role + "_text"]}</p>`;
}

function renderSessions(lang){
  const feed = document.getElementById("sessions-feed");
  feed.innerHTML = "";
  sessions.forEach(s => {
    const t = s[lang];
    const statusWord = s.status === "done" ? ui[lang].status_done : ui[lang].status_progress;
    const dotClass = s.status === "done" ? "status-dot--ok" : "status-dot--progress";

    const details = document.createElement("details");
    details.className = "entry";

    const summary = document.createElement("summary");
    summary.innerHTML = `
      <div class="entry-meta">
        <span class="status-dot ${dotClass}"></span>
        <time>${s.date}</time>
        <span class="entry-hash">#${s.hash}</span>
        <span class="entry-status-label">· ${statusWord}</span>
      </div>
      <h3 class="entry-title">${t.title}</h3>
      <p class="entry-lead">${t.summary}</p>
      <div class="entry-tags">${s.tags.map(tag => `<span class="chip">${tag}</span>`).join("")}</div>
      <span class="entry-toggle"><span class="chevron">›</span> ${ui[lang].read_more}</span>
    `;

    const body = document.createElement("div");
    body.className = "entry-body";
    body.innerHTML = `
      <div class="entry-field"><h4>${ui[lang].did_label}</h4><ul>${t.did.map(i => `<li>${i}</li>`).join("")}</ul></div>
      <div class="entry-field"><h4>${ui[lang].learned_label}</h4><ul>${t.learned.map(i => `<li>${i}</li>`).join("")}</ul></div>
      <div class="entry-field"><h4>${ui[lang].challenges_label}</h4><ul>${t.challenges.map(i => `<li>${i}</li>`).join("")}</ul></div>
      <div class="entry-field entry-evidence"><h4>${ui[lang].evidence_label}</h4><pre><code>${t.evidence}</code></pre></div>
    `;

    details.appendChild(summary);
    details.appendChild(body);
    feed.appendChild(details);
  });
}

function updateDynamicStatus(lang){
  const startDate = new Date("2026-05-01T00:00:00");
  const days = Math.max(0, Math.floor((Date.now() - startDate) / 86400000));
  document.getElementById("started-value").textContent = "2026-05-01";
  document.getElementById("uptime-value").textContent = `${ui[lang].day_word} ${days}`;
}

function setLang(lang){
  currentLang = lang;
  document.querySelectorAll(".lang-btn").forEach(btn => {
    const active = btn.dataset.lang === lang;
    btn.classList.toggle("active", active);
    btn.setAttribute("aria-pressed", active ? "true" : "false");
  });
  applyI18n(lang);
  updateDynamicStatus(lang);
  renderSessions(lang);
  renderRolePanel(currentRole, lang);
}

function setRole(role){
  currentRole = role;
  document.querySelectorAll(".role-tab").forEach(btn => {
    const active = btn.dataset.role === role;
    btn.classList.toggle("active", active);
    btn.setAttribute("aria-selected", active ? "true" : "false");
  });
  renderRolePanel(role, currentLang);
}

document.querySelectorAll(".lang-btn").forEach(btn => {
  btn.addEventListener("click", () => setLang(btn.dataset.lang));
});
document.querySelectorAll(".role-tab").forEach(btn => {
  btn.addEventListener("click", () => setRole(btn.dataset.role));
});

setLang("en");
setRole("recruiter");
</script>
</body>
</html>