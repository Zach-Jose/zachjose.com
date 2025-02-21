---
layout: default
title: Every Day with Zach Jose
---

<a href="https://giving.younglife.org/s/?GiftType=Staff&Name=ZachJose&Sponsoring=Zach%20Jose&AppealCodeId=70141000000tvBDAAY&BypassDesignationPage=false&MissionUnitId=a2s410000002wa2AAA&MissionUnitName=Greater%20Roseville%2FAntelope&ClassCodeId=a2j41000000Nj93AAC&ClassCodeName=Operating&StaffId=0034100002PWJ3WAAX&StaffName=Zachariah%20Jose">Click here to donate to Young Life!</a>

[Phone Number Input](/phone-input.html)

# Welcome to My Website  
[Click here to visit my YouTube Channel](https://www.youtube.com/@zachariahjose5622)

<button onclick="document.getElementById('message').innerText='You clicked the button! 🎉'">
  Click Me!
</button>

<p id="message">Click the button to see something cool.</p>



<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Every Day with Zach Jose</title>
  <link rel="stylesheet" href="styles.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bangers&display=swap" rel="stylesheet">
</head>
<body>

  <div class="banner">
    <h1>Welcome to Zach Jose Academy</h1>
  </div>

  <div class="chalkboard">
    <h2>Zach’s Latest Video</h2>
    <p><a href="#">Check it out here!</a></p>
    <iframe width="560" height="315" src="https://www.youtube.com/watch?v=jf1yDKMbp_k" frameborder="0" allowfullscreen></iframe>
  </div>

  <div class="register">
    <p>📚 Register for Zach 101 Now!</p>
  </div>

</body>


<p>Total Visits: <span id="counter">Loading...</span></p>

<script>
  fetch("https://api.countapi.xyz/update/zachjose.com/visits/?amount=1")
    .then(response => response.json())
    .then(data => {
      document.getElementById("counter").innerText = data.value;
    })
    .catch(error => {
      console.error("Error fetching count:", error);
      document.getElementById("counter").innerText = "Error";
    });
</script>
