mkdir -p /home/claude/portfolio
cat > /home/claude/portfolio/index.html << 'HTMLEOF'
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Yassin ElSeba3e — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;700;900&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
:root {
  --gold: #eab308;
  --gold2: #ca8a04;
  --bg: #060608;
  --card: #0f0f13;
  --card2: #14141a;
  --border: rgba(234,179,8,0.12);
  --text: #f0f0f0;
  --muted: #555566;
  --glow: 0 0 40px rgba(234,179,8,0.15);
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: 'Cairo', sans-serif;
  background: var(--bg);
  color: var(--text);
  overflow-x: hidden;
  cursor: none;
}

/* ─── CURSOR ─── */
.cursor {
  position: fixed; width: 12px; height: 12px;
  background: var(--gold); border-radius: 50%;
  pointer-events: none; z-index: 9999;
  transform: translate(-50%,-50%);
  transition: transform 0.1s, width 0.2s, height 0.2s, opacity 0.2s;
  mix-blend-mode: difference;
}
.cursor-ring {
  position: fixed; width: 36px; height: 36px;
  border: 1.5px solid var(--gold); border-radius: 50%;
  pointer-events: none; z-index: 9998;
  transform: translate(-50%,-50%);
  transition: transform 0.15s ease, width 0.3s, height 0.3s;
  opacity: 0.5;
}

/* ─── NOISE OVERLAY ─── */
body::before {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 1; opacity: 0.4;
}

/* ─── GRID BG ─── */
body::after {
  content: '';
  position: fixed; inset: 0;
  background-image:
    linear-gradient(rgba(234,179,8,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(234,179,8,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  pointer-events: none; z-index: 0;
}

/* ─── NAV ─── */
nav {
  position: fixed; top: 0; left: 0; right: 0;
  z-index: 100;
  background: rgba(6,6,8,0.85);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
  padding: 0 40px;
  height: 64px;
  display: flex; align-items: center; justify-content: space-between;
}
.nav-brand {
  font-family: 'Space Mono', monospace;
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--gold);
  letter-spacing: 1px;
}
.nav-brand span { color: var(--text); }
.nav-links { display: flex; gap: 32px; list-style: none; }
.nav-links a {
  color: var(--muted);
  text-decoration: none;
  font-size: 0.85rem;
  font-weight: 700;
  transition: color 0.2s;
  letter-spacing: 1px;
}
.nav-links a:hover { color: var(--gold); }

/* ─── HERO ─── */
#hero {
  position: relative;
  min-height: 100vh;
  display: flex; align-items: center; justify-content: center;
  text-align: center;
  z-index: 2;
  padding: 80px 20px 60px;
  overflow: hidden;
}
.hero-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
}
.orb1 { width: 500px; height: 500px; background: rgba(234,179,8,0.07); top: -100px; right: -100px; animation: orbFloat 8s ease-in-out infinite; }
.orb2 { width: 300px; height: 300px; background: rgba(202,138,4,0.05); bottom: 0; left: -50px; animation: orbFloat 10s ease-in-out infinite reverse; }
@keyframes orbFloat { 0%,100%{transform:translateY(0) scale(1)} 50%{transform:translateY(-30px) scale(1.05)} }

.hero-badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(234,179,8,0.08);
  border: 1px solid rgba(234,179,8,0.2);
  border-radius: 100px;
  padding: 6px 18px;
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--gold);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 28px;
  animation: fadeUp 0.8s ease both;
}
.badge-dot { width: 7px; height: 7px; background: var(--gold); border-radius: 50%; animation: pulse 2s infinite; }
@keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.5;transform:scale(1.4)} }

.hero-name {
  font-size: clamp(3rem, 8vw, 6rem);
  font-weight: 900;
  line-height: 1.05;
  letter-spacing: -2px;
  animation: fadeUp 0.8s 0.1s ease both;
}
.hero-name .gold { color: var(--gold); }
.hero-name .outline {
  -webkit-text-stroke: 1.5px var(--gold);
  color: transparent;
}

.hero-title {
  font-family: 'Space Mono', monospace;
  font-size: clamp(0.75rem, 2vw, 1rem);
  color: var(--muted);
  letter-spacing: 4px;
  text-transform: uppercase;
  margin: 16px 0 32px;
  animation: fadeUp 0.8s 0.2s ease both;
}

.hero-desc {
  max-width: 540px;
  margin: 0 auto 44px;
  font-size: 1.05rem;
  color: #888899;
  line-height: 1.8;
  animation: fadeUp 0.8s 0.3s ease both;
}

.hero-cta {
  display: flex; gap: 14px; justify-content: center; flex-wrap: wrap;
  animation: fadeUp 0.8s 0.4s ease both;
}
.btn-primary {
  display: inline-flex; align-items: center; gap: 8px;
  background: linear-gradient(135deg, var(--gold), var(--gold2));
  color: #000;
  font-family: 'Cairo', sans-serif;
  font-weight: 900;
  font-size: 0.9rem;
  padding: 13px 28px;
  border-radius: 12px;
  text-decoration: none;
  border: none; cursor: none;
  transition: opacity 0.2s, transform 0.2s;
  box-shadow: 0 4px 20px rgba(234,179,8,0.3);
}
.btn-primary:hover { opacity: 0.9; transform: translateY(-2px); }
.btn-ghost {
  display: inline-flex; align-items: center; gap: 8px;
  background: transparent;
  color: var(--text);
  font-family: 'Cairo', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 12px 28px;
  border-radius: 12px;
  text-decoration: none;
  border: 1px solid var(--border);
  cursor: none;
  transition: border-color 0.2s, color 0.2s, transform 0.2s;
}
.btn-ghost:hover { border-color: var(--gold); color: var(--gold); transform: translateY(-2px); }

.scroll-hint {
  position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%);
  display: flex; flex-direction: column; align-items: center; gap: 6px;
  color: var(--muted); font-size: 0.7rem; letter-spacing: 2px; text-transform: uppercase;
  animation: fadeUp 1s 0.8s ease both;
}
.scroll-line { width: 1px; height: 40px; background: linear-gradient(to bottom, var(--gold), transparent); animation: scrollAnim 2s ease-in-out infinite; }
@keyframes scrollAnim { 0%{opacity:0;transform:scaleY(0);transform-origin:top} 50%{opacity:1;transform:scaleY(1)} 100%{opacity:0;transform:scaleY(0);transform-origin:bottom} }

@keyframes fadeUp { from{opacity:0;transform:translateY(24px)} to{opacity:1;transform:translateY(0)} }

/* ─── SECTION SHARED ─── */
section { position: relative; z-index: 2; padding: 100px 40px; }
.section-label {
  font-family: 'Space Mono', monospace;
  font-size: 0.7rem;
  color: var(--gold);
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.section-title {
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 16px;
}
.section-sub {
  color: var(--muted);
  font-size: 1rem;
  max-width: 500px;
}
.section-head { margin-bottom: 60px; }
.max-w { max-width: 1100px; margin: 0 auto; }

/* ─── SKILLS ─── */
#skills { background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
  gap: 16px;
}
.skill-pill {
  display: flex; flex-direction: column; align-items: center; gap: 10px;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 20px 14px;
  font-size: 0.82rem;
  font-weight: 700;
  color: #aaa;
  transition: all 0.25s;
  text-align: center;
}
.skill-pill:hover {
  border-color: var(--gold);
  color: var(--gold);
  transform: translateY(-4px);
  box-shadow: var(--glow);
}
.skill-pill i { font-size: 1.6rem; color: var(--gold); }
.skill-pill img { width: 28px; height: 28px; object-fit: contain; filter: brightness(0.8); }
.skill-pill:hover img { filter: brightness(1.2); }

/* ─── PROJECTS ─── */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(480px, 1fr));
  gap: 28px;
}
@media(max-width:560px){ .projects-grid { grid-template-columns: 1fr; } }

.project-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 24px;
  overflow: hidden;
  transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
  position: relative;
}
.project-card:hover {
  transform: translateY(-8px);
  border-color: rgba(234,179,8,0.4);
  box-shadow: var(--glow);
}
.project-preview {
  height: 220px;
  position: relative;
  overflow: hidden;
  background: #0a0a0e;
}
.project-preview iframe {
  width: 100%; height: 100%;
  border: none;
  pointer-events: none;
  transform: scale(1); transform-origin: top left;
  opacity: 0.85;
  transition: opacity 0.3s;
}
.project-card:hover .project-preview iframe { opacity: 1; }
.preview-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(to bottom, transparent 40%, var(--card) 100%);
  z-index: 1;
}
.preview-badge {
  position: absolute; top: 14px; right: 14px; z-index: 2;
  display: flex; align-items: center; gap: 6px;
  background: rgba(6,6,8,0.85);
  border: 1px solid var(--border);
  border-radius: 100px;
  padding: 5px 12px;
  font-size: 0.72rem; font-weight: 700; color: var(--gold);
  backdrop-filter: blur(10px);
}
.live-dot { width: 6px; height: 6px; background: #22c55e; border-radius: 50%; animation: pulse 2s infinite; }

.project-body { padding: 24px 28px 28px; }
.project-icon {
  width: 52px; height: 52px;
  border-radius: 14px;
  background: linear-gradient(135deg, rgba(234,179,8,0.15), rgba(234,179,8,0.05));
  border: 1px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  font-size: 1.4rem;
  margin-bottom: 16px;
}
.project-name {
  font-size: 1.3rem; font-weight: 900;
  margin-bottom: 8px;
}
.project-desc {
  color: #77778a;
  font-size: 0.88rem;
  line-height: 1.7;
  margin-bottom: 20px;
}
.project-tags { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 24px; }
.tag {
  background: rgba(234,179,8,0.06);
  border: 1px solid rgba(234,179,8,0.15);
  color: var(--gold);
  font-size: 0.72rem; font-weight: 700;
  padding: 4px 12px; border-radius: 100px;
  font-family: 'Space Mono', monospace;
}
.project-features {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 8px; margin-bottom: 24px;
}
.feat {
  display: flex; align-items: center; gap: 8px;
  font-size: 0.8rem; color: #888899;
}
.feat i { color: var(--gold); font-size: 0.75rem; width: 14px; }
.project-btn {
  display: inline-flex; align-items: center; gap: 10px;
  width: 100%;
  background: linear-gradient(135deg, var(--gold), var(--gold2));
  color: #000;
  font-family: 'Cairo', sans-serif;
  font-weight: 900;
  font-size: 0.9rem;
  padding: 13px 20px;
  border-radius: 12px;
  text-decoration: none;
  border: none; cursor: none;
  transition: opacity 0.2s, transform 0.2s;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(234,179,8,0.2);
}
.project-btn:hover { opacity: 0.88; transform: translateY(-1px); }

/* ─── ABOUT ─── */
#about { background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center; }
@media(max-width:700px){ .about-grid { grid-template-columns: 1fr; gap: 40px; } }

.about-code {
  background: #0a0a0e;
  border: 1px solid var(--border);
  border-radius: 18px;
  padding: 28px;
  font-family: 'Space Mono', monospace;
  font-size: 0.82rem;
  line-height: 1.9;
  color: #888899;
  position: relative;
  overflow: hidden;
}
.about-code::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 3px;
  background: linear-gradient(90deg, var(--gold), transparent);
}
.code-line { display: block; }
.c-key { color: #7ee8a2; }
.c-str { color: #e6a817; }
.c-val { color: #aaaaff; }
.c-muted { color: #444455; }
.c-gold { color: var(--gold); }

.about-text h3 { font-size: 1.6rem; font-weight: 900; margin-bottom: 16px; }
.about-text p { color: #77778a; line-height: 1.8; margin-bottom: 16px; font-size: 0.95rem; }
.stat-row { display: flex; gap: 28px; margin-top: 28px; flex-wrap: wrap; }
.stat-item { text-align: center; }
.stat-num { font-size: 2rem; font-weight: 900; color: var(--gold); font-family: 'Space Mono', monospace; }
.stat-lbl { font-size: 0.72rem; color: var(--muted); letter-spacing: 2px; text-transform: uppercase; }

/* ─── CONTACT ─── */
#contact { text-align: center; }
.contact-card {
  max-width: 600px;
  margin: 0 auto;
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 28px;
  padding: 52px 44px;
  position: relative;
  overflow: hidden;
}
.contact-card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, transparent, var(--gold), transparent);
}
.contact-card h3 { font-size: 1.5rem; font-weight: 900; margin-bottom: 12px; }
.contact-card p { color: var(--muted); margin-bottom: 36px; line-height: 1.7; }

.contact-links { display: flex; justify-content: center; gap: 16px; flex-wrap: wrap; margin-bottom: 28px; }
.contact-link {
  width: 52px; height: 52px;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: 14px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem;
  color: var(--muted);
  text-decoration: none;
  transition: all 0.2s;
  cursor: none;
}
.contact-link:hover { border-color: var(--gold); color: var(--gold); transform: translateY(-3px); box-shadow: var(--glow); }

.contact-email {
  display: inline-flex; align-items: center; gap: 10px;
  background: rgba(234,179,8,0.06);
  border: 1px solid rgba(234,179,8,0.15);
  border-radius: 12px;
  padding: 12px 24px;
  color: var(--gold);
  font-family: 'Space Mono', monospace;
  font-size: 0.85rem;
  text-decoration: none;
  transition: all 0.2s;
  cursor: none;
}
.contact-email:hover { background: rgba(234,179,8,0.12); }

/* ─── FOOTER ─── */
footer {
  position: relative; z-index: 2;
  border-top: 1px solid var(--border);
  padding: 28px 40px;
  display: flex; align-items: center; justify-content: space-between;
  flex-wrap: wrap; gap: 12px;
}
footer p { color: var(--muted); font-size: 0.8rem; }
footer .mono { font-family: 'Space Mono', monospace; color: var(--gold); font-size: 0.78rem; }

/* ─── SCROLL ANIMATIONS ─── */
.reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
.reveal.visible { opacity: 1; transform: translateY(0); }

/* ─── RESPONSIVE ─── */
@media(max-width:768px){
  nav { padding: 0 20px; }
  .nav-links { display: none; }
  section { padding: 80px 20px; }
  footer { padding: 20px; flex-direction: column; text-align: center; }
  .projects-grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-brand">YS<span>.</span>dev</div>
  <ul class="nav-links">
    <li><a href="#projects">المشاريع</a></li>
    <li><a href="#skills">المهارات</a></li>
    <li><a href="#about">عني</a></li>
    <li><a href="#contact">تواصل</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-orb orb1"></div>
  <div class="hero-orb orb2"></div>
  <div>
    <div class="hero-badge"><div class="badge-dot"></div> متاح للعمل · Available for Work</div>
    <h1 class="hero-name">
      <span class="gold">Yassin</span><br>
      <span class="outline">ElSeba3e</span>
    </h1>
    <p class="hero-title">Full-Stack Developer · Egypt 🇪🇬</p>
    <p class="hero-desc">بحوّل الأفكار لمنتجات رقمية حقيقية — من الـ UI للـ API للـ Database. أسلوبي: بسيط، سريع، يشتغل.</p>
    <div class="hero-cta">
      <a href="#projects" class="btn-primary"><i class="fas fa-rocket"></i> شوف مشاريعي</a>
      <a href="#contact" class="btn-ghost"><i class="fas fa-envelope"></i> تواصل معي</a>
    </div>
  </div>
  <div class="scroll-hint">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="max-w">
    <div class="section-head reveal">
      <div class="section-label">// Tech Stack</div>
      <h2 class="section-title">الأدوات اللي بشتغل بيها</h2>
      <p class="section-sub">كل حاجة اشتغلت بيها في مشاريع حقيقية على Production</p>
    </div>
    <div class="skills-grid">
      <div class="skill-pill reveal"><i class="fab fa-html5" style="color:#e34f26"></i>HTML5</div>
      <div class="skill-pill reveal"><i class="fab fa-css3-alt" style="color:#1572b6"></i>CSS3</div>
      <div class="skill-pill reveal"><i class="fab fa-js" style="color:#f7df1e"></i>JavaScript</div>
      <div class="skill-pill reveal"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg" alt="Tailwind">Tailwind CSS</div>
      <div class="skill-pill reveal"><img src="https://alpinejs.dev/alpine_long.svg" alt="Alpine.js" style="height:20px;width:auto">Alpine.js</div>
      <div class="skill-pill reveal"><i class="fab fa-node-js" style="color:#339933"></i>Node.js</div>
      <div class="skill-pill reveal"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/supabase/supabase-original.svg" alt="Supabase">Supabase</div>
      <div class="skill-pill reveal"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" alt="PostgreSQL">PostgreSQL</div>
      <div class="skill-pill reveal"><i class="fab fa-git-alt" style="color:#f05032"></i>Git</div>
      <div class="skill-pill reveal"><i class="fab fa-github"></i>GitHub</div>
      <div class="skill-pill reveal"><img src="https://assets.vercel.com/image/upload/front/favicon/vercel/57x57.png" alt="Vercel">Vercel</div>
      <div class="skill-pill reveal"><img src="https://www.gstatic.com/devrel-devsite/prod/ve79f18a3b2c059f9d3e0cf78bd7b67ebbcf02f3e7fdb06b9bad42bdc26c8fb73/firebase/images/touchicon-180.png" alt="Firebase">Firebase</div>
      <div class="skill-pill reveal"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg" alt="VS Code">VS Code</div>
      <div class="skill-pill reveal"><i class="fas fa-server" style="color:#ff6c37"></i>REST API</div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="max-w">
    <div class="section-head reveal">
      <div class="section-label">// Projects</div>
      <h2 class="section-title">أبرز المشاريع</h2>
      <p class="section-sub">مشاريع حقيقية على Production — مش demos</p>
    </div>
    <div class="projects-grid">

      <!-- OMAR STORE -->
      <div class="project-card reveal">
        <div class="project-preview">
          <div class="preview-badge"><div class="live-dot"></div> Live</div>
          <iframe src="https://omar-storee.vercel.app" title="Omar Store" loading="lazy" sandbox="allow-scripts allow-same-origin"></iframe>
          <div class="preview-overlay"></div>
        </div>
        <div class="project-body">
          <div class="project-icon">🏪</div>
          <div class="project-name">Omar Store</div>
          <p class="project-desc">متجر مكملات رياضية متكامل — صفحة رئيسية ديناميكية، لوحة إدارة محمية، API كاملة للمنتجات والفئات، نظام خصومات، ورفع صور. ربط كامل مع Supabase.</p>
          <div class="project-tags">
            <span class="tag">Vanilla JS</span>
            <span class="tag">Tailwind CSS</span>
            <span class="tag">Supabase</span>
            <span class="tag">Vercel</span>
            <span class="tag">REST API</span>
          </div>
          <div class="project-features">
            <div class="feat"><i class="fas fa-check"></i>Admin Panel محمي</div>
            <div class="feat"><i class="fas fa-check"></i>نظام خصومات مرن</div>
            <div class="feat"><i class="fas fa-check"></i>CRUD كامل للفئات</div>
            <div class="feat"><i class="fas fa-check"></i>رفع صور مباشر</div>
            <div class="feat"><i class="fas fa-check"></i>Responsive design</div>
            <div class="feat"><i class="fas fa-check"></i>إدارة آراء العملاء</div>
          </div>
          <a href="https://omar-storee.vercel.app" target="_blank" class="project-btn">
            <i class="fas fa-external-link-alt"></i> زيارة المشروع
          </a>
        </div>
      </div>

      <!-- STEM SADK -->
      <div class="project-card reveal">
        <div class="project-preview">
          <div class="preview-badge"><div class="live-dot"></div> Live</div>
          <iframe src="https://stem-sadk.web.app/challenge.html" title="SADK Deutsch Klub" loading="lazy" sandbox="allow-scripts allow-same-origin"></iframe>
          <div class="preview-overlay"></div>
        </div>
        <div class="project-body">
          <div class="project-icon">🇩🇪</div>
          <div class="project-name">SADK Deutsch Klub</div>
          <p class="project-desc">منصة تفاعلية لتعلم اللغة الألمانية — تحديات يومية، نظام مستويات (A1→C2)، leaderboard عالمي، نظام XP وStreaks، وتسجيل دخول كامل.</p>
          <div class="project-tags">
            <span class="tag">HTML5</span>
            <span class="tag">CSS3</span>
            <span class="tag">JavaScript</span>
            <span class="tag">Firebase</span>
            <span class="tag">Auth System</span>
          </div>
          <div class="project-features">
            <div class="feat"><i class="fas fa-check"></i>تحديات يومية تفاعلية</div>
            <div class="feat"><i class="fas fa-check"></i>نظام XP و Streaks</div>
            <div class="feat"><i class="fas fa-check"></i>مستويات A1 → C2</div>
            <div class="feat"><i class="fas fa-check"></i>Global Leaderboard</div>
            <div class="feat"><i class="fas fa-check"></i>تسجيل دخول كامل</div>
            <div class="feat"><i class="fas fa-check"></i>تقييم فوري للإجابات</div>
          </div>
          <a href="https://stem-sadk.web.app/challenge.html" target="_blank" class="project-btn">
            <i class="fas fa-external-link-alt"></i> زيارة المشروع
          </a>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="max-w">
    <div class="about-grid">
      <div class="about-code reveal">
        <span class="code-line"><span class="c-muted">// about.js</span></span>
        <span class="code-line"> </span>
        <span class="code-line"><span class="c-key">const</span> <span class="c-gold">yassin</span> = {</span>
        <span class="code-line">  <span class="c-key">name</span>: <span class="c-str">"ياسين السباعي"</span>,</span>
        <span class="code-line">  <span class="c-key">role</span>: <span class="c-str">"Full-Stack Developer"</span>,</span>
        <span class="code-line">  <span class="c-key">location</span>: <span class="c-str">"🇪🇬 Egypt"</span>,</span>
        <span class="code-line">  <span class="c-key">passion</span>: <span class="c-str">"Products, not demos"</span>,</span>
        <span class="code-line">  <span class="c-key">stack</span>: [</span>
        <span class="code-line">    <span class="c-str">"JS"</span>, <span class="c-str">"Supabase"</span>,</span>
        <span class="code-line">    <span class="c-str">"Vercel"</span>, <span class="c-str">"Firebase"</span>,</span>
        <span class="code-line">  ],</span>
        <span class="code-line">  <span class="c-key">motto</span>: <span class="c-str">"Ship fast. Fix faster."</span>,</span>
        <span class="code-line">  <span class="c-key">coffee</span>: <span class="c-val">Infinity</span> ☕,</span>
        <span class="code-line">};</span>
      </div>
      <div class="about-text reveal">
        <div class="section-label">// About Me</div>
        <h3>من أنا؟</h3>
        <p>مطور Full-Stack بعشق بناء منتجات رقمية حقيقية — مش بس تمارين أو tutorials. بدأت من الصفر وبشتغل على مشاريع كاملة من تصميم الـ UI وحتى قواعد البيانات والـ API.</p>
        <p>أسلوبي: <strong style="color:var(--gold)">بسيط، سريع، يشتغل.</strong> بحوّل الأفكار لـ production في أقصر وقت ممكن.</p>
        <div class="stat-row">
          <div class="stat-item">
            <div class="stat-num">2+</div>
            <div class="stat-lbl">مشاريع Live</div>
          </div>
          <div class="stat-item">
            <div class="stat-num">5+</div>
            <div class="stat-lbl">Tech Used</div>
          </div>
          <div class="stat-item">
            <div class="stat-num">∞</div>
            <div class="stat-lbl">console.log</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="max-w">
    <div class="contact-card reveal">
      <div class="section-label" style="text-align:center;margin-bottom:8px">// Contact</div>
      <h3>خليني أسمع منك 👋</h3>
      <p>مهتم بمشروع؟ فرصة تعاون؟ أو بس عايز تقول سلام — الباب مفتوح دايماً.</p>
      <div class="contact-links">
        <a href="https://wa.me/201550434880" target="_blank" class="contact-link" title="WhatsApp" style="color:#25d366">
          <i class="fab fa-whatsapp"></i>
        </a>
        <a href="mailto:y2776970@gmail.com" class="contact-link" title="Email">
          <i class="fas fa-envelope"></i>
        </a>
        <a href="https://github.com/yasenyasenya123586744-png" target="_blank" class="contact-link" title="GitHub">
          <i class="fab fa-github"></i>
        </a>
      </div>
      <a href="mailto:y2776970@gmail.com" class="contact-email">
        <i class="fas fa-envelope"></i> y2776970@gmail.com
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p>© 2026 Yassin ElSeba3e — جميع الحقوق محفوظة</p>
  <span class="mono">Crafted with ☕ & console.log()</span>
</footer>

<script>
// ─── CURSOR ───
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursorRing');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx+'px'; cursor.style.top = my+'px'; });
(function animateRing(){ rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12; ring.style.left = rx+'px'; ring.style.top = ry+'px'; requestAnimationFrame(animateRing); })();
document.querySelectorAll('a,button,.skill-pill,.project-card').forEach(el => {
  el.addEventListener('mouseenter', () => { cursor.style.width='20px'; cursor.style.height='20px'; ring.style.width='52px'; ring.style.height='52px'; });
  el.addEventListener('mouseleave', () => { cursor.style.width='12px'; cursor.style.height='12px'; ring.style.width='36px'; ring.style.height='36px'; });
});

// ─── SCROLL REVEAL ───
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => { if(e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>
HTMLEOF
echo "Done"
