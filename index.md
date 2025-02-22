<link rel="stylesheet" type="text/css" href="/style.css">

<a href="https://giving.younglife.org/s/?GiftType=Staff&Name=ZachJose&Sponsoring=Zach%20Jose&AppealCodeId=70141000000tvBDAAY&BypassDesignationPage=false&MissionUnitId=a2s410000002wa2AAA&MissionUnitName=Greater%20Roseville%2FAntelope&ClassCodeId=a2j41000000Nj93AAC&ClassCodeName=Operating&StaffId=0034100002PWJ3WAAX&StaffName=Zachariah%20Jose">Click here to donate to Young Life!</a>

[Check out the Hot Dog! 🌭](/hotdog/)


<button onclick="setPapyrus()">Make It Papyrus</button>

<script>
  function setPapyrus() {
    document.body.classList.toggle("papyrus");
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

---

<style>
  @keyframes flash {
    0%, 50%, 100% { background-color: white; }
    25%, 75% { background-color: black; }
  }
</style>

<script>
  let initialPositionsSet = false;
  let initialCatLeft = "10%";
  let initialDiscoLeft = "50%";

  function startParty() {
    // Play a new instance of the song every click
    let newSong = new Audio("/APT.mp3");
    newSong.play();

    // Create a new cat GIF
    let cat = document.createElement("img");
    cat.src = "/cat-dance.gif";
    cat.style.width = "250px"; // Bigger cat
    cat.style.position = "absolute";
    cat.style.bottom = "50px";

    // Set initial or random position for the cat
    if (!initialPositionsSet) {
      cat.style.left = initialCatLeft;
    } else {
      cat.style.left = Math.random() * (window.innerWidth - 300) + "px";
    }
    document.body.appendChild(cat);

    // Animate the cat moving left & right
    let moveRight = true;
    let moveInterval = setInterval(() => {
      let leftPos = parseInt(cat.style.left);
      cat.style.left = moveRight ? (leftPos + 10) + "px" : (leftPos - 10) + "px";
      if (leftPos > window.innerWidth - 300) moveRight = false;
      if (leftPos < 10) moveRight = true;
    }, 100);

    // Create a new disco ball
    let discoBall = document.createElement("img");
    discoBall.src = "/disco.gif";
    discoBall.style.width = "200px"; // Bigger disco ball
    discoBall.style.position = "absolute";
    discoBall.style.top = "10px";

    // Set initial or random position for the disco ball
    if (!initialPositionsSet) {
      discoBall.style.left = initialDiscoLeft;
    } else {
      discoBall.style.left = Math.random() * (window.innerWidth - 200) + "px";
    }
    document.body.appendChild(discoBall);

    // Flash effect for only 1 second
    document.body.style.animation = "flash 1s";

    // Remove everything after 11 seconds
    setTimeout(() => {
      clearInterval(moveInterval);
      cat.remove();
      discoBall.remove();
    }, 11000);

    // Mark initial positions as set after the first click
    initialPositionsSet = true;
  }
</script>

<button onclick="startParty()">Start Party!</button>

---

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Every Day with Zach Jose</title>
  <link rel="stylesheet" href="styles.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bangers&display=swap" rel="stylesheet">
</head>



<p id="visitorCounter" style="font-size: 14px; font-weight: bold;"></p>

<script>
  function updateVisitorCount() {
    // Define start date: April 5, 2000 (UTC)
    const startDate = new Date("2000-04-05T00:00:00Z");

    // Get current time in UTC
    const now = new Date();

    // Calculate hours passed since startDate
    const hoursPassed = Math.floor((now - startDate) / (1000 * 60 * 60));

    // Display the counter in the footer
    document.getElementById("visitorCounter").innerText = "Total Visitors: " + hoursPassed;
  }

  updateVisitorCount(); // Run function when page loads
</script>
