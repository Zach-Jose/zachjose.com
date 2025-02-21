---
layout: default
---

<h2>Enter Your Phone Number</h2>
<form id="phoneForm">
  <label for="phone">Phone Number:</label>
  <input type="tel" id="phone" name="phone" placeholder="e.g., 832-696-6904" required>
  <button type="button" id="rollButton">Roll a Random Number</button>
  <button type="submit">Submit</button>
</form>

<p id="result"></p>

<script>
  document.getElementById('rollButton').addEventListener('click', function() {
    // Generate a random 10-digit phone number in (XXX)-XXX-XXXX format
    const randomPhone = `(${Math.floor(Math.random() * 900 + 100)})-${Math.floor(Math.random() * 900 + 100)}-${Math.floor(Math.random() * 9000 + 1000)}`;
    
    // Set the input value to the generated number
    document.getElementById('phone').value = randomPhone;
  });

  document.getElementById('phoneForm').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent the form from submitting
    
    const phoneNumber = document.getElementById('phone').value;
    
    // Generate a random "odds" fact (just for fun)
    const odds = (1 / Math.pow(10, 10)).toExponential(); // Approximate odds of rolling an exact number
    
    // Display the congratulatory message
    document.getElementById('result').innerHTML = `
      🎉 Congratulations! You have locked in the number: <strong>${phoneNumber}</strong>.<br>
      The odds of rolling this exact number are **${odds}**, which is basically astronomical! 🚀
    `;
  });
</script>
