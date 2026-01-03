<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mini Pacman on GitHub</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <style>
    body {
      margin: 0;
      background: #020617;
      color: #e5e7eb;
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }
    header {
      width: 100%;
      text-align: center;
      padding: 12px;
      background: #0f172a;
      border-bottom: 1px solid #1f2937;
    }
    main {
      padding: 16px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
    }
    #gameCanvas {
      background: #000;
      border: 2px solid #22c55e;
      border-radius: 8px;
      display: block;
    }
    .info {
      font-size: 14px;
      text-align: center;
      max-width: 400px;
      color: #9ca3af;
    }
  </style>
</head>
<body>
  <header>
    <h1>Mini Pacman (Arrow Keys)</h1>
  </header>

  <main>
    <canvas id="gameCanvas" width="480" height="320"></canvas>
    <p class="info">
      Use <strong>Arrow keys</strong> to move the yellow Pac‑Man and eat all the white dots.
    </p>
  </main>

  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    const tileSize = 24;
    const cols = Math.floor(canvas.width / tileSize);
    const rows = Math.floor(canvas.height / tileSize);

    // Simple map: 0 = empty, 1 = dot
    const map = [];
    for (let y = 0; y < rows; y++) {
      map[y] = [];
      for (let x = 0; x < cols; x++) {
        // Put dots everywhere except outer border
        if (x === 0 || y === 0 || x === cols - 1 || y === rows - 1) {
          map[y][x] = 0;
        } else {
          map[y][x] = 1;
        }
      }
    }

    const pacman = {
      x: 2,
      y: 2,
      dirX: 1,
      dirY: 0,
      speed: 0.12, // tiles per frame
      offsetX: 0,
      offsetY: 0,
      mouthAngle: 0.3,
    };

    let lastTime = 0;

    function drawMap() {
      ctx.fillStyle = '#000';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = '#fff';
      for (let y = 0; y < rows; y++) {
        for (let x = 0; x < cols; x++) {
          if (map[y][x] === 1) {
            const cx = x * tileSize + tileSize / 2;
            const cy = y * tileSize + tileSize / 2;
            ctx.beginPath();
            ctx.arc(cx, cy, 3, 0, Math.PI * 2);
            ctx.fill();
          }
        }
      }
    }

    function drawPacman() {
      const centerX = (pacman.x + pacman.offsetX) * tileSize + tileSize / 2;
      const centerY = (pacman.y + pacman.offsetY) * tileSize + tileSize / 2;
      const radius = tileSize / 2 - 2;

      // Determine facing angle
      let angle = 0;
      if (pacman.dirX === 1) angle = 0;
      else if (pacman.dirX === -1) angle = Math.PI;
      else if (pacman.dirY === -1) angle = -Math.PI / 2;
      else if (pacman.dirY === 1) angle = Math.PI / 2;

      const open = pacman.mouthAngle;

      ctx.fillStyle = '#facc15';
      ctx.beginPath();
      ctx.moveTo(centerX, centerY);
      ctx.arc(centerX, centerY, radius, angle + open, angle + Math.PI * 2 - open);
      ctx.closePath();
      ctx.fill();

      // Eye
      ctx.fillStyle = '#000';
      const eyeX = centerX + Math.cos(angle - Math.PI / 2) * (radius / 2);
      const eyeY = centerY + Math.sin(angle - Math.PI / 2) * (radius / 2);
      ctx.beginPath();
      ctx.arc(eyeX, eyeY, 2, 0, Math.PI * 2);
      ctx.fill();
    }

    function update(delta) {
      // Animate mouth
      pacman.mouthAngle = 0.2 + 0.1 * Math.sin(performance.now() / 100);

      const move = pacman.speed * delta;
      pacman.offsetX += pacman.dirX * move;
      pacman.offsetY += pacman.dirY * move;

      // When offset reaches 1 tile, snap to grid
      if (pacman.offsetX >= 1 || pacman.offsetX <= -1 || pacman.offsetY >= 1 || pacman.offsetY <= -1) {
        pacman.x += Math.round(pacman.offsetX);
        pacman.y += Math.round(pacman.offsetY);
        pacman.offsetX = 0;
        pacman.offsetY = 0;

        // Eat dot on tile
        if (map[pacman.y] && map[pacman.y][pacman.x] === 1) {
          map[pacman.y][pacman.x] = 0;
        }

        // Stay inside bounds
        if (pacman.x < 1) pacman.x = 1;
        if (pacman.y < 1) pacman.y = 1;
        if (pacman.x > cols - 2) pacman.x = cols - 2;
        if (pacman.y > rows - 2) pacman.y = rows - 2;
      }
    }

    function gameLoop(timestamp) {
      const delta = timestamp - lastTime;
      lastTime = timestamp;

      update(delta);
      drawMap();
      drawPacman();

      requestAnimationFrame(gameLoop);
    }

    // Controls
    window.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowLeft') {
        pacman.dirX = -1; pacman.dirY = 0;
      } else if (e.key === 'ArrowRight') {
        pacman.dirX = 1; pacman.dirY = 0;
      } else if (e.key === 'ArrowUp') {
        pacman.dirX = 0; pacman.dirY = -1;
      } else if (e.key === 'ArrowDown') {
        pacman.dirX = 0; pacman.dirY = 1;
      }
    });

    // Start
    drawMap();
    drawPacman();
    requestAnimationFrame(gameLoop);
  </script>
</body>
</html>
