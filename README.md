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

  <!-- FIREWORKS ANIMATION -->
  <div id="fireworks"></div>

  <style>
    #fireworks {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: black;
      z-index: 99999;
      animation: fadeOut 4s ease-in-out forwards;
    }
  </style>

  <script>
    // Simple fireworks effect
    for (let i = 0; i < 30; i++) {
      let spark = document.createElement('div');
      spark.style.position = 'absolute';
      spark.style.width = '6px';
      spark.style.height = '6px';
      spark.style.borderRadius = '50%';
      spark.style.background = 'gold';
      spark.style.top = Math.random() * 100 + '%';
      spark.style.left = Math.random() * 100 + '%';
      spark.style.boxShadow = '0 0 12px gold';
      spark.style.animation = 'boom 1s ease-out forwards';
      document.getElementById('fireworks').appendChild(spark);
    }
  </script>

  <h1 style="margin-top: 160px; font-size: 42px; text-shadow: 0 0 20px gold;">Happy Birthday PAPANI ❤️🎉</h1>

  <div class="cake-section">
    <img src="cake.png" class="cake-img" alt="Cake" />

    <!-- Correct pinned image -->
    <img src="/mnt/data/WhatsApp Image 2025-11-21 at 5.22.48 PM.jpeg" class="photo-pin" alt="Pinned Photo" />

    <div class="message-box">
      <p>Sorry for everything I have done & I LOVE YOU HENDTHI ❤️</p>
      <p style="font-size:20px; margin-top:10px;">ಕ್ಷಮಿಸು ನನ್ನ ತಪ್ಪುಗಳನ್ನ… ನಾನು ನಿನ್ನನ್ನು ತುಂಬಾ ಪ್ರೀತಿಸುತ್ತೇನೆ 💖</p>
    </div>
  </div>

</body>
</html>

