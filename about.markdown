---
layout: default
title: OPERATOR PROFILE // CLASSIFIED
permalink: /about/
---

<style>
/* ==========================================
   OTHMANE01 // INTELLIGENCE DOSSIER
========================================== */

.operator-file {
  --lime: #b5e853;
  --olive: #788b55;
  --red: #b75b50;
  --paper: #171b15;
  --paper-dark: #10140f;
  --line: #394333;
  --muted: #89917e;
  --white: #dce1d4;

  max-width: 1000px;
  margin: 35px auto;
  color: var(--white);
  font-family: "Courier New", monospace;
  font-size: 13px;
  position: relative;
}

.operator-file *,
.operator-file *::before,
.operator-file *::after {
  box-sizing: border-box;
}

/* Document background */

.operator-file .file-sheet {
  position: relative;
  overflow: hidden;
  padding: 28px;
  background:
    radial-gradient(ellipse at 15% 10%, rgba(181,232,83,.055), transparent 45%),
    repeating-linear-gradient(
      0deg,
      transparent,
      transparent 3px,
      rgba(255,255,255,.008) 4px
    ),
    var(--paper);
  border: 1px solid #46513d;
  box-shadow:
    0 20px 60px rgba(0,0,0,.35),
    inset 0 0 50px rgba(0,0,0,.2);
}

.operator-file .file-sheet::before {
  content: "";
  position: absolute;
  inset: 7px;
  border: 1px solid rgba(181,232,83,.09);
  pointer-events: none;
}

.operator-file .file-sheet::after {
  content: "OTH-001";
  position: absolute;
  right: -37px;
  top: 45%;
  transform: rotate(90deg);
  color: rgba(181,232,83,.10);
  font-size: 35px;
  font-weight: bold;
  letter-spacing: 8px;
  pointer-events: none;
}

/* Top metadata */

.operator-file .file-header {
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 15px;
  padding-bottom: 17px;
  border-bottom: 1px solid var(--line);
}

.operator-file .agency {
  color: var(--lime);
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 3px;
}

.operator-file .agency-sub {
  margin-top: 5px;
  color: var(--muted);
  font-size: 9px;
  letter-spacing: 2px;
}

.operator-file .file-reference {
  color: var(--muted);
  text-align: right;
  font-size: 10px;
  line-height: 1.8;
  letter-spacing: 1px;
}

.operator-file .classification-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  margin: 22px 0;
}

.operator-file .classification {
  padding: 7px 15px;
  color: var(--red);
  border: 1px solid var(--red);
  font-weight: bold;
  letter-spacing: 4px;
  transform: rotate(-2deg);
  text-shadow: 0 0 12px rgba(183,91,80,.2);
}

.operator-file .classification-note {
  color: var(--muted);
  font-size: 9px;
  letter-spacing: 2px;
}

/* Main heading */

.operator-file .file-title {
  position: relative;
  z-index: 1;
  margin: 25px 0 5px;
  color: var(--white);
  font-size: clamp(27px, 5vw, 45px);
  font-weight: bold;
  line-height: 1.1;
  letter-spacing: 3px;
}

.operator-file .file-title span {
  color: var(--lime);
}

.operator-file .file-subtitle {
  color: var(--muted);
  font-size: 10px;
  letter-spacing: 3px;
}

/* Subject section */

.operator-file .subject-grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: minmax(190px, 270px) 1fr;
  gap: 30px;
  margin-top: 30px;
  padding: 22px;
  background: rgba(0,0,0,.17);
  border: 1px solid var(--line);
}

.operator-file .portrait-frame {
  position: relative;
  min-height: 320px;
  padding: 8px;
  background: var(--paper-dark);
  border: 1px solid #536148;
}

.operator-file .portrait-frame::before,
.operator-file .portrait-frame::after {
  content: "";
  position: absolute;
  width: 27px;
  height: 27px;
  z-index: 2;
  pointer-events: none;
}

.operator-file .portrait-frame::before {
  top: 4px;
  left: 4px;
  border-top: 2px solid var(--lime);
  border-left: 2px solid var(--lime);
}

.operator-file .portrait-frame::after {
  right: 4px;
  bottom: 4px;
  border-right: 2px solid var(--lime);
  border-bottom: 2px solid var(--lime);
}

.operator-file .portrait-frame img {
  display: block;
  width: 100%;
  height: 100%;
  min-height: 302px;
  object-fit: cover;
  object-position: center;
  filter: grayscale(100%) contrast(1.08) brightness(.82);
  border: 1px solid #303b2c;
  transition: filter .4s ease, transform .4s ease;
}

.operator-file .portrait-frame:hover img {
  filter: grayscale(35%) contrast(1.05) brightness(.95);
  transform: scale(.99);
}

.operator-file .portrait-caption {
  position: absolute;
  z-index: 3;
  left: 15px;
  right: 15px;
  bottom: 14px;
  padding: 7px;
  background: rgba(10,14,10,.88);
  color: var(--lime);
  text-align: center;
  font-size: 9px;
  letter-spacing: 2px;
}

.operator-file .subject-details {
  min-width: 0;
}

.operator-file .field-label {
  display: block;
  margin-bottom: 8px;
  color: var(--olive);
  font-size: 9px;
  letter-spacing: 2px;
}

.operator-file .subject-name {
  margin: 0;
  color: var(--white);
  font-size: clamp(30px, 5vw, 47px);
  line-height: 1.1;
  letter-spacing: 4px;
}

.operator-file .codename {
  margin-top: 8px;
  color: var(--lime);
  font-size: 13px;
  letter-spacing: 3px;
}

.operator-file .subject-role {
  margin-top: 22px;
  padding-left: 13px;
  border-left: 2px solid var(--lime);
  color: var(--white);
  line-height: 1.9;
  font-size: 12px;
  letter-spacing: 1px;
}

.operator-file .subject-summary {
  margin-top: 20px;
  color: #aeb6a4;
  font-size: 12px;
  line-height: 1.9;
}

.operator-file .subject-summary strong {
  color: var(--lime);
  font-weight: normal;
}

.operator-file .status-line {
  display: flex;
  align-items: center;
  gap: 9px;
  margin-top: 20px;
  color: var(--muted);
  font-size: 10px;
  letter-spacing: 1px;
}

.operator-file .status-dot {
  width: 8px;
  height: 8px;
  flex: 0 0 8px;
  border-radius: 50%;
  background: var(--lime);
  box-shadow: 0 0 10px rgba(181,232,83,.65);
  animation: statusPulse 2s infinite;
}

@keyframes statusPulse {
  0%, 100% { opacity: 1; }
  50% { opacity: .35; }
}

/* Section headings */

.operator-file .record-section {
  position: relative;
  z-index: 1;
  margin-top: 32px;
}

.operator-file .section-heading {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 0 0 18px;
  padding-bottom: 11px;
  border-bottom: 1px solid var(--line);
  color: var(--lime);
  font-size: 12px;
  letter-spacing: 2px;
}

.operator-file .section-heading small {
  color: var(--muted);
  font-size: 9px;
  font-weight: normal;
  letter-spacing: 1px;
}

/* Information fields */

.operator-file .record-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 10px;
}

.operator-file .record-field {
  padding: 13px;
  background: rgba(0,0,0,.18);
  border-left: 2px solid #4b5b3d;
}

.operator-file .record-value {
  color: var(--white);
  font-size: 12px;
  line-height: 1.7;
  overflow-wrap: anywhere;
}

.operator-file .record-value.green {
  color: var(--lime);
}

/* Technical areas */

.operator-file .skill-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.operator-file .skill-list span {
  position: relative;
  padding: 8px 11px;
  background: rgba(181,232,83,.035);
  border: 1px solid #414d38;
  color: #c5ccb9;
  font-size: 10px;
  letter-spacing: 1px;
  transition: .2s ease;
}

.operator-file .skill-list span:hover {
  color: var(--lime);
  border-color: var(--lime);
  background: rgba(181,232,83,.08);
}

/* Operational records */

.operator-file .operations {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 10px;
}

.operator-file .operation {
  min-height: 110px;
  padding: 14px;
  background: rgba(0,0,0,.18);
  border: 1px solid var(--line);
}

.operator-file .operation-number {
  color: var(--olive);
  font-size: 10px;
  letter-spacing: 2px;
}

.operator-file .operation-name {
  margin-top: 12px;
  color: var(--lime);
  font-size: 12px;
  letter-spacing: 1px;
}

.operator-file .operation-desc {
  margin-top: 7px;
  color: var(--muted);
  font-size: 10px;
  line-height: 1.6;
}

/* Redacted note */

.operator-file .intel-note {
  position: relative;
  margin-top: 30px;
  padding: 20px;
  background: rgba(0,0,0,.24);
  border: 1px dashed #59634b;
}

.operator-file .intel-note-title {
  margin-bottom: 12px;
  color: var(--olive);
  font-size: 10px;
  letter-spacing: 2px;
}

.operator-file .intel-note p {
  margin: 0;
  color: #aeb6a4;
  font-size: 11px;
  line-height: 2;
}

.operator-file .redacted {
  display: inline-block;
  padding: 0 7px;
  background: #080b08;
  color: #080b08;
  user-select: none;
}

/* Links */

.operator-file .access-links {
  display: flex;
  flex-wrap: wrap;
  gap: 9px;
}

.operator-file .access-links a {
  display: inline-block;
  padding: 10px 13px;
  color: var(--lime);
  background: #10150f;
  border: 1px solid var(--line);
  text-decoration: none;
  font-size: 10px;
  letter-spacing: 1px;
  transition: .2s ease;
}

.operator-file .access-links a:hover {
  color: var(--paper-dark);
  background: var(--lime);
  border-color: var(--lime);
  transform: translateY(-2px);
}

/* Barcode and footer */

.operator-file .document-bottom {
  display: flex;
  justify-content: space-between;
  align-items: end;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 35px;
  padding-top: 20px;
  border-top: 1px solid var(--line);
}

.operator-file .barcode {
  width: 170px;
  height: 38px;
  background: repeating-linear-gradient(
    90deg,
    #aeb99d 0px,
    #aeb99d 2px,
    transparent 2px,
    transparent 4px,
    #aeb99d 4px,
    #aeb99d 5px,
    transparent 5px,
    transparent 8px,
    #aeb99d 8px,
    #aeb99d 11px,
    transparent 11px,
    transparent 13px
  );
  opacity: .65;
}

.operator-file .barcode-label {
  margin-top: 6px;
  color: var(--muted);
  font-size: 9px;
  letter-spacing: 2px;
}

.operator-file .footer-info {
  color: var(--muted);
  text-align: right;
  font-size: 9px;
  line-height: 1.9;
  letter-spacing: 1px;
}

.operator-file .file-end {
  margin-top: 22px;
  padding: 10px;
  background: rgba(181,232,83,.035);
  color: var(--olive);
  text-align: center;
  font-size: 9px;
  letter-spacing: 3px;
}

/* Responsive */

@media (max-width: 650px) {
  .operator-file .file-sheet {
    padding: 17px;
  }

  .operator-file .subject-grid {
    grid-template-columns: 1fr;
    padding: 14px;
    gap: 20px;
  }

  .operator-file .portrait-frame {
    max-width: 330px;
    width: 100%;
    margin: 0 auto;
  }

  .operator-file .record-grid {
    grid-template-columns: 1fr;
  }

  .operator-file .operations {
    grid-template-columns: 1fr;
  }

  .operator-file .file-reference {
    text-align: left;
  }

  .operator-file .document-bottom {
    align-items: start;
  }

  .operator-file .footer-info {
    text-align: left;
  }
}

@media (prefers-reduced-motion: reduce) {
  .operator-file *,
  .operator-file *::before,
  .operator-file *::after {
    animation: none !important;
    transition: none !important;
  }
}
</style>

<div class="operator-file">
  <div class="file-sheet">

    <!-- DOCUMENT HEADER -->

    <div class="file-header">
      <div>
        <div class="agency">INTELLIGENCE DIVISION</div>
        <div class="agency-sub">CYBERSECURITY // PERSONNEL ARCHIVE</div>
      </div>

      <div class="file-reference">
        DOCUMENT: OTH-001<br>
        REVISION: 01.04<br>
        RECORD: ACTIVE
      </div>
    </div>

    <!-- CLASSIFICATION -->

    <div class="classification-bar">
      <div class="classification">CLASSIFIED</div>
      <div class="classification-note">
        PERSONNEL DOSSIER // PUBLIC RELEASE
      </div>
    </div>

    <h1 class="file-title">
      OPERATOR <span>PROFILE</span>
    </h1>

    <div class="file-subtitle">
      SUBJECT IDENTIFICATION & OPERATIONAL RECORD
    </div>

    <!-- SUBJECT PROFILE -->

    <div class="subject-grid">

      <div class="portrait-frame">
        <img
          src="{{ '/images/01/01.jpg' | relative_url }}"
          alt="Othmane01 operator portrait"
        >
        <div class="portrait-caption">
          SUBJECT IMAGE // OTH-001
        </div>
      </div>

      <div class="subject-details">

        <span class="field-label">SUBJECT NAME</span>
        <h2 class="subject-name">OTHMANE</h2>

        <div class="codename">
          CODENAME // OTHMANE01
        </div>

        <div class="subject-role">
          WEB SECURITY RESEARCHER<br>
          PENETRATION TESTER<br>
          CTF PLAYER // BUG BOUNTY HUNTER
        </div>

        <p class="subject-summary">
          Focused on exploring the security of
          <strong>web applications, APIs, and network infrastructure.</strong>

          Interested in understanding how vulnerabilities work,
          how they can be exploited, and how their impact can be
          demonstrated through practical security research.
          <br><br>
          Every finding deserves a clear explanation,
          reproducible evidence, and responsible disclosure.
        </p>

        <div class="status-line">
          <span class="status-dot"></span>
          RESEARCH STATUS: ACTIVE
        </div>

      </div>
    </div>

    <!-- PERSONNEL RECORD -->

    <section class="record-section">

      <h3 class="section-heading">
        01 // PERSONNEL RECORD
        <small>IDENTIFICATION DATA</small>
      </h3>

      <div class="record-grid">

        <div class="record-field">
          <span class="field-label">SUBJECT IDENTIFIER</span>
          <div class="record-value green">OTH-001</div>
        </div>

        <div class="record-field">
          <span class="field-label">OPERATOR CODENAME</span>
          <div class="record-value">OTHMANE01</div>
        </div>

        <div class="record-field">
          <span class="field-label">PRIMARY SPECIALIZATION</span>
          <div class="record-value">WEB APPLICATION SECURITY</div>
        </div>

        <div class="record-field">
          <span class="field-label">RESEARCH APPROACH</span>
          <div class="record-value">HANDS-ON // PRACTICAL</div>
        </div>

      </div>
    </section>

    <!-- SPECIALIZATION -->

    <section class="record-section">

      <h3 class="section-heading">
        02 // AREAS OF INVESTIGATION
        <small>TECHNICAL FOCUS</small>
      </h3>

      <div class="skill-list">
        <span>SQL INJECTION</span>
        <span>CROSS-SITE SCRIPTING</span>
        <span>SSRF</span>
        <span>IDOR</span>
        <span>CSRF</span>
        <span>AUTHENTICATION</span>
        <span>ACCESS CONTROL</span>
        <span>BUSINESS LOGIC</span>
        <span>COMMAND INJECTION</span>
        <span>API SECURITY</span>
        <span>PRIVILEGE ESCALATION</span>
        <span>NETWORK SECURITY</span>
        <span>LINUX</span>
        <span>WINDOWS</span>
        <span>ACTIVE DIRECTORY</span>
      </div>

    </section>

    <!-- OPERATIONAL RECORDS -->

    <section class="record-section">

      <h3 class="section-heading">
        03 // FIELD RECORDS
        <small>RESEARCH ENVIRONMENTS</small>
      </h3>

      <div class="operations">

        <div class="operation">
          <div class="operation-number">RECORD // 001</div>
          <div class="operation-name">HACK THE BOX</div>
          <div class="operation-desc">
            Machine exploitation, enumeration, privilege escalation,
            and technical challenges.
          </div>
        </div>

        <div class="operation">
          <div class="operation-number">RECORD // 002</div>
          <div class="operation-name">TRYHACKME</div>
          <div class="operation-desc">
            Hands-on security labs, practical learning,
            and documented walkthroughs.
          </div>
        </div>

        <div class="operation">
          <div class="operation-number">RECORD // 003</div>
          <div class="operation-name">HACKERONE</div>
          <div class="operation-desc">
            Vulnerability research, web security testing,
            and responsible disclosure.
          </div>
        </div>

      </div>
    </section>

    <!-- INTELLIGENCE NOTE -->

    <div class="intel-note">
      <div class="intel-note-title">
        // INTERNAL INTELLIGENCE NOTE
      </div>

      <p>
        Primary objective: identify, validate, and document security
        weaknesses in controlled environments and authorized programs.
        <br><br>
        Research materials include technical walkthroughs, exploitation
        notes, CTF writeups, and vulnerability analysis.
        <br><br>
        Additional information:
        <span class="redacted">REDACTED</span>
        <span class="redacted">REDACTED</span>
      </p>
    </div>

    <!-- EXTERNAL RECORDS -->

    <section class="record-section">

      <h3 class="section-heading">
        04 // EXTERNAL RECORDS
        <small>AUTHORIZED ACCESS POINTS</small>
      </h3>

      <div class="access-links">
        <a href="https://github.com/othmane01-bin"
           target="_blank" rel="noopener noreferrer">GITHUB ↗</a>

        <a href="https://www.linkedin.com/in/othmane-labiyad/"
           target="_blank" rel="noopener noreferrer">LINKEDIN ↗</a>

        <a href="https://hackerone.com/othmane01"
           target="_blank" rel="noopener noreferrer">HACKERONE ↗</a>

        <a href="https://tryhackme.com/p/zuul"
           target="_blank" rel="noopener noreferrer">TRYHACKME ↗</a>

        <a href="https://app.hackthebox.com/users/1778179"
           target="_blank" rel="noopener noreferrer">HACK THE BOX ↗</a>

      </div>
    </section>

    <!-- DOCUMENT FOOTER -->

    <div class="document-bottom">

      <div>
        <div class="barcode"></div>
        <div class="barcode-label">OTH-001 // 01-04-2026</div>
      </div>

      <div class="footer-info">
        FILE: OTHMANE01<br>
        DOCUMENT CLASS: PERSONNEL<br>
        ARCHIVE: SECURITY RESEARCH
      </div>

    </div>

    <div class="file-end">
      END OF DOCUMENT // OTHMANE01 // INTELLIGENCE ARCHIVE
    </div>

  </div>
</div>
