<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <title>🔪 Potong Buah - Mobile</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
      -webkit-user-select: none;
      user-select: none;
      -webkit-touch-callout: none;
    }

    body {
      background: linear-gradient(180deg, #0a1f2e 0%, #153e4a 50%, #0d2a33 100%);
      min-height: 100vh;
      min-height: 100dvh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', 'Poppins', Roboto, system-ui, sans-serif;
      padding: 0;
      margin: 0;
      overflow: hidden;
      touch-action: none;
      -ms-touch-action: none;
    }

    .game-container {
      width: 100vw;
      width: 100dvw;
      height: 100vh;
      height: 100dvh;
      max-width: 500px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 10px;
      background: rgba(255, 248, 240, 0.08);
      backdrop-filter: blur(10px);
      position: relative;
      padding: 10px 8px;
    }

    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      padding: 0 12px;
      gap: 10px;
    }

    h1 {
      font-size: clamp(1.5rem, 5vw, 2rem);
      font-weight: 900;
      color: #ffecaa;
      text-shadow: 3px 3px 0 #8b3a3a, 5px 5px 0 rgba(0,0,0,0.4);
      letter-spacing: 1px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .score-badge {
      background: #fde7b4;
      color: #3e2c1b;
      padding: 10px 22px;
      border-radius: 40px;
      font-weight: 800;
      font-size: clamp(1.1rem, 4vw, 1.4rem);
      box-shadow: 0 5px 0 #b47c48, 0 8px 18px rgba(0,0,0,0.5);
      display: flex;
      align-items: center;
      gap: 6px;
      border: 2px solid #fff2cf;
    }

    .canvas-wrapper {
      position: relative;
      width: 100%;
      flex: 1;
      min-height: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 5px 0;
    }

    canvas {
      display: block;
      width: 100%;
      height: 100%;
      max-height: 70vh;
      max-height: 70dvh;
      border-radius: 40px;
      background: radial-gradient(circle at 30% 25%, #ffe7c4, #c98f5c);
      box-shadow: inset 0 0 50px rgba(0, 0, 0, 0.6), 0 20px 35px rgba(0, 0, 0, 0.7);
      border: 4px solid #ffdead;
      touch-action: none;
    }

    .controls {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 15px;
      width: 100%;
      padding: 5px 12px 15px;
      flex-wrap: wrap;
    }

    .btn {
      background: #fed082;
      border: none;
      padding: 14px 28px;
      border-radius: 50px;
      font-weight: 800;
      font-size: clamp(0.95rem, 3.5vw, 1.15rem);
      letter-spacing: 1px;
      color: #2e2e1f;
      box-shadow: 0 6px 0 #b4532a, 0 8px 20px rgba(0,0,0,0.5);
      cursor: pointer;
      transition: 0.08s linear;
      display: flex;
      align-items: center;
      gap: 8px;
      border: 1px solid #fff2cf;
      text-transform: uppercase;
      -webkit-tap-highlight-color: transparent;
    }

    .btn:active {
      transform: translateY(4px);
      box-shadow: 0 2px 0 #87481f, 0 5px 12px rgba(0,0,0,0.5);
      background: #f5c470;
    }

    .info-text {
      color: #ffeac5;
      font-weight: 600;
      font-size: clamp(0.75rem, 2.5vw, 0.9rem);
      background: rgba(0,0,0,0.5);
      padding: 8px 20px;
      border-radius: 30px;
      text-align: center;
      width: 100%;
    }

    .combo-pop {
      position: fixed;
      top: 30%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 2.5rem;
      font-weight: 900;
      color: #ffd700;
      text-shadow: 0 0 20px #ff8c00, 0 0 40px #ff4500;
      pointer-events: none;
      z-index: 100;
      animation: popUp 0.8s ease-out forwards;
    }

    @keyframes popUp {
      0% { opacity: 1; transform: translate(-50%, -50%) scale(0.5); }
      50% { opacity: 1; transform: translate(-50%, -80%) scale(1.3); }
      100% { opacity: 0; transform: translate(-50%, -150%) scale(0.8); }
    }

    @media (orientation: landscape) {
      .game-container {
        flex-direction: row;
        flex-wrap: wrap;
      }
      .canvas-wrapper {
        flex: 2;
        min-width: 250px;
      }
      canvas {
        max-height: 80vh;
        max-height: 80dvh;
      }
    }
  </style>
</head>
<body>
<div class="game-container">
  <div class="header">
    <h1>
      <span>🔪</span> BUAH
    </h1>
    <div class="score-badge">
      <span>⭐</span> <span id="scoreDisplay">0</span>
    </div>
  </div>

  <div class="canvas-wrapper">
    <canvas id="gameCanvas"></canvas>
  </div>

  <div class="controls">
    <button class="btn" id="restartButton">
      <span>🔄</span> MULAI LAGI
    </button>
  </div>
  <div class="info-text">
    ✦ GESEK layar untuk potong buah ✦ <strong>+5 poin</strong> per buah ✦
  </div>
</div>

<script>
  (function() {
    // ============ GAME ENGINE MOBILE ============
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    // Ukuran canvas responsif mengikuti layar HP
    let W, H;

    function resizeCanvas() {
      const container = canvas.parentElement;
      const rect = container.getBoundingClientRect();
      const size = Math.min(rect.width, rect.height * 0.9);
      W = Math.floor(size);
      H = Math.floor(size);
      canvas.width = W;
      canvas.height = H;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    // State game
    let fruits = [];
    let score = 0;
    let gameActive = true;
    let comboCount = 0;
    let comboTimer = null;

    // Touch state untuk swipe detection
    let touchActive = false;
    let lastTouchPos = { x: 0, y: 0 };
    let currentTouchPos = { x: 0, y: 0 };
    let touchTrail = []; // menyimpan jejak untuk deteksi lebih akurat

    const POINTS_PER_FRUIT = 5;
    const GRAVITY = 0.3;
    const MAX_FRUITS = 12;
    const SPAWN_INTERVAL = 40;
    let frameCount = 0;
    let animationId = null;

    // Jenis buah dengan emoji dan warna
    const fruitTypes = [
      { emoji: '🍉', name: 'semangka', color: '#2e6b2e', radius: 30 },
      { emoji: '🍎', name: 'apel', color: '#c42e2e', radius: 28 },
      { emoji: '🍌', name: 'pisang', color: '#f4e04a', radius: 26 },
      { emoji: '🍊', name: 'jeruk', color: '#f78c2e', radius: 27 },
      { emoji: '🍇', name: 'anggur', color: '#8e4a9e', radius: 24 },
      { emoji: '🥝', name: 'kiwi', color: '#7b943e', radius: 25 },
      { emoji: '🍑', name: 'persik', color: '#f9ac7c', radius: 27 },
      { emoji: '🍓', name: 'stroberi', color: '#d4444f', radius: 23 },
    ];

    // Kelas Buah
    class Fruit {
      constructor(x, y, type) {
        this.x = x;
        this.y = y;
        this.type = type;
        this.radius = type.radius * (W / 500); // skala sesuai ukuran canvas
        this.vx = (Math.random() - 0.5) * 5;
        this.vy = -(Math.random() * 8 + 7);
        this.cut = false;
        this.rotation = Math.random() * Math.PI * 2;
        this.rotSpeed = (Math.random() - 0.5) * 0.3;
      }

      update() {
        if (this.cut) return false;
        
        this.vy += GRAVITY;
        this.x += this.vx;
        this.y += this.vy;
        this.rotation += this.rotSpeed;

        // Batas kiri/kanan
        const margin = this.radius + 5;
        if (this.x - this.radius < margin) {
          this.x = margin + this.radius;
          this.vx *= -0.5;
        } else if (this.x + this.radius > W - margin) {
          this.x = W - margin - this.radius;
          this.vx *= -0.5;
        }

        // Hapus jika jatuh keluar layar
        if (this.y - this.radius > H + 50) {
          return false;
        }
        return true;
      }

      draw(ctx) {
        if (this.cut) return;
        
        ctx.save();
        ctx.translate(this.x, this.y);
        ctx.rotate(this.rotation);

        // Badan buah
        ctx.beginPath();
        ctx.arc(0, 0, this.radius, 0, Math.PI * 2);
        ctx.fillStyle = this.type.color;
        ctx.fill();
        ctx.strokeStyle = '#3a2e1e';
        ctx.lineWidth = 2;
        ctx.stroke();

        // Kilau
        ctx.beginPath();
        ctx.arc(-this.radius*0.25, -this.radius*0.3, this.radius*0.25, 0, Math.PI*2);
        ctx.fillStyle = 'rgba(255,255,240,0.5)';
        ctx.fill();

        // Emoji
        const fontSize = this.radius * 1.4;
        ctx.font = `${fontSize}px "Segoe UI Emoji", "Apple Color Emoji", "Noto Color Emoji", sans-serif`;
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.shadowColor = 'rgba(0,0,0,0.3)';
        ctx.shadowBlur = 3;
        ctx.fillText(this.type.emoji, 0, 1);
        ctx.shadowColor = 'transparent';
        ctx.shadowBlur = 0;

        ctx.restore();
      }
    }

    // Spawn buah
    function spawnFruit() {
      if (!gameActive) return;
      if (fruits.length >= MAX_FRUITS) return;
      
      const type = fruitTypes[Math.floor(Math.random() * fruitTypes.length)];
      const x = 25 + Math.random() * (W - 50);
      const y = H - 20 - Math.random() * 30;
      
      fruits.push(new Fruit(x, y, type));
    }

    // Deteksi potongan berbasis segmen garis
    function lineIntersectsCircle(x1, y1, x2, y2, cx, cy, r) {
      const dx = x2 - x1;
      const dy = y2 - y1;
      const fx = x1 - cx;
      const fy = y1 - cy;

      const a = dx * dx + dy * dy;
      if (a === 0) return false; // titik sama
      
      const b = 2 * (fx * dx + fy * dy);
      const c = fx * fx + fy * fy - r * r;
      let discriminant = b * b - 4 * a * c;
      
      if (discriminant < 0) return false;
      
      discriminant = Math.sqrt(discriminant);
      const t1 = (-b - discriminant) / (2 * a);
      const t2 = (-b + discriminant) / (2 * a);
      
      return (t1 >= 0 && t1 <= 1) || (t2 >= 0 && t2 <= 1);
    }

    // Cek slice dengan semua buah
    function checkSlice(x1, y1, x2, y2) {
      if (!gameActive) return;
      
      let sliced = false;
      
      for (let i = fruits.length - 1; i >= 0; i--) {
        const fruit = fruits[i];
        if (fruit.cut) continue;
        
        if (lineIntersectsCircle(x1, y1, x2, y2, fruit.x, fruit.y, fruit.radius)) {
          fruit.cut = true;
          score += POINTS_PER_FRUIT;
          comboCount++;
          sliced = true;
          
          // Hapus buah
          fruits.splice(i, 1);
        }
      }
      
      if (sliced) {
        updateScore();
        
        // Tampilkan combo jika lebih dari 1
        if (comboCount >= 2) {
          showComboPop(comboCount);
        }
        
        // Reset combo setelah 500ms tanpa potongan
        clearTimeout(comboTimer);
        comboTimer = setTimeout(() => {
          comboCount = 0;
        }, 500);
      }
    }

    // Tampilkan popup combo
    function showComboPop(count) {
      const pop = document.createElement('div');
      pop.className = 'combo-pop';
      pop.textContent = count >= 5 ? `🔥 ${count}x COMBO!` : `✨ ${count}x`;
      document.body.appendChild(pop);
      setTimeout(() => pop.remove(), 800);
    }

    function updateScore() {
      document.getElementById('scoreDisplay').textContent = score;
    }

    // Reset game
    function resetGame() {
      fruits = [];
      score = 0;
      comboCount = 0;
      gameActive = true;
      touchActive = false;
      touchTrail = [];
      updateScore();
      
      for (let i = 0; i < 5; i++) {
        spawnFruit();
      }
    }

    // Game loop
    function gameLoop() {
      ctx.clearRect(0, 0, W, H);
      
      // Background
      ctx.fillStyle = '#f9e3b6';
      ctx.fillRect(0, 0, W, H);
      
      if (gameActive) {
        // Update buah
        for (let i = fruits.length - 1; i >= 0; i--) {
          if (!fruits[i].update()) {
            fruits.splice(i, 1);
          }
        }
        
        // Spawn berkala
        frameCount++;
        if (frameCount % SPAWN_INTERVAL === 0) {
          spawnFruit();
          if (Math.random() < 0.4) spawnFruit();
        }
      }
      
      // Gambar buah
      fruits.forEach(f => f.draw(ctx));
      
      // Gambar jejak gesekan (efek pedang)
      if (touchActive && touchTrail.length > 1) {
        ctx.beginPath();
        ctx.moveTo(touchTrail[0].x, touchTrail[0].y);
        for (let i = 1; i < touchTrail.length; i++) {
          ctx.lineTo(touchTrail[i].x, touchTrail[i].y);
        }
        ctx.strokeStyle = 'rgba(255, 255, 200, 0.85)';
        ctx.lineWidth = 6;
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        ctx.shadowColor = '#ffbb00';
        ctx.shadowBlur = 18;
        ctx.stroke();
        ctx.shadowColor = 'transparent';
        ctx.shadowBlur = 0;
        
        // Batasi panjang trail
        if (touchTrail.length > 20) {
          touchTrail.shift();
        }
      }
      
      animationId = requestAnimationFrame(gameLoop);
    }

    // ============ TOUCH HANDLERS (KHUSUS MOBILE) ============
    function getCanvasTouchPos(touch) {
      const rect = canvas.getBoundingClientRect();
      const scaleX = W / rect.width;
      const scaleY = H / rect.height;
      
      return {
        x: Math.min(Math.max((touch.clientX - rect.left) * scaleX, 0), W),
        y: Math.min(Math.max((touch.clientY - rect.top) * scaleY, 0), H)
      };
    }

    function handleTouchStart(e) {
      e.preventDefault();
      if (!gameActive) return;
      
      const touch = e.touches[0];
      if (!touch) return;
      
      touchActive = true;
      const pos = getCanvasTouchPos(touch);
      lastTouchPos = { x: pos.x, y: pos.y };
      currentTouchPos = { x: pos.x, y: pos.y };
      touchTrail = [{ x: pos.x, y: pos.y }];
    }

    function handleTouchMove(e) {
      e.preventDefault();
      if (!touchActive || !gameActive) return;
      
      const touch = e.touches[0];
      if (!touch) return;
      
      const pos = getCanvasTouchPos(touch);
      currentTouchPos = { x: pos.x, y: pos.y };
      
      // Tambahkan ke trail
      touchTrail.push({ x: pos.x, y: pos.y });
      
      // Cek slice antara posisi sebelumnya dan sekarang
      checkSlice(lastTouchPos.x, lastTouchPos.y, currentTouchPos.x, currentTouchPos.y);
      
      // Update posisi terakhir
      lastTouchPos = { x: currentTouchPos.x, y: currentTouchPos.y };
    }

    function handleTouchEnd(e) {
      e.preventDefault();
      touchActive = false;
      touchTrail = [];
      
      // Reset combo setelah sentuhan berakhir
      clearTimeout(comboTimer);
      comboTimer = setTimeout(() => {
        comboCount = 0;
      }, 300);
    }

    function handleTouchCancel(e) {
      e.preventDefault();
      touchActive = false;
      touchTrail = [];
    }

    // Nonaktifkan mouse events sepenuhnya (hanya touch)
    function disableMouseEvents() {
      canvas.addEventListener('mousedown', (e) => e.preventDefault());
      canvas.addEventListener('mousemove', (e) => e.preventDefault());
      canvas.addEventListener('mouseup', (e) => e.preventDefault());
      canvas.style.pointerEvents = 'auto'; // tetap bisa touch
    }

    // Binding event listeners
    function bindEvents() {
      // Touch events (mobile)
      canvas.addEventListener('touchstart', handleTouchStart, { passive: false });
      canvas.addEventListener('touchmove', handleTouchMove, { passive: false });
      canvas.addEventListener('touchend', handleTouchEnd, { passive: false });
      canvas.addEventListener('touchcancel', handleTouchCancel, { passive: false });
      
      // Mencegah gesture browser (zoom, scroll)
      document.addEventListener('gesturestart', (e) => e.preventDefault());
      document.addEventListener('gesturechange', (e) => e.preventDefault());
      document.addEventListener('gestureend', (e) => e.preventDefault());
      
      // Mencegah double-tap zoom
      document.addEventListener('dblclick', (e) => {
        if (e.target === canvas || canvas.contains(e.target)) {
          e.preventDefault();
        }
      });
      
      disableMouseEvents();
    }

    // Tombol restart
    document.getElementById('restartButton').addEventListener('click', (e) => {
      e.preventDefault();
      resetGame();
    });
    
    // Hindari klik ganda yang menyebabkan zoom
    document.getElementById('restartButton').addEventListener('touchstart', (e) => {
      e.preventDefault();
      resetGame();
    });

    // Inisialisasi
    function init() {
      resizeCanvas();
      bindEvents();
      resetGame();
      if (animationId) cancelAnimationFrame(animationId);
      gameLoop();
    }

    // Tangani perubahan orientasi layar
    window.addEventListener('orientationchange', () => {
      setTimeout(() => {
        resizeCanvas();
        // Update radius buah yang ada
        fruits.forEach(f => {
          f.radius = f.type.radius * (W / 500);
        });
      }, 300);
    });

    init();
  })();
</script>
</body>
</html>
