---
layout: default
title: Hot Dog
permalink: /hotdog/
---

<style>
  body {
    background-color: #000;
    color: #fff;
    font-family: Arial, sans-serif;
    text-align: center;
    padding-top: 100px;
    cursor: default;
    user-select: none;
  }

  #hotdog-title {
    font-size: 72px;
    transition: all 0.3s;
  }

  #hotdog-title:hover {
    color: #ff0000;
    cursor: pointer;
  }

  #battle-container {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.9);
    z-index: 100;
  }

  /* [Previous battle CSS styles would go here - kept hidden] */
</style>

<div id="hotdog-title">🌭 Hot Dog</div>

<!-- Hidden battle container (initially invisible) -->
<div id="battle-container">
  <!-- [All the previous battle HTML would go here] -->
</div>

<script>
  // Easter egg activation
  const title = document.getElementById('hotdog-title');
  const battleContainer = document.getElementById('battle-container');
  let clickCount = 0;
  let secretCode = [4, 4, 4, 2]; // Sequence: 4 clicks, 4 clicks, 4 clicks, 2 clicks

  title.addEventListener('click', function() {
    clickCount++;
    
    // Check if user has entered the secret code
    if (clickCount === secretCode.reduce((a,b) => a + b, 0)) {
      // Load all the battle elements
      battleContainer.innerHTML = `
        <!-- [Insert all the previous battle HTML here] -->
      `;
      
      // Load all the battle JavaScript here
      const battleScript = document.createElement('script');
      battleScript.textContent = `
        // [Insert all the previous battle JavaScript here]
      `;
      battleContainer.appendChild(battleScript);
      
      // Show the battle
      battleContainer.style.display = 'block';
      document.body.style.overflow = 'hidden';
      clickCount = 0;
    }
    
    // Reset count if too much time passes between clicks
    setTimeout(() => {
      if (clickCount > 0 && clickCount < secretCode.reduce((a,b) => a + b, 0)) {
        clickCount = 0;
      }
    }, 2000);
  });

  // Close battle if clicked outside
  battleContainer.addEventListener('click', function(e) {
    if (e.target === this) {
      this.style.display = 'none';
      document.body.style.overflow = 'auto';
    }
  });
</script>
