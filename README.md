<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>WinBet - Demo Betting Site</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 20px;
      background-color: #121212;
      color: #f0f0f0;
    }
    .hidden { display: none; }
    input, button, select {
      padding: 10px;
      margin: 10px;
      font-size: 1em;
    }
    .match {
      background: #1e1e1e;
      padding: 15px;
      margin: 10px;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <h1>🎲 Welcome to <span style="color:#00ffcc">WinBet</span></h1>

  <div id="login">
    <input id="username" placeholder="Enter your name" />
    <button onclick="login()">Start Betting</button>
  </div>

  <div id="main" class="hidden">
    <h2>Hello, <span id="userNameDisplay"></span>!</h2>
    <p>💰 Balance: <span id="balance">1000</span> BDT</p>

    <div class="match">
      <h3>Match: Team A vs Team B</h3>
      <select id="betChoice">
        <option value="A">Team A Wins</option>
        <option value="B">Team B Wins</option>
      </select>
      <input id="betAmount" type="number" placeholder="Bet amount in BDT" />
      <button onclick="placeBet()">Place Bet</button>
      <p id="betResult"></p>
    </div>
  </div>

  <script>
    let balance = 1000;

    function login() {
      const name = document.getElementById('username').value.trim();
      if (name === "") return alert("Enter your name!");
      document.getElementById("userNameDisplay").innerText = name;
      document.getElementById("login").classList.add("hidden");
      document.getElementById("main").classList.remove("hidden");
    }

    function placeBet() {
      const choice = document.getElementById("betChoice").value;
      const amount = parseInt(document.getElementById("betAmount").value);
      if (isNaN(amount) || amount <= 0) {
        alert("Enter a valid bet amount.");
        return;
      }
      if (amount > balance) {
        alert("Not enough BDT.");
        return;
      }

      const winner = Math.random() < 0.5 ? "A" : "B";
      let resultText = "";

      if (choice === winner) {
        balance += amount;
        resultText = `🎉 You won! Team ${winner} won. +${amount} BDT`;
      } else {
        balance -= amount;
        resultText = `😢 You lost. Team ${winner} won. -${amount} BDT`;
      }

      document.getElementById("balance").innerText = balance;
      document.getElementById("betResult").innerText = resultText;
    }
  </script>
</body>
</html>
