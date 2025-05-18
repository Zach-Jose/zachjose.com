---
layout: default
title: Hot Dog
permalink: /hotdog/
---

<style>
  /* Normal page styles */
  body {
    background-color: #f5f5f5;
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
  }
  
  #main-content {
    padding: 50px 20px;
    max-width: 800px;
    margin: 0 auto;
  }
  
  #hotdog-title {
    font-size: 72px;
    color: #333;
    margin-bottom: 20px;
  }
  
  #hotdog-img {
    width: 300px;
    max-width: 100%;
    margin: 20px auto;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    cursor: pointer;
    transition: transform 0.2s;
  }
  
  #hotdog-img:hover {
    transform: scale(1.05);
  }

  /* Battle arena styles */
  #battle-container {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #121212;
    z-index: 1000;
    overflow: auto;
  }
  
  #battle-arena {
    position: relative;
    width: 90%;
    max-width: 800px;
    height: 400px;
    margin: 30px auto;
    background: #1a1a1a;
    border: 3px solid #333;
    border-radius: 10px;
    overflow: hidden;
  }
  
  #battle-hotdog {
    position: absolute;
    width: 120px;
    left: 50px;
    bottom: 50px;
    z-index: 2;
  }
  
  #battle-gorilla {
    position: absolute;
    width: 180px;
    right: 100px;
    bottom: 50px;
    z-index: 2;
    display: none;
  }
  
  .health-container {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 20px auto;
    max-width: 800px;
  }
  
  .health-bar {
    width: 300px;
    height: 25px;
    background-color: #333;
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    border: 2px solid #444;
  }
  
  .health-fill {
    height: 100%;
    width: 100%;
    transition: width 0.3s;
  }
  
  #hotdog-health .health-fill {
    background: linear-gradient(to right, #ff5e62, #ff2400);
  }
  
  #gorilla-health .health-fill {
    background: linear-gradient(to right, #4facfe, #00f2fe);
  }
  
  .health-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-size: 12px;
    font-weight: bold;
    text-shadow: 1px 1px 2px #000;
  }
  
  /* Animations */
  .punch {
    animation: punch 0.3s linear;
  }
  
  @keyframes punch {
    0% { transform: translateX(0); }
    50% { transform: translateX(-15px); }
    100% { transform: translateX(0); }
  }
  
  .gorilla-attack {
    animation: gorillaAttack 0.5s;
  }
  
  @keyframes gorillaAttack {
    0% { transform: scale(0.5); opacity: 0; }
    100% { transform: scale(1); opacity: 1; }
  }
  
  .victory {
    animation: victory 1s infinite alternate;
  }
  
  @keyframes victory {
    0% { transform: translateY(0); }
    100% { transform: translateY(-10px); }
  }
  
  .defeat {
    filter: grayscale(80%) brightness(60%);
    animation: defeat 0.5s forwards;
  }
  
  @keyframes defeat {
    100% { transform: rotate(90deg); }
  }
  
  #battle-log {
    width: 90%;
    max-width: 800px;
    height: 100px;
    margin: 20px auto;
    padding: 10px;
    background-color: rgba(0,0,0,0.5);
    color: white;
    border-radius: 5px;
    overflow-y: auto;
    font-family: monospace;
  }
  
  #close-battle {
    position: fixed;
    top: 20px;
    right: 20px;
    background: #e74c3c;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 8px 15px;
    cursor: pointer;
    z-index: 1001;
  }
</style>

<!-- Normal page content -->
<div id="main-content">
  <h1 id="hotdog-title">🌭 Hot Dog</h1>
  <img id="hotdog-img" src="/hotdog.jpg" alt="Hot Dog">
  <p id="hotdog-description">Click the hot dog to reveal a surprise...</p>
</div>

<!-- Battle container (hidden by default) -->
<div id="battle-container">
  <button id="close-battle">✕ Close Battle</button>
  <h1 style="color: white; text-align: center;">GORILLA VS. HOT DOG SHOWDOWN</h1>
  
  <div class="health-container">
    <div class="health-bar" id="hotdog-health">
      <div class="health-fill" style="width: 100%"></div>
      <div class="health-text">Hot Dog: 100%</div>
    </div>
    <div class="health-bar" id="gorilla-health">
      <div class="health-fill" style="width: 100%"></div>
      <div class="health-text">Gorilla: 100%</div>
    </div>
  </div>
  
  <div id="battle-arena">
    <img id="battle-hotdog" src="/hotdog.jpg" alt="Hot Dog">
    <img id="battle-gorilla" src="/gorilla.png" alt="Gorilla">
  </div>
  
  <div id="battle-log"></div>
</div>

<script>
  // Get DOM elements
  const hotdogImg = document.getElementById('hotdog-img');
  const mainContent = document.getElementById('main-content');
  const battleContainer = document.getElementById('battle-container');
  const closeButton = document.getElementById('close-battle');
  const battleGorilla = document.getElementById('battle-gorilla');
  const battleLog = document.getElementById('battle-log');
  
  // Start battle when hot dog is clicked
  hotdogImg.addEventListener('click', startBattle);
  
  // Close battle when X is clicked
  closeButton.addEventListener('click', function() {
    battleContainer.style.display = 'none';
    mainContent.style.display = 'block';
    location.reload();
  });
  
  function startBattle() {
    // Hide main content and show battle
    mainContent.style.display = 'none';
    battleContainer.style.display = 'block';
    
    // Initialize battle state
    let hotdogHP = 100;
    let gorillaHP = 100;
    let battleInterval;
    
    // Show gorilla with animation
    battleGorilla.style.display = 'block';
    battleGorilla.classList.add('gorilla-attack');
    
    // Clear log and add first message
    battleLog.innerHTML = '';
    addLog('🚨 A wild gorilla appears!');
    
    // Start auto-battle after 1 second
    setTimeout(() => {
      addLog('⚔️ The battle begins!');
      battleInterval = setInterval(performAttack, 800);
    }, 1000);
    
    function addLog(message) {
      const entry = document.createElement('div');
      entry.textContent = message;
      battleLog.appendChild(entry);
      battleLog.scrollTop = battleLog.scrollHeight;
    }
    
    function updateHealth() {
      document.querySelector('#hotdog-health .health-fill').style.width = `${hotdogHP}%`;
      document.querySelector('#gorilla-health .health-fill').style.width = `${gorillaHP}%`;
      document.querySelector('#hotdog-health .health-text').textContent = `Hot Dog: ${hotdogHP}%`;
      document.querySelector('#gorilla-health .health-text').textContent = `Gorilla: ${gorillaHP}%`;
    }
    
    function performAttack() {
      // Random damage (5-20)
      const damage = Math.floor(Math.random() * 16) + 5;
      const isCritical = Math.random() < 0.1; // 10% critical chance
      const finalDamage = isCritical ? damage * 2 : damage;
      
      // Random attacker (60% gorilla, 40% hot dog)
      const attacker = Math.random() < 0.6 ? 'gorilla' : 'hotdog';
      
      if (attacker === 'gorilla') {
        hotdogHP = Math.max(0, hotdogHP - finalDamage);
        document.getElementById('battle-hotdog').classList.add('punch');
        addLog(`🦍 Gorilla hits for ${finalDamage} damage${isCritical ? ' (CRITICAL!)' : ''}`);
      } else {
        gorillaHP = Math.max(0, gorillaHP - finalDamage);
        document.getElementById('battle-gorilla').classList.add('punch');
        addLog(`🌭 Hot dog fights back for ${finalDamage} damage${isCritical ? ' (CRITICAL!)' : ''}`);
      }
      
      // Remove punch animation
      setTimeout(() => {
        document.getElementById('battle-hotdog').classList.remove('punch');
        document.getElementById('battle-gorilla').classList.remove('punch');
      }, 300);
      
      updateHealth();
      
      // Check for winner
      if (hotdogHP <= 0) {
        endBattle('gorilla');
      } else if (gorillaHP <= 0) {
        endBattle('hotdog');
      }
    }
    
    function endBattle(winner) {
      clearInterval(battleInterval);
      
      if (winner === 'gorilla') {
        addLog('💀 The gorilla WINS! Hot dog was defeated.');
        document.getElementById('battle-hotdog').classList.add('defeat');
        document.getElementById('battle-gorilla').classList.add('victory');
      } else {
        addLog('🎉 The hot dog WINS! Gorilla was defeated.');
        document.getElementById('battle-gorilla').classList.add('defeat');
        document.getElementById('battle-hotdog').classList.add('victory');
      }
    }
  }
</script>
