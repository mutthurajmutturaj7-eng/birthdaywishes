<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday PAPANI</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {
    margin: 0;
    overflow: hidden;
    background: linear-gradient(135deg, #ff77b4, #ffb7d5);
    font-family: "Poppins", sans-serif;
    color: #ffeccd;
}

/* Typewriter Message */
#message {
    position: absolute;
    top: 55%;
    width: 100%;
    text-align: center;
    font-size: 1.8rem;
    font-weight: bold;
    text-shadow: 0 0 10px #fff6d9, 0 0 25px #ffdf8c;
    opacity: 0;
    transition: opacity 1s ease-in-out;
}

/* Floating Hearts Background */
.heart {
    position: fixed;
    bottom: -10vh;
    font-size: 18px;
    color: rgba(255,255,255,0.8);
    animation: floatUp 6s linear infinite;
}
@keyframes floatUp {
    from { transform: translateY(0); opacity: 1; }
    to { transform: translateY(-120vh); opacity: 0; }
}

/* Heart Burst on Tap */
.burst {
    position: fixed;
    font-size: 28px;
    animation: burstAnim 0.8s ease-out forwards;
}
@keyframes burstAnim {
    from { transform: scale(0.2); opacity: 1; }
    to { transform: scale(2.2); opacity: 0; }
}

canvas {
    position: absolute;
    top: 0; left: 0;
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>

<div id="message"></div>

<audio id="bgm" autoplay loop>
    <source src="https://files.catbox.moe/7j9nfm.mp3" type="audio/mpeg">
</audio>

<script>
/* Floating Hearts Generator */
function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.animationDuration = 4 + Math.random() * 4 + "s";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 8000);
}
setInterval(createHeart, 400);

/* Heart Burst on Tap */
document.addEventListener("click", (e) => {
    const burst = document.createElement("div");
    burst.className = "burst";
    burst.innerHTML = "💖";
    burst.style.left = e.pageX + "px";
    burst.style.top = e.pageY + "px";
    document.body.appendChild(burst);
    setTimeout(() => burst.remove(), 800);
});

/* Typewriter Reveal */
const msg = "SORRY FOR EVERYTHING. I LOVE YOU WIFE ❤️I MISS YOU EVERY UNIVERS❤️\nHAPPY BIRTHDAY PAPANI 💫";
const messageDiv = document.getElementById("message");

function typeWriter(text, i = 0) {
    if (i === 0) messageDiv.innerHTML = "";
    if (i < text.length) {
        messageDiv.innerHTML += text.charAt(i);
        setTimeout(() => typeWriter(text, i + 1), 80);
    }
}

setTimeout(() => {
    messageDiv.style.opacity = 1;
    typeWriter(msg);
}, 3500);

/* Fireworks Canvas */
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");
resizeCanvas();

window.addEventListener("resize", resizeCanvas);

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}

let fireworks = [];

function createFirework() {
    const x = Math.random() * canvas.width;
    const y = Math.random() * canvas.height * 0.6;
    const count = 40;
    for (let i = 0; i < count; i++) {
        fireworks.push({
            x, y,
            angle: (Math.PI * 2 * i) / count,
            radius: 0,
            maxRadius: 60 + Math.random() * 50,
            alpha: 1
        });
    }
}
setInterval(createFirework, 500);

function animateFireworks() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    fireworks.forEach((fw, i) => {
        fw.radius += 2;
        fw.alpha -= 0.015;
        const fx = fw.x + Math.cos(fw.angle) * fw.radius;
        const fy = fw.y + Math.sin(fw.angle) * fw.radius;
        ctx.fillStyle = `rgba(255,255,255,${fw.alpha})`;
        ctx.beginPath();
        ctx.arc(fx, fy, 3, 0, Math.PI * 2);
        ctx.fill();
        if (fw.alpha <= 0) fireworks.splice(i, 1);
    });
    requestAnimationFrame(animateFireworks);
}
animateFireworks();
</script>

</body>
</html>




