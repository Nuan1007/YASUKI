<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>スピード因数分解</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 30px;
    }

    input, button {
      font-size: 20px;
      padding: 10px;
      margin: 10px;
    }

    h1 {
      font-size: 32px;
    }

    .problem {
      font-size: 28px;
      margin: 20px;
    }

    .result {
      font-size: 24px;
      margin: 20px;
      color: #007700;
    }

    .qr-button {
      position: fixed;
      bottom: 10px;
      left: 10px;
      font-size: 16px;
      padding: 10px 15px;
    }
  </style>
</head>
<body>
  <h1>スピード因数分解</h1>

  <div>
    <button onclick="easyProblem()">イージーモード</button>
    <button onclick="hardProblem()">ハードモード</button>
  </div>

  <div class="problem" id="problem">ここに問題が表示されます</div>

  <div id="inputs"></div>

  <div class="result" id="result"></div>

  <button class="qr-button" onclick="openQR()">QRコードを表示</button>

  <script>
    let a, b, c, d;
    let mode = "easy";

    function randomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function formatTerm(coef, isX = false) {
      if (isX) {
        if (coef === 1) return 'x';
        if (coef === -1) return '-x';
        return coef + 'x';
      } else {
        return coef >= 0 ? `+${coef}` : coef.toString();
      }
    }

    function easyProblem() {
      mode = "easy";
      a = randomInt(1, 10);
      b = randomInt(1, 10);
      document.getElementById("problem").innerHTML =
        `(x + □)(x + □)<br>= x² + ${(a + b)}x + ${a * b}`;
      document.getElementById("inputs").innerHTML = `
        <input type="number" id="inputA" placeholder="a を入力">
        <input type="number" id="inputB" placeholder="b を入力">
        <br><button onclick="checkAnswer()">答え</button>`;
      document.getElementById("result").textContent = '';
    }

    function hardProblem() {
      mode = "hard";
      a = randomInt(1, 4);
      b = randomInt(-10, 10); while (b === 0) b = randomInt(-10, 10);
      c = randomInt(1, 4);
      d = randomInt(-10, 10); while (d === 0) d = randomInt(-10, 10);
      

      const coefX2 = a * c;
      const coefX = a * d + b * c;
      const constant = b * d;

      const leftExpr = `(${formatTerm(a, true)} ${formatTerm(b)})(${formatTerm(c, true)} ${formatTerm(d)})`;
      const rightExpr = `${coefX2 === 1 ? '' : coefX2}x² ${coefX >= 0 ? '+' : ''}${coefX}x ${constant >= 0 ? '+' : ''}${constant}`;

      document.getElementById("problem").innerHTML =
        `${leftExpr}<br>= ${rightExpr}`;
      document.getElementById("inputs").innerHTML = `
        <input type="number" id="inputA" placeholder="1つ目の x の係数">
        <input type="number" id="inputB" placeholder="1つ目の定数項">
        <input type="number" id="inputC" placeholder="2つ目の x の係数">
        <input type="number" id="inputD" placeholder="2つ目の定数項">
        <br><button onclick="checkAnswer()">答え</button>`;
      document.getElementById("result").textContent = '';
    }

    function checkAnswer() {
      if (mode === "easy") {
        const userA = parseInt(document.getElementById("inputA").value);
        const userB = parseInt(document.getElementById("inputB").value);
        if (isNaN(userA) || isNaN(userB)) {
          document.getElementById("result").textContent = "整数を入力してね。";
          return;
        }
        const correct = (userA === a && userB === b) || (userA === b && userB === a);
        document.getElementById("result").textContent = correct
          ? `正解！(x + ${a})(x + ${b}) 〇`
          : "不正解";
      } else {
        const userA = parseInt(document.getElementById("inputA").value);
        const userB = parseInt(document.getElementById("inputB").value);
        const userC = parseInt(document.getElementById("inputC").value);
        const userD = parseInt(document.getElementById("inputD").value);
        if ([userA, userB, userC, userD].some(isNaN)) {
          document.getElementById("result").textContent = "すべての項を入力してね。";
          return;
        }

        const correct =
          (userA === a && userB === b && userC === c && userD === d) ||
          (userA === c && userB === d && userC === a && userD === b);

        document.getElementById("result").textContent = correct
          ? `正解！(${a}x + ${b})(${c}x + ${d}) 〇`
          : "不正解";
      }
    }

    function openQR() {
      window.open("YASUKI.png", "_blank");
    }

    easyProblem(); // 初期表示
  </script>
</body>
</html>
