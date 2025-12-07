# For-my-princess-
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>surprise</title>
  <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background: #111;
      color: white;
      font-family: Arial, sans-serif;
      text-align: center;
    }

    input {
      padding: 10px;
      font-size: 18px;
      border-radius: 8px;
      border: none;
      outline: none;
      margin-bottom: 20px;
    }

    canvas {
      background: transparent;
    }
  </style>
</head>
<body>
  <h2>Digite seu nome</h2>
  <input type="text" id="nameInput" placeholder="Seu nome..." />
  <canvas id="canvas" width="400" height="400"></canvas>

  <script>
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");
    const input = document.getElementById("nameInput");

    input.addEventListener("input", () => {
      const name = input.value.trim();
      drawHeartWithName(name);
    });

    function drawHeartWithName(name) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      if (!name) return;

      const particles = [];
      const heartPoints = [];

      // Gera pontos no formato de coração
      for (let t = 0; t < Math.PI * 2; t += 0.1) {
        const x = 16 * Math.pow(Math.sin(t), 3);
        const y =
          13 * Math.cos(t) -
          5 * Math.cos(2 * t) -
          2 * Math.cos(3 * t) -
          Math.cos(4 * t);
        heartPoints.push({
          x: x * 10 + 200,
          y: -y * 10 + 200,
        });
      }

      // Cada ponto do coração recebe uma letra do nome
      heartPoints.forEach((p, i) => {
        const letter = name[i % name.length];
        particles.push({ x: p.x, y: p.y, letter });
      });

      // Animação
      let progress = 0;

      function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        particles.forEach((part, index) => {
          if (index / particles.length < progress) {
            ctx.fillStyle = "#ff4d6d";
            ctx.font = "15px Arial";
            ctx.fillText(part.letter, part.x, part.y);
          }
        });

        progress += 0.01;
        if (progress <= 1) requestAnimationFrame(animate);
      }

      animate();
    }
  </script>
</body>
</html>
