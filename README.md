<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday PAPANI</title>
<style>
body {
  margin: 0;
  overflow: hidden;
  background: linear-gradient(#ff94c2, #ff4f81);
  font-family: "Poppins", sans-serif;
}

/* Floating hearts background */
.hearts {
  position: fixed;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 0;
}

.heart {
  position: absolute;
  width: 15px;
  height: 15px;
  background: pink;
  transform: rotate(45deg);
  opacity: 0.6;
  animation: float 6s infinite ease-in;
}

.heart:before,
.heart:after {
  content: "";
  position: absolute;
  width: 15px;
  height: 15px;
  background: pink;
  border-radius: 50%;
}

.heart:before { top: -8px; }
.heart:after { left: -8px; }

@keyframes float {
  0% { transform: translateY(0) rotate(45deg); opacity: 0.8; }
  100% { transform: translateY(-800px) rotate(45deg); opacity: 0; }
}

/* Typewriter message */
#message {
  position: absolute;
  top: 55%;
  width: 100%;
  text-align: center;
  font-size: 26px;
  color: gold;
  font-weight: bold;
  text-shadow: 0 0 10px white, 0 0 25px gold;
  opacity: 0;
  z-index: 5;
}

/* Heart burst tap animation */
.burst {
  position: absolute;
  color: red;
  font-size: 25px;
  animation: burstAnim 0.8s forwards ease-out;
}

@keyframes burstAnim {
  0% { transform: scale(0.3); opacity: 1; }
  100% { transform: scale(2.5); opacity: 0; }
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>
<div class="hearts" id="hearts"></div>

<div id="message"></div>

<audio id="music" autoplay loop>
  <source src="https://files.catbox.moe/6u4h1p.mp3">
</audio>

<script>
// Floating hearts generator
function createHearts() {
  const container = document.getElementById("hearts");
  for (let i = 0; i < 25; i++) {
    let h = document.createElement("div");
    h.className = "heart";
    h.style.left = Math.random() * window.innerWidth + "px";
    h.style.top = window.innerHeight + "px";
    h.style.animationDuration = (4 + Math.random() * 5) + "s";
    container.appendChild(h);
  }
}
createHearts();

// Typewriter Message Reveal
const msg = "SORRY FOR EVERYTHING. I LOVE YOU WIFE ❤️\nHAPPY BIRTHDAY PAPANI 🎂💖";
let index = 0;
function typeWriter() {
  const messageBox = document.getElementById("message");
  messageBox.style.opacity = 1;
  if (index < msg.length) {
    messageBox.innerHTML += msg.charAt(index);
    index++;
    setTimeout(typeWriter, 70);
  }
}

// Fireworks Canvas + Trigger Message
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];

function firework() {
  const x = Math.random() * canvas.width;
  const y = Math.random() * canvas.height / 2;
  for (let i = 0; i < 60; i++) {
    particles.push({
      x: x,
      y: y,
      angle: Math.random() * 2 * Math.PI,
      speed: Math.random() * 3 + 2,
      size: Math.random() * 3,
      alpha: 1
    });
  }
}

function animateFireworks() {
  ctx.fillStyle = "rgba(0,0,0,0.2)";
  ctx.fillRect(0, 0, canvas.width, canvas.height);

  particles.forEach((p, i) => {
    p.x += Math.cos(p.angle) * p.speed;
    p.y += Math.sin(p.angle) * p.speed;
    p.alpha -= 0.015;

    ctx.fillStyle = `rgba(255,215,0,${p.alpha})`;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
    ctx.fill();

    if (p.alpha <= 0) particles.splice(i, 1);
  });

  requestAnimationFrame(animateFireworks);
}

// Start fireworks and message timing
firework();
animateFireworks();

// MESSAGE REVEAL AFTER 2 SECONDS
setTimeout(typeWriter, 2000);

// Heart burst tap effect
document.addEventListener("click", function(e) {
  let h = document.createElement("div");
  h.className = "burst";
  h.style.left = e.clientX + "px";
  h.style.top = e.clientY + "px";
  h.innerHTML = "❤️";
  document.body.appendChild(h);
  setTimeout(() => h.remove(), 800);
});
</script>

</body>
</html>



