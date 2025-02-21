<a href="https://giving.younglife.org/s/?GiftType=Staff&Name=ZachJose&Sponsoring=Zach%20Jose&AppealCodeId=70141000000tvBDAAY&BypassDesignationPage=false&MissionUnitId=a2s410000002wa2AAA&MissionUnitName=Greater%20Roseville%2FAntelope&ClassCodeId=a2j41000000Nj93AAC&ClassCodeName=Operating&StaffId=0034100002PWJ3WAAX&StaffName=Zachariah%20Jose">Click here to donate to Young Life!</a>

# Welcome to My Website  
[Click here to visit my YouTube Channel](https://www.youtube.com/@zachariahjose5622)

<p id="message">Click the button to see something cool.</p>
<button onclick="document.getElementById('message').innerText='You clicked the button! 🎉'">
  Click Me!
</button>



<button id="invertButton" style="padding: 10px; font-size: 16px; cursor: pointer;">Invert Colors</button>

<script>
  document.getElementById("invertButton").addEventListener("click", function() {
    document.body.style.filter = document.body.style.filter === "invert(1)" ? "none" : "invert(1)";
  });
</script>

---


<style>
  @keyframes flash {
    0%, 50%, 100% { background-color: white; }
    25%, 75% { background-color: black; }
  }
</style>

<script>
  function startParty() {
    // Play music
    document.getElementById("song").play();

    // Show and animate the cat
    let cat = document.getElementById("cat");
    cat.style.display = "block";
    cat.style.width = "250px"; // Make the cat bigger
    cat.style.position = "absolute";
    cat.style.bottom = "50px";
    cat.style.left = "10%";
    
    let moveRight = true;
    let catInterval = setInterval(() => {
      let leftPos = parseInt(cat.style.left);
      cat.style.left = moveRight ? (leftPos + 10) + "px" : (leftPos - 10) + "px";
      if (leftPos > window.innerWidth - 300) moveRight = false;
      if (leftPos < 10) moveRight = true;
    }, 100);

    // Show the disco ball
    let discoBall = document.getElementById("discoBall");
    discoBall.style.display = "block";
    discoBall.style.width = "200px"; // Make the disco ball bigger

    // Flash effect for only 1 second
    document.body.style.animation = "flash 1s";

    // Stop everything after 11 seconds
    setTimeout(() => {
      clearInterval(catInterval);
      cat.style.display = "none";
      discoBall.style.display = "none";
      document.body.style.animation = "";
    }, 11000);
  }
</script>

<button onclick="startParty()">Start Party!</button>
<audio id="song" src="/Phil.mp3"></audio>
<img id="cat" src="/cat-dance.gif" style="display: none;">
<img id="discoBall" src="/disco.gif" style="display: none;">


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
