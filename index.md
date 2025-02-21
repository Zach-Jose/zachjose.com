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
