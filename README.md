<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>Happy Birthday PAPANI</title>
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"/>
<style>
  /* ---------- Base ---------- */
  :root{
    --pink:#ff98c8;
    --deep-pink:#ff3b6b;
    --gold:#ffd166;
    --bg1:#ffd0e8;
    --bg2:#ff6b99;
  }
  html,body{height:100%; margin:0; padding:0; -webkit-tap-highlight-color: transparent; font-family: 'Poppins', sans-serif;}
  body{
    overflow:hidden;
    background: linear-gradient(180deg, var(--bg1) 0%, var(--bg2) 60%, #b40039 100%);
    display:flex;
    align-items:center;
    justify-content:center;
  }

  /* ---------- FIREWORKS CANVAS ---------- */
  #fireworksCanvas{
    position:fixed;
    inset:0;
    z-index:10;
    touch-action:none;
  }

  /* ---------- CONTENT (hidden during fireworks) ---------- */
  #content{
    position:relative;
    z-index:20;
    text-align:center;
    pointer-events:none; /* let taps fall through for heart burst */
    opacity:0;
    transition:opacity 1s ease;
    width:100%;
    padding: 20px;
    box-sizing:border-box;
  }
  .name{
    font-size: clamp(36px, 10vw, 72px);
    font-weight:800;
    color:var(--gold);
    letter-spacing:4px;
    text-shadow: 0 6px 30px rgba(255,30,110,0.25), 0 0 8px rgba(255,0,85,0.15);
    animation: nameGlow 2s infinite alternate;
    margin:0;
  }
  @keyframes nameGlow{
    from { text-shadow: 0 6px 20px rgba(255,50,120,0.25), 0 0 6px rgba(255,0,80,0.12); transform:translateY(0); }
    to { text-shadow: 0 12px 40px rgba(255,90,150,0.35), 0 0 20px rgba(255,0,80,0.2); transform:translateY(-4px); }
  }

  .wish {
    margin-top:12px;
    font-size: clamp(16px, 4.5vw, 26px);
    color:#fff;
    text-shadow: 0 2px 12px rgba(255,120,180,0.28);
    min-height: 1.2em; /* keeps space while typewriter runs */
  }

  /* ---------- TYPEWRITER CURSOR ---------- */
  .cursor{
    display:inline-block;
    width:8px;
    height:1.0em;
    background: linear-gradient(180deg, var(--deep-pink), var(--pink));
    margin-left:6px;
    vertical-align:middle;
    animation: blink 1s step-start infinite;
    border-radius:2px;
  }
  @keyframes blink{ 50% {opacity:0} }

  /* ---------- FLOATING HEARTS (background) ---------- */
  .floating-heart{
    position:fixed;
    width:18px;
    height:18px;
    pointer-events:none;
    transform:translate(-50%,-50%) rotate(0deg);
    will-change: transform, opacity;
    z-index:5;
    opacity:0.9;
    filter: drop-shadow(0 6px 18px rgba(180,0,50,0.25));
  }
  .heart-shape{
    width:100%;
    height:100%;
    display:inline-block;
    transform:scale(1);
  }
  @keyframes floatUp{
    0% { transform: translateY(0) scale(0.7) rotate(-10deg); opacity:0; }
    10% { opacity:1; }
    100% { transform: translateY(-140vh) scale(1.3) rotate(30deg); opacity:0; }
  }

  /* ---------- HEART BURST (tap) ---------- */
  .tap-heart{
    position:fixed;
    font-size:18px;
    pointer-events:none;
    z-index:50;
    will-change: transform, opacity;
    user-select:none;
    transform-origin:center;
    animation: burst 900ms cubic-bezier(.2,.8,.2,1);
  }
  @keyframes burst {
    0% { transform: translate(-50%,-50%) scale(0.6) rotate(0deg); opacity:1; }
    60% { transform: translate(-50%,-50%) scale(1.8) rotate(15deg); opacity:1; }
    100% { transform: translate(-50%,-50%) scale(2.4) rotate(40deg); opacity:0; }
  }

  /* ---------- RESPONSIVE TWEAKS FOR PHONES ---------- */
  @media (max-width:420px){
    body{background-position:center top;}
  }

  /* ---------- START BUTTON (mobile music permission) ---------- */
  #startOverlay{
    position:fixed;
    inset:0;
    z-index:60;
    display:flex;
    align-items:center;
    justify-content:center;
    background: linear-gradient(180deg, rgba(20,10,12,0.15), rgba(0,0,0,0.25));
  }
  .start-btn{
    background: linear-gradient(90deg,var(--pink),var(--deep-pink));
    border: none;
    color:white;
    padding:14px 22px;
    font-size:18px;
    border-radius:12px;
    box-shadow: 0 8px 30px rgba(255,40,110,0.18);
    cursor:pointer;
  }
  .start-hint{ color:#fff; margin-top:12px; font-size:14px; text-align:center; opacity:0.95; }
</style>
</head>
<body>

<canvas id="fireworksCanvas"></canvas>

<!-- Floating hearts will be appended to body by JS -->

<!-- Main content (revealed after fireworks) -->
<div id="content" aria-hidden="true">
  <h1 class="name">PAPANI</h1>
  <div class="wish" id="wishText"></div>
</div>

<!-- Start overlay (required to allow autoplay on mobile when user taps) -->
<div id="startOverlay">
  <div style="text-align:center;">
    <button class="start-btn" id="startBtn">Tap to Open Surprise</button>
    <div class="start-hint">Tap once to start music & fireworks (required on phones)</div>
  </div>
</div>

<!-- background music (looped) -->
<audio id="bgMusic" loop preload="auto">
  <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_7e2c508d25.mp3?filename=romantic-piano-ambient-110397.mp3" type="audio/mpeg">
</audio>

<script>
/* ================ UTILS ================ */
const $ = (s)=>document.querySelector(s);

/* ================ CANVAS SETUP ================ */
const canvas = document.getElementById('fireworksCanvas');
const ctx = canvas.getContext('2d');
function resizeCanvas(){
  const DPR = window.devicePixelRatio || 1;
  canvas.width = Math.floor(window.innerWidth * DPR);
  canvas.height = Math.floor(window.innerHeight * DPR);
  canvas.style.width = window.innerWidth + 'px';
  canvas.style.height = window.innerHeight + 'px';
  ctx.setTransform(DPR,0,0,DPR,0,0);
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

/* ================ FIREWORKS (keeps running) ================ */
let fireworks = [], particles = [];
function rand(min,max){ return Math.random()*(max-min)+min; }

class Firework {
  constructor(){
    this.x = rand(50, window.innerWidth-50);
    this.y = window.innerHeight + 10;
    this.targetY = rand(window.innerHeight*0.18, window.innerHeight*0.45);
    this.speedY = rand(3.4, 5);
    this.hue = rand(320, 10) > 360 ? rand(0,40) : rand(300,360); // pink/red hues
    this.exploded=false;
  }
  update(){
    this.y -= this.speedY;
    if(this.y <= this.targetY && !this.exploded){
      this.exploded = true;
      this.explode();
    }
  }
  explode(){
    const count = 40;
    for(let i=0;i<count;i++){
      particles.push(new Particle(this.x, this.y, this.hue));
    }
    // small shimmer at origin
    for(let i=0;i<6;i++){
      particles.push(new Particle(this.x, this.y, this.hue, true));
    }
  }
  draw(){
    ctx.beginPath();
    ctx.fillStyle = `hsl(${this.hue}, 95%, 60%)`;
    ctx.arc(this.x, this.y, 3.5,0,Math.PI*2);
    ctx.fill();
  }
}

class Particle {
  constructor(x,y,hue, small=false){
    this.x = x; this.y = y; this.hue = hue;
    this.speed = rand(1.2,4.2) * (small?0.6:1);
    this.angle = rand(0, Math.PI*2);
    this.size = small?1.2:rand(1.6,3.6);
    this.alpha = 1;
    this.decay = rand(0.008, 0.018);
    this.gravity = 0.02;
  }
  update(){
    this.x += Math.cos(this.angle) * this.speed;
    this.y += Math.sin(this.angle) * this.speed + this.gravity;
    this.alpha -= this.decay;
  }
  draw(){
    ctx.beginPath();
    ctx.fillStyle = `hsla(${this.hue}, 90%, 60%, ${this.alpha})`;
    ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
    ctx.fill();
  }
}

function animate(){
  requestAnimationFrame(animate);
  // subtle darkening to create trails
  ctx.fillStyle = 'rgba(0,0,0,0.18)';
  ctx.fillRect(0,0,canvas.width,canvas.height);

  // spawn fireworks randomly (but after initial start produce more)
  if(Math.random() < 0.06) fireworks.push(new Firework());

  // update/draw fireworks
  for(let i = fireworks.length - 1; i >= 0; i--){
    fireworks[i].update();
    fireworks[i].draw();
    if(fireworks[i].exploded) fireworks.splice(i,1);
  }

  // update/draw particles
  for(let i = particles.length - 1; i >= 0; i--){
    particles[i].update();
    particles[i].draw();
    if(particles[i].alpha <= 0) particles.splice(i,1);
  }
}
animate();

/* ================ FLOATING HEARTS BACKGROUND ================ */
function createFloatingHeart(leftPct, delay, sizePx){
  const el = document.createElement('div');
  el.className = 'floating-heart';
  el.style.left = leftPct + 'vw';
  el.style.top = (100 + (Math.random()*10)) + 'vh';
  el.style.opacity = (0.6 + Math.random()*0.4);
  el.style.width = sizePx + 'px';
  el.style.height = sizePx + 'px';
  el.style.animation = `floatUp ${8 + Math.random()*6}s linear ${delay}s infinite`;
  el.innerHTML = `
    <svg class="heart-shape" viewBox="0 0 32 29" xmlns="http://www.w3.org/2000/svg">
      <path d="M23.6 0c-2.9 0-4.9 1.8-5.6 3.2-.7-1.4-2.7-3.2-5.6-3.2C6 0 0 5.6 0 12.2 0 22.1 15.2 29 16 29c.8 0 16-6.9 16-16.8C32 5.6 26 0 23.6 0z" fill="url(#g)"/>
      <defs>
        <linearGradient id="g" x1="0" x2="1" y1="0" y2="1">
          <stop offset="0" stop-color="var(--pink)"/>
          <stop offset="1" stop-color="var(--deep-pink)"/>
        </linearGradient>
      </defs>
    </svg>`;
  document.body.appendChild(el);
}
for(let i=0;i<24;i++){
  createFloatingHeart(i*4 + Math.random()*4, Math.random()*5, 12 + Math.random()*16);
}

/* ================ TYPEWRITER MESSAGE (runs after initial fireworks burst) ================ */
const messageText = 'SORRU FPR EVERYTHING. I LOVE YOU WIFE';
const wishEl = document.getElementById('wishText');

function typewriter(text, speed=70, cb){
  let i=0;
  wishEl.innerHTML = '';
  const cursor = document.createElement('span');
  cursor.className = 'cursor';
  wishEl.appendChild(cursor);

  const t = setInterval(()=>{
    if(i < text.length){
      cursor.insertAdjacentText('beforebegin', text[i]);
      i++;
    } else {
      clearInterval(t);
      // keep cursor for a short while then remove
      setTimeout(()=>{ cursor.remove(); if(cb) cb(); }, 900);
    }
  }, speed);
}

/* reveal content after 6 seconds (fireworks intro duration) */
function revealContent(){
  const content = document.getElementById('content');
  content.style.opacity = '1';
  content.setAttribute('aria-hidden','false');
  // start typewriter after small pause for effect
  setTimeout(()=> typewriter(messageText, 65), 700);
}

/* ================ HEART BURST ON TAP/CLICK ================ */
function spawnTapBurst(x, y, count = 12){
  for(let i=0;i<count;i++){
    const el = document.createElement('div');
    el.className = 'tap-heart';
    const hueShift = Math.floor(rand(-10,10));
    el.style.left = x + 'px';
    el.style.top = y + 'px';
    el.style.color = `hsl(${340 + hueShift}, 90%, 60%)`;
    el.style.fontSize = `${12 + Math.random()*18}px`;
    el.innerText = '❤';
    document.body.appendChild(el);
    // remove after animation
    setTimeout(()=> el.remove(), 950);
  }
}

/* Allow both click and touch. Clicking also plays a little chord via particles. */
function pointerHandler(ev){
  const x = ev.clientX || (ev.touches && ev.touches[0].clientX) || window.innerWidth/2;
  const y = ev.clientY || (ev.touches && ev.touches[0].clientY) || window.innerHeight/2;
  spawnTapBurst(x,y, 10 + Math.round(Math.random()*10));
}

/* Listen for taps/clicks anywhere on screen (but not on start button) */
window.addEventListener('click', pointerHandler);
window.addEventListener('touchstart', pointerHandler, {passive:true});

/* ================ START BUTTON (for mobile to allow audio + initial reveal) ================ */
const startOverlay = document.getElementById('startOverlay');
const startBtn = document.getElementById('startBtn');
const music = document.getElementById('bgMusic');

startBtn.addEventListener('click', ()=>{
  // play music (will be allowed because of user gesture)
  music.currentTime = 0;
  music.volume = 0.7;
  music.play().catch(()=>{ /* ignore autoplay errors */ });

  // do an initial big clustered firework burst for dramatic intro
  for(let i=0;i<6;i++){
    setTimeout(()=>{ fireworks.push(new Firework()); }, i*220);
  }

  // show content after a short fireworks intro
  setTimeout(revealContent, 6200);

  // fade out overlay
  startOverlay.style.transition = 'opacity 600ms ease';
  startOverlay.style.opacity = 0;
  setTimeout(()=> startOverlay.remove(), 700);
});

/* Also allow keyboard/mouse for desktop (just show content & start music) */
document.addEventListener('keydown', (e)=>{
  if(startOverlay.parentNode && (e.key === 'Enter' || e.key === ' ')){
    startBtn.click();
  }
});

/* If user opens on desktop and doesn't press start, we still reveal after 1.3s for instant preview */
if(!/Mobi|Android/i.test(navigator.userAgent)){
  setTimeout(()=> {
    // small intro fireworks
    for(let i=0;i<4;i++) fireworks.push(new Firework());
    setTimeout(revealContent, 1800);
    // remove start overlay immediately
    startOverlay.remove();
  }, 800);
}

</script>
</body>
</html>



