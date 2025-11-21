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
      background: linear-gradient(135deg, #ff4fa3, #ffb6c8);
      color: #fff;
      text-align: center;
      overflow-x: hidden;
    }

    /* PARTY BLAST */
    #blast {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.8);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 9999;
      font-size: 50px;
      animation: fadeOut 3s ease-in-out forwards;
    }

    @keyframes fadeOut {
      0% { opacity: 1; }
      80% { opacity: 1; }
      100% { opacity: 0; visibility: hidden; }
    }

    /* Cake Section */
    .cake-section {
      margin-top: 80px;
    }

    .cake-img {
      width: 280px;
      height: auto;
      border-radius: 20px;
      border: 4px solid gold;
      box-shadow: 0 0 25px gold;
    }

    .message-box {
      margin-top: 20px;
      font-size: 22px;
      font-weight: 600;
      color: #fff;
      text-shadow: 0 0 10px #ff007f;
    }

    .photo-pin {
      width: 200px;
      border-radius: 14px;
      border: 4px solid gold;
      margin-top: -50px;
      box-shadow: 0 0 20px gold;
    }
  </style>
</head>
<body>

  <!-- FULL SCREEN REAL FIREWORKS -->
  <canvas id="fwCanvas"></canvas>

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
        for (let i = 0; i < 50; i++) this.particles.push(new Particle(this.x, this.y));
        setTimeout(() => { this.remove = true; }, 1500);
      }
      draw() {
        if (!this.exploded) {
          ctx.fillStyle = 'gold';
          ctx.beginPath();
          ctx.arc(this.x, this.y, 4, 0, Math.PI * 2);
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
      if (Math.random() < 0.1) fireworks.push(new Firework());
      requestAnimationFrame(loop);
    }
    loop();

    setTimeout(() => {
      document.getElementById('fwCanvas').style.display = 'none';
    }, 5000);
  </script>

  <h1 style="margin-top: 160px; font-size: 42px; text-shadow: 0 0 20px gold;">Happy Birthday PAPANI ❤️🎉</h1>

  <div class="cake-section">
    <img src="cake.png" class="cake-img" alt="Cake" />

    <!-- Correct pinned uploaded photo -->
    <img src="/mnt/data/WhatsApp Image 2025-11-21 at 5.22.48 PM.jpeg" class="photo-pin" alt="Pinned Photo" />

    <div class="message-box">
      <p>Sorry for everything I have done & I LOVE YOU HENDTHI ❤️</p>
      <p style="font-size:20px; margin-top:10px;">ಕ್ಷಮಿಸು ನನ್ನ ತಪ್ಪುಗಳನ್ನ… ನಾನು ನಿನ್ನನ್ನು ತುಂಬಾ ಪ್ರೀತಿಸುತ್ತೇನೆ 💖</p>
    </div>
  </div>

</body>
</html>

