<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Mint In-Progress Site</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <style>
    :root {
      --mint: #10a37f;           /* mint accent (ChatGPT-style) */
      --radius-lg: 16px;
      --radius-pill: 999px;
      --transition-fast: 0.18s ease-out;

      /* Light theme */
      --bg: #f5faf9;
      --bg-elevated: #ffffff;
      --bg-subtle: #e9f5f1;
      --text: #0f172a;
      --text-soft: #6b7280;
      --border-subtle: rgba(15, 23, 42, 0.06);
      --shadow-soft: 0 18px 45px rgba(15, 23, 42, 0.06);
    }

    body.dark {
      /* Dark theme (ChatGPT-ish) */
      --bg: #202123;
      --bg-elevated: #2b2c2f;
      --bg-subtle: #18191c;
      --text: #e5e7eb;
      --text-soft: #9ca3af;
      --border-subtle: rgba(148, 163, 184, 0.16);
      --shadow-soft: 0 18px 45px rgba(0, 0, 0, 0.65);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text",
        "Inter", sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: stretch;
      padding: 24px;
      transition:
        background-color var(--transition-fast),
        color var(--transition-fast);
    }

    .shell {
      width: 100%;
      max-width: 960px;
      background: linear-gradient(
        135deg,
        rgba(16, 163, 127, 0.12),
        rgba(16, 163, 127, 0)
      );
      border-radius: 28px;
      padding: 1px;
    }

    .frame {
      background: var(--bg);
      border-radius: 26px;
      padding: 20px 18px;
      box-shadow: var(--shadow-soft);
      border: 1px solid var(--border-subtle);
      display: flex;
      flex-direction: column;
      gap: 18px;
      min-height: calc(100vh - 80px);
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .brand-logo {
      width: 32px;
      height: 32px;
      border-radius: 12px;
      background: radial-gradient(circle at 0 0, #6ee7b7, var(--mint));
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      color: white;
      font-size: 16px;
      box-shadow: 0 10px 25px rgba(16, 163, 127, 0.45);
    }

    .brand-text-main {
      font-weight: 600;
      letter-spacing: 0.01em;
      font-size: 16px;
    }

    .brand-text-sub {
      font-size: 12px;
      color: var(--text-soft);
    }

    /* Dark mode toggle button */
    .theme-toggle {
      border-radius: var(--radius-pill);
      border: 1px solid rgba(148, 163, 184, 0.4);
      background: radial-gradient(circle at 0 0, rgba(16, 163, 127, 0.18), rgba(24, 24, 27, 0));
      padding: 4px 7px;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      cursor: pointer;
      font-size: 13px;
      color: var(--text-soft);
      position: relative;
      overflow: hidden;
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      transition:
        border-color var(--transition-fast),
        background-color var(--transition-fast),
        color var(--transition-fast),
        transform 0.12s ease-out;
    }

    .theme-toggle:hover {
      transform: translateY(-1px);
      border-color: rgba(16, 163, 127, 0.7);
    }

    .theme-toggle .pill {
      width: 22px;
      height: 22px;
      border-radius: 999px;
      background: var(--bg-elevated);
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 6px 20px rgba(15, 23, 42, 0.36);
      transition:
        background-color var(--transition-fast),
        transform var(--transition-fast);
    }

    .theme-toggle-icon {
      width: 13px;
      height: 13px;
    }

    body.dark .theme-toggle .pill {
      transform: translateX(8px);
      background: var(--mint);
    }

    body.dark .theme-toggle {
      color: #e5e7eb;
      border-color: rgba(148, 163, 184, 0.6);
    }

    /* Main content */
    main {
      flex: 1;
      display: grid;
      grid-template-columns: minmax(0, 1.4fr) minmax(0, 1fr);
      gap: 16px;
    }

    @media (max-width: 768px) {
      main {
        grid-template-columns: minmax(0, 1fr);
      }
    }

    .hero {
      background: radial-gradient(circle at top left, rgba(16, 163, 127, 0.16), transparent),
        var(--bg-elevated);
      border-radius: var(--radius-lg);
      padding: 18px 18px 16px;
      border: 1px solid var(--border-subtle);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .hero-label {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--mint);
      background: rgba(16, 163, 127, 0.08);
      border-radius: 999px;
      padding: 3px 9px;
      border: 1px dashed rgba(16, 163, 127, 0.4);
    }

    .hero-title {
      font-size: clamp(24px, 3vw, 30px);
      line-height: 1.15;
      margin-top: 12px;
      margin-bottom: 8px;
    }

    .hero-subtitle {
      font-size: 13px;
      color: var(--text-soft);
      max-width: 32rem;
    }

    .hero-footer {
      margin-top: 18px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
      font-size: 11px;
      color: var(--text-soft);
    }

    .hero-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--mint);
      box-shadow: 0 0 0 6px rgba(16, 163, 127, 0.25);
    }

    .hero-progress {
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .hero-progress-bar {
      position: relative;
      width: 120px;
      height: 3px;
      border-radius: 999px;
      background: var(--bg-subtle);
      overflow: hidden;
    }

    .hero-progress-bar span {
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      width: 60%;
      border-radius: inherit;
      background: linear-gradient(90deg, #6ee7b7, var(--mint));
    }

    .quick-panels {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .card {
      background: var(--bg-elevated);
      border-radius: var(--radius-lg);
      padding: 12px 13px;
      border: 1px solid var(--border-subtle);
      font-size: 12px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .card-title {
      font-size: 12px;
      font-weight: 600;
    }

    .pill-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }

    .pill-chip {
      font-size: 11px;
      padding: 4px 9px;
      border-radius: 999px;
      background: var(--bg-subtle);
      border: 1px solid rgba(148, 163, 184, 0.25);
      color: var(--text-soft);
    }

    .pill-chip strong {
      color: var(--mint);
      font-weight: 600;
    }

    .placeholder-line {
      height: 6px;
      border-radius: 999px;
      background: linear-gradient(
        90deg,
        rgba(148, 163, 184, 0.4),
        rgba(148, 163, 184, 0.12)
      );
      max-width: 160px;
    }

    footer {
      font-size: 11px;
      color: var(--text-soft);
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
      border-top: 1px dashed rgba(148, 163, 184, 0.25);
      padding-top: 10px;
      margin-top: 4px;
    }

    footer a {
      color: var(--mint);
      text-decoration: none;
      font-weight: 500;
      border-bottom: 1px solid transparent;
      padding-bottom: 1px;
    }

    footer a:hover {
      border-bottom-color: rgba(16, 163, 127, 0.5);
    }
  </style>
</head>
<body>
  <div class="shell">
    <div class="frame">
      <header>
        <div class="brand">
          <div class="brand-logo">M</div>
          <div>
            <div class="brand-text-main">Mint Studio</div>
            <div class="brand-text-sub">in-progress concept page</div>
          </div>
        </div>

        <button class="theme-toggle" id="theme-toggle" aria-label="Toggle dark mode">
          <div class="pill">
            <!-- minimal sun/moon icon -->
            <svg class="theme-toggle-icon" viewBox="0 0 24 24" aria-hidden="true">
              <path
                d="M12 4.5a7.5 7.5 0 1 0 7.04 9.9A6.5 6.5 0 0 1 12 4.5z"
                fill="currentColor"
              />
            </svg>
          </div>
          <span id="theme-label">Dark</span>
        </button>
      </header>

      <main>
        <section class="hero">
          <div>
            <div class="hero-label">
              <span>WIP</span>
              <span>mint interface</span>
            </div>

            <h1 class="hero-title">
              A calm, mint-tinted workspace<br />
              that’s still in the making.
            </h1>

            <p class="hero-subtitle">
              This is just a skeleton. Add sections, content blocks, and interactions as your
              idea grows. The mint accent keeps everything clean and focused, while the
              ChatGPT-style dark mode is ready to go.
            </p>
          </div>

          <div class="hero-footer">
            <div class="hero-progress">
              <span class="hero-dot"></span>
              <span>Prototype status · 60%</span>
            </div>

            <div class="hero-progress-bar">
              <span></span>
            </div>
          </div>
        </section>

        <section class="quick-panels">
          <article class="card">
            <div class="card-title">Next steps</div>
            <div class="pill-row">
              <span class="pill-chip"><strong>01</strong> · Navigation</span>
              <span class="pill-chip"><strong>02</strong> · About section</span>
              <span class="pill-chip"><strong>03</strong> · Project grid</span>
              <span class="pill-chip"><strong>04</strong> · Contact form</span>
            </div>
          </article>

          <article class="card">
            <div class="card-title">In-progress blocks</div>
            <div class="placeholder-line"></div>
            <div class="placeholder-line" style="max-width: 120px;"></div>
            <div class="placeholder-line" style="max-width: 80px;"></div>
          </article>

          <article class="card">
            <div class="card-title">Theme &amp; tokens</div>
            <div class="pill-row">
              <span class="pill-chip">Accent · <strong>Mint</strong></span>
              <span class="pill-chip">Corners · <strong>16px+</strong></span>
              <span class="pill-chip">Shadow · <strong>Soft</strong></span>
              <span class="pill-chip">Mode · <strong>Light/Dark</strong></span>
            </div>
          </article>
        </section>
      </main>

      <footer>
        <span>Designed as a minimal starter — customize freely.</span>
        <span>Dark mode is synced with your preference.</span>
      </footer>
    </div>
  </div>

  <script>
    (function () {
      const body = document.body;
      const toggle = document.getElementById("theme-toggle");
      const label = document.getElementById("theme-label");

      const prefersDark = window.matchMedia &&
        window.matchMedia("(prefers-color-scheme: dark)").matches;

      const stored = window.localStorage.getItem("mint-theme");

      if (stored === "dark" || (!stored && prefersDark)) {
        body.classList.add("dark");
      }

      function updateLabel() {
        const isDark = body.classList.contains("dark");
        label.textContent = isDark ? "Light" : "Dark";
      }

      updateLabel();

      toggle.addEventListener("click", () => {
        const isDark = body.classList.toggle("dark");
        window.localStorage.setItem("mint-theme", isDark ? "dark" : "light");
        updateLabel();
      });
    })();
  </script>
</body>
</html>
