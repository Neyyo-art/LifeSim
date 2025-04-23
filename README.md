# LifeSim

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>BitLife-Style Life Simulator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f7f7f7;
      color: #222;
      text-align: center;
      padding: 2rem;
    }
    button {
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      border: none;
      border-radius: 6px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    #info {
      margin: 20px auto;
      width: 80%;
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 8px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>
  <div id="game">
    <h1>BitLife-Style Life Simulator</h1>
    <div id="info"></div>
    <button onclick="nextYear()">Age Up</button>
    <button onclick="getJob()">Get Job</button>
    <button onclick="relationship()">Relationship</button>
  </div>
  <script>
    let age = 0;
    let career = "Unemployed";
    let partner = "Single";
    let hasChild = false;

    function updateInfo() {
      document.getElementById("info").innerHTML = `
        <strong>Age:</strong> ${age}<br>
        <strong>Job:</strong> ${career}<br>
        <strong>Relationship:</strong> ${partner}<br>
        <strong>Child:</strong> ${hasChild ? "Yes" : "No"}
      `;
    }

    function nextYear() {
      age++;
      if (partner !== "Single" && Math.random() < 0.3 && !hasChild) {
        hasChild = true;
        alert("You had an unplanned pregnancy!");
      }
      updateInfo();
    }

    function getJob() {
      if (age < 16) {
        alert("You're too young to work!");
        return;
      }
      const jobs = ["Cashier", "Teacher", "Engineer", "Musician", "Doctor"];
      career = jobs[Math.floor(Math.random() * jobs.length)];
      updateInfo();
    }

    function relationship() {
      if (age < 13) {
        alert("You're too young to date!");
        return;
      }
      const statuses = ["Single", "Dating", "Hookup", "Engaged", "Married", "Divorced"];
      partner = statuses[Math.floor(Math.random() * statuses.length)];
      updateInfo();
    }

    updateInfo();
  </script>
</body>
</html>
