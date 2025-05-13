---
layout: default
title: Ultimate Gorilla vs. Hot Dog
permalink: /hotdog/
---

<style>
  :root {
    --bg-color: #121212;
    --text-color: #f0f0f0;
    --arena-bg: #1e1e1e;
    --border-color: #333;
    --health-bg: #333;
  }

  body {
    background-color: var(--bg-color);
    color: var(--text-color);
    font-family: 'Arial', sans-serif;
  }

  #battle-container {
    position: relative;
    height: 500px;
    width: 800px;
    margin: 30px auto;
    background: var(--arena-bg);
    border: 3px solid var(--border-color);
    overflow: hidden;
    background-image: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://img.freepik.com/free-vector/hand-drawn-colorful-comic-background_23-2148883772.jpg');
    background-size: cover;
    box-shadow: 0 0 30px rgba(255,255,255,0.1);
  }

  #hotdog {
    position: absolute;
    width: 150px;
    left: 50px;
    bottom: 50px;
    transition: transform 0.2s;
    filter: drop-shadow(5px 5px 5px #000);
  }

  #gorilla {
    position: absolute;
    width: 200px;
    right: -200px;
    bottom: 50px;
    transition: right 1s;
    filter: drop-shadow(5px 5px 5px #000);
  }

  #health-bars {
    display: flex;
    justify-content: space-between;
    width: 800px;
    margin: 0 auto 20px;
  }

  .health-bar {
    height: 30px;
    width: 350px;
    background-color: var(--health-bg);
    border-radius: 15px;
    overflow: hidden;
    position: relative;
    border: 2px solid var(--border-color);
  }

  .health-fill {
    height: 100%;
    width: 100%;
    transition: width 0.5s;
  }

  #hotdog-health .health-fill {
    background: linear-gradient(90deg, #FF5733, #C70039);
  }

  #gorilla-health .health-fill {
    background: linear-gradient(90deg, #5DADE2, #2874A6);
  }

  .health-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-weight: bold;
    color: white;
    text-shadow: 1px 1px 2px black;
    font-size: 14px;
  }

  #controls {
    text-align: center;
    margin: 20px 0;
  }

  .battle-button {
    padding: 15px 30px;
    font-size: 20px;
    margin: 0 10px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    font-weight: bold;
    transition: all 0.3s;
  }

  #start-button {
    background: #27AE60;
    color: white;
  }

  #start-button:hover {
    background: #2ECC71;
    transform: scale(1.05);
  }

  #reset-button {
    background: #E74C3C;
    color: white;
  }

  #reset-button:hover {
    background: #C0392B;
    transform: scale(1.05);
  }

  .punch {
    animation: punch 0.3s linear;
  }

  @keyframes punch {
    0% { transform: translateX(0) rotate(0deg); }
    50% { transform: translateX(-20px) rotate(-10deg); }
    100% { transform: translateX(0) rotate(0deg); }
  }

  .gorilla-attack {
    animation: gorillaAttack 1s forwards;
  }

  @keyframes gorillaAttack {
    0% { right: -200px; }
    100% { right: 100px; }
  }

  .victory {
    animation: victory 1s infinite alternate;
    filter: drop-shadow(0 0 10px gold);
  }

  @keyframes victory {
    0% { transform: translateY(0); }
    100% { transform: translateY(-10px); }
  }

  .defeat {
    filter: grayscale(100%) brightness(40%);
    animation: defeat 0.5s forwards;
  }

  @keyframes defeat {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(90deg); }
  }

  #battle-log {
    width: 800px;
    height: 150px;
    margin: 20px auto;
    padding: 10px;
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    border-radius: 10px;
    overflow-y: auto;
    font-family: monospace;
    border: 1px solid var(--border-color);
  }

  .log-entry {
    margin: 5px 0;
    padding: 3px;
    border-bottom: 1px solid #444;
  }

  .crown {
    position: absolute;
    width: 80px;
    top: -40px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 10;
    display: none;
  }

  .critical {
    color: gold;
    font-weight: bold;
    animation: critical 0.5s;
  }

  @keyframes critical {
    0% { transform: scale(1); }
    50% { transform: scale(1.5); }
    100% { transform: scale(1); }
  }

  #battle-speed {
    margin: 20px auto;
    text-align: center;
  }

  #speed-control {
    width: 200px;
    margin: 0 10px;
  }

  #speed-value {
    display: inline-block;
    width: 40px;
  }
</style>

# Ultimate Gorilla vs. Hot Dog Battle 🦍🌭

<div id="health-bars">
  <div class="health-bar" id="hotdog-health">
    <div class="health-fill" style="width: 100%"></div>
    <div class="health-text">Hot Dog: 100%</div>
    <img class="crown" id="hotdog-crown" src="https://emojicdn.elk.sh/👑" alt="Crown">
  </div>
  <div class="health-bar" id="gorilla-health">
    <div class="health-fill" style="width: 100%"></div>
    <div class="health-text">Gorilla: 100%</div>
    <img class="crown" id="gorilla-crown" src="https://emojicdn.elk.sh/👑" alt="Crown">
  </div>
</div>

<div id="battle-container">
  <img id="hotdog" src="https://emojicdn.elk.sh/🌭?size=160" alt="Hot Dog">
  <img id="gorilla" src="https://emojicdn.elk.sh/🦍?size=200" alt="Gorilla">
</div>

<div id="controls">
  <button id="start-button" class="battle-button">START BATTLE</button>
  <button id="reset-button" class="battle-button">RESET</button>
</div>

<div id="battle-speed">
  <span>Battle Speed:</span>
  <input type="range" id="speed-control" min="100" max="1000" value="500">
  <span id="speed-value">0.5x</span>
</div>

<div id="battle-log"></div>

<script>
  // Game state
  const gameState = {
    hotdogHP: 100,
    gorillaHP: 100,
    battleStarted: false,
    gameOver: false,
    battleInterval: null,
    battleSpeed: 500
  };

  // DOM elements
  const startButton = document.getElementById('start-button');
  const resetButton = document.getElementById('reset-button');
  const hotdog = document.getElementById('hotdog');
  const gorilla = document.getElementById('gorilla');
  const hotdogHealth = document.querySelector('#hotdog-health .health-fill');
  const gorillaHealth = document.querySelector('#gorilla-health .health-fill');
  const hotdogText = document.querySelector('#hotdog-health .health-text');
  const gorillaText = document.querySelector('#gorilla-health .health-text');
  const hotdogCrown = document.getElementById('hotdog-crown');
  const gorillaCrown = document.getElementById('gorilla-crown');
  const battleLog = document.getElementById('battle-log');
  const speedControl = document.getElementById('speed-control');
  const speedValue = document.getElementById('speed-value');

  // Sound effects
  const sounds = {
    roar: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-monkey-roar-37.mp3'),
    punch: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-boxing-punch-2051.mp3'),
    victory: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-winning-chimes-2015.mp3'),
    defeat: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-arcade-retro-game-over-213.mp3'),
    critical: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-achievement-bell-600.mp3')
  };

  // Add log entry
  function addLog(message, isCritical = false) {
    const entry = document.createElement('div');
    entry.className = 'log-entry';
    if (isCritical) {
      const span = document.createElement('span');
      span.className = 'critical';
      span.textContent = message;
      entry.appendChild(span);
    } else {
      entry.textContent = message;
    }
    battleLog.appendChild(entry);
    battleLog.scrollTop = battleLog.scrollHeight;
  }

  // Update health bars
  function updateHealth() {
    hotdogHealth.style.width = `${gameState.hotdogHP}%`;
    gorillaHealth.style.width = `${gameState.gorillaHP}%`;
    hotdogText.textContent = `Hot Dog: ${gameState.hotdogHP}%`;
    gorillaText.textContent = `Gorilla: ${gameState.gorillaHP}%`;
  }

  // Check for winner
  function checkWinner() {
    if (gameState.hotdogHP <= 0) {
      endBattle('gorilla');
      return true;
    } else if (gameState.gorillaHP <= 0) {
      endBattle('hotdog');
      return true;
    }
    return false;
  }

  // End battle
  function endBattle(winner) {
    gameState.gameOver = true;
    clearInterval(gameState.battleInterval);
    startButton.disabled = true;
    
    if (winner === 'gorilla') {
      addLog('💀 The gorilla has CRUSHED the hot dog!');
      hotdog.classList.add('defeat');
      gorilla.classList.add('victory');
      gorillaCrown.style.display = 'block';
      sounds.victory.play();
    } else {
      addLog('🌭🔥 The hot dog has DEFEATED the gorilla!');
      gorilla.classList.add('defeat');
      hotdog.classList.add('victory');
      hotdogCrown.style.display = 'block';
      sounds.victory.play();
    }
  }

  // Reset battle
  function resetBattle() {
    clearInterval(gameState.battleInterval);
    
    gameState.hotdogHP = 100;
    gameState.gorillaHP = 100;
    gameState.battleStarted = false;
    gameState.gameOver = false;
    
    hotdog.classList.remove('defeat', 'victory');
    gorilla.classList.remove('defeat', 'victory', 'gorilla-attack');
    gorilla.style.right = '-200px';
    
    hotdogCrown.style.display = 'none';
    gorillaCrown.style.display = 'none';
    
    updateHealth();
    startButton.textContent = 'START BATTLE';
    startButton.disabled = false;
    battleLog.innerHTML = '';
    addLog('Battle ready! Click START to begin the epic fight!');
  }

  // Attack logic
  function performAttack() {
    if (gameState.gameOver) return;
    
    // Random damage (5-20)
    let damage = Math.floor(Math.random() * 16) + 5;
    let isCritical = Math.random() < 0.1; // 10% chance for critical hit
    
    if (isCritical) {
      damage = Math.floor(damage * 1.5); // 50% bonus damage
      sounds.critical.play();
    }
    
    // Random chance to attack (60% gorilla, 40% hot dog)
    const attacker = Math.random() < 0.6 ? 'gorilla' : 'hotdog';
    
    if (attacker === 'gorilla') {
      gameState.hotdogHP = Math.max(0, gameState.hotdogHP - damage);
      hotdog.classList.add('punch');
      addLog(`🦍 Gorilla hits hot dog for ${damage} damage!${isCritical ? ' CRITICAL HIT!' : ''}`, isCritical);
    } else {
      gameState.gorillaHP = Math.max(0, gameState.gorillaHP - damage);
      gorilla.classList.add('punch');
      addLog(`🌭 Hot dog fights back for ${damage} damage!${isCritical ? ' CRITICAL HIT!' : ''}`, isCritical);
    }
    
    sounds.punch.play();
    updateHealth();
    
    // Remove punch animation after it completes
    setTimeout(() => {
      hotdog.classList.remove('punch');
      gorilla.classList.remove('punch');
    }, 300);
    
    checkWinner();
  }

  // Start auto battle
  function startAutoBattle() {
    if (gameState.battleStarted) return;
    
    gameState.battleStarted = true;
    startButton.disabled = true;
    gorilla.classList.add('gorilla-attack');
    sounds.roar.play();
    addLog('🦍 The gorilla has entered the arena!');
    addLog('🌭 The hot dog stands its ground!');
    
    // Start attacking after gorilla enters
    setTimeout(() => {
      addLog('⚔️ The battle begins!');
      gameState.battleInterval = setInterval(performAttack, gameState.battleSpeed);
    }, 1000);
  }

  // Event listeners
  startButton.addEventListener('click', startAutoBattle);
  resetButton.addEventListener('click', resetBattle);

  speedControl.addEventListener('input', function() {
    gameState.battleSpeed = 1100 - this.value; // Invert so higher value = faster
    const speedDisplay = (1000 / gameState.battleSpeed).toFixed(1);
    speedValue.textContent = `${speedDisplay}x`;
    
    if (gameState.battleInterval) {
      clearInterval(gameState.battleInterval);
      gameState.battleInterval = setInterval(performAttack, gameState.battleSpeed);
    }
  });

  // Initial setup
  resetBattle();
</script>

### Battle Features:
- **Auto-battling system** - Watch the fight unfold automatically
- **Adjustable speed** - Control how fast the battle progresses
- **Critical hits** - 10% chance for bonus damage
- **Victory crowns** - The winner gets a golden crown 👑
- **Dark theme** - Easy on the eyes for extended viewing
- **Detailed battle log** - Tracks every move
- **Sound effects** - For punches, crits, and victory

### How It Works:
1. Click **START BATTLE** to begin the automatic fight
2. Use the slider to adjust battle speed
3. Watch as the gorilla and hot dog trade blows
4. Click **RESET** to start a new battle

The battle continues automatically until one fighter's health reaches 0, with dynamic animations and sound effects throughout!
