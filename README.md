<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday PAPANI</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body {
    margin: 0;
    overflow: hidden;
    font-family: 'Poppins', sans-serif;
    background: radial-gradient(circle, #ffb6d9, #ff4f75, #b40039);
}

/* Fireworks Canvas */
#fireworksCanvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 10;
}

/* Main Content (hidden at start) */
#content {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    opacity: 0;
    transition: opacity 2s ease-in-out;
    z-index: 5;
}

/* Name Animation */
.name {
    font-size: 55px;
    font-weight: 700;
    color: #ffd700;
    text-shadow: 0 0 15px #ff2e77, 0 0 30px #ff0055;
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from { text-shadow: 0 0 10px #ff7eb3, 0 0 20px #ff004c; }
    to { text-shadow: 0 0 25px #ffb3d9, 0 0 45px #ff006a; }
}

/* Message */
.message {
    margin-top: 20px;
    font-size: 26px;
    color: white;
    text-shadow: 0 0 10px #ff9ac8;
    animation: pulse 2s infinite ease-in-out;
}

@keyframes pulse {
    0% { transform: scale(1); opacity: 0.9; }
    100% { transform: scale(1.05); opacity: 1; }
}

/* Floating Sparkles */
.sparkle {
    position: fixed;
    width: 10px;
    height: 10px;
    background: radial-gradient(circle, #ffd1f0, #ff006a);
    border-radius: 50%;
    animation: floatUp 6s linear infinite;
    opacity: 0.8;
}

@keyframes floatUp {
    from { transform: translateY(100vh) scale(0.5); }
    to { transform: translateY(-10vh) scale(1.3); }
}
</style>
</head>

<body>

<canvas id="fireworksCanvas"></canvas>

<div id="content">
    <div class="name">PAPANI</div>
    <div class="message">SORRU FPR EVERYTHING. I LOVE YOU WIFE</div>
</div>

<audio id="bgMusic" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_7e2c508d25.mp3?filename=romantic-piano-ambient-110397.mp3" type="audio/mpeg">
</audio>

<script>
// ===== FIREWORKS EFFECT =====
const canvas = document.getElementById("fireworksCanvas");
const ctx = canvas.getContext("2d");
canvas.width = innerWidth;
canvas.height = innerHeight;

let fireworks = [];
function random(min, max){ return Math.random() * (max - min) + min; }

class Firework {
    constructor(){
        this.x = random(0, canvas.width);
        this.y = canvas.height;
        this.targetY = random(canvas.height/4, canvas.height/2);
        this.size = 2;
        this.speed = random(2, 4);
        this.hue = random(0, 360);
        this.exploded = false;
    }
    update(){
        this.y -= this.speed;
        if(this.y <= this.targetY){ this.exploded = true; this.explode(); }
    }
    explode(){
        for(let i=0; i<40; i++){
            particles.push(new Particle(this.x, this.y, this.hue));
        }
    }
    draw(){
        ctx.fillStyle = `hsl(${this.hue}, 100%, 60%)`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
        ctx.fill();
    }
}

let particles = [];
class Particle {
    constructor(x,y,hue){
        this.x = x;
        this.y = y;
        this.angle = random(0, Math.PI*2);
        this.speed = random(1, 5);
        this.size = 2;
        this.alpha = 1;
        this.decay = random(0.01, 0.02);
        this.hue = hue;
    }
    update(){
        this.x += Math.cos(this.angle)*this.speed;
        this.y += Math.sin(this.angle)*this.speed;
        this.alpha -= this.decay;
    }
    draw(){
        ctx.fillStyle = `hsla(${this.hue}, 100%, 60%, ${this.alpha})`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI*2);
        ctx.fill();
    }
}

function animate(){
    requestAnimationFrame(animate);
    ctx.fillStyle = "rgba(0,0,0,0.2)";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    if(Math.random() < 0.06){
        fireworks.push(new Firework());
    }

    fireworks.forEach((fw,i)=>{ fw.update(); fw.draw(); if(fw.exploded) fireworks.splice(i,1); });
    particles.forEach((p,i)=>{ p.update(); p.draw(); if(p.alpha<=0) particles.splice(i,1); });
}
animate();

// AFTER 6 SECONDS SHOW CONTENT
setTimeout(()=>{
    document.getElementById("content").style.opacity = 1;
}, 6000);

// ===== FLOATING SPARKLES =====
for(let i=0; i<35; i++){
    let s = document.createElement("div");
    s.classList.add("sparkle");
    s.style.left = Math.random()*100+"vw";
    s.style.animationDelay = Math.random()*5+"s";
    document.body.appendChild(s);
}

// ===== MUSIC AUTO START =====
const music = document.getElementById("bgMusic");
document.body.addEventListener("click", ()=>{ music.play(); }, { once: true });
</script>

</body>
</html>





