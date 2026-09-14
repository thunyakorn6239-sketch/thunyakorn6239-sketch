<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>THUNYAKORN PIAMANBOONTEE — 3D Portfolio</title>
  <meta name="description" content="THUNYAKORN PIAMANBOONTEE — 3D Artist & Digital Media Designer Portfolio" />

  <style>
    :root {
      --bg: #030504;
      --panel: rgba(7, 12, 9, 0.84);
      --line: rgba(160, 255, 185, 0.2);
      --text: #e6ffe9;
      --muted: #82a88b;
      --accent: #8dff9f;
      --accent-2: #d8ffe0;
    }

    * { box-sizing: border-box; }

    html {
      scroll-behavior: smooth;
      background: var(--bg);
    }

    body {
      margin: 0;
      min-height: 100vh;
      background:
        radial-gradient(circle at 75% 20%, rgba(45, 120, 62, 0.14), transparent 32%),
        radial-gradient(circle at 15% 80%, rgba(45, 120, 62, 0.09), transparent 28%),
        var(--bg);
      color: var(--text);
      font-family: "Courier New", Courier, monospace;
      overflow-x: hidden;
    }

    #scene {
      position: fixed;
      inset: 0;
      z-index: 0;
    }

    #scene canvas {
      display: block;
      width: 100%;
      height: 100%;
    }

    .scanlines {
      position: fixed;
      inset: 0;
      z-index: 1;
      pointer-events: none;
      opacity: 0.10;
      background:
        repeating-linear-gradient(
          to bottom,
          transparent 0px,
          transparent 2px,
          rgba(255,255,255,0.06) 3px,
          transparent 4px
        );
      mix-blend-mode: screen;
    }

    .vignette {
      position: fixed;
      inset: 0;
      z-index: 1;
      pointer-events: none;
      background: radial-gradient(circle, transparent 42%, rgba(0,0,0,0.55) 100%);
    }

    .ui {
      position: relative;
      z-index: 2;
    }

    header {
      min-height: 100vh;
      display: grid;
      grid-template-rows: auto 1fr auto;
      padding: 24px 5vw 28px;
    }

    nav {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 30px;
    }

    .brand {
      letter-spacing: 0.18em;
      font-size: 12px;
      color: var(--accent);
      text-transform: uppercase;
    }

    nav a {
      color: var(--muted);
      text-decoration: none;
      font-size: 11px;
      margin-left: 22px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      transition: color 180ms ease;
    }

    nav a:hover { color: var(--accent-2); }

    .hero {
      max-width: 960px;
      align-self: center;
      pointer-events: none;
    }

    .eyebrow {
      margin: 0 0 16px;
      color: var(--accent);
      font-size: clamp(10px, 1.2vw, 13px);
      letter-spacing: 0.30em;
      text-transform: uppercase;
    }

    h1 {
      margin: 0;
      max-width: 950px;
      font-size: clamp(48px, 9vw, 132px);
      line-height: 0.88;
      letter-spacing: -0.06em;
      text-transform: uppercase;
      text-shadow: 0 0 30px rgba(141,255,159,0.12);
    }

    .hero-line {
      width: min(520px, 55vw);
      height: 1px;
      background: linear-gradient(90deg, var(--accent), transparent);
      margin: 30px 0 18px;
      opacity: 0.7;
    }

    .hero-copy {
      width: min(560px, 100%);
      margin: 0;
      color: var(--muted);
      font-size: clamp(12px, 1.25vw, 15px);
      line-height: 1.8;
    }

    .hero-copy strong { color: var(--accent-2); }

    .controls-hint {
      align-self: end;
      display: flex;
      justify-content: space-between;
      gap: 20px;
      color: rgba(230,255,233,0.5);
      font-size: 10px;
      letter-spacing: 0.14em;
      text-transform: uppercase;
    }

    .scroll {
      animation: blink 1.6s ease-in-out infinite;
    }

    @keyframes blink {
      50% { opacity: 0.25; }
    }

    main {
      position: relative;
      z-index: 2;
      padding: 8vh 5vw 10vh;
      background: linear-gradient(to bottom, transparent, rgba(3,5,4,0.96) 10%);
    }

    section {
      max-width: 1200px;
      margin: 0 auto;
      padding: 9vh 0;
      border-top: 1px solid var(--line);
    }

    .section-head {
      display: grid;
      grid-template-columns: 0.25fr 1fr;
      gap: 30px;
      align-items: start;
    }

    .index {
      color: var(--accent);
      font-size: 11px;
      letter-spacing: 0.18em;
    }

    h2 {
      margin: 0;
      font-size: clamp(30px, 5vw, 58px);
      line-height: 0.98;
      letter-spacing: -0.05em;
      text-transform: uppercase;
    }

    .about-grid {
      margin-top: 48px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 50px;
    }

    .about-grid p {
      color: var(--muted);
      line-height: 1.9;
      font-size: 13px;
      margin: 0;
    }

    .manifest {
      display: grid;
      gap: 14px;
    }

    .manifest div {
      padding: 16px 0;
      border-bottom: 1px solid rgba(160,255,185,0.12);
      display: flex;
      justify-content: space-between;
      gap: 20px;
    }

    .manifest span:first-child { color: var(--muted); }
    .manifest span:last-child { color: var(--accent-2); text-align: right; }

    .projects {
      margin-top: 48px;
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 18px;
    }

    .card {
      padding: 24px;
      min-height: 220px;
      border: 1px solid rgba(160,255,185,0.18);
      background: rgba(7,12,9,0.5);
      backdrop-filter: blur(8px);
      transition: border-color 180ms ease, transform 180ms ease, background 180ms ease;
    }

    .card:hover {
      border-color: rgba(141,255,159,0.55);
      background: rgba(15,24,17,0.68);
      transform: translateY(-3px);
    }

    .card .tag {
      color: var(--accent);
      font-size: 10px;
      letter-spacing: 0.18em;
      text-transform: uppercase;
    }

    .card h3 {
      margin: 22px 0 12px;
      font-size: 25px;
      letter-spacing: -0.03em;
      text-transform: uppercase;
    }

    .card p {
      color: var(--muted);
      font-size: 12px;
      line-height: 1.7;
      max-width: 560px;
    }

    .skills {
      margin-top: 48px;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      border: 1px solid rgba(160,255,185,0.16);
    }

    .skill {
      min-height: 150px;
      padding: 22px;
      border-right: 1px solid rgba(160,255,185,0.16);
      border-bottom: 1px solid rgba(160,255,185,0.16);
    }

    .skill:nth-child(4n) { border-right: none; }
    .skill:nth-last-child(-n+4) { border-bottom: none; }

    .skill-num {
      color: rgba(141,255,159,0.55);
      font-size: 10px;
    }

    .skill h3 {
      margin: 30px 0 8px;
      font-size: 15px;
      text-transform: uppercase;
    }

    .skill p {
      color: var(--muted);
      font-size: 10px;
      line-height: 1.6;
    }

    .contact-box {
      margin-top: 46px;
      padding: 30px;
      border: 1px solid rgba(141,255,159,0.35);
      background: rgba(7,12,9,0.62);
    }

    .contact-box p {
      margin: 0 0 18px;
      color: var(--muted);
      line-height: 1.8;
      font-size: 12px;
    }

    .contact-mail {
      color: var(--accent-2);
      font-size: clamp(16px, 2.5vw, 28px);
      text-decoration: none;
      word-break: break-word;
    }

    footer {
      border-top: 1px solid var(--line);
      padding-top: 28px;
      display: flex;
      justify-content: space-between;
      gap: 20px;
      color: rgba(230,255,233,0.44);
      font-size: 10px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
    }

    .status {
      position: fixed;
      right: 18px;
      bottom: 16px;
      z-index: 3;
      padding: 8px 10px;
      background: rgba(4,8,5,0.72);
      border: 1px solid rgba(141,255,159,0.18);
      color: rgba(230,255,233,0.5);
      font-size: 9px;
      letter-spacing: 0.12em;
      backdrop-filter: blur(8px);
    }

    @media (max-width: 820px) {
      header { padding: 18px 22px 24px; }
      nav a { margin-left: 10px; font-size: 9px; }
      .section-head { grid-template-columns: 1fr; gap: 14px; }
      .about-grid, .projects { grid-template-columns: 1fr; }
      .skills { grid-template-columns: 1fr 1fr; }
      .skill:nth-child(4n) { border-right: 1px solid rgba(160,255,185,0.16); }
      .skill:nth-child(2n) { border-right: none; }
      .skill:nth-last-child(-n+4) { border-bottom: 1px solid rgba(160,255,185,0.16); }
      .skill:nth-last-child(-n+2) { border-bottom: none; }
      main { padding-left: 22px; padding-right: 22px; }
      section { padding: 7vh 0; }
    }

    @media (max-width: 560px) {
      nav { align-items: flex-start; }
      nav div:last-child { display: none; }
      h1 { font-size: clamp(45px, 16vw, 84px); }
      .hero-copy { font-size: 11px; }
      .controls-hint { font-size: 8px; }
      .skills { grid-template-columns: 1fr; }
      .skill, .skill:nth-child(2n), .skill:nth-child(4n),
      .skill:nth-last-child(-n+2), .skill:nth-last-child(-n+4) {
        border-right: none;
        border-bottom: 1px solid rgba(160,255,185,0.16);
      }
      .skill:last-child { border-bottom: none; }
      footer { flex-direction: column; }
    }
  </style>

  <script type="importmap">
  {
    "imports": {
      "three": "https://cdn.jsdelivr.net/npm/three@0.180.0/build/three.module.js",
      "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.180.0/examples/jsm/"
    }
  }
  </script>
</head>

<body>
  <div id="scene" aria-hidden="true"></div>
  <div class="scanlines"></div>
  <div class="vignette"></div>

  <div class="ui">
    <header>
      <nav>
        <div class="brand">TPB / 3D PORTFOLIO</div>
        <div>
          <a href="#about">About</a>
          <a href="#work">Work</a>
          <a href="#skills">Skills</a>
          <a href="#contact">Contact</a>
        </div>
      </nav>

      <div class="hero">
        <p class="eyebrow">Digital Media Designer / 3D Artist</p>
        <h1>THUNYAKORN<br />PIAMANBOONTEE</h1>
        <div class="hero-line"></div>
        <p class="hero-copy">
          Building <strong>3D worlds, characters, animation and interactive experiences</strong>
          with a focus on shape, atmosphere and visual storytelling.
        </p>
      </div>

      <div class="controls-hint">
        <span>Mouse / Touch — Rotate & Explore</span>
        <span class="scroll">↓ Scroll to enter portfolio</span>
      </div>
    </header>

    <main>
      <section id="about">
        <div class="section-head">
          <div class="index">01 / ABOUT</div>
          <h2>From pixels<br />to worlds.</h2>
        </div>

        <div class="about-grid">
          <p>
            I am a Digital Media Design student exploring 3D modeling, animation,
            environment design and real-time interactive media. My approach combines
            clean forms, expressive visuals and technical experimentation.
          </p>

          <div class="manifest">
            <div><span>Focus</span><span>3D / Animation / Interactive</span></div>
            <div><span>Style</span><span>Stylized / Cinematic / Experimental</span></div>
            <div><span>Tools</span><span>Blender / Unity / Maya</span></div>
            <div><span>Based</span><span>Thailand</span></div>
          </div>
        </div>
      </section>

      <section id="work">
        <div class="section-head">
          <div class="index">02 / SELECTED WORK</div>
          <h2>Projects<br />in motion.</h2>
        </div>

        <div class="projects">
          <article class="card">
            <div class="tag">Thesis / 3D Animation</div>
            <h3>Flowers of Memory</h3>
            <p>
              A psychological fantasy animation that uses a forgotten garden as
              a visual metaphor for pain, memory and the process of healing.
            </p>
          </article>

          <article class="card">
            <div class="tag">Real-Time / Unity</div>
            <h3>Interactive Worlds</h3>
            <p>
              Real-time environments, character interaction, particles and
              gameplay prototypes designed with atmosphere and exploration in mind.
            </p>
          </article>

          <article class="card">
            <div class="tag">Modeling / Blender</div>
            <h3>Character Lab</h3>
            <p>
              Stylized character studies focused on readable silhouettes,
              simple shapes, expressive poses and production-ready topology.
            </p>
          </article>

          <article class="card">
            <div class="tag">Environment / 3D</div>
            <h3>World Building</h3>
            <p>
              Modular assets, terrain, props and lighting studies for creating
              immersive spaces with a strong visual identity.
            </p>
          </article>
        </div>
      </section>

      <section id="skills">
        <div class="section-head">
          <div class="index">03 / SKILLS</div>
          <h2>What<br />I build.</h2>
        </div>

        <div class="skills">
          <div class="skill">
            <div class="skill-num">01</div>
            <h3>3D Modeling</h3>
            <p>Characters, props, environments, UVs and optimization.</p>
          </div>
          <div class="skill">
            <div class="skill-num">02</div>
            <h3>Animation</h3>
            <p>Keyframe animation, timing, camera work and visual storytelling.</p>
          </div>
          <div class="skill">
            <div class="skill-num">03</div>
            <h3>Blender</h3>
            <p>Modeling, rigging, materials, lighting and procedural workflows.</p>
          </div>
          <div class="skill">
            <div class="skill-num">04</div>
            <h3>Unity</h3>
            <p>Real-time scenes, gameplay prototypes, VFX and interactive media.</p>
          </div>
          <div class="skill">
            <div class="skill-num">05</div>
            <h3>Maya</h3>
            <p>Animation fundamentals, cameras, rigs and production workflows.</p>
          </div>
          <div class="skill">
            <div class="skill-num">06</div>
            <h3>Design</h3>
            <p>Composition, color, mood, atmosphere and concept direction.</p>
          </div>
          <div class="skill">
            <div class="skill-num">07</div>
            <h3>Interactive</h3>
            <p>Web 3D, AR experiments and experimental visual interfaces.</p>
          </div>
          <div class="skill">
            <div class="skill-num">08</div>
            <h3>Storytelling</h3>
            <p>Symbolism, emotion and visual narratives through 3D media.</p>
          </div>
        </div>
      </section>

      <section id="contact">
        <div class="section-head">
          <div class="index">04 / CONTACT</div>
          <h2>Let's make<br />something.</h2>
        </div>

        <div class="contact-box">
          <p>
            Replace the email below with your real portfolio contact address.
            You can also add Behance, ArtStation, LinkedIn or other portfolio links here.
          </p>
          <a class="contact-mail" href="mailto:your-email@example.com">
            your-email@example.com ↗
          </a>
        </div>
      </section>

      <footer>
        <span>© 2026 THUNYAKORN PIAMANBOONTEE</span>
        <span>3D / DIGITAL MEDIA / CREATIVE TECHNOLOGY</span>
      </footer>
    </main>
  </div>

  <div class="status">ASCII ENGINE // THREE.JS // ONLINE</div>

  <script type="module">
    import * as THREE from "three";
    import { OrbitControls } from "three/addons/controls/OrbitControls.js";
    import { AsciiEffect } from "three/addons/effects/AsciiEffect.js";

    const mount = document.getElementById("scene");

    // -----------------------------
    // Scene
    // -----------------------------
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0x030504);

    const camera = new THREE.PerspectiveCamera(
      42,
      window.innerWidth / window.innerHeight,
      0.1,
      100
    );
    camera.position.set(0, 0.15, 5.4);

    const renderer = new THREE.WebGLRenderer({
      antialias: true,
      alpha: false,
      powerPreference: "high-performance"
    });
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 1.5));
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.outputColorSpace = THREE.SRGBColorSpace;
    mount.appendChild(renderer.domElement);

    // -----------------------------
    // ASCII post effect
    // -----------------------------
    const ascii = new AsciiEffect(renderer, " .:-=+*#%@", {
      invert: true,
      resolution: 0.16
    });

    ascii.setSize(window.innerWidth, window.innerHeight);
    ascii.domElement.style.color = "#8dff9f";
    ascii.domElement.style.backgroundColor = "#030504";
    ascii.domElement.style.fontFamily = '"Courier New", monospace';
    ascii.domElement.style.fontWeight = "700";
    ascii.domElement.style.fontSize = "10px";
    ascii.domElement.style.lineHeight = "10px";
    ascii.domElement.style.textAlign = "center";
    ascii.domElement.style.whiteSpace = "pre";
    mount.replaceChildren(ascii.domElement);

    // -----------------------------
    // Lights
    // -----------------------------
    const key = new THREE.DirectionalLight(0xeaffee, 2.8);
    key.position.set(3, 4, 4);
    scene.add(key);

    const rim = new THREE.DirectionalLight(0x88ff9a, 2.0);
    rim.position.set(-4, 1, -3);
    scene.add(rim);

    const fill = new THREE.AmbientLight(0x55775c, 1.0);
    scene.add(fill);

    // -----------------------------
    // Stylized portfolio sculpture
    // -----------------------------
    const heroGroup = new THREE.Group();
    scene.add(heroGroup);

    const mat = new THREE.MeshStandardMaterial({
      color: 0xd8ffe0,
      roughness: 0.42,
      metalness: 0.18
    });

    const darkMat = new THREE.MeshStandardMaterial({
      color: 0x315b39,
      roughness: 0.55,
      metalness: 0.08
    });

    // Main floating torus-knot
    const knot = new THREE.Mesh(
      new THREE.TorusKnotGeometry(1.05, 0.28, 180, 32, 2, 3),
      mat
    );
    heroGroup.add(knot);

    // Ring orbit
    const ring = new THREE.Mesh(
      new THREE.TorusGeometry(1.8, 0.022, 12, 180),
      darkMat
    );
    ring.rotation.x = Math.PI * 0.42;
    ring.rotation.y = Math.PI * 0.13;
    heroGroup.add(ring);

    // Small satellites
    const satelliteGroup = new THREE.Group();
    heroGroup.add(satelliteGroup);

    const satelliteGeo = new THREE.IcosahedronGeometry(0.08, 1);
    for (let i = 0; i < 30; i++) {
      const a = (i / 30) * Math.PI * 2;
      const radius = 1.8 + Math.sin(i * 2.15) * 0.18;
      const y = Math.cos(i * 1.6) * 0.8;
      const s = new THREE.Mesh(satelliteGeo, i % 3 === 0 ? mat : darkMat);
      s.position.set(
        Math.cos(a) * radius,
        y,
        Math.sin(a) * radius
      );
      s.scale.setScalar(0.55 + (i % 4) * 0.18);
      satelliteGroup.add(s);
    }

    // Floor grid
    const grid = new THREE.GridHelper(14, 38, 0x294530, 0x102216);
    grid.position.y = -2.15;
    grid.rotation.y = 0.02;
    scene.add(grid);

    // Subtle vertical "data" columns
    const dataGroup = new THREE.Group();
    scene.add(dataGroup);

    for (let i = 0; i < 24; i++) {
      const h = 0.2 + ((i * 17) % 11) * 0.17;
      const bar = new THREE.Mesh(
        new THREE.BoxGeometry(0.018, h, 0.018),
        darkMat
      );
      const x = (i - 11.5) * 0.42;
      const z = -1.5 - (i % 3) * 0.25;
      bar.position.set(x, -1.9 + h / 2, z);
      dataGroup.add(bar);
    }

    // -----------------------------
    // Controls
    // -----------------------------
    const controls = new OrbitControls(camera, ascii.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.055;
    controls.enablePan = false;
    controls.minDistance = 3.8;
    controls.maxDistance = 7;
    controls.autoRotate = false;
    controls.rotateSpeed = 0.45;

    // Start with a gentle camera target.
    controls.target.set(0, 0.05, 0);

    // -----------------------------
    // Pointer parallax
    // -----------------------------
    const pointer = { x: 0, y: 0 };
    const smoothPointer = { x: 0, y: 0 };

    window.addEventListener("pointermove", (event) => {
      pointer.x = (event.clientX / window.innerWidth) * 2 - 1;
      pointer.y = (event.clientY / window.innerHeight) * 2 - 1;
    }, { passive: true });

    // -----------------------------
    // Animation
    // -----------------------------
    const clock = new THREE.Clock();

    function animate() {
      requestAnimationFrame(animate);

      const t = clock.getElapsedTime();

      smoothPointer.x += (pointer.x - smoothPointer.x) * 0.035;
      smoothPointer.y += (pointer.y - smoothPointer.y) * 0.035;

      // Organic motion
      knot.rotation.x = t * 0.18 + smoothPointer.y * 0.16;
      knot.rotation.y = t * 0.24 + smoothPointer.x * 0.22;
      knot.rotation.z = Math.sin(t * 0.37) * 0.08;

      ring.rotation.z = t * 0.12;
      ring.rotation.y = Math.sin(t * 0.22) * 0.15;

      satelliteGroup.rotation.y = -t * 0.08;
      satelliteGroup.rotation.x = Math.sin(t * 0.17) * 0.1;

      heroGroup.position.x += ((smoothPointer.x * 0.18) - heroGroup.position.x) * 0.02;
      heroGroup.position.y = Math.sin(t * 0.55) * 0.08 + (-smoothPointer.y * 0.11);
      heroGroup.rotation.y += (smoothPointer.x * 0.05 - heroGroup.rotation.y) * 0.018;

      dataGroup.position.z = Math.sin(t * 0.3) * 0.05;

      controls.update();
      ascii.render(scene, camera);
    }

    animate();

    // -----------------------------
    // Responsive
    // -----------------------------
    function resize() {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();

      renderer.setSize(window.innerWidth, window.innerHeight);
      ascii.setSize(window.innerWidth, window.innerHeight);

      const mobile = window.innerWidth < 700;
      ascii.domElement.style.fontSize = mobile ? "7px" : "10px";
      ascii.domElement.style.lineHeight = mobile ? "7px" : "10px";
    }

    window.addEventListener("resize", resize);

    // Prevent browser gestures on the 3D viewport from feeling awkward.
    ascii.domElement.style.touchAction = "none";
  </script>
</body>
</html>
