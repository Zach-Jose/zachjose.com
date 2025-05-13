---
layout: default
title: Ultimate Gorilla vs. Hot Dog
permalink: /hotdog/
---

<style>
  #battle-container {
    position: relative;
    height: 500px;
    width: 800px;
    margin: 30px auto;
    background: #f0f0f0;
    border: 3px solid #333;
    overflow: hidden;
    background-image: url('https://img.freepik.com/free-vector/hand-drawn-colorful-comic-background_23-2148883772.jpg');
    background-size: cover;
  }

  #hotdog {
    position: absolute;
    width: 150px;
    left: 50px;
    bottom: 50px;
    transition: transform 0.2s;
    filter: drop-shadow(5px 5px 5px #222);
  }

  #gorilla {
    position: absolute;
    width: 200px;
    right: -200px;
    bottom: 50px;
    transition: right 1s;
    filter: drop-shadow(5px 5px 5px #222);
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
    background-color: #ddd;
    border-radius: 15px;
    overflow: hidden;
    position: relative;
  }

  .health-fill {
    height: 100%;
    width: 100%;
    background-color: #4CAF50;
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

  #fight-button {
    background: #E74C3C;
    color: white;
  }

  #fight-button:hover {
    background: #C0392B;
    transform: scale(1.05);
  }

  #reset-button {
    background: #3498DB;
    color: white;
  }

  #reset-button:hover {
    background: #2980B9;
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
  }

  @keyframes victory {
    0% { transform: translateY(0); }
    100% { transform: translateY(-20px); }
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
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    border-radius: 10px;
    overflow-y: auto;
    font-family: monospace;
  }

  .log-entry {
    margin: 5px 0;
    padding: 3px;
    border-bottom: 1px solid #444;
  }
</style>

# Ultimate Gorilla vs. Hot Dog Battle 🦍🌭

<div id="health-bars">
  <div class="health-bar" id="hotdog-health">
    <div class="health-fill" style="width: 100%"></div>
    <div class="health-text">Hot Dog: 100%</div>
  </div>
  <div class="health-bar" id="gorilla-health">
    <div class="health-fill" style="width: 100%"></div>
    <div class="health-text">Gorilla: 100%</div>
  </div>
</div>

<div id="battle-container">
  <img id="hotdog" src="https://emojicdn.elk.sh/🌭?size=160" alt="Hot Dog">
  <img id="gorilla" src="https://emojicdn.elk.sh/🦍?size=200" alt="Gorilla">
</div>

<div id="controls">
  <button id="fight-button" class="battle-button">RELEASE THE GORILLA!</button>
  <button id="reset-button" class="battle-button">RESET BATTLE</button>
</div>

<div id="battle-log"></div>

<script>
  // Game state
  const gameState = {
    hotdogHP: 100,
    gorillaHP: 100,
    battleStarted: false,
    gameOver: false
  };

  // DOM elements
  const fightButton = document.getElementById('fight-button');
  const resetButton = document.getElementById('reset-button');
  const hotdog = document.getElementById('hotdog');
  const gorilla = document.getElementById('gorilla');
  const hotdogHealth = document.querySelector('#hotdog-health .health-fill');
  const gorillaHealth = document.querySelector('#gorilla-health .health-fill');
  const hotdogText = document.querySelector('#hotdog-health .health-text');
  const gorillaText = document.querySelector('#gorilla-health .health-text');
  const battleLog = document.getElementById('battle-log');

  // Sound effects
  const sounds = {
    roar: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-monkey-roar-37.mp3'),
    punch: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-boxing-punch-2051.mp3'),
    victory: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-winning-chimes-2015.mp3'),
    defeat: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-arcade-retro-game-over-213.mp3')
  };

  // Add log entry
  function addLog(message) {
    const entry = document.createElement('div');
    entry.className = 'log-entry';
    entry.textContent = message;
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
    fightButton.disabled = true;
    
    if (winner === 'gorilla') {
      addLog('💀 The gorilla has CRUSHED the hot dog!');
      hotdog.classList.add('defeat');
      gorilla.classList.add('victory');
      sounds.victory.play();
    } else {
      addLog('🌭🔥 The hot dog has DEFEATED the gorilla!');
      gorilla.classList.add('defeat');
      hotdog.classList.add('victory');
      sounds.victory.play();
    }
  }

  // Reset battle
  function resetBattle() {
    gameState.hotdogHP = 100;
    gameState.gorillaHP = 100;
    gameState.battleStarted = false;
    gameState.gameOver = false;
    
    hotdog.classList.remove('defeat', 'victory');
    gorilla.classList.remove('defeat', 'victory', 'gorilla-attack');
    gorilla.style.right = '-200px';
    
    updateHealth();
    fightButton.textContent = 'RELEASE THE GORILLA!';
    fightButton.disabled = false;
    battleLog.innerHTML = '';
    addLog('Battle reset! Ready for a new fight!');
  }

  // Attack logic
  function performAttack() {
    if (gameState.gameOver) return;
    
    // Random damage (5-15)
    const damage = Math.floor(Math.random() * 11) + 5;
    
    // Random chance to attack (60% gorilla, 40% hot dog)
    const attacker = Math.random() < 0.6 ? 'gorilla' : 'hotdog';
    
    if (attacker === 'gorilla') {
      gameState.hotdogHP = Math.max(0, gameState.hotdogHP - damage);
      hotdog.classList.add('punch');
      addLog(`🦍 Gorilla hits hot dog for ${damage} damage!`);
    } else {
      gameState.gorillaHP = Math.max(0, gameState.gorillaHP - damage);
      gorilla.classList.add('punch');
      addLog(`🌭 Hot dog fights back for ${damage} damage!`);
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

  // Event listeners
  fightButton.addEventListener('click', function() {
    if (!gameState.battleStarted) {
      // Start the battle
      gorilla.classList.add('gorilla-attack');
      fightButton.textContent = 'FIGHT!';
      gameState.battleStarted = true;
      sounds.roar.play();
      addLog('🦍 The gorilla has entered the arena!');
      addLog('🌭 The hot dog stands its ground!');
    } else if (!gameState.gameOver) {
      performAttack();
    }
  });

  resetButton.addEventListener('click', resetBattle);

  // Reset punch animation when it ends
  hotdog.addEventListener('animationend', () => {
    hotdog.classList.remove('punch');
  });

  gorilla.addEventListener('animationend', () => {
    gorilla.classList.remove('punch');
  });

  // Initial log
  addLog('Welcome to the Ultimate Gorilla vs. Hot Dog Battle!');
</script>

### Battle Instructions:
1. Click "RELEASE THE GORILLA!" to start the battle
2. Click "FIGHT!" to make the combatants attack
3. Watch the health bars and battle log
4. Click "RESET BATTLE" to start over

### Features:
- **Health bars** for both fighters
- **Randomized attacks** (gorilla attacks 60% of the time)
- **Variable damage** (5-15 damage per hit)
- **Victory/defeat animations**
- **Battle log** showing all actions
- **Sound effects** for attacks and outcomes
- **Reset button** to restart the battle
- **Responsive design** that works on most devices

The battle continues until one fighter's health reaches 0, with a random chance for either the gorilla or hot dog to win!
