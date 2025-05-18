---
layout: default
title: Hot Dog
permalink: /hotdog/
---

<style>
  body {
    background-color: #f5f5f5;
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    overflow-x: hidden;
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
    width: 150px;
    cursor: pointer;
    transition: transform 0.2s;
    margin-bottom: 30px;
  }
  
  #hotdog-img:hover {
    transform: scale(1.1);
  }

  /* Battle arena */
  #battle-container {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #000;
    z-index: 1000;
    overflow: hidden;
  }
  
  #battle-arena {
    position: relative;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, #444, #000);
  }
  
  #battle-hotdog {
    position: absolute;
    width: 150px;
    left: 30%;
    bottom: 20%;
    transform: translateX(-50%);
    z-index: 2;
  }
  
  #battle-gorilla {
    position: absolute;
    width: 200px;
    right: -200px;
    bottom: 20%;
    z-index: 2;
  }
  
  #result-message {
    position: absolute;
    top: 20%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-size: 36px;
    font-weight: bold;
    text-shadow: 0 0 10px #000;
    opacity: 0;
    z-index: 3;
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
    display: none;
  }
  
  /* Animations */
  @keyframes gorillaEntrance {
    0% { right: -200px; }
    70% { right: 35%; }
    100% { right: 30%; }
  }
  
  @keyframes clash {
    0% { transform: translateX(0); }
    50% { transform: translateX(-20px); }
    100% { transform: translateX(0); }
  }
  
  @keyframes winner {
    0% { transform: scale(1); }
    50% { transform: scale(1.2); }
    100% { transform: scale(1); }
  }
  
  @keyframes loser {
    100% { transform: rotate(90deg) translateY(100px); opacity: 0.5; }
  }
  
  @keyframes victoryDance {
    0% { transform: translateY(0); }
    50% { transform: translateY(-30px); }
    100% { transform: translateY(0); }
  }
  
  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
  
  .confetti {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: #f00;
    opacity: 0;
  }
</style>

<!-- Normal page content -->
<div id="main-content">
  <h1 id="hotdog-title">🌭 Hot Dog</h1>
  <img id="hotdog-img" src="/hotdog.jpg" alt="Hot Dog">
  <p>Click the hot dog for a surprise battle!</p>
</div>

<!-- Battle container -->
<div id="battle-container">
  <button id="close-battle">✕ Close</button>
  <div id="battle-arena">
    <img id="battle-hotdog" src="/hotdog.jpg" alt="Hot Dog">
    <img id="battle-gorilla" src="/gorilla.png" alt="Gorilla">
    <div id="result-message"></div>
  </div>
</div>

<script>
  const hotdogImg = document.getElementById('hotdog-img');
  const mainContent = document.getElementById('main-content');
  const battleContainer = document.getElementById('battle-container');
  const battleHotdog = document.getElementById('battle-hotdog');
  const battleGorilla = document.getElementById('battle-gorilla');
  const resultMessage = document.getElementById('result-message');
  const closeButton = document.getElementById('close-battle');
  const battleArena = document.getElementById('battle-arena');
  
  hotdogImg.addEventListener('click', startBattle);
  closeButton.addEventListener('click', () => location.reload());
  
  function startBattle() {
    mainContent.style.display = 'none';
    battleContainer.style.display = 'block';
    
    // Reset positions and styles
    battleHotdog.style.left = '30%';
    battleHotdog.style.transform = 'translateX(-50%)';
    battleHotdog.style.animation = '';
    battleHotdog.style.opacity = '1';
    
    battleGorilla.style.right = '-200px';
    battleGorilla.style.transform = '';
    battleGorilla.style.animation = '';
    battleGorilla.style.opacity = '1';
    
    resultMessage.style.opacity = '0';
    closeButton.style.display = 'none';
    
    // Gorilla entrance animation
    battleGorilla.style.animation = 'gorillaEntrance 1.5s forwards';
    
    // After gorilla arrives, start the clash
    setTimeout(() => {
      // Both characters move toward each other
      battleHotdog.style.animation = 'clash 0.5s forwards';
      battleGorilla.style.animation = 'clash 0.5s forwards';
      
      // Determine winner by coin flip
      setTimeout(() => {
        const winner = Math.random() < 0.5 ? 'hotdog' : 'gorilla';
        showResult(winner);
      }, 500);
    }, 1500);
  }
  
  function showResult(winner) {
    if (winner === 'hotdog') {
      resultMessage.textContent = '🌭 HOT DOG WINS! 🌭';
      battleGorilla.style.animation = 'loser 1s forwards';
      battleHotdog.style.animation = 'victoryDance 0.5s infinite';
      createConfetti();
    } else {
      resultMessage.textContent = '🦍 GORILLA WINS! 🦍';
      battleHotdog.style.animation = 'loser 1s forwards';
      battleGorilla.style.animation = 'victoryDance 0.5s infinite';
      createConfetti();
    }
    
    resultMessage.style.animation = 'fadeIn 1s forwards';
    closeButton.style.display = 'block';
  }
  
  function createConfetti() {
    const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff'];
    for (let i = 0; i < 50; i++) {
      const confetti = document.createElement('div');
      confetti.className = 'confetti';
      confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
      confetti.style.left = Math.random() * 100 + '%';
      confetti.style.top = '-10px';
      confetti.style.opacity = '1';
      confetti.style.animation = `fall ${Math.random() * 2 + 1}s linear forwards`;
      battleArena.appendChild(confetti);
      
      // Keyframes for falling animation
      const style = document.createElement('style');
      style.textContent = `
        @keyframes fall {
          to {
            transform: translateY(${window.innerHeight + 10}px) rotate(${Math.random() * 360}deg);
            opacity: 0;
          }
        }
      `;
      document.head.appendChild(style);
    }
  }
</script>
