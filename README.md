# Juanes-let player = {
  x: 300,
  y: 350,
  width: 40,
  height: 20,
  color: "cyan",
  lives: 3,
  score: 0
};

let bullets = [];
let enemies = [];
let keys = {};
let shootCooldown = 0;

function drawPlayer() {
  ctx.fillStyle = player.color;
  ctx.fillRect(player.x, player.y, player.width, player.height);
}

function drawBullets() {
  ctx.fillStyle = "yellow";
  bullets.forEach((b, i) => {
    b.y -= 5;
    ctx.fillRect(b.x, b.y, 4, 10);
    if (b.y < 0) bullets.splice(i, 1);
  });
}

function drawEnemies() {
  if (Math.random() < 0.02) {
    enemies.push({ x: Math.random() * 560, y: 0, width: 40, height: 20 });
  }

  ctx.fillStyle = "red";
  enemies.forEach((e, i) => {
    e.y += 2;
    ctx.fillRect(e.x, e.y, e.width, e.height);

    // colisión con jugador
    if (
      e.y + e.height > player.y &&
      e.x < player.x + player.width &&
      e.x + e.width > player.x
    ) {
      enemies.splice(i, 1);
      player.lives--;
    }

    // colisión con balas
    bullets.forEach((b, j) => {
      if (
        b.x < e.x + e.width &&
        b.x + 4 > e.x &&
        b.y < e.y + e.height &&
        b.y + 10 > e.y
      ) {
        enemies.splice(i, 1);
        bullets.splice(j, 1);
        player.score += 1000;
      }
    });
  });
}

function drawHUD() {
  ctx.fillStyle = "white";
  ctx.font = "16px sans-serif";
  ctx.fillText(`Vidas: ${player.lives}`, 10, 20);
  ctx.fillText(`Puntaje: ${player.score.toLocaleString()}`, 450, 20);
}

function gameLoop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Movimiento
  if (keys["ArrowLeft"] && player.x > 0) player.x -= 5;
  if (keys["ArrowRight"] && player.x + player.width < canvas.width) player.x += 5;

  // Disparo en ráfaga
  if (keys[" "] && shootCooldown <= 0) {
    bullets.push({ x: player.x + player.width / 2 - 2, y: player.y });
    shootCooldown = 5; // delay entre disparos
  } else {
    shootCooldown--;
  }

  drawPlayer();
  drawBullets();
  drawEnemies();
  drawHUD();

  if (player.lives <= 0) {
    ctx.fillStyle = "white";
    ctx.font = "40px sans-serif";
    ctx.fillText("¡Game Over!", 180, 200);
    return;
  }

  if (player.score >= 1000000) {
    ctx.fillStyle = "lightgreen";
    ctx.font = "36px sans-serif";
    ctx.fillText("¡Has ganado!", 190, 200);
    return;
  }

  requestAnimationFrame(gameLoop);
}

window.addEventListener("keydown", e => keys[e.key] = true);
window.addEventListener("keyup", e => keys[e.key] = false);

gameLoop();let player = {
  x: 300,
  y: 350,
  width: 40,
  height: 20,
  color: "cyan",
  lives: 3,
  score: 0
};

let bullets = [];
let enemies = [];
let keys = {};
let shootCooldown = 0;

function drawPlayer() {
  ctx.fillStyle = player.color;
  ctx.fillRect(player.x, player.y, player.width, player.height);
}

function drawBullets() {
  ctx.fillStyle = "yellow";
  bullets.forEach((b, i) => {
    b.y -= 5;
    ctx.fillRect(b.x, b.y, 4, 10);
    if (b.y < 0) bullets.splice(i, 1);
  });
}

function drawEnemies() {
  if (Math.random() < 0.02) {
    enemies.push({ x: Math.random() * 560, y: 0, width: 40, height: 20 });
  }

  ctx.fillStyle = "red";
  enemies.forEach((e, i) => {
    e.y += 2;
    ctx.fillRect(e.x, e.y, e.width, e.height);

    // colisión con jugador
    if (
      e.y + e.height > player.y &&
      e.x < player.x + player.width &&
      e.x + e.width > player.x
    ) {
      enemies.splice(i, 1);
      player.lives--;
    }

    // colisión con balas
    bullets.forEach((b, j) => {
      if (
        b.x < e.x + e.width &&
        b.x + 4 > e.x &&
        b.y < e.y + e.height &&
        b.y + 10 > e.y
      ) {
        enemies.splice(i, 1);
        bullets.splice(j, 1);
        player.score += 1000;
      }
    });
  });
}

function drawHUD() {
  ctx.fillStyle = "white";
  ctx.font = "16px sans-serif";
  ctx.fillText(`Vidas: ${player.lives}`, 10, 20);
  ctx.fillText(`Puntaje: ${player.score.toLocaleString()}`, 450, 20);
}

function gameLoop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Movimiento
  if (keys["ArrowLeft"] && player.x > 0) player.x -= 5;
  if (keys["ArrowRight"] && player.x + player.width < canvas.width) player.x += 5;

  // Disparo en ráfaga
  if (keys[" "] && shootCooldown <= 0) {
    bullets.push({ x: player.x + player.width / 2 - 2, y: player.y });
    shootCooldown = 5; // delay entre disparos
  } else {
    shootCooldown--;
  }

  drawPlayer();
  drawBullets();
  drawEnemies();
  drawHUD();

  if (player.lives <= 0) {
    ctx.fillStyle = "white";
    ctx.font = "40px sans-serif";
    ctx.fillText("¡Game Over!", 180, 200);
    return;
  }

  if (player.score >= 1000000) {
    ctx.fillStyle = "lightgreen";
    ctx.font = "36px sans-serif";
    ctx.fillText("¡Has ganado!", 190, 200);
    return;
  }

  requestAnimationFrame(gameLoop);
}

window.addEventListener("keydown", e => keys[e.key] = true);
window.addEventListener("keyup", e => keys[e.key] = false);

gameLoop();
