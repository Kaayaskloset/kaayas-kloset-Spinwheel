<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kaaya's Kloset Spin Wheel</title>
  <style>
    body {
      background: #2d2d2d;
      font-family: Arial, sans-serif;
      text-align: center;
      color: white;
      margin: 0;
      padding: 0;
    }
    h1 {
      margin-top: 20px;
      font-size: 2em;
    }
    canvas {
      margin-top: 20px;
    }
    #spinBtn {
      margin-top: 20px;
      padding: 10px 30px;
      font-size: 1.2em;
      background: #e91e63;
      border: none;
      color: white;
      border-radius: 10px;
      cursor: pointer;
    }
    .logo {
      margin-top: 20px;
      width: 200px;
    }
  </style>
</head>
<body>
  <h1>🎉 Spin the Wheel - Shop Above ₹1100 🎉</h1>
  <canvas id="wheelCanvas" width="500" height="500"></canvas>
  <br/>
  <button id="spinBtn">SPIN</button>
  <br/>
  <img class="logo" src="https://your-logo-url.com/kaayas-logo.png" alt="Kaaya's Kloset Logo"/>
  <script>
    const options = [
      "Better luck next time",
      "5% Discount",
      "Oxidised jewellery upto ₹100",
      "10% Discount",
      "Gift Card",
      "Spin again",
      "T-shirt of ₹299",
      "Leggings",
      "15% Discount",
      "20% Discount"
    ];

    const colors = ["#FF5722", "#F44336", "#4CAF50", "#FF9800", "#9C27B0", "#03A9F4", "#E91E63", "#8BC34A", "#FFC107", "#00BCD4"];

    const canvas = document.getElementById("wheelCanvas");
    const ctx = canvas.getContext("2d");
    const spinBtn = document.getElementById("spinBtn");
    const radius = canvas.width / 2;
    let angle = 0;
    let isSpinning = false;

    function drawWheel() {
      const sliceAngle = 2 * Math.PI / options.length;
      for (let i = 0; i < options.length; i++) {
        ctx.beginPath();
        ctx.moveTo(radius, radius);
        ctx.arc(radius, radius, radius, i * sliceAngle, (i + 1) * sliceAngle);
        ctx.fillStyle = colors[i];
        ctx.fill();
        ctx.save();
        ctx.translate(radius, radius);
        ctx.rotate(i * sliceAngle + sliceAngle / 2);
        ctx.textAlign = "right";
        ctx.fillStyle = "#fff";
        ctx.font = "16px Arial";
        ctx.fillText(options[i], radius - 10, 10);
        ctx.restore();
      }
    }

    function spinWheel() {
      if (isSpinning) return;
      isSpinning = true;
      let spinAngle = Math.random() * 360 + 720; // 2-3 rotations
      let duration = 4000;
      let start = null;

      function animate(timestamp) {
        if (!start) start = timestamp;
        const progress = timestamp - start;
        const easing = 1 - Math.pow(1 - progress / duration, 3);
        const rotate = easing * spinAngle;
        angle = rotate % 360;
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.save();
        ctx.translate(radius, radius);
        ctx.rotate(angle * Math.PI / 180);
        ctx.translate(-radius, -radius);
        drawWheel();
        ctx.restore();

        if (progress < duration) {
          requestAnimationFrame(animate);
        } else {
          isSpinning = false;
          const selected = options[Math.floor((360 - angle % 360) / (360 / options.length))];
          setTimeout(() => alert("🎁 You got: " + selected + "!"), 100);
        }
      }
      requestAnimationFrame(animate);
    }

    drawWheel();
    spinBtn.addEventListener("click", spinWheel);
  </script>
</body>
</html>
# kaayas-kloset-Spinwheel
