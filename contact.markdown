---
layout: contact
title: SECURE COMMUNICATION
permalink: /about/contact
---

<style>
/* =========================================
   OTHMANE01 // FULL-PAGE CONTACT THEME
========================================= */

/* Apply dark background to the entire page */

html:has(.contact-terminal),
body:has(.contact-terminal) {
  background: #10110f !important;
}

body:has(.contact-terminal) #wrapper,
body:has(.contact-terminal) #main_content,
body:has(.contact-terminal) .inner {
  background: #10110f !important;
}

/* Contact content */

.contact-terminal {
  --ct-text: #e6e8e2;
  --ct-muted: #92958d;
  --ct-green: #b5e853;
  --ct-border: rgba(181, 232, 83, .20);

  max-width: 850px;
  margin: 35px auto;
  padding: 35px 0;
  background: transparent !important;
  border: none !important;
  box-shadow: none !important;
  color: var(--ct-text);
  font-family: inherit;
  font-size: 14px;
  line-height: 1.7;
}

.contact-terminal * {
  box-sizing: border-box;
}

/* Sequential reveal */

.contact-terminal .ct-reveal {
  opacity: 0;
  transform: translateY(12px);
  animation: ct-appear .6s ease forwards;
}

.contact-terminal .ct-1 { animation-delay: .15s; }
.contact-terminal .ct-2 { animation-delay: .4s; }
.contact-terminal .ct-3 { animation-delay: .65s; }
.contact-terminal .ct-4 { animation-delay: .9s; }
.contact-terminal .ct-5 { animation-delay: 1.15s; }

@keyframes ct-appear {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Header */

.contact-terminal .ct-header {
  margin-bottom: 42px;
}

.contact-terminal .ct-topline {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--ct-border);
  color: var(--ct-muted);
  font-size: 10px;
  letter-spacing: 1.5px;
}

.contact-terminal .ct-status {
  color: var(--ct-green);
}

.contact-terminal .ct-status::before {
  content: "";
  display: inline-block;
  width: 6px;
  height: 6px;
  margin-right: 7px;
  border-radius: 50%;
  background: var(--ct-green);
  box-shadow: 0 0 8px var(--ct-green);
  animation: ct-pulse 1.5s infinite;
}

@keyframes ct-pulse {
  50% { opacity: .35; }
}

.contact-terminal .ct-heading {
  margin: 30px 0 5px;
  color: var(--ct-text);
  font-family: inherit;
  font-size: clamp(27px, 5vw, 43px);
  font-weight: bold;
  line-height: 1.2;
  letter-spacing: -1px;
}

.contact-terminal .ct-heading span {
  color: var(--ct-green);
}

.contact-terminal .ct-subtitle {
  margin: 0;
  color: var(--ct-muted);
  font-size: 10px;
  letter-spacing: 1.5px;
}

/* Channel directory */

.contact-terminal .ct-section-label {
  margin-bottom: 8px;
  color: var(--ct-muted);
  font-size: 10px;
  letter-spacing: 1.5px;
}

.contact-terminal .ct-channel {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  padding: 23px 0;
  border-bottom: 1px solid var(--ct-border);
  transition: padding-left .25s ease;
}

.contact-terminal .ct-channel:first-of-type {
  border-top: 1px solid var(--ct-border);
}

.contact-terminal .ct-channel:hover {
  padding-left: 9px;
}

.contact-terminal .ct-channel-info {
  min-width: 0;
}

.contact-terminal .ct-channel-number {
  display: block;
  margin-bottom: 5px;
  color: var(--ct-muted);
  font-size: 10px;
  letter-spacing: 1.5px;
}

.contact-terminal .ct-channel-name {
  display: inline-block;
  color: var(--ct-text);
  font-size: clamp(20px, 4vw, 28px);
  font-weight: bold;
  line-height: 1.3;
  text-decoration: none;
  transition: color .2s ease;
}

.contact-terminal .ct-channel-name:hover {
  color: var(--ct-green);
  text-decoration: none;
}

.contact-terminal .ct-username {
  display: block;
  margin-top: 3px;
  color: var(--ct-muted);
  font-size: 13px;
  overflow-wrap: anywhere;
}

/* Actions */

.contact-terminal .ct-channel-actions {
  display: flex;
  align-items: center;
  gap: 15px;
  flex-shrink: 0;
}

.contact-terminal .ct-open {
  color: var(--ct-green);
  font-size: 25px;
  line-height: 1;
  text-decoration: none;
  transition: transform .2s ease, color .2s ease;
}

.contact-terminal .ct-open:hover {
  color: #fff;
  transform: translate(3px, -3px);
  text-decoration: none;
}

.contact-terminal .ct-copy {
  padding: 5px 0;
  border: 0;
  background: transparent;
  color: var(--ct-muted);
  font-family: inherit;
  font-size: 9px;
  letter-spacing: 1px;
  cursor: pointer;
  transition: color .2s ease;
}

.contact-terminal .ct-copy:hover {
  color: var(--ct-green);
}

/* Footer */

.contact-terminal .ct-footer {
  margin-top: 35px;
  color: var(--ct-muted);
  font-size: 10px;
  letter-spacing: 1px;
}

.contact-terminal .ct-prompt {
  margin-top: 12px;
  color: var(--ct-green);
}

.contact-terminal .ct-cursor {
  display: inline-block;
  width: 7px;
  height: 13px;
  margin-left: 5px;
  vertical-align: middle;
  background: var(--ct-green);
  animation: ct-blink 1s steps(2, start) infinite;
}

@keyframes ct-blink {
  to { visibility: hidden; }
}

/* Mobile */

@media (max-width: 600px) {
  .contact-terminal {
    margin: 20px auto;
    padding: 22px 0;
  }

  .contact-terminal .ct-channel {
    gap: 8px;
    padding: 20px 0;
  }

  .contact-terminal .ct-channel-actions {
    gap: 10px;
  }

  .contact-terminal .ct-copy {
    font-size: 8px;
  }
}

/* Accessibility */

@media (prefers-reduced-motion: reduce) {
  .contact-terminal .ct-reveal {
    opacity: 1;
    transform: none;
    animation: none;
  }

  .contact-terminal .ct-status::before,
  .contact-terminal .ct-cursor {
    animation: none;
  }

  .contact-terminal .ct-channel,
  .contact-terminal .ct-open {
    transition: none;
  }
}
</style>

<div class="contact-terminal">

  <!-- HEADER -->
  <header class="ct-header ct-reveal ct-1">

    <div class="ct-topline">
      <span>OTHMANE01 / CONTACT</span>
      <span class="ct-status">ONLINE</span>
    </div>

    <h2 class="ct-heading">
      LET'S <span>CONNECT.</span>
    </h2>

    <p class="ct-subtitle">
      SELECT A COMMUNICATION CHANNEL
    </p>

  </header>

  <!-- PUBLIC CHANNELS -->
  <section>

    <div class="ct-section-label ct-reveal ct-2">
      01 // PUBLIC CHANNELS
    </div>

    <!-- X -->
    <article class="ct-channel ct-reveal ct-2">

      <div class="ct-channel-info">
        <span class="ct-channel-number">01 / SOCIAL</span>

        <a class="ct-channel-name"
           href="https://x.com/othmane01_"
           target="_blank"
           rel="noopener noreferrer">X / TWITTER</a>

        <span class="ct-username">@othmane01_</span>
      </div>

      <div class="ct-channel-actions">

        <button class="ct-copy"
                type="button"
                data-copy="@othmane01_">COPY ID</button>

        <a class="ct-open"
           href="https://x.com/othmane01_"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Open X profile">↗</a>

      </div>

    </article>

    <!-- GITHUB -->
    <article class="ct-channel ct-reveal ct-3">

      <div class="ct-channel-info">
        <span class="ct-channel-number">02 / SOURCE CODE</span>

        <a class="ct-channel-name"
           href="https://github.com/othmane01-bin"
           target="_blank"
           rel="noopener noreferrer">GITHUB</a>

        <span class="ct-username">othmane01-bin</span>
      </div>

      <div class="ct-channel-actions">

        <button class="ct-copy"
                type="button"
                data-copy="othmane01-bin">COPY ID</button>

        <a class="ct-open"
           href="https://github.com/othmane01-bin"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Open GitHub profile">↗</a>

      </div>

    </article>

    <!-- LINKEDIN -->
    <article class="ct-channel ct-reveal ct-4">

      <div class="ct-channel-info">
        <span class="ct-channel-number">03 / PROFESSIONAL</span>

        <a class="ct-channel-name"
           href="https://www.linkedin.com/in/othmane-labiyad/"
           target="_blank"
           rel="noopener noreferrer">LINKEDIN</a>

        <span class="ct-username">othmane01</span>
      </div>

      <div class="ct-channel-actions">

        <button class="ct-copy"
                type="button"
                data-copy="othmane01">COPY ID</button>

        <a class="ct-open"
           href="https://www.linkedin.com/in/othmane-labiyad/"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Open LinkedIn profile">↗</a>

      </div>

    </article>

  </section>

  <!-- FOOTER -->
  <footer class="ct-footer ct-reveal ct-5">

    OTH-COM-001 // PUBLIC DIRECTORY

    <div class="ct-prompt">
      root@othmane01:~$ establish_connection<span class="ct-cursor"></span>
    </div>

  </footer>

</div>

<script>
// Copy usernames
document.addEventListener("click", function(event) {
  const button = event.target.closest(".contact-terminal .ct-copy");

  if (!button) return;

  const value = button.getAttribute("data-copy");
  const originalText = button.textContent;

  function copied() {
    button.textContent = "COPIED ✓";

    window.setTimeout(function() {
      button.textContent = originalText;
    }, 1500);
  }

  if (navigator.clipboard && window.isSecureContext) {
    navigator.clipboard.writeText(value)
      .then(copied)
      .catch(function() {
        button.textContent = "COPY FAILED";
      });
  } else {
    const temporary = document.createElement("textarea");
    temporary.value = value;
    temporary.style.position = "fixed";
    temporary.style.opacity = "0";

    document.body.appendChild(temporary);
    temporary.select();

    try {
      document.execCommand("copy");
      copied();
    } catch (error) {
      button.textContent = "COPY FAILED";
    }

    temporary.remove();
  }
});

// Scroll to top only when the page is reloaded
(function() {
  const navigation = performance.getEntriesByType("navigation")[0];

  if (!navigation || navigation.type !== "reload") return;

  if ("scrollRestoration" in history) {
    history.scrollRestoration = "manual";
  }

  window.addEventListener("pageshow", function() {
    window.scrollTo(0, 0);
  }, { once: true });
})();
</script>
