<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Every Day with Zach Jose</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&display=swap" rel="stylesheet">
</head>
<body>
    <link rel="stylesheet" type="text/css" href="/style.css"><a href="https://giving.younglife.org/s/?GiftType=Staff&Name=ZachJose&Sponsoring=Zach%20Jose&AppealCodeId=70141000000tvBDAAY&BypassDesignationPage=false&MissionUnitId=a2s410000002wa2AAA&MissionUnitName=Greater%20Roseville%2FAntelope&ClassCodeId=a2j41000000Nj93AAC&ClassCodeName=Operating&StaffId=0034100002PWJ3WAAX&StaffName=Zachariah%20Jose">Click here to donate to Young Life!</a>

<button id="papyrusButton" onclick="togglePapyrus()">Make It Papyrus</button>

<script>
  function togglePapyrus() {
    const button = document.getElementById("papyrusButton");
    document.body.classList.toggle("papyrus");

    if (document.body.classList.contains("papyrus")) {
      button.textContent = "Go Back";
    } else {
      button.textContent = "Make It Papyrus";
    }
  }
</script>

<div id="top-right-menu">
<details>
  <summary><strong>🔽 Menu</strong></summary>
  <ul>
    <li><a href="/hotdog">🌭 Hot Dog</a></li>
    <li><a href="/phone-input">📞 Phone Number</a></li>
  </ul>
</details>
</div>

<h1>Zachariah <span id="justice" style="color: blue; cursor: pointer; text-decoration: underline;">Justice</span> Jose</h1>
<img id="batman" src="/i-find-it-weird-weve-yet-to-have-a-scene-of-him-swinging-in-v0-bco5g9e195cc1.jpg" width="150">

<script>
    document.getElementById("justice").addEventListener("click", function() {
        document.body.classList.add("dark");
        let batman = document.getElementById("batman");
        batman.style.opacity = "1";
        batman.style.top = "50px";
        setTimeout(() => {
            batman.style.top = "-200px";
            batman.style.opacity = "0";
            setTimeout(() => document.body.classList.remove("dark"), 1000);
        }, 1500);
    });
</script>

<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        transition: background 1s ease-in-out;
    }
    .dark {
        background: black;
        color: white;
    }
    #batman {
        position: fixed;
        top: -200px;
        left: 50%;
        transform: translateX(-50%) scale(1.5);
        opacity: 0;
        transition: all 0.8s ease-in-out;
    }
</style>

<button onclick="startParty()">Start Party!</button>

<p id="visitorCounter" style="font-size: 14px; font-weight: bold;"></p>

<script>
  function updateVisitorCount() {
    const startDate = new Date("2000-04-05T00:00:00Z");
    const now = new Date();
    const hoursPassed = Math.floor((now - startDate) / (1000 * 60 * 60));
    document.getElementById("visitorCounter").innerText = "Total Visitors: " + hoursPassed;
  }
  updateVisitorCount();
</script>

</body>
</html>