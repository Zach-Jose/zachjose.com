---
layout: default
title: Random Phone Number Generator
---

<h2>Random Phone Number Generator</h2>
<p>Click the button to generate 10 random phone numbers:</p>
<button id="generateButton">Generate Numbers</button>

<div id="results"></div>

<script>
  // Function to generate a single random phone number
  function generateRandomPhoneNumber() {
    const areaCode = Math.floor(Math.random() * 900) + 100; // Random 3-digit area code (100-999)
    const firstPart = Math.floor(Math.random() * 900) + 100; // Random 3-digit number (100-999)
    const secondPart = Math.floor(Math.random() * 9000) + 1000; // Random 4-digit number (1000-9999)
    return `(${areaCode}) ${firstPart}-${secondPart}`; // Format as (XXX) XXX-XXXX
  }

  // Function to generate 10 random phone numbers
  function generateNumbers() {
    const resultsDiv = document.getElementById('results');
    resultsDiv.innerHTML = ''; // Clear previous results

    for (let i = 0; i < 10; i++) {
      const phoneNumber = generateRandomPhoneNumber();
      const p = document.createElement('p');
      p.textContent = phoneNumber;
      resultsDiv.appendChild(p);
    }
  }

  // Add event listener to the button
  document.getElementById('generateButton').addEventListener('click', generateNumbers);
</script>

<style>
  #generateButton {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
  }

  #generateButton:hover {
    background-color: #0056b3;
  }

  #results {
    margin-top: 20px;
    font-family: monospace;
  }
</style>
