<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quantum QA — Roblox QA Testing & Anti-Cheat</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@500;600;700;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0c0c0f;
    --panel:#17171b;
    --panel-2:#1e1e23;
    --border:#2a2a30;
    --text:#f5f5f7;
    --text-muted:#9a9aa3;
    --text-dim:#68686f;
    --accent:#5170ff;
    --accent-soft:#7b93ff;
    --disp:'Plus Jakarta Sans', sans-serif;
    --body:'Inter', sans-serif;
  }
  *{ margin:0; padding:0; box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    background:var(--bg); color:var(--text); font-family:var(--body);
    line-height:1.6; -webkit-font-smoothing:antialiased;
  }
  a{ color:inherit; text-decoration:none; }
  ::selection{ background:var(--accent); color:#fff; }
  img,svg{ display:block; }

  section{ padding:150px 8vw; }
  @media(max-width:820px){ section{ padding:96px 6vw; } }

  /* ---------- NAV ---------- */
  .navwrap{ position:sticky; top:22px; z-index:50; display:flex; justify-content:center; padding:0 20px; }
  nav{
    width:100%; max-width:900px;
    display:flex; align-items:center; justify-content:space-between;
    background:rgba(23,23,27,0.82); backdrop-filter:blur(14px);
    border:1px solid var(--border); border-radius:999px;
    padding:10px 10px 10px 26px;
    box-shadow:0 20px 50px -25px rgba(0,0,0,0.6);
  }
  .logo{ font-family:var(--disp); font-weight:800; font-size:17px; letter-spacing:-0.01em; }
  .navlinks{ display:flex; gap:6px; }
  .navlinks a{
    font-size:14px; font-weight:500; color:var(--text-muted); padding:9px 16px;
    border-radius:999px; transition:all .2s;
  }
  .navlinks a:hover{ color:var(--text); background:var(--panel-2); }
  .navcta{
    background:#fff; color:#0c0c0f; font-weight:600; font-size:13.5px;
    padding:11px 22px; border-radius:999px; transition:transform .15s ease, opacity .15s ease;
  }
  .navcta:hover{ opacity:0.88; }
  @media(max-width:640px){ .navlinks{ display:none; } }

  /* ---------- HERO ---------- */
  .hero{
    padding-top:110px;
    display:grid; grid-template-columns:1.05fr 0.95fr; gap:70px; align-items:center;
  }
  @media(max-width:980px){ .hero{ grid-template-columns:1fr; padding-top:70px; } }

  .eyebrow{
    display:inline-flex; align-items:center; gap:8px; font-size:13.5px; font-weight:600;
    color:var(--accent-soft); background:rgba(81,112,255,0.1); border:1px solid rgba(81,112,255,0.25);
    padding:7px 16px; border-radius:999px; margin-bottom:26px;
  }
  .eyebrow .dot{ width:6px; height:6px; border-radius:50%; background:var(--accent-soft); }

  .hero h1{
    font-family:var(--disp); font-weight:800; font-size:clamp(38px,4.6vw,60px);
    line-height:1.06; letter-spacing:-0.02em; margin-bottom:24px;
  }
  .hero h1 .accent{ color:var(--accent-soft); }

  .hero p.lede{ color:var(--text-muted); font-size:17px; max-width:480px; margin-bottom:38px; }

  .ctas{ display:flex; gap:12px; flex-wrap:wrap; }
  .btn{
    font-weight:600; font-size:14.5px; padding:14px 26px; border-radius:999px;
    display:inline-flex; align-items:center; gap:8px; transition:all .2s;
  }
  .btn.primary{ background:#fff; color:#0c0c0f; }
  .btn.primary:hover{ opacity:0.88; }
  .btn.secondary{ border:1px solid var(--border); color:var(--text); }
  .btn.secondary:hover{ border-color:var(--text-dim); background:var(--panel); }

  /* signature glow block */
  .glowblock{
    position:relative; aspect-ratio:1/1; max-width:420px; margin:0 auto;
    border-radius:32px; background:linear-gradient(155deg, #5170ff 0%, #2c3fb0 100%);
    box-shadow: 0 40px 90px -30px rgba(81,112,255,0.45);
    display:flex; align-items:center; justify-content:center;
  }
  .glowblock svg{ width:46%; height:46%; }
  .glowblock::after{
    content:''; position:absolute; inset:-1px; border-radius:32px; border:1px solid rgba(255,255,255,0.14);
  }

  /* stat cards */
  .stats{ display:grid; grid-template-columns:repeat(3,1fr); gap:16px; margin-top:64px; }
  @media(max-width:820px){ .stats{ grid-template-columns:1fr; } }
  .stat{
    background:var(--panel); border:1px solid var(--border); border-radius:20px; padding:26px 24px;
  }
  .stat .n{ font-family:var(--disp); font-weight:800; font-size:30px; letter-spacing:-0.01em; }
  .stat .l{ color:var(--text-muted); font-size:14px; margin-top:6px; }

  /* ---------- SECTION HEAD ---------- */
  .shead{ max-width:600px; margin-bottom:56px; }
  .shead h2{ font-family:var(--disp); font-weight:800; font-size:clamp(30px,3.6vw,42px); letter-spacing:-0.02em; }
  .shead p{ color:var(--text-muted); margin-top:16px; font-size:16px; }

  /* ---------- SERVICES ---------- */
  .svc-grid{ display:grid; grid-template-columns:repeat(2,1fr); gap:20px; }
  @media(max-width:820px){ .svc-grid{ grid-template-columns:1fr; } }
  .svc{
    background:var(--panel); border:1px solid var(--border); border-radius:24px; padding:38px;
    transition:border-color .2s, transform .2s;
  }
  .svc:hover{ border-color:#3a3a42; transform:translateY(-3px); }
  .svc .icon{
    width:52px; height:52px; border-radius:16px; background:var(--panel-2);
    display:flex; align-items:center; justify-content:center; margin-bottom:24px;
  }
  .svc .icon svg{ width:24px; height:24px; stroke:var(--accent-soft); }
  .svc h3{ font-family:var(--disp); font-weight:700; font-size:22px; margin-bottom:12px; letter-spacing:-0.01em; }
  .svc p.d{ color:var(--text-muted); font-size:15px; margin-bottom:22px; }
  .svc ul{ list-style:none; display:flex; flex-direction:column; gap:12px; }
  .svc li{ display:flex; gap:10px; font-size:14.5px; color:var(--text); }
  .svc li svg{ width:18px; height:18px; stroke:var(--accent-soft); flex-shrink:0; margin-top:1px; }

  /* ---------- PREVIOUS WORK ---------- */
  .work-grid{ display:grid; grid-template-columns:repeat(3,1fr); gap:20px; }
  @media(max-width:980px){ .work-grid{ grid-template-columns:repeat(2,1fr); } }
  @media(max-width:640px){ .work-grid{ grid-template-columns:1fr; } }

  .card{
    background:var(--panel); border:1px solid var(--border); border-radius:22px; padding:0;
    overflow:hidden; transition:transform .2s, border-color .2s;
  }
  .card:hover{ transform:translateY(-4px); border-color:#3a3a42; }
  .card .top{
    height:130px; display:flex; align-items:center; justify-content:center; position:relative;
  }
  .card .top svg{ width:38px; height:38px; }
  .card .body{ padding:24px 24px 26px; }
  .card .tag{
    display:inline-block; font-size:12px; font-weight:600; color:var(--text-muted);
    background:var(--panel-2); padding:5px 12px; border-radius:999px; margin-bottom:14px;
  }
  .card h4{ font-family:var(--disp); font-weight:700; font-size:19px; margin-bottom:14px; letter-spacing:-0.01em; }
  .card .rowstats{ display:flex; gap:20px; padding-top:16px; border-top:1px solid var(--border); }
  .card .rowstats .m .n{ font-family:var(--disp); font-weight:700; font-size:16px; }
  .card .rowstats .m .l{ font-size:11.5px; color:var(--text-dim); margin-top:2px; }

  /* ---------- FOOTER / CONTACT ---------- */
  .footer-cta{
    text-align:center; max-width:640px; margin:0 auto;
  }
  .footer-cta h2{ font-family:var(--disp); font-weight:800; font-size:clamp(30px,3.8vw,44px); letter-spacing:-0.02em; margin-bottom:18px; }
  .footer-cta p{ color:var(--text-muted); font-size:16px; margin-bottom:34px; }
  .footer-cta .ctas{ justify-content:center; margin-bottom:0; }

  footer{
    border-top:1px solid var(--border); padding:36px 8vw; margin-top:0;
    display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:14px;
    color:var(--text-dim); font-size:13.5px;
  }
  footer .flogo{ font-family:var(--disp); font-weight:700; color:var(--text-muted); }

  .reveal{ opacity:0; transform:translateY(16px); transition:opacity .6s ease, transform .6s ease; }
  .reveal.in{ opacity:1; transform:translateY(0); }

  @media (prefers-reduced-motion: reduce){ * { transition:none !important; } }
</style>
</head>
<body>

  <div class="navwrap">
    <nav>
      <div class="logo">Quantum QA</div>
      <div class="navlinks">
        <a href="#home">Home</a>
        <a href="#services">Services</a>
        <a href="#work">Previous Work</a>
      </div>
      <a href="#contact" class="navcta">Get Started</a>
    </nav>
  </div>

  <!-- HOME -->
  <section class="hero" id="home">
    <div>
      <div class="eyebrow"><span class="dot"></span>Roblox QA & Anti-Cheat</div>
      <h1>Ship games your players trust — <span class="accent">bug-free, cheat-free.</span></h1>
      <p class="lede">Quantum QA runs structured playtests and exploit audits for Roblox studios, so the bugs and the cheaters get caught before your players do.</p>
      <div class="ctas">
        <a href="#contact" class="btn primary">Get Started</a>
        <a href="#work" class="btn secondary">See Previous Work</a>
      </div>
    </div>
    <div class="glowblock">
      <svg viewBox="0 0 100 100" fill="none">
        <path d="M50 6 L88 20 V48 C88 70 72 86 50 94 C28 86 12 70 12 48 V20 Z" fill="#fff" opacity="0.96"/>
        <path d="M40 50 L47 57 L62 40" stroke="#5170ff" stroke-width="6" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
      </svg>
    </div>
  </section>

  <section style="padding-top:0;">
    <div class="stats reveal">
      <div class="stat"><div class="n">26</div><div class="l">Games Tested</div></div>
      <div class="stat"><div class="n">190+</div><div class="l">Exploits Patched</div></div>
      <div class="stat"><div class="n">261.6M+</div><div class="l">Total Visits Covered</div></div>
    </div>
  </section>

  <!-- SERVICES -->
  <section id="services">
    <div class="shead reveal">
      <h2>Services</h2>
      <p>Two disciplines, one pipeline — structured feedback on the game, and structured pressure on the systems that protect it.</p>
    </div>
    <div class="svc-grid reveal">
      <div class="svc">
        <div class="icon"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="4" y="4" width="16" height="16" rx="4"/><path d="M9 12l2 2 4-4"/></svg></div>
        <h3>QA Testing</h3>
        <p class="d">Multi-device playtests that surface what internal testers miss, with reports your team can act on the same day.</p>
        <ul>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Cross-platform pass — PC, mobile, console</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Reproducible bug reports with footage</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Onboarding & UX friction audits</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Peak-CCU server load observation</li>
        </ul>
      </div>
      <div class="svc">
        <div class="icon"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3l7 3v6c0 5-3 8-7 9-4-1-7-4-7-9V6z"/></svg></div>
        <h3>Anti-Cheat</h3>
        <p class="d">We attack your game the way exploiters do, then hand over exactly what we found and how to close it.</p>
        <ul>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Executor & exploit-script simulation</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Remote event & DataStore abuse checks</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Speed, fly & teleport exploit testing</li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>Post-patch re-verification</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- PREVIOUS WORK -->
  <section id="work">
    <div class="shead reveal">
      <h2>Previous Work</h2>
      <p>A sample of recent engagements across genres — each closed out with a written report and a re-test to confirm the fix held.</p>
    </div>
    <div class="work-grid reveal">
      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#5170ff,#2c3fb0);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><path d="M3 13l3-7h12l3 7M5 13h14v5H5z"/><circle cx="8" cy="18" r="1.4" fill="#fff"/><circle cx="16" cy="18" r="1.4" fill="#fff"/></svg></div>
        <div class="body">
          <span class="tag">Racing</span>
          <h4>Driving Empire</h4>
          <div class="rowstats">
            <div class="m"><div class="n">312</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">14</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#3a3a42,#1c1c21);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><rect x="4" y="9" width="16" height="10" rx="2"/><path d="M8 9V6a4 4 0 018 0v3"/></svg></div>
        <div class="body">
          <span class="tag">Tower Defense</span>
          <h4>Toilet Tower Defense</h4>
          <div class="rowstats">
            <div class="m"><div class="n">205</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">9</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#ff6fae,#a13a6b);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><path d="M12 21c4-3 7-6 7-10a7 7 0 00-14 0c0 4 3 7 7 10z"/></svg></div>
        <div class="body">
          <span class="tag">Social</span>
          <h4>Dress to Impress</h4>
          <div class="rowstats">
            <div class="m"><div class="n">168</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">5</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#f0ac52,#a06a1e);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><rect x="3" y="4" width="18" height="14" rx="2"/><path d="M8 21h8M12 18v3"/></svg></div>
        <div class="body">
          <span class="tag">Roleplay</span>
          <h4>Bayside High</h4>
          <div class="rowstats">
            <div class="m"><div class="n">94</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">3</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#7b93ff,#3f4fbd);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><path d="M12 2l3 6 6 1-4.5 4.5L18 20l-6-3.2L6 20l1.5-6.5L3 9l6-1z"/></svg></div>
        <div class="body">
          <span class="tag">RPG</span>
          <h4>World // Zero</h4>
          <div class="rowstats">
            <div class="m"><div class="n">276</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">21</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="top" style="background:linear-gradient(135deg,#59c26a,#276b34);"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><path d="M12 2C8 6 4 10 4 14a8 8 0 0016 0c0-4-4-8-8-12z"/></svg></div>
        <div class="body">
          <span class="tag">Survival</span>
          <h4>Primal Hunt</h4>
          <div class="rowstats">
            <div class="m"><div class="n">183</div><div class="l">Bugs Found</div></div>
            <div class="m"><div class="n">11</div><div class="l">Exploits Patched</div></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT / CTA -->
  <section id="contact">
    <div class="footer-cta reveal">
      <h2>Have a project in mind?</h2>
      <p>Send over your place and what's on your mind — a launch deadline, a live exploit, or a QA pass you've been putting off.</p>
      <div class="ctas">
        <a href="mailto:cases@quantumqa.cc" class="btn primary">Email Us</a>
      </div>
    </div>
  </section>

  <footer>
    <div class="flogo">Quantum QA</div>
    <div>© 2026 Quantum QA · cases@quantumqa.cc</div>
  </footer>

<script>
  const revealEls = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{ if(e.isIntersecting){ e.target.classList.add('in'); io.unobserve(e.target); } });
  }, { threshold: 0.12 });
  revealEls.forEach(el=>io.observe(el));
</script>
</body>
</html>
