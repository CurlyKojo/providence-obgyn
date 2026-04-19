<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Patient Portal — Providence OBGYN</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;1,9..144,400;1,9..144,500&family=Cormorant+Garamond:ital,wght@0,400;0,500;1,400;1,500&family=Inter:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="shared.css?v=2">
<style>
  body { background: var(--paper-2); }

  /* Compact portal header below main nav */
  .portal-bar { background: var(--wine-deep); color: var(--paper); padding: 14px 40px; display: flex; justify-content: space-between; align-items: center; font-family: 'JetBrains Mono', monospace; font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase; }
  .portal-bar .left { display: flex; align-items: center; gap: 14px; }
  .portal-bar .left::before { content: "●"; color: #c2a25a; font-size: 8px; }
  .portal-bar .right { color: rgba(244,239,230,0.7); }

  .portal { display: grid; grid-template-columns: 260px 1fr; min-height: calc(100vh - 140px); }
  .side { background: var(--paper); border-right: 1px solid var(--rule); padding: 36px 22px; position: sticky; top: 92px; align-self: start; height: calc(100vh - 92px); overflow-y: auto; }
  .side .who { padding: 8px 10px 20px; border-bottom: 1px solid var(--rule); margin-bottom: 20px; }
  .side .who .label { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.22em; color: var(--ink-light); text-transform: uppercase; }
  .side .who .n { font-family: 'Fraunces', serif; font-size: 22px; margin-top: 6px; letter-spacing: -0.01em; }
  .side .who .n em { font-style: italic; color: var(--wine); }
  .side .who .m { font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 14px; color: var(--ink-light); margin-top: 2px; }
  .side .sect { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.22em; color: var(--ink-light); text-transform: uppercase; padding: 14px 10px 8px; }
  .side ul { list-style: none; padding: 0; margin: 0 0 10px; }
  .side li { padding: 10px 12px; font-size: 14px; color: var(--ink-soft); cursor: pointer; display: flex; justify-content: space-between; align-items: center; border-left: 2px solid transparent; transition: all .15s; }
  .side li:hover { background: var(--paper-2); }
  .side li.active { background: var(--paper-2); color: var(--wine); border-left-color: var(--wine); font-weight: 500; }
  .side li .bdg { background: var(--wine); color: var(--paper); font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.1em; padding: 2px 7px; border-radius: 10px; }

  .main { padding: 48px 64px 80px; }
  .main h2 { font-family: 'Fraunces', serif; font-weight: 400; font-size: 44px; letter-spacing: -0.02em; line-height: 1; margin: 0; }
  .main h2 em { font-style: italic; color: var(--wine); }
  .hello { font-family: 'Cormorant Garamond', serif; font-size: 20px; color: var(--ink-soft); margin: 12px 0 36px; }

  .cards-row { display: grid; grid-template-columns: 1.4fr 1fr; gap: 20px; margin-bottom: 24px; }

  .card-pt { background: var(--paper); border: 1px solid var(--rule-2); padding: 26px 28px; }
  .card-pt .card-head { display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px; padding-bottom: 14px; border-bottom: 1px solid var(--rule); }
  .card-pt .card-head h3 { font-family: 'Fraunces', serif; font-weight: 400; font-size: 22px; margin: 0; letter-spacing: -0.01em; }
  .card-pt .card-head h3 em { font-style: italic; color: var(--wine); }
  .card-pt .card-head .link { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.2em; color: var(--wine); text-transform: uppercase; }

  /* Next visit hero card */
  .visit-hero { background: var(--wine-deep); color: var(--paper); padding: 32px 32px 30px; position: relative; overflow: hidden; }
  .visit-hero::before { content: ""; position: absolute; top: -40px; right: -40px; width: 180px; height: 180px; border-radius: 50%; background: radial-gradient(circle, rgba(194,162,90,0.25), transparent 70%); }
  .visit-hero .tag { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.22em; color: #c2a25a; text-transform: uppercase; }
  .visit-hero h3 { font-family: 'Fraunces', serif; font-weight: 400; font-size: 34px; margin: 10px 0 4px; letter-spacing: -0.015em; }
  .visit-hero h3 em { font-style: italic; color: #c2a25a; }
  .visit-hero .date { font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 22px; margin: 4px 0 18px; color: rgba(244,239,230,0.9); }
  .visit-hero .rows { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; padding: 16px 0 18px; border-top: 1px solid rgba(244,239,230,0.15); border-bottom: 1px solid rgba(244,239,230,0.15); margin-bottom: 18px; }
  .visit-hero .rows .k { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.2em; color: #c2a25a; text-transform: uppercase; }
  .visit-hero .rows .v { font-family: 'Fraunces', serif; font-style: italic; font-size: 16px; margin-top: 4px; color: rgba(244,239,230,0.95); }
  .visit-hero .ctas { display: flex; gap: 10px; flex-wrap: wrap; }
  .visit-hero .ctas .btn { border-color: rgba(244,239,230,0.35); color: var(--paper); }
  .visit-hero .ctas .btn:hover { background: var(--paper); color: var(--wine-deep); }
  .visit-hero .ctas .btn.primary { background: #c2a25a; border-color: #c2a25a; color: var(--wine-deep); }
  .visit-hero .ctas .btn.primary:hover { background: var(--paper); border-color: var(--paper); }

  /* Quick actions */
  .quick-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 16px; }
  .quick { background: var(--paper-2); border: 1px solid var(--rule-2); padding: 16px 14px; cursor: pointer; transition: all .15s; text-decoration: none; color: inherit; display: block; }
  .quick:hover { border-color: var(--wine); background: var(--paper); }
  .quick .ic { width: 28px; height: 28px; border-radius: 50%; border: 1px solid var(--wine); color: var(--wine); display: flex; align-items: center; justify-content: center; font-family: 'Fraunces', serif; font-size: 16px; margin-bottom: 10px; }
  .quick h5 { font-family: 'Fraunces', serif; font-weight: 400; font-size: 16px; margin: 0 0 2px; letter-spacing: -0.01em; }
  .quick h5 em { font-style: italic; color: var(--wine); }
  .quick p { font-size: 12px; color: var(--ink-light); margin: 0; line-height: 1.4; }

  /* Messages */
  .msg-item { padding: 16px 0; border-bottom: 1px solid var(--rule); display: grid; grid-template-columns: 40px 1fr auto; gap: 14px; align-items: start; cursor: pointer; }
  .msg-item:first-child { padding-top: 0; }
  .msg-item:last-child { border-bottom: 0; padding-bottom: 0; }
  .msg-avatar { width: 40px; height: 40px; border-radius: 50%; background: var(--wine); color: var(--paper); display: flex; align-items: center; justify-content: center; font-family: 'Fraunces', serif; font-style: italic; font-size: 16px; border: 2px solid var(--paper); box-shadow: 0 0 0 1px var(--rule-2); }
  .msg-item .content .from { font-family: 'Fraunces', serif; font-size: 15px; letter-spacing: -0.01em; }
  .msg-item .content .from em { font-style: italic; color: var(--wine); }
  .msg-item .content .subj { font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 15px; color: var(--ink-soft); margin-top: 2px; }
  .msg-item .content .pre { font-size: 13px; color: var(--ink-light); margin-top: 4px; line-height: 1.5; }
  .msg-item .meta { text-align: right; font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.18em; color: var(--ink-light); text-transform: uppercase; }
  .msg-item .meta .new { background: var(--wine); color: var(--paper); padding: 2px 6px; border-radius: 8px; margin-top: 6px; display: inline-block; }
  .msg-item.unread .content .from { font-weight: 500; color: var(--ink); }

  /* Pregnancy tracker */
  .preg-card { background: var(--paper); border: 1px solid var(--rule-2); padding: 28px 30px; margin-bottom: 24px; }
  .preg-head { display: grid; grid-template-columns: 1fr auto; gap: 24px; align-items: end; margin-bottom: 22px; }
  .preg-head h3 { font-family: 'Fraunces', serif; font-weight: 400; font-size: 24px; margin: 0; letter-spacing: -0.01em; }
  .preg-head h3 em { font-style: italic; color: var(--wine); }
  .preg-head .wk { font-family: 'Fraunces', serif; font-style: italic; font-size: 44px; line-height: 1; color: var(--wine); }
  .preg-head .wk small { display: block; font-family: 'JetBrains Mono', monospace; font-style: normal; font-size: 9px; letter-spacing: 0.22em; color: var(--ink-light); text-transform: uppercase; margin-top: 6px; }

  .preg-bar { height: 8px; background: var(--paper-2); border: 1px solid var(--rule-2); position: relative; margin-bottom: 8px; }
  .preg-fill { position: absolute; left: 0; top: 0; bottom: 0; width: 56%; background: linear-gradient(90deg, var(--wine) 0%, var(--wine-soft) 100%); }
  .preg-marker { position: absolute; top: -6px; bottom: -6px; width: 2px; background: var(--gold); }
  .preg-marker.m1 { left: 32%; }
  .preg-marker.m2 { left: 67%; }
  .preg-scale { display: flex; justify-content: space-between; font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.18em; color: var(--ink-light); text-transform: uppercase; }
  .preg-next { padding: 14px 0 0; margin-top: 18px; border-top: 1px solid var(--rule); font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 17px; color: var(--ink-soft); }
  .preg-next strong { font-family: 'Fraunces', serif; font-style: normal; font-weight: 500; color: var(--wine); }

  /* Records / results table */
  .records-card { background: var(--paper); border: 1px solid var(--rule-2); padding: 0; }
  .records-card .card-head { padding: 22px 28px; }
  .rec-row { display: grid; grid-template-columns: 110px 1fr auto auto; gap: 20px; padding: 14px 28px; border-bottom: 1px solid var(--rule); align-items: center; }
  .rec-row:last-child { border-bottom: 0; }
  .rec-row .dt { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--ink-light); letter-spacing: 0.08em; }
  .rec-row .nm { font-family: 'Fraunces', serif; font-size: 16px; letter-spacing: -0.01em; }
  .rec-row .nm em { font-style: italic; color: var(--wine); }
  .rec-row .nm small { display: block; font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 13px; color: var(--ink-light); margin-top: 2px; }
  .rec-row .st { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.2em; text-transform: uppercase; padding: 4px 10px; border: 1px solid var(--rule-2); }
  .rec-row .st.normal { color: #2d5f3f; border-color: #2d5f3f; }
  .rec-row .st.review { color: var(--wine); border-color: var(--wine); background: rgba(86,19,33,0.06); }
  .rec-row .st.pending { color: var(--ink-light); }
  .rec-row .action { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.2em; color: var(--wine); text-transform: uppercase; cursor: pointer; }

  @media (max-width: 1100px) {
    .portal { grid-template-columns: 1fr; }
    .side { position: static; height: auto; border-right: 0; border-bottom: 1px solid var(--rule); }
    .cards-row { grid-template-columns: 1fr; }
    .visit-hero .rows { grid-template-columns: 1fr; gap: 10px; }
    .rec-row { grid-template-columns: 1fr; gap: 6px; }
  }
  @media (max-width: 620px) {
    .main { padding: 32px 24px 64px; }
    .quick-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="announce">
  <span><span class="dot"></span>Now welcoming new patients · limited panel</span>
  <span class="right">Summerlin Medical Plaza · (702) 555-0142</span>
</div>
<header class="nav">
  <a href="index.html" class="logo">
    <div class="logo-mark">P</div>
    <div class="logo-text">
      <div class="name">Providence <em>OBGYN</em></div>
      <div class="sub">Dr. Symone · Las Vegas</div>
    </div>
  </a>
  <nav class="links">
    <a href="index.html">Home</a>
    <a href="about.html">About</a>
    <a href="services.html">Services</a>
    <a href="resources.html">Resources</a>
    <a href="portal.html" class="active">Patient Portal</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="nav-right">
    <span class="nav-phone">Signed in · A. Martinez</span>
    <a href="index.html" class="btn sm">Sign out</a>
  </div>
</header>

<div class="portal-bar">
  <span class="left">Secure patient portal · encrypted · HIPAA-compliant</span>
  <span class="right">Last signed in · Yesterday, 9:14 pm</span>
</div>

<div class="portal">
  <aside class="side">
    <div class="who">
      <div class="label">Signed in as</div>
      <div class="n">Alana <em>Martinez</em></div>
      <div class="m">Patient since 2021 · Week 22 pregnancy</div>
    </div>

    <div class="sect">Overview</div>
    <ul>
      <li class="active">Dashboard</li>
      <li>Messages <span class="bdg">2</span></li>
      <li>Appointments</li>
      <li>Pregnancy journey</li>
    </ul>

    <div class="sect">Records</div>
    <ul>
      <li>Visit summaries</li>
      <li>Lab results <span class="bdg">1</span></li>
      <li>Ultrasound images</li>
      <li>Medications</li>
      <li>Immunizations</li>
    </ul>

    <div class="sect">Admin</div>
    <ul>
      <li>Billing &amp; statements</li>
      <li>Insurance on file</li>
      <li>Forms &amp; documents</li>
      <li>Account &amp; privacy</li>
    </ul>
  </aside>

  <div class="main">
    <span class="eyebrow">Dashboard</span>
    <h2 style="margin-top:10px">Good morning, <em>Alana.</em></h2>
    <p class="hello">A quiet Thursday · your next visit is in five days.</p>

    <div class="cards-row">
      <div class="visit-hero">
        <span class="tag">Next appointment</span>
        <h3>Prenatal visit · <em>week 23</em></h3>
        <div class="date">Tuesday, April 22 · 11:00 am</div>
        <div class="rows">
          <div><div class="k">With</div><div class="v">Dr. Symone</div></div>
          <div><div class="k">Length</div><div class="v">45 minutes</div></div>
          <div><div class="k">Location</div><div class="v">Summerlin · Suite 200</div></div>
        </div>
        <div class="ctas">
          <a href="book.html" class="btn primary sm">Confirm attendance <span class="arrow">→</span></a>
          <a href="book.html" class="btn sm">Reschedule</a>
          <a href="book.html" class="btn sm">Add to calendar</a>
        </div>
      </div>

      <div class="card-pt">
        <div class="card-head">
          <h3>Quick <em>actions</em></h3>
        </div>
        <div class="quick-grid">
          <a class="quick" href="contact.html"><div class="ic">✉</div><h5>Message <em>Dr. Symone</em></h5><p>Non-urgent · reply in 1 day</p></a>
          <a class="quick" href="contact.html"><div class="ic">℞</div><h5>Refill <em>a prescription</em></h5><p>Current meds + pharmacy</p></a>
          <a class="quick" href="book.html"><div class="ic">📅</div><h5>Request <em>an appointment</em></h5><p>Follow-up · annual · other</p></a>
          <a class="quick" href="resources.html"><div class="ic">↓</div><h5>Download <em>records</em></h5><p>PDF · last 12 months</p></a>
        </div>
      </div>
    </div>

    <div class="preg-card">
      <div class="preg-head">
        <div>
          <span class="eyebrow">Pregnancy journey</span>
          <h3 style="margin-top:6px">Second <em>trimester.</em></h3>
        </div>
        <div class="wk">22<small>Weeks</small></div>
      </div>
      <div class="preg-bar">
        <div class="preg-fill"></div>
        <div class="preg-marker m1" title="Trimester 2 begins"></div>
        <div class="preg-marker m2" title="Trimester 3 begins"></div>
      </div>
      <div class="preg-scale">
        <span>Week 0</span>
        <span>Tri 2 · wk 14</span>
        <span>Tri 3 · wk 28</span>
        <span>Week 40</span>
      </div>
      <div class="preg-next">Next milestone: <strong>Glucose screen</strong> at your week 26 visit · estimated due date <strong>August 18, 2026</strong>.</div>
    </div>

    <div class="cards-row" style="grid-template-columns: 1.2fr 1fr">
      <div class="card-pt">
        <div class="card-head">
          <h3>Recent <em>messages</em></h3>
          <span class="link">View all →</span>
        </div>
        <div class="msg-item unread">
          <div class="msg-avatar">S</div>
          <div class="content">
            <div class="from">Dr. <em>Symone</em></div>
            <div class="subj">Anatomy scan results — everything looks lovely</div>
            <div class="pre">Hi Alana — I've reviewed the images from Tuesday's scan. Baby is measuring right on track, all anatomy within normal limits…</div>
          </div>
          <div class="meta">2h ago<div class="new">NEW</div></div>
        </div>
        <div class="msg-item unread">
          <div class="msg-avatar" style="background:var(--gold)">M</div>
          <div class="content">
            <div class="from">Monica · <em>Front desk</em></div>
            <div class="subj">Your prenatal vitamins — one small note</div>
            <div class="pre">Just a reminder that your refill is ready for pickup at Walgreens on Town Center. Let us know if you'd like us to send it elsewhere…</div>
          </div>
          <div class="meta">Yesterday<div class="new">NEW</div></div>
        </div>
        <div class="msg-item">
          <div class="msg-avatar">S</div>
          <div class="content">
            <div class="from">Dr. <em>Symone</em></div>
            <div class="subj">RE: Feeling more tired lately — is that normal?</div>
            <div class="pre">Completely — your body is doing more invisible work than it ever has. A few questions: how's your iron intake been, and are you sleeping on your left side yet…</div>
          </div>
          <div class="meta">Apr 11</div>
        </div>
      </div>

      <div class="card-pt">
        <div class="card-head">
          <h3>Upcoming <em>schedule</em></h3>
          <span class="link">Calendar →</span>
        </div>
        <div style="padding-top:6px">
          <div style="padding:14px 0;border-bottom:1px solid var(--rule);display:grid;grid-template-columns:56px 1fr auto;gap:14px;align-items:center">
            <div style="text-align:center;border:1px solid var(--rule-2);padding:6px 0;background:var(--wine-deep);color:var(--paper)"><div style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.18em">APR</div><div style="font-family:'Fraunces',serif;font-style:italic;font-size:22px;line-height:1">22</div></div>
            <div><div style="font-family:'Fraunces',serif;font-size:15px">Prenatal visit · <em style="font-style:italic;color:var(--wine)">week 23</em></div><div style="font-family:'Cormorant Garamond',serif;font-style:italic;font-size:14px;color:var(--ink-light)">11:00 am · Dr. Symone</div></div>
            <span style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.2em;color:var(--wine)">CONFIRM</span>
          </div>
          <div style="padding:14px 0;border-bottom:1px solid var(--rule);display:grid;grid-template-columns:56px 1fr auto;gap:14px;align-items:center">
            <div style="text-align:center;border:1px solid var(--rule-2);padding:6px 0"><div style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.18em;color:var(--ink-light)">MAY</div><div style="font-family:'Fraunces',serif;font-style:italic;font-size:22px;line-height:1">14</div></div>
            <div><div style="font-family:'Fraunces',serif;font-size:15px">Glucose screen · <em style="font-style:italic;color:var(--wine)">week 26</em></div><div style="font-family:'Cormorant Garamond',serif;font-style:italic;font-size:14px;color:var(--ink-light)">10:30 am · Dr. Symone</div></div>
            <span style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.2em;color:var(--ink-light)">SCHEDULED</span>
          </div>
          <div style="padding:14px 0;display:grid;grid-template-columns:56px 1fr auto;gap:14px;align-items:center">
            <div style="text-align:center;border:1px solid var(--rule-2);padding:6px 0"><div style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.18em;color:var(--ink-light)">JUN</div><div style="font-family:'Fraunces',serif;font-style:italic;font-size:22px;line-height:1">09</div></div>
            <div><div style="font-family:'Fraunces',serif;font-size:15px">Prenatal visit · <em style="font-style:italic;color:var(--wine)">week 30</em></div><div style="font-family:'Cormorant Garamond',serif;font-style:italic;font-size:14px;color:var(--ink-light)">11:00 am · Dr. Symone</div></div>
            <span style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.2em;color:var(--ink-light)">SCHEDULED</span>
          </div>
        </div>
      </div>
    </div>

    <div class="records-card" style="margin-top:24px">
      <div class="card-head" style="display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid var(--rule)">
        <h3 style="font-family:'Fraunces',serif;font-weight:400;font-size:22px;margin:0;letter-spacing:-0.01em">Recent <em style="font-style:italic;color:var(--wine)">results &amp; records</em></h3>
        <span style="font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:0.2em;color:var(--wine);text-transform:uppercase">View all records →</span>
      </div>
      <div class="rec-row">
        <span class="dt">APR 15 · 2026</span>
        <div class="nm">Anatomy ultrasound · <em>20-week scan</em><small>Findings normal · baby measuring 50th %ile</small></div>
        <span class="st normal">Normal</span>
        <span class="action">View images ↗</span>
      </div>
      <div class="rec-row">
        <span class="dt">APR 10 · 2026</span>
        <div class="nm">Prenatal labs · <em>CBC, ferritin, thyroid</em><small>Dr. Symone has left a note · please read</small></div>
        <span class="st review">Reviewed</span>
        <span class="action">Open note ↗</span>
      </div>
      <div class="rec-row">
        <span class="dt">MAR 28 · 2026</span>
        <div class="nm">Visit summary · <em>week 17 prenatal</em><small>Signed by Dr. Symone · 42-minute visit</small></div>
        <span class="st normal">Complete</span>
        <span class="action">Download ↓</span>
      </div>
      <div class="rec-row">
        <span class="dt">MAR 14 · 2026</span>
        <div class="nm">NIPT screening · <em>cell-free DNA</em><small>Low-risk for all screened conditions</small></div>
        <span class="st normal">Low risk</span>
        <span class="action">View details ↗</span>
      </div>
      <div class="rec-row">
        <span class="dt">MAR 01 · 2026</span>
        <div class="nm">Dating ultrasound · <em>week 8</em><small>EDD confirmed · August 18, 2026</small></div>
        <span class="st normal">Normal</span>
        <span class="action">View images ↗</span>
      </div>
    </div>

    <p style="margin-top:36px;font-family:'Cormorant Garamond',serif;font-style:italic;font-size:16px;color:var(--ink-light);text-align:center">This portal is not for urgent or emergency care. For emergencies, call 911 or proceed to Summerlin Hospital Labor &amp; Delivery.</p>
  </div>
</div>

<footer>
  <div class="footer-grid">
    <div class="brand">
      <div class="logo">
        <div class="logo-mark">P</div>
        <div class="logo-text">
          <div class="name">Providence <em>OBGYN</em></div>
          <div class="sub">Dr. Symone · Las Vegas</div>
        </div>
      </div>
      <p>Fearfully made. Faithfully cared for.</p>
    </div>
    <div><h5>Care</h5><ul><li><a href="services.html">Prenatal &amp; obstetrics</a></li><li><a href="services.html">Well-woman exams</a></li><li><a href="services.html">Fertility support</a></li><li><a href="services.html">Menopause care</a></li><li><a href="services.html">Gyn surgery</a></li><li><a href="services.html">Adolescent care</a></li></ul></div>
    <div><h5>Practice</h5><ul><li><a href="about.html">About Dr. Symone</a></li><li><a href="about.html">Our values</a></li><li><a href="book.html">New patient info</a></li><li><a href="resources.html">Pregnancy resources</a></li><li><a href="faq.html">FAQ</a></li></ul></div>
    <div><h5>Visit</h5><ul><li><a href="contact.html">Summerlin Medical Plaza</a></li><li><a href="contact.html">Suite 200</a></li><li><a href="contact.html">Las Vegas, NV 89135</a></li><li><a href="contact.html">(702) 555-0142</a></li><li><a href="contact.html">hello@providenceobgyn.com</a></li></ul></div>
  </div>
  <div class="footer-bottom">
    <span>© 2026 Providence OBGYN · Solo practice</span>
    <span class="tagline">Every woman, every season.</span>
    <span>Privacy · Accessibility · Patient rights</span>
  </div>
</footer>
</body>
</html>
