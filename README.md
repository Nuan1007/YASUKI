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
      position: relative;
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

    /* 左下固定のQR表示ボタン */
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

  <div class="problem" id="problem">ここに問題が表示されます</div>

  <div>
    <input type="number" id="inputA" placeholder="a を入力">
    <input type="number" id="inputB" placeholder="b を入力"><br>
    <button onclick="checkAnswer()">答え</button>

  </div>

  <div class="result" id="result"></div>

  <!-- QRコードを別画面で開くボタン -->
  <button class="qr-button" onclick="openQR()">QRコードを表示</button>

  <script>
    let a, b;

    function newProblem() {
      a = Math.floor(Math.random() * 10) + 1;
      b = Math.floor(Math.random() * 10) + 1;
      document.getElementById("problem").innerHTML = `(x + □)(x + □)<br>= x² + ${(a + b)}x + ${(a * b)}`;
      document.getElementById("inputA").value = '';
      document.getElementById("inputB").value = '';
      document.getElementById("result").textContent = '';
    }

    function checkAnswer() {
      const userA = parseInt(document.getElementById("inputA").value);
      const userB = parseInt(document.getElementById("inputB").value);

      if (isNaN(userA) || isNaN(userB)) {
        document.getElementById("result").textContent = "整数を入力してね。";
        return;
      }

      if ((userA === a && userB === b) || (userA === b && userB === a)) {
        document.getElementById("result").textContent = `正解！(x + ${a})(x + ${b}) 〇`;
      } else {
        document.getElementById("result").textContent = "不正解";
      }
    }

    // QRコード画像を別画面で開く
    function openQR() {
      window.open("ダウンロード.png", "_blank");
    }

    newProblem();
  </script>
</body>
</html>
