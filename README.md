<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thunyakorn Piamanboontee — ASCII 3D Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #060605;
    --tile: #0C0B08;
    --ink: #F4F0E4;
    --ink-dim: #948C7B;
    --gold: #E8B84B;
    --gold-dim: #7A6329;
    --line: #201C13;
  }
  *{ margin:0; padding:0; box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:'Inter', sans-serif;
    overflow-x:hidden;
  }
  h1,h2,h3{ font-family:'Space Grotesk', sans-serif; font-weight:600; letter-spacing:-0.01em; line-height:1.05; }
  .mono{ font-family:'JetBrains Mono', monospace; }
  a{ color:inherit; text-decoration:none; }
  ::selection{ background:var(--gold); color:#000; }

  /* ---------- nav ---------- */
  nav{
    position:fixed; top:0; left:0; right:0; z-index:70;
    display:flex; justify-content:space-between; align-items:center;
    padding:22px clamp(20px,4.5vw,56px);
    mix-blend-mode:difference;
  }
  .nav-mark{ font-family:'Space Grotesk', sans-serif; font-weight:600; font-size:15px; }
  .nav-mark span{ color:var(--gold); }
  .nav-links{ display:flex; gap:30px; }
  .nav-links a{ font-size:13px; color:var(--ink); opacity:.75; transition:opacity .25s ease; }
  .nav-links a:hover{ opacity:1; color:var(--gold); }

  /* ---------- ascii hero ---------- */
  .hero{
    position:relative;
    height:100svh;
    overflow:hidden;
    background:#000;
    border-bottom:1px solid var(--line);
  }
  #ascii-holder{
    position:absolute; inset:0;
    display:flex; align-items:center; justify-content:center;
  }
  #ascii-holder table{
    image-rendering:pixelated;
  }
  #ascii-holder td{
    font-family:'JetBrains Mono', monospace !important;
  }
  .ascii-loading{
    position:absolute; inset:0; z-index:5;
    display:flex; align-items:center; justify-content:center;
    font-family:'JetBrains Mono', monospace; font-size:12px; color:var(--gold-dim);
    letter-spacing:.08em; background:#000;
    transition:opacity .5s ease;
  }

  .hero-top{
    position:absolute; top:0; left:0; right:0; z-index:6; pointer-events:none;
    display:flex; justify-content:space-between; align-items:flex-start;
    padding:90px clamp(20px,4.5vw,56px) 0;
  }
  .hero-id{ font-size:13px; color:var(--ink-dim); }
  .hero-id b{ color:var(--gold); font-weight:600; display:block; font-size:15px; margin-top:4px; }
  .hero-tag{
    font-family:'JetBrains Mono', monospace; font-size:11px; color:var(--gold-dim);
    border:1px solid rgba(232,184,75,0.25); padding:6px 12px; border-radius:100px;
  }

  .hero-bottom{
    position:absolute; bottom:0; left:0; right:0; z-index:6; pointer-events:none;
    display:flex; justify-content:space-between; align-items:flex-end;
    padding:0 clamp(20px,4.5vw,56px) 40px;
  }
  .hero-title{
    font-size:clamp(30px, 4.4vw, 54px);
    color:var(--ink);
    max-width:9ch;
  }
  .hero-title .out{ -webkit-text-stroke:1px var(--gold); color:transparent; }
  .hero-hint{
    font-family:'JetBrains Mono', monospace; font-size:11px; color:var(--ink-dim);
    text-align:right; line-height:1.6;
  }
  .hero-hint b{ color:var(--gold); }

  /* ---------- control panel ---------- */
  .panel{
    position:absolute; right:clamp(16px,3vw,40px); top:50%; transform:translateY(-50%);
    z-index:10; width:220px;
    background:rgba(8,7,5,0.7); backdrop-filter:blur(10px);
    border:1px solid rgba(232,184,75,0.18); border-radius:12px;
    padding:18px 16px;
    display:flex; flex-direction:column; gap:14px;
    pointer-events:auto;
  }
  .panel h4{
    font-family:'JetBrains Mono', monospace; font-size:10px; letter-spacing:.1em;
    color:var(--gold); text-transform:uppercase; margin-bottom:2px;
  }
  .panel-group{ display:flex; flex-direction:column; gap:8px; }
  .panel-row{ display:flex; justify-content:space-between; align-items:center; gap:8px; }
  .panel-row label{ font-size:11px; color:var(--ink-dim); font-family:'JetBrains Mono', monospace; }
  .seg{ display:flex; gap:4px; flex-wrap:wrap; }
  .seg button{
    font-family:'JetBrains Mono', monospace; font-size:10.5px;
    background:transparent; border:1px solid rgba(244,240,228,0.15); color:var(--ink-dim);
    padding:5px 8px; border-radius:6px; cursor:pointer; transition:all .2s ease;
  }
  .seg button.active{ background:var(--gold); border-color:var(--gold); color:#0a0805; }
  .seg button:hover{ border-color:var(--gold); color:var(--ink); }
  input[type="range"]{
    -webkit-appearance:none; width:100%; height:2px; background:var(--line); border-radius:2px;
  }
  input[type="range"]::-webkit-slider-thumb{
    -webkit-appearance:none; width:11px; height:11px; border-radius:50%;
    background:var(--gold); cursor:pointer; margin-top:-4.5px;
  }
  .toggle{
    width:34px; height:19px; border-radius:100px; border:1px solid rgba(244,240,228,0.2);
    position:relative; cursor:pointer; background:transparent; flex-shrink:0;
  }
  .toggle::after{
    content:''; position:absolute; top:2px; left:2px; width:13px; height:13px; border-radius:50%;
    background:var(--ink-dim); transition:all .2s ease;
  }
  .toggle.on{ border-color:var(--gold); }
  .toggle.on::after{ background:var(--gold); left:17px; }
  .panel-div{ height:1px; background:var(--line); }

  /* ---------- sections ---------- */
  section{ padding:clamp(80px,12vh,130px) clamp(20px,4.5vw,56px); border-top:1px solid var(--line); }
  .section-label{ font-family:'JetBrains Mono', monospace; font-size:12px; color:var(--gold); margin-bottom:22px; }
  .section-head{ display:flex; justify-content:space-between; align-items:flex-end; gap:32px; flex-wrap:wrap; margin-bottom:48px; }
  .section-head h2{ font-size:clamp(26px,3.6vw,44px); max-width:16ch; }
  .section-head p{ color:var(--ink-dim); max-width:38ch; font-size:14.5px; line-height:1.6; }

  /* ---------- about ---------- */
  .about{ display:grid; grid-template-columns:1.2fr .8fr; gap:48px; }
  .about-text p{ font-size:clamp(17px,1.9vw,21px); line-height:1.55; color:var(--ink); max-width:42ch; }
  .about-text p + p{ margin-top:18px; color:var(--ink-dim); font-size:14.5px; max-width:46ch; font-weight:400; }
  .about-note{
    align-self:start;
    font-family:'JetBrains Mono', monospace; font-size:12px; color:var(--ink-dim);
    border-left:1px solid var(--gold-dim); padding-left:18px; line-height:1.8;
  }
  .about-note b{ color:var(--gold); display:block; margin-bottom:6px; font-size:13px; }

  /* ---------- work list ---------- */
  .work-list{ display:flex; flex-direction:column; }
  .work-row{
    display:grid; grid-template-columns:60px 1fr auto; align-items:center;
    gap:28px; padding:26px 0; border-top:1px solid var(--line);
    transition:background .3s ease;
  }
  .work-row:last-child{ border-bottom:1px solid var(--line); }
  .work-row:hover{ background:rgba(232,184,75,0.04); }
  .work-num{ font-family:'JetBrains Mono', monospace; font-size:12px; color:var(--gold-dim); }
  .work-info h3{ font-size:clamp(19px,2.2vw,26px); font-weight:600; }
  .work-info p{ margin-top:6px; color:var(--ink-dim); font-size:13.5px; max-width:56ch; font-weight:400; }
  .work-meta{ text-align:right; font-family:'JetBrains Mono', monospace; color:var(--ink-dim); font-size:11.5px; display:flex; flex-direction:column; gap:5px; }
  .work-meta span:first-child{ color:var(--gold); }

  /* ---------- skills ---------- */
  .process{ display:grid; grid-template-columns:.8fr 1.4fr; gap:48px; }
  .process-list{ display:flex; flex-wrap:wrap; gap:10px 24px; }
  .process-list li{ list-style:none; font-family:'Space Grotesk', sans-serif; font-weight:500; font-size:clamp(17px,2vw,24px); color:var(--ink-dim); transition:color .25s ease; }
  .process-list li:hover{ color:var(--gold); }

  /* ---------- contact ---------- */
  .contact{ display:flex; flex-direction:column; align-items:flex-start; gap:22px; }
  .contact h2{ font-size:clamp(28px,5vw,64px); max-width:16ch; }
  .contact-link{ font-size:clamp(15px,1.6vw,18px); color:var(--ink); padding-bottom:6px; border-bottom:1px solid var(--gold-dim); transition:border-color .25s ease,color .25s ease; }
  .contact-link:hover{ border-color:var(--gold); color:var(--gold); }
  .contact-socials{ display:flex; gap:20px; margin-top:4px; font-size:13px; color:var(--ink-dim); }
  .contact-socials a:hover{ color:var(--gold); }
  footer{ padding:22px clamp(20px,4.5vw,56px); display:flex; justify-content:space-between; font-family:'JetBrains Mono', monospace; font-size:11px; color:var(--ink-dim); border-top:1px solid var(--line); }

  @media (max-width:900px){
    .about, .process{ grid-template-columns:1fr; gap:28px; }
    .panel{ position:static; transform:none; width:auto; margin:16px clamp(20px,4.5vw,56px) 0; }
    .hero-bottom{ flex-direction:column; align-items:flex-start; gap:16px; }
    .hero-hint{ text-align:left; }
    .work-row{ grid-template-columns:36px 1fr; }
    .work-meta{ display:none; }
  }
</style>
</head>
<body>

<nav>
  <span class="nav-mark">Thunyakorn <span>Piamanboontee</span></span>
  <div class="nav-links">
    <a href="#work">ผลงาน</a>
    <a href="#about">เกี่ยวกับ</a>
    <a href="#contact">ติดต่อ</a>
  </div>
</nav>

<section class="hero">
  <div id="ascii-holder"></div>
  <div class="ascii-loading" id="ascii-loading">initializing ascii renderer…</div>

  <div class="hero-top">
    <div class="hero-id">Thunyakorn Piamanboontee<b>3D Product Artist</b></div>
    <div class="hero-tag mono">ASCII RENDER · LIVE</div>
  </div>

  <h1 class="hero-title" style="position:absolute; left:clamp(20px,4.5vw,56px); top:50%; transform:translateY(-50%); z-index:6; pointer-events:none;">
    PORT<span class="out">FOLIO</span>
  </h1>

  <div class="hero-bottom">
    <div class="hero-hint">ลากเมาส์เพื่อหมุนโมเดล · เลือกฟอนต์และรูปทรงได้ที่แผงด้านขวา<br>ทุกพิกเซลคือ<b>ตัวอักษร</b> ไม่ใช่รูปภาพ</div>
  </div>

  <div class="panel">
    <div class="panel-group">
      <h4>Model</h4>
      <div class="seg" id="model-seg">
        <button data-v="gem" class="active">Gem</button>
        <button data-v="knot">Knot</button>
        <button data-v="capsule">Capsule</button>
      </div>
    </div>
    <div class="panel-div"></div>
    <div class="panel-group">
      <h4>Character Set</h4>
      <div class="seg" id="chars-seg">
        <button data-v=" .:-+*=%@#" class="active">Classic</button>
        <button data-v=" .,:;+*?%#@">Dense</button>
        <button data-v=" 01">Binary</button>
      </div>
    </div>
    <div class="panel-div"></div>
    <div class="panel-group">
      <div class="panel-row"><label>Resolution</label></div>
      <input type="range" id="res-slider" min="6" max="22" value="12">
    </div>
    <div class="panel-div"></div>
    <div class="panel-group">
      <div class="panel-row"><label>Invert</label><button class="toggle" id="invert-toggle"></button></div>
      <div class="panel-row"><label>Color mode</label><button class="toggle" id="color-toggle"></button></div>
      <div class="panel-row"><label>Auto-rotate</label><button class="toggle on" id="rotate-toggle"></button></div>
    </div>
  </div>
</section>

<section class="about" id="about">
  <div class="about-text">
    <p>ผมออกแบบและขึ้นโมเดล 3 มิติให้กับผลิตภัณฑ์ ตั้งแต่งานเรนเดอร์ทั่วไปไปจนถึงการทดลองนำเสนอรูปทรง 3 มิติผ่านตัวอักษรแบบเรียลไทม์บนเว็บ</p>
    <p>ทำงานด้วย Blender เป็นหลักในขั้นตอนขึ้นรูปและจัดแสง ก่อนนำไปพัฒนาต่อด้วย Three.js ให้กลายเป็นชิ้นงานที่โต้ตอบกับผู้ชมได้จริง เช่นเอฟเฟกต์ ASCII ด้านบนที่แปลงพิกเซลของโมเดลให้เป็นตัวอักษรสดในเบราว์เซอร์</p>
  </div>
  <div class="about-note mono">
    <b>Technique note</b>
    โมเดลถูกเรนเดอร์ปกติในฉาก 3 มิติ จากนั้นแปลงค่าความสว่างของแต่ละพิกเซลเป็นตัวอักษรตามชุดที่เลือกไว้ — ยิ่งพื้นที่สว่างมาก อักขระจะยิ่งหนาแน่น ให้ความรู้สึกแบบเทอร์มินัลย้อนยุคแต่ยังคงมิติของโมเดลจริงไว้ครบ
  </div>
</section>

<section id="work">
  <div class="section-head">
    <h2>ผลิตภัณฑ์ 3 มิติที่ผ่านมา</h2>
    <p>ผลงานสร้างวัตถุและผลิตภัณฑ์ 3 มิติ คัดเลือกจากงานสตูดิโอและงานทดลองส่วนตัว</p>
  </div>
  <div class="work-list">
    <div class="work-row">
      <span class="work-num mono">01</span>
      <div class="work-info"><h3>ASCII Product Viewer</h3><p>ตัวเรนเดอร์ผลิตภัณฑ์แบบ ASCII แบบเรียลไทม์ ใช้สำรวจฟอร์มโดยไม่ต้องพึ่งพื้นผิวจริง</p></div>
      <div class="work-meta"><span>Experiment</span><span>2026</span></div>
    </div>
    <div class="work-row">
      <span class="work-num mono">02</span>
      <div class="work-info"><h3>อัญมณีหรู</h3><p>ศึกษาการหักเหของแสงบนฟอร์มเหลี่ยม สำหรับพรีเซนต์แนวคิดเครื่องประดับ</p></div>
      <div class="work-meta"><span>Product Study</span><span>2025</span></div>
    </div>
    <div class="work-row">
      <span class="work-num mono">03</span>
      <div class="work-info"><h3>ขวดน้ำหอม</h3><p>ทดลองพื้นผิวกระจกและแสงสะท้อนสำหรับพรีเซนต์บรรจุภัณฑ์</p></div>
      <div class="work-meta"><span>Packaging</span><span>2025</span></div>
    </div>
    <div class="work-row">
      <span class="work-num mono">04</span>
      <div class="work-info"><h3>ยานสำรวจ</h3><p>ออกแบบฟอร์มยานขนาดเล็กสำหรับงานภาพประกอบแนวไซไฟ</p></div>
      <div class="work-meta"><span>Sci-fi</span><span>2024</span></div>
    </div>
  </div>
</section>

<section class="process">
  <div class="section-head" style="margin-bottom:0;">
    <h2>เครื่องมือที่ใช้</h2>
    <p>ซอฟต์แวร์และเทคนิคที่ใช้ประจำในงานผลิตภัณฑ์ 3 มิติ</p>
  </div>
  <ul class="process-list">
    <li>Blender</li><li>Three.js</li><li>WebGL</li><li>Substance Painter</li><li>Cinema 4D</li><li>Figma</li>
  </ul>
</section>

<section class="contact" id="contact">
  <div class="section-label mono">ติดต่องาน</div>
  <h2>สนใจงานออกแบบผลิตภัณฑ์ 3 มิติ ทักมาคุยกันได้เลย</h2>
  <a class="contact-link" href="mailto:hello@thunyakorn.studio">hello@thunyakorn.studio</a>
  <div class="contact-socials">
    <a href="#">Instagram</a>
    <a href="#">Behance</a>
    <a href="#">ArtStation</a>
  </div>
</section>

<footer>
  <span>© 2026 Thunyakorn Piamanboontee</span>
  <span>Three.js · AsciiEffect</span>
</footer>

<script type="importmap">
{
  "imports": {
    "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
    "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
  }
}
</script>
<script type="module">
import * as THREE from 'three';
import { AsciiEffect } from 'three/addons/effects/AsciiEffect.js';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

const GOLD = 0xE8B84B;

const holder = document.getElementById('ascii-holder');
const loadingEl = document.getElementById('ascii-loading');

let width = holder.clientWidth, height = holder.clientHeight;

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(42, width/height, 0.1, 100);
camera.position.set(0, 1, 8);

const renderer = new THREE.WebGLRenderer({ alpha:true });
renderer.setSize(width, height);

const ambient = new THREE.AmbientLight(0xffffff, 0.35);
const key = new THREE.PointLight(0xffffff, 22, 40);
key.position.set(5, 5, 6);
const rim = new THREE.PointLight(0xffffff, 8, 40);
rim.position.set(-6, -3, -4);
scene.add(ambient, key, rim);

/* ---------- models ---------- */
const mat = new THREE.MeshStandardMaterial({ color:0xffffff, metalness:0.25, roughness:0.35, flatShading:true });

function buildGem(){
  const g = new THREE.Group();
  g.add(new THREE.Mesh(new THREE.IcosahedronGeometry(2.3, 1), mat));
  return g;
}
function buildKnot(){
  const g = new THREE.Group();
  g.add(new THREE.Mesh(new THREE.TorusKnotGeometry(1.5, 0.45, 140, 12), mat));
  return g;
}
function buildCapsule(){
  const g = new THREE.Group();
  const body = new THREE.Mesh(new THREE.CylinderGeometry(1.0,1.0,2.6,10), mat);
  body.rotation.z = Math.PI/2;
  const nose = new THREE.Mesh(new THREE.ConeGeometry(1.0,1.3,10), mat);
  nose.position.x = 1.95; nose.rotation.z = -Math.PI/2;
  const tail = new THREE.Mesh(new THREE.ConeGeometry(1.0,1.0,10), mat);
  tail.position.x = -1.8; tail.rotation.z = Math.PI/2;
  g.add(body, nose, tail);
  return g;
}

const models = { gem: buildGem, knot: buildKnot, capsule: buildCapsule };
let current = new THREE.Group();
scene.add(current);

function setModel(name){
  scene.remove(current);
  current = models[name]();
  scene.add(current);
}
setModel('gem');

/* ---------- ascii effect ---------- */
let charSet = ' .:-+*=%@#';
let effect = new AsciiEffect(renderer, charSet, { invert:false, resolution:0.14, color:false });
effect.setSize(width, height);
effect.domElement.style.color = '#E8B84B';
effect.domElement.style.backgroundColor = 'transparent';
effect.domElement.style.letterSpacing = '-1px';
holder.appendChild(effect.domElement);

const controls = new OrbitControls(camera, effect.domElement);
controls.enablePan = false;
controls.enableZoom = false;
controls.autoRotate = true;
controls.autoRotateSpeed = 2.2;
controls.enableDamping = true;
controls.dampingFactor = 0.06;

function rebuildEffect(){
  const invert = document.getElementById('invert-toggle').classList.contains('on');
  const color = document.getElementById('color-toggle').classList.contains('on');
  const resSlider = document.getElementById('res-slider');
  const resolution = Number(resSlider.value) / 100;

  holder.removeChild(effect.domElement);
  effect = new AsciiEffect(renderer, charSet, { invert, resolution, color });
  effect.setSize(width, height);
  effect.domElement.style.backgroundColor = 'transparent';
  effect.domElement.style.letterSpacing = '-1px';
  effect.domElement.style.color = color ? '' : '#E8B84B';
  holder.appendChild(effect.domElement);
  controls.domElement = effect.domElement;
}

function resize(){
  width = holder.clientWidth; height = holder.clientHeight;
  camera.aspect = width/height;
  camera.updateProjectionMatrix();
  renderer.setSize(width, height);
  effect.setSize(width, height);
}
window.addEventListener('resize', resize);

function animate(t){
  controls.update();
  effect.render(scene, camera);
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);

setTimeout(()=>{ loadingEl.style.opacity = '0'; setTimeout(()=> loadingEl.remove(), 500); }, 350);

/* ---------- panel wiring ---------- */
document.getElementById('model-seg').addEventListener('click', (e)=>{
  const btn = e.target.closest('button'); if(!btn) return;
  document.querySelectorAll('#model-seg button').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  setModel(btn.dataset.v);
});

document.getElementById('chars-seg').addEventListener('click', (e)=>{
  const btn = e.target.closest('button'); if(!btn) return;
  document.querySelectorAll('#chars-seg button').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  charSet = btn.dataset.v;
  rebuildEffect();
});

document.getElementById('res-slider').addEventListener('input', rebuildEffect);

['invert-toggle','color-toggle'].forEach(id=>{
  document.getElementById(id).addEventListener('click', (e)=>{
    e.target.classList.toggle('on');
    rebuildEffect();
  });
});

document.getElementById('rotate-toggle').addEventListener('click', (e)=>{
  e.target.classList.toggle('on');
  controls.autoRotate = e.target.classList.contains('on');
});
</script>

</body>
</html>
