<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday PAPANI</title>
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body {
    overflow: hidden;
    background: linear-gradient(135deg, #ff79c9, #ffb6e6);
    font-family: "Poppins", sans-serif;
}

/* Fireworks Canvas Behind */
canvas {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
}

/* Typewriter Message */
#message {
    position: fixed;
    top: 55vh;
    left: 50%;
    transform: translateX(-50%);
    width: 90vw;
    text-align: center;
    font-size: 5vw;
    font-weight: 700;
    color: #fff5d9;
    text-shadow: 0 0 8px #fff, 0 0 20px #ffd98c;
    opacity: 0;
    z-index: 3;
    line-height: 1.4;
}

/* Floating Hearts */
.heart {
    position: fixed;
    bottom: -5vh;
    font-size: 4vw;
    color: rgba(255,255,255,0.85);
    animation: floatUp 7s linear;
    z-index: 2;
}
@keyframes floatUp {
    from { transform: translateY(0); opacity: 1; }
    to { transform: translateY(-120vh); opacity: 0; }
}

/* Tap Burst */
.burst {
    position: fixed;
    font-size: 7vw;
    animation: burstAnim 0.7s ease-out forwards;
    z-index: 4;
}
@keyframes burstAnim {
    from { transform: scale(0.3); opacity: 1; }
    to { transform: scale(2); opacity: 0; }
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>
<div id="message"></div>

<audio id="bgm" loop>
    <source src="https://files.catbox.moe/7j9nfm.mp3" type="audio/mpeg">
</audio>

<script>
/* Mobile-Friendly Autoplay */
document.addEventListener("touchstart", () => {
    const bgm = document.getElementById("bgm");
    if (bgm.paused) bgm.play();
}, { once: true });

/* Floating Hearts */
function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.animationDuration = 5 + Math.random() * 3 + "s";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 8000);
}
setInterval(createHeart, 600);

/* Tap Burst */
function triggerBurst(x, y) {
    const burst = document.createElement("div");
    burst.className = "burst";
    burst.innerHTML = "💖";
    burst.style.left = x + "px";
    burst.style.top = y + "px";
    document.body.appendChild(burst);
    setTimeout(() => burst.remove(), 800);
}

document.addEventListener("click", e => triggerBurst(e.pageX, e.pageY));
document.addEventListener("touchstart", e => {
    const t = e.touches[0];
    triggerBurst(t.pageX, t.pageY);
});

/* Typewriter */
const text = "SORRY FOR EVERYTHING. I LOVE YOU WIFE ❤️\nHAPPY BIRTHDAY PAPANI 💫";
const msgBox = document.getElementById("message");

function typeWriter(i = 0) {
    if (i === 0) msgBox.innerHTML = "";
    if (i < text.length) {
        msgBox.innerHTML += text.charAt(i);
        setTimeout(() => typeWriter(i + 1), 70);
    }
}

setTimeout(() => {
    msgBox.style.opacity = 1;
    typeWriter();
}, 2800);

/* Fireworks (lighter for phones) */
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");

function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resize();
window.addEventListener("resize", resize);

let fireworks = [];

function createFirework() {
    const x = Math.random() * canvas.width;
    const y = Math.random() * canvas.height * 0.5;
    const count = 28;
    for (let i = 0; i < count; i++) {
        fireworks.push({
            x, y,
            angle: (Math.PI * 2 * i) / count,
            radius: 0,
            maxRadius: 45 + Math.random() * 35,
            alpha: 1
        });
    }
}
setInterval(createFirework, 550);

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    fireworks.forEach((fw, index) => {
        fw.radius += 1.8;
        fw.alpha -= 0.018;
        const fx = fw.x + Math.cos(fw.angle) * fw.radius;
        const fy = fw.y + Math.sin(fw.angle) * fw.radius;
        ctx.fillStyle = `rgba(255,255,255,${fw.alpha})`;
        ctx.beginPath();
        ctx.arc(fx, fy, 2.5, 0, Math.PI * 2);
        ctx.fill();
        if (fw.alpha <= 0) fireworks.splice(index, 1);
    });
    requestAnimationFrame(animate);
}
animate();
</script>

</body>
</html>




