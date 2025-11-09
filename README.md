<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Calculator with Dark Mode</title>
  <style>
    :root {
      --bg-color: #f2f2f2;
      --text-color: #000;
      --card-color: #fff;
      --button-color: #eee;
      --button-hover: #ddd;
      --special-button: #f77;
    }

    body.dark {
      --bg-color: #1e1e1e;
      --text-color: #fff;
      --card-color: #2a2a2a;
      --button-color: #444;
      --button-hover: #555;
      --special-button: #f44;
    }

    body {
      font-family: Arial, sans-serif;
      background: var(--bg-color);
      color: var(--text-color);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      transition: background 0.3s, color 0.3s;
    }

    .calculator {
      background: var(--card-color);
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      width: 300px;
      transition: background 0.3s;
    }

    #display {
      width: 100%;
      height: 50px;
      text-align: right;
      padding: 10px;
      font-size: 1.5em;
      border: none;
      background: var(--button-color);
      border-radius: 8px;
      margin-bottom: 10px;
      color: var(--text-color);
    }

    .buttons button {
      width: 60px;
      height: 60px;
      margin: 5px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      background: var(--button-color);
      color: var(--text-color);
      cursor: pointer;
      transition: background 0.2s;
    }

    .buttons button:hover {
      background: var(--button-hover);
    }

    #history {
      margin-top: 15px;
      background: var(--button-color);
      border-radius: 8px;
      padding: 10px;
      max-height: 100px;
      overflow-y: auto;
      font-size: 14px;
    }

    #history h3 {
      margin-top: 0;
      text-align: center;
      font-size: 16px;
    }

    .clear-history {
      background: var(--special-button);
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 5px;
    }

    .mode-toggle {
      text-align: center;
      margin-bottom: 10px;
    }

    .mode-toggle button {
      background: var(--button-color);
      color: var(--text-color);
      border: none;
      padding: 5px 10px;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s;
    }

    .mode-toggle button:hover {
      background: var(--button-hover);
    }
  </style>
</head>
<body>

  <div class="calculator">
    <div class="mode-toggle">
      <button id="toggleMode">🌙 Dark Mode</button>
    </div>

    <input type="text" id="display" readonly>

    <div class="buttons">
      <button onclick="appendValue('7')">7</button>
      <button onclick="appendValue('8')">8</button>
      <button onclick="appendValue('9')">9</button>
      <button onclick="appendValue('/')">÷</button><br>

      <button onclick="appendValue('4')">4</button>
      <button onclick="appendValue('5')">5</button>
      <button onclick="appendValue('6')">6</button>
      <button onclick="appendValue('*')">×</button><br>

      <button onclick="appendValue('1')">1</button>
      <button onclick="appendValue('2')">2</button>
      <button onclick="appendValue('3')">3</button>
      <button onclick="appendValue('-')">−</button><br>

      <button onclick="appendValue('0')">0</button>
      <button onclick="appendValue('.')">.</button>
      <button onclick="calculate()">=</button>
      <button onclick="appendValue('+')">+</button><br>

      <button onclick="clearDisplay()">C</button>
    </div>

    <div id="history">
      <h3>History</h3>
      <div id="historyList"></div>
      <button class="clear-history" onclick="clearHistory()">Clear History</button>
    </div>
  </div>

  <script>
    let display = document.getElementById('display');
    let historyList = document.getElementById('historyList');
    let toggleButton = document.getElementById('toggleMode');

    function appendValue(value) {
      display.value += value;
    }

    function clearDisplay() {
      display.value = '';
    }

    function calculate() {
      try {
        let result = eval(display.value);
        historyList.innerHTML += `<div>${display.value} = ${result}</div>`;
        display.value = result;
      } catch {
        display.value = 'Error';
      }
    }

    function clearHistory() {
      historyList.innerHTML = '';
    }

    toggleButton.addEventListener('click', () => {
      document.body.classList.toggle('dark');
      if (document.body.classList.contains('dark')) {
        toggleButton.textContent = '☀️ Light Mode';
      } else {
        toggleButton.textContent = '🌙 Dark Mode';
      }
    });
  </script>

</body>
</html>
