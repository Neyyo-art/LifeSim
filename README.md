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

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Avatar Genetics</title>
  <style>
    body { font-family: sans-serif; background: #111; color: white; text-align: center; }
    .avatar-container { display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; margin-top: 30px; }
    .avatar { background: #222; padding: 10px; border-radius: 10px; }
    img { image-rendering: pixelated; width: 100px; height: 100px; }
    label, select { display: block; margin: 5px auto; }
    select { width: 150px; }
  </style>
</head>
<body>

  <h1>BitLife-style Avatar Genetics</h1>

  <h2>Parent 1</h2>
  <div id="parent1-form">
    <label>Eye Shape: <select id="p1_eye"> <option>almond</option><option>round</option><option>monolid</option><option>upturned</option><option>hooded</option> </select></label>
    <label>Nose Shape: <select id="p1_nose"> <option>big</option><option>hawk</option><option>button</option><option>fleshy</option><option>Roman</option> </select></label>
    <label>Skin Tone: <select id="p1_skin"> <option>black</option><option>caramel</option><option>chocolate</option><option>white</option> </select></label>
    <label>Hair Texture: <select id="p1_texture"> <option>curly</option><option>straight</option><option>wavy</option><option>coiled</option> </select></label>
    <label>Hair Color: <select id="p1_color"> <option>black</option><option>blonde</option><option>red</option> </select></label>
    <label>Gender: <select id="p1_gender"> <option>male</option><option>female</option> </select></label>
  </div>

  <h2>Parent 2</h2>
  <div id="parent2-form">
    <label>Eye Shape: <select id="p2_eye"> <option>almond</option><option>round</option><option>monolid</option><option>upturned</option><option>hooded</option> </select></label>
    <label>Nose Shape: <select id="p2_nose"> <option>big</option><option>hawk</option><option>button</option><option>fleshy</option><option>Roman</option> </select></label>
    <label>Skin Tone: <select id="p2_skin"> <option>black</option><option>caramel</option><option>chocolate</option><option>white</option> </select></label>
    <label>Hair Texture: <select id="p2_texture"> <option>curly</option><option>straight</option><option>wavy</option><option>coiled</option> </select></label>
    <label>Hair Color: <select id="p2_color"> <option>black</option><option>blonde</option><option>red</option> </select></label>
    <label>Gender: <select id="p2_gender"> <option>male</option><option>female</option> </select></label>
  </div>

  <button onclick="generateChild()">Generate Child</button>

  <div class="avatar-container">
    <div class="avatar">
      <p>Child Avatar (Baby)</p>
      <img id="child_avatar" src="" alt="Child Avatar"/>
    </div>
  </div>

  <script>
    function randomFrom(a, b) {
      return Math.random() < 0.5 ? a : b;
    }

    function blendSkin(skin1, skin2) {
      const order = ["white", "caramel", "chocolate", "black"];
      const i1 = order.indexOf(skin1);
      const i2 = order.indexOf(skin2);
      const avg = Math.round((i1 + i2) / 2);
      return order[avg];
    }

    function generateChild() {
      const eye = randomFrom(
        document.getElementById("p1_eye").value,
        document.getElementById("p2_eye").value
      );
      const nose = randomFrom(
        document.getElementById("p1_nose").value,
        document.getElementById("p2_nose").value
      );
      const skin = blendSkin(
        document.getElementById("p1_skin").value,
        document.getElementById("p2_skin").value
      );
      const texture = randomFrom(
        document.getElementById("p1_texture").value,
        document.getElementById("p2_texture").value
      );
      const color = randomFrom(
        document.getElementById("p1_color").value,
        document.getElementById("p2_color").value
      );
      const gender = Math.random() < 0.5 ? "male" : "female";
      const age = "baby";

      const filename = `${eye}_${nose}_${skin}_${texture}_${color}_${gender}_${age}.png`;
      document.getElementById("child_avatar").src = `avatars/${filename}`;
    }
  </script>

</body>
</html>
