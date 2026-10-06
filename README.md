<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Homework: Responsive Media Queries</title>
  <style>
    :root {
      --bg-main: #0f172a;
      --bg-card: #1e293b;
      --bg-inner: #0f172a;
      --accent: #38bdf8;
      --accent-hover: #0284c7;
      --accent-green: #34d399;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --border-color: #334155;
      --font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg-main);
      color: var(--text-main);
      font-family: var(--font-family);
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    /* Skip link */
    .skip-link {
      position: absolute;
      top: -100px;
      left: 10px;
      background: #f59e0b;
      color: #000;
      padding: 8px 16px;
      z-index: 1000;
      font-weight: bold;
      border-radius: 4px;
      text-decoration: none;
      transition: top 0.2s ease;
    }
    .skip-link:focus {
      top: 10px;
    }

    header {
      background-color: #1a2234;
      border-bottom: 1px solid var(--border-color);
      padding: 1rem 1.5rem;
    }

    .header-content {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
    }

    h1 {
      font-size: 1.4rem;
      color: var(--accent);
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .badge {
      background-color: rgba(56, 189, 248, 0.15);
      color: var(--accent);
      padding: 0.2rem 0.6rem;
      border-radius: 999px;
      font-size: 0.75rem;
      border: 1px solid rgba(56, 189, 248, 0.3);
    }

    .tab-bar {
      display: flex;
      gap: 0.5rem;
      background: var(--bg-main);
      padding: 4px;
      border-radius: 8px;
      border: 1px solid var(--border-color);
    }

    .tab-btn {
      background: transparent;
      border: none;
      color: var(--text-muted);
      padding: 0.5rem 1rem;
      font-size: 0.875rem;
      font-weight: 500;
      border-radius: 6px;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .tab-btn.active {
      background-color: var(--accent);
      color: #0f172a;
      font-weight: 600;
    }

    main {
      flex: 1;
      max-width: 1200px;
      width: 100%;
      margin: 0 auto;
      padding: 1.5rem;
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    /* Workbench Area */
    .viewport-controls {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: var(--bg-card);
      padding: 0.75rem 1rem;
      border-radius: 8px 8px 0 0;
      border: 1px solid var(--border-color);
      border-bottom: none;
    }

    .device-buttons {
      display: flex;
      gap: 0.5rem;
    }

    .device-btn {
      background: var(--bg-main);
      border: 1px solid var(--border-color);
      color: var(--text-muted);
      padding: 0.4rem 0.8rem;
      border-radius: 6px;
      font-size: 0.8rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 0.4rem;
    }

    .device-btn.active {
      border-color: var(--accent);
      color: var(--accent);
      background: rgba(56, 189, 248, 0.08);
    }

    .viewport-indicator {
      font-size: 0.8rem;
      color: var(--text-muted);
      font-family: monospace;
    }

    .stage-container {
      background: #000;
      border: 1px solid var(--border-color);
      border-radius: 0 0 8px 8px;
      padding: 1.5rem;
      display: flex;
      justify-content: center;
      min-height: 520px;
      overflow-x: auto;
    }

    /* Embedded Simulated Site */
    .simulated-viewport {
      background: #ffffff;
      color: #1e293b;
      transition: width 0.4s ease;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
      border-radius: 6px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }

    /* Simulated Site Specific Styles */
    .sim-site {
      font-family: var(--font-family);
      padding: 1rem;
      height: 100%;
      overflow-y: auto;
    }

    .sim-header {
      background-color: #3b82f6;
      color: white;
      text-align: center;
      padding: 1rem;
      border-radius: 4px;
      margin-bottom: 1rem;
    }

    /* Mobile First Base Styles (Starter) */
    .sim-container {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .sim-card {
      background: #f1f5f9;
      border: 1px solid #cbd5e1;
      border-radius: 6px;
      padding: 1rem;
      text-align: center;
    }

    .sim-card img {
      width: 100%;
      height: 140px;
      object-fit: cover;
      border-radius: 4px;
      margin-bottom: 0.5rem;
      border: 2px solid #e2e8f0;
    }

    .sim-card h3 {
      font-size: 1.1rem;
      margin-bottom: 0.25rem;
      color: #0f172a;
    }

    .sim-card p {
      font-size: 0.85rem;
      color: #475569;
    }

    /* Media Query 1 Demonstration (Tablet >= 600px) */
    @media (min-width: 600px) {
      .sim-container.mq1-active {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
      }
      .sim-container.mq1-active .sim-card img {
        height: 180px;
        border-color: #3b82f6;
      }
    }

    /* Media Query 2 Demonstration (Desktop >= 900px) */
    @media (min-width: 900px) {
      .sim-container.mq2-active {
        grid-template-columns: repeat(3, 1fr);
      }
      .sim-container.mq2-active .sim-card {
        background: #e0f2fe;
        border-color: #7dd3fc;
      }
    }

    /* Code View */
    .code-container {
      background: #090d16;
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 1rem;
      overflow-x: auto;
    }

    pre {
      font-family: 'Courier New', Courier, monospace;
      font-size: 0.9rem;
      color: #e2e8f0;
    }

    .code-keyword { color: #f472b6; }
    .code-selector { color: #38bdf8; }
    .code-property { color: #34d399; }
    .code-value { color: #fbbf24; }
    .code-comment { color: #64748b; font-style: italic; }

    /* Checklist & Instructions */
    .checklist-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1rem;
      margin-top: 1rem;
    }

    .step-card {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 1.25rem;
    }

    .step-card h3 {
      font-size: 1rem;
      color: var(--accent);
      margin-bottom: 0.5rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .step-number {
      background: rgba(56, 189, 248, 0.2);
      color: var(--accent);
      width: 24px;
      height: 24px;
      border-radius: 50%;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-size: 0.8rem;
      font-weight: bold;
    }

    .step-card p, .step-card ul {
      font-size: 0.875rem;
      color: var(--text-muted);
    }

    .step-card ul {
      list-style-type: disc;
      padding-left: 1.2rem;
      margin-top: 0.5rem;
    }

    footer {
      border-top: 1px solid var(--border-color);
      padding: 1rem;
      text-align: center;
      font-size: 0.8rem;
      color: var(--text-muted);
      margin-top: auto;
    }
  </style>
</head>
<body>
  <a href="#main-content" class="skip-link">Skip to Main Content</a>

  <header>
    <div class="header-content">
      <h1>
        Homework: Responsive Web Design
        <span class="badge">Media Queries</span>
      </h1>
      <nav class="tab-bar">
        <button class="tab-btn active" onclick="switchTab('preview')">Live Viewport Tester</button>
        <button class="tab-btn" onclick="switchTab('code')">styles.css Inspector</button>
        <button class="tab-btn" onclick="switchTab('workflow')">Submission Workflow</button>
      </nav>
    </div>
  </header>

  <main id="main-content">
    <!-- TAB 1: PREVIEW -->
    <section id="tab-preview" class="tab-content active">
      <div class="viewport-controls">
        <div class="device-buttons">
          <button class="device-btn active" onclick="setViewport('mobile')">
            📱 Mobile (&lt;600px)
          </button>
          <button class="device-btn" onclick="setViewport('tablet')">
            📱 Tablet (600px - 899px)
          </button>
          <button class="device-btn" onclick="setViewport('desktop')">
            💻 Desktop (&ge;900px)
          </button>
        </div>
        <div class="viewport-indicator" id="viewport-label">
          Width: 375px (Default Mobile Layout)
        </div>
      </div>

      <div class="stage-container">
        <div id="sim-viewport" class="simulated-viewport" style="width: 375px;">
          <div class="sim-site">
            <header class="sim-header">
              <h2>Responsive Parks Gallery</h2>
              <p style="font-size:0.8rem; opacity:0.9;">Mobile First Baseline</p>
            </header>
            <div id="sim-container" class="sim-container mq1-active mq2-active">
              <div class="sim-card">
                <img src="https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=400&q=80" alt="Yosemite Valley view" />
                <h3>Yosemite Valley</h3>
                <p>Stacked 100% full width layout on mobile devices.</p>
              </div>
              <div class="sim-card">
                <img src="https://images.unsplash.com/photo-1511497584788-8767611136f6?auto=format&fit=crop&w=400&q=80" alt="Pine forest landscape" />
                <h3>Yellowstone Park</h3>
                <p>Adjusts layout based on active CSS media query breakpoints.</p>
              </div>
              <div class="sim-card">
                <img src="https://images.unsplash.com/photo-1426604966848-d7adac402bff?auto=format&fit=crop&w=400&q=80" alt="Mountain lake reflection" />
                <h3>Glacier Park</h3>
                <p>Grid columns expand from 1 column to 2 and 3 columns.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB 2: CODE -->
    <section id="tab-code" class="tab-content">
      <div class="code-container">
        <pre><code><span class="code-comment">/* ============================================================
   HOMEWORK: RESPONSIVE MEDIA QUERIES (styles.css)
   ============================================================ */</span>

<span class="code-comment">/* Step 3: Base Mobile Styles (Mobile-First approach) */</span>
<span class="code-selector">.sim-container</span> {
  <span class="code-property">display</span>: <span class="code-value">flex</span>;
  <span class="code-property">flex-direction</span>: <span class="code-value">column</span>;
  <span class="code-property">gap</span>: <span class="code-value">1rem</span>;
}

<span class="code-selector">.sim-card img</span> {
  <span class="code-property">width</span>: <span class="code-value">100%</span>;
  <span class="code-property">height</span>: <span class="code-value">auto</span>;
  <span class="code-property">border</span>: <span class="code-value">2px solid #cbd5e1</span>;
}

<span class="code-comment">/* Step 4 & 5: First Media Query (Tablet Breakpoint >= 600px) */</span>
<span class="code-keyword">@media</span> <span class="code-value">screen and (min-width: 600px)</span> {
  <span class="code-selector">.sim-container</span> {
    <span class="code-property">display</span>: <span class="code-value">grid</span>;
    <span class="code-property">grid-template-columns</span>: <span class="code-value">repeat(2, 1fr)</span>;
    <span class="code-property">gap</span>: <span class="code-value">1.5rem</span>;
  }

  <span class="code-selector">.sim-card img</span> {
    <span class="code-property">border-color</span>: <span class="code-value">#3b82f6</span>; <span class="code-comment">/* Highlight image border change */</span>
    <span class="code-property">border-radius</span>: <span class="code-value">8px</span>;
  }
}

<span class="code-comment">/* Step 6 & 7: Second Media Query (Desktop Breakpoint >= 900px) */</span>
<span class="code-keyword">@media</span> <span class="code-value">screen and (min-width: 900px)</span> {
  <span class="code-selector">.sim-container</span> {
    <span class="code-property">grid-template-columns</span>: <span class="code-value">repeat(3, 1fr)</span>;
  }

  <span class="code-selector">.sim-card</span> {
    <span class="code-property">background-color</span>: <span class="code-value">#e0f2fe</span>; <span class="code-comment">/* Adjust div styling for desktop */</span>
    <span class="code-property">padding</span>: <span class="code-value">1.25rem</span>;
  }
}</code></pre>
      </div>
    </section>

    <!-- TAB 3: WORKFLOW STEPS -->
    <section id="tab-workflow" class="tab-content">
      <div class="checklist-grid">
        <div class="step-card">
          <h3><span class="step-number">1</span> Starter Setup</h3>
          <p>Clone or download the starter code repository from GitHub and open the directory in VS Code or your preferred text editor.</p>
        </div>

        <div class="step-card">
          <h3><span class="step-number">2</span> Mobile Review</h3>
          <p>Open <code>index.html</code> in your browser. Open Developer Tools (F12) and toggle Device Toolbar to inspect the base layout at 375px width.</p>
        </div>

        <div class="step-card">
          <h3><span class="step-number">3</span> First Media Query</h3>
          <p>Add <code>@media screen and (min-width: 600px)</code> to your CSS. Write rules to convert the layout to 2 columns and update image border properties.</p>
        </div>

        <div class="step-card">
          <h3><span class="step-number">4</span> Second Media Query</h3>
          <p>Add <code>@media screen and (min-width: 900px)</code>. Update the div container to 3 columns and adjust card background/padding styles.</p>
        </div>

        <div class="step-card">
          <h3><span class="step-number">5</span> Verification</h3>
          <p>Resize your browser window from 320px up to 1200px to ensure smooth layout transitions across mobile, tablet, and desktop viewports.</p>
        </div>

        <div class="step-card">
          <h3><span class="step-number">6</span> Hosting & Sharing</h3>
          <p>Push your completed code to GitHub Pages, Netlify, or Vercel, and submit your live site URL alongside your repository link.</p>
        </div>
      </div>
    </section>
  </main>

  <footer>
    Homework Assistant &bull; Responsive Media Queries Guide
  </footer>

  <script>
    function switchTab(tabId) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

      event.target.classList.add('active');
      document.getElementById('tab-' + tabId).classList.add('active');
    }

    function setViewport(device) {
      const viewport = document.getElementById('sim-viewport');
      const label = document.getElementById('viewport-label');
      const buttons = document.querySelectorAll('.device-btn');

      buttons.forEach(btn => btn.classList.remove('active'));
      event.currentTarget.classList.add('active');

      if (device === 'mobile') {
        viewport.style.width = '375px';
        label.textContent = 'Width: 375px (Default Mobile Layout)';
      } else if (device === 'tablet') {
        viewport.style.width = '680px';
        label.textContent = 'Width: 680px (Active: 1st Media Query @ min-width: 600px)';
      } else if (device === 'desktop') {
        viewport.style.width = '960px';
        label.textContent = 'Width: 960px (Active: 2nd Media Query @ min-width: 900px)';
      }
    }
  </script>
</body>
</html>
