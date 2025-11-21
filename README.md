<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Happy Birthday PAPANI</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
      color: #fff;
      text-align: center;
      overflow-x: hidden;
      background: url('pink-gold-glitter.gif');
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
    }

    /* Remove photos */
    .photo-pin { display: none !important; }

    /* Heart floating particles */
    .heart {
      position: fixed;
      bottom: -20px;
      font-size: 22px;
      opacity: 0.8;
      animation: floatUp 6s linear infinite;
      color: #ff79c6;
      text-shadow: 0 0 8px gold;
    }
    @keyframes floatUp {
      0% { transform: translateY(0) scale(1); opacity: 1; }
      100% { transform: translateY(-120vh) scale(1.6); opacity: 0; }
    }

    /* Name Animation */
    .name-animate {
      font-size: 48px;
      font-weight: 700;
      color: #ffdede;
      text-shadow: 0 0 20px gold;
      animation: glowName 2.5s ease-in-out infinite alternate;
      margin-top: 160px;
    }
    @keyframes glowName {
      0% { text-shadow: 0 0 10px gold, 0 0 20px #ff4fa3; }
      100% { text-shadow: 0 0 25px gold, 0 0 40px #ff9ed6; }
    }

    /* Cake bounce */
    .cake-animated {
      width: 260px;
      animation: bounce 2s infinite ease-in-out;
      filter: drop-shadow(0 0 20px gold);
    }
    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-18px); }
    }

    .reveal {
      opacity: 0;
      animation: fadeIn 1.5s ease-in-out forwards;
      animation-delay: 5s;
    }
    @keyframes fadeIn {
      0% { opacity: 0; }
      100% { opacity: 1; }
    }
  </style>
</head>
<body>

  <!-- FULL SCREEN FIREWORKS OVERLAY BEFORE REVEAL -->
  <div id="fwCover">
    <canvas id="fwCanvas"></canvas>
  </div>

  <style>
    #fwCover {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: black;
      z-index: 99999;
    }
    #fwCanvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .reveal {
      opacity: 0;
      animation: fadeIn 1.5s ease-in-out forwards;
      animation-delay: 5s;
    }

    @keyframes fadeIn {
      0% { opacity: 0; }
      100% { opacity: 1; }
    }

    /* Animated Cake */
    .cake-animated {
      width: 260px;
      animation: bounce 2s infinite ease-in-out;
      filter: drop-shadow(0 0 20px gold);
    }
    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-18px); }
    }
  </style>

  <script>
    // REALISTIC FIREWORKS EFFECT
    const canvas = document.getElementById('fwCanvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    let fireworks = [];

    class Firework {
      constructor() {
        this.x = Math.random() * canvas.width;
        this.y = canvas.height;
        this.targetY = Math.random() * (canvas.height / 2);
        this.speed = 4;
        this.particles = [];
        this.exploded = false;
      }
      update() {
        if (!this.exploded) {
          this.y -= this.speed;
          if (this.y < this.targetY) this.explode();
        }
        this.particles.forEach(p => p.update());
      }
      explode() {
        this.exploded = true;
        for (let i = 0; i < 70; i++) this.particles.push(new Particle(this.x, this.y));
        setTimeout(() => { this.remove = true; }, 1500);
      }
      draw() {
        if (!this.exploded) {
          ctx.fillStyle = 'gold';
          ctx.beginPath();
          ctx.arc(this.x, this.y, 5, 0, Math.PI * 2);
          ctx.fill();
        }
        this.particles.forEach(p => p.draw());
      }
    }

    class Particle {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.speed = Math.random() * 4 + 1;
        this.angle = Math.random() * Math.PI * 2;
        this.alpha = 1;
      }
      update() {
        this.x += Math.cos(this.angle) * this.speed;
        this.y += Math.sin(this.angle) * this.speed;
        this.alpha -= 0.02;
      }
      draw() {
        ctx.fillStyle = `rgba(255,215,0,${this.alpha})`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, 3, 0, Math.PI * 2);
        ctx.fill();
      }
    }

    function loop() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      fireworks.forEach((fw, i) => {
        fw.update();
        fw.draw();
        if (fw.remove) fireworks.splice(i, 1);
      });
      if (Math.random() < 0.15) fireworks.push(new Firework());
      requestAnimationFrame(loop);
    }
    loop();

    // REMOVE FIREWORK SCREEN AFTER 5 SECONDS
    setTimeout(() => {
      document.getElementById('fwCover').style.display = 'none';
    }, 5000);
  </script>

  <div class="reveal">
    <div class="name-animate">Happy Birthday PAPANI ❤️✨</div>

    <div class="cake-section" style="margin-top: 40px;">
      <img src="cake.png" class="cake-animated" alt="Cake" />

      <div class="message-box" style="margin-top: 20px; font-size: 22px; font-weight: 600; color: #fff; text-shadow: 0 0 10px #ff007f;">
        <p>Sorry for everything I have done & I LOVE YOU HENDTHI ❤️</p>
        <p style="font-size:20px; margin-top:10px;">ಕ್ಷಮಿಸು ನನ್ನ ತಪ್ಪುಗಳನ್ನ… ನಾನು ನಿನ್ನನ್ನು ತುಂಬಾ ಪ್ರೀತಿಸುತ್ತೇನೆ 💖</p>
      </div>
    </div>
  </div>

  <!-- Heart particles script -->
  <script>
    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.innerHTML = '❤️';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.fontSize = (20 + Math.random() * 20) + 'px';
      heart.style.animationDuration = (4 + Math.random() * 4) + 's';
      document.body.appendChild(heart);
      setTimeout(() => { heart.remove(); }, 6000);
    }
    setInterval(createHeart, 400);
  </script>
    </div>
  </div>

</body>
</html>


