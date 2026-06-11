<!DOCTYPE html>
<html>
<head>
<title>Advanced Calculator</title>

<style>
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-family: Arial;
    transition: 0.3s;
  }

  .dark {
    background: #1e1e2f;
  }

  .light {
    background: #f4f4f4;
  }

  .calculator {
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0 20px rgba(0,0,0,0.3);
    background: #2c2c3e;
  }

  .light .calculator {
    background: white;
  }

  #display {
    width: 100%;
    height: 50px;
    font-size: 22px;
    margin-bottom: 10px;
    text-align: right;
    padding: 10px;
    border-radius: 10px;
    border: none;
  }

  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 60px);
    gap: 10px;
  }

  button {
    height: 60px;
    font-size: 18px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: #4e4e70;
    color: white;
  }

  .light button {
    background: #ddd;
    color: black;
  }

  .equal { background: orange; }
  .clear { background: red; }

  .toggle {
    margin-bottom: 10px;
    cursor: pointer;
  }
</style>
</head>

<body class="dark">

<div class="calculator">
  <button class="toggle" onclick="toggleMode()">🌙/☀️</button>

  <input type="text" id="display" readonly>

  <div class="buttons">
    <button onclick="clearDisplay()" class="clear">C</button>
    <button onclick="append('/')">/</button>
    <button onclick="append('*')">*</button>
    <button onclick="append('-')">-</button>

    <button onclick="append('7')">7</button>
    <button onclick="append('8')">8</button>
    <button onclick="append('9')">9</button>
    <button onclick="append('+')">+</button>

    <button onclick="append('4')">4</button>
    <button onclick="append('5')">5</button>
    <button onclick="append('6')">6</button>
    <button onclick="calculate()" class="equal">=</button>

    <button onclick="append('1')">1</button>
    <button onclick="append('2')">2</button>
    <button onclick="append('3')">3</button>
    <button onclick="append('0')">0</button>

    <!-- Scientific -->
    <button onclick="square()">x²</button>
    <button onclick="sqrt()">√</button>
    <button onclick="percent()">%</button>
    <button onclick="append('.')">.</button>
  </div>
</div>

<script>
let display = document.getElementById("display");

// Basic functions
function append(val) {
  display.value += val;
}

function clearDisplay() {
  display.value = "";
}

function calculate() {
  try {
    display.value = eval(display.value);
  } catch {
    display.value = "Error";
  }
}

// Scientific
function square() {
  display.value = display.value * display.value;
}

function sqrt() {
  display.value = Math.sqrt(display.value);
}

function percent() {
  display.value = display.value / 100;
}

// Theme toggle
function toggleMode() {
  document.body.classList.toggle("light");
  document.body.classList.toggle("dark");
}

// Keyboard support
document.addEventListener("keydown", function(event) {
  if (!isNaN(event.key) || "+-*/.".includes(event.key)) {
    append(event.key);
  } else if (event.key === "Enter") {
    calculate();
  } else if (event.key === "Backspace") {
    display.value = display.value.slice(0, -1);
  }
});
</script>

</body>
</html>
