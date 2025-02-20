---
layout: default
title: Phone Number Input
---

<h2>Enter Your Phone Number</h2>
<form id="phoneForm">
  <label for="phone">Phone Number:</label>
  <input type="tel" id="phone" name="phone" placeholder="e.g., 123-456-7890" required>
  <button type="submit">Submit</button>
</form>

<p id="result"></p>

<script>
  document.getElementById('phoneForm').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent the form from submitting

    // Generate a random number
    const randomNumber = Math.floor(Math.random() * 1000000);

    // Display the result
    document.getElementById('result').innerText = `Your random number is: ${randomNumber}`;
  });
</script>
