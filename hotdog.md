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
   
