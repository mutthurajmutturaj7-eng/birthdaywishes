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

  <!-- PARTY BLAST -->
  <div id="blast">🎉🎉🎉 HAPPY BIRTHDAY PAPANI 🎉🎉🎉</div>

  <!-- MUSIC -->
  <audio autoplay loop>
    <source src="song.mp3" type="audio/mpeg" />
  </audio>

  <h1 style="margin-top: 120px; font-size: 40px; text-shadow: 0 0 15px gold;">Happy Birthday PAPANI ❤️🎉</h1>

  <!-- Cake Section -->
  <div class="cake-section">
    <img src="cake.png" class="cake-img" alt="Cake" />

    <br />

    <!-- Pinned Photo -->
    <img src="/mnt/data/WhatsApp Image 2025-11-21 at 5.22.48 PM.jpeg" class="photo-pin" alt="Pinned Photo" />

    <div class="message-box">
      Sorry for everything I have done & I LOVE YOU HENDTHI ❤️<br />
      ಕ್ಷಮಿಸು ನನ್ನ ತಪ್ಪುಗಳನ್ನ… ನಾನು ನಿನ್ನನ್ನು ತುಂಬಾ ಪ್ರೀತಿಸುತ್ತೇನೆ 💖
    </div>
  </div>

</body>
</html>
