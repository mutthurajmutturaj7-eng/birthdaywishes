<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>PAPANI Wishes</title>

<style>
    body {
        margin: 0;
        padding: 0;
        overflow: hidden;
        font-family: "Poppins", sans-serif;
        color: white;
        text-align: center;

        /* Pink–Gold Glitter Gradient Background */
        background: radial-gradient(circle at center,
            #ffb7e2 0%, #ff69b4 30%, #ffcc99 70%, #ffb347 100%);
        background-size: 200% 200%;
        animation: glitterMove 6s infinite alternate ease-in-out;
    }

    @keyframes glitterMove {
        0% { background-position: 0% 0%; }
        100% { background-position: 100% 100%; }
    }

    /* Floating Heart Particles */
    .heart {
        position: absolute;
        font-size: 14px;
        color: rgba(255, 0, 85, 0.8);
        animation: floatUp linear infinite;
        opacity: 0.9;
    }

    @keyframes floatUp {
        0% { transform: translateY(0) scale(1); opacity: 1; }
        100% { transform: translateY(-120vh) scale(1.8); opacity: 0; }
    }

    /* Message Box */
    .message {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 90%;
        max-width: 500px;
        font-size: 28px;
        line-height: 1.4;
        font-weight: bold;
        display: none;
        animation: fadeIn 2s ease forwards;
        padding: 20px;
        backdrop-filter: blur(8px);
        border-radius: 20px;
        background: rgba(255, 255, 255, 0.15);
        box-shadow: 0 0 25px rgba(255, 0, 80, 0.6);
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translate(-50%, -60%); }
        to { opacity: 1; transform: translate(-50%, -50%); }
    }
</style>
</head>

<body>

<!-- Message Text -->
<div id="msg" class="message">
    💖 Happy Birthday, PAPANI 💖<br>
    Wishing you love, happiness, and magical moments! ✨
</div>

<script>
/* Create Floating Hearts */
function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";

    const size = Math.random() * 20 + 10; 
    heart.style.fontSize = size + "px";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.bottom = "-20px";

    heart.style.animationDuration = (Math.random() * 5 + 4) + "s";

    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 9000);
}

setInterval(createHeart, 200);

/* Reveal Message After 2 Seconds */
setTimeout(() => {
    document.getElementById("msg").style.display = "block";
}, 2000);
</script>

</body>
</html>




