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

<button id="partyButton" style="padding: 10px; font-size: 16px; cursor: pointer;">Start the Party!</button>

<audio id="song" src="/Phil.mp3"></audio>
<img id="cat" src="/cat-dance.gif" alt="Cat" style="position: absolute; bottom: -100px; left: 50%; width: 100px; display: none;">
<img id="discoBall" src="/disco.gif" alt="Disco Ball" style="position: absolute; top: -150px; left: 50%; width: 100px; display: none;">
<div id="fireworks"></div>

<style>
  @keyframes dance {
    0%, 100% { transform: rotate(0deg); }
    25% { transform: rotate(10deg); }
    50% { transform: rotate(-10deg); }
    75% { transform: rotate(10deg); }
  }
  
  @keyframes flash {
    0%, 100% { background-color: white; }
    50% { background-color: black; }
  }
  
  @keyframes fireworks {
    0% { opacity: 0; transform: scale(0.5); }
    50% { opacity: 1; transform: scale(1.5); }
    100% { opacity: 0; transform: scale(2); }
  }
  
  .flashing { animation: flash 0.2s infinite alternate; }
  .dancing { animation: dance 0.2s infinite alternate; }
  .firework { 
    position: absolute; width: 20px; height: 20px; border-radius: 50%; 
    background-color: red; animation: fireworks 1s ease-out; 
  }
</style>

<script>
  document.getElementById("partyButton").addEventListener("click", function() {
    let song = document.getElementById("song");
    let cat = document.getElementById("cat");
    let discoBall = document.getElementById("discoBall");
    let body = document.body;

    // Play the song
    song.play();

    // Show the cat and disco ball
    cat.style.display = "block";
    cat.style.bottom = "50px";
    cat.style.left = "50%";
    
    discoBall.style.display = "block";
    discoBall.style.top = "10px";

    // Make the cat dance
    cat.classList.add("dancing");

    // Flashing lights effect
    body.classList.add("flashing");

    // Fireworks
    function createFirework() {
      let firework = document.createElement("div");
      firework.classList.add("firework");
      firework.style.left = Math.random() * window.innerWidth + "px";
      firework.style.top = Math.random() * window.innerHeight + "px";
      firework.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
      document.getElementById("fireworks").appendChild(firework);
      
      setTimeout(() => firework.remove(), 1000);
    }
    
    let fireworkInterval = setInterval(createFirework, 300);

    // Stop the dance and lights after 11 seconds
    setTimeout(() => {
      cat.classList.remove("dancing");
      body.classList.remove("flashing");
      discoBall.style.display = "none";
      clearInterval(fireworkInterval);

      // Make the cat walk away
      cat.style.transition = "left 2s ease-in-out, bottom 1s ease-in-out";
      cat.style.left = "110%";
      setTimeout(() => { cat.style.display = "none"; }, 2000);
    }, 11000);
  });
</script>

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
