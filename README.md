<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Тамаққа шақыру 🍕</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 0;
      padding: 20px;
    }
    .card {
      background: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.15);
      text-align: center;
      max-width: 450px;
      width: 100%;
      position: relative;
    }
    h1 {
      color: #333;
      font-size: 24px;
      margin-bottom: 20px;
    }
    .btn-group {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin-top: 20px;
      min-height: 60px;
    }
    button {
      padding: 12px 25px;
      font-size: 18px;
      font-weight: bold;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.2s;
    }
    .btn-yes {
      background-color: #ff4757;
      color: white;
    }
    .btn-yes:hover {
      transform: scale(1.05);
    }
    .btn-no {
      background-color: #747d8c;
      color: white;
      position: absolute;
    }
    .options-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-top: 20px;
    }
    .food-btn {
      background-color: #f1f2f6;
      border: 2px solid #ffa502;
      color: #2f3542;
      padding: 15px;
      font-size: 16px;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.2s;
    }
    .food-btn:hover {
      background-color: #ffa502;
      color: white;
    }
    .hidden {
      display: none;
    }
    .address-card {
      background: #eccc68;
      padding: 15px;
      border-radius: 10px;
      margin-top: 15px;
      font-weight: bold;
      color: #2f3542;
    }
    a.map-link {
      display: inline-block;
      margin-top: 10px;
      color: #2ed573;
      text-decoration: underline;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <!-- 1-ШІ КЕЗЕҢ: Шақыру -->
  <div class="card" id="step1">
    <h1>Мені тамаққа шақырасың ба? 🥺</h1>
    <div class="btn-group">
      <button class="btn-yes" onclick="goStep2()">ИӘ! 💖</button>
      <button class="btn-no" id="noBtn" onmouseover="moveButton()" onclick="moveButton()">Жоқ 😜</button>
    </div>
  </div>

  <!-- 2-ШІ КЕЗЕҢ: Тамақ таңдау -->
  <div class="card hidden" id="step2">
    <h1>Орал, тамаша! 😍<br>Не жейміз?</h1>
    <div class="options-grid">
      <button class="food-btn" onclick="selectFood('Донер')">🥙 Донер</button>
      <button class="food-btn" onclick="selectFood('Бургер')">🍔 Бургер</button>
      <button class="food-btn" onclick="selectFood('Суши')">🍣 Суши</button>
      <button class="food-btn" onclick="selectFood('Плов')">🍲 Плов</button>
      <button class="food-btn" onclick="selectFood('Самса')" style="grid-column: span 2;">🥐 Самса</button>
    </div>
  </div>

  <!-- 3-ШІ КЕЗЕҢ: Мекенжай -->
  <div class="card hidden" id="step3">
    <h1 id="resultTitle">Таңдауыңа рахмет! 🎉</h1>
    <p style="font-size: 18px; color: #555;">Кездесетін орнымыз:</p>
    <div class="address-card" id="addressText"></div>
  </div>

  <script>
    // Жоқ батырмасын қашыру функциясы
    function moveButton() {
      const btn = document.getElementById('noBtn');
      const card = document.querySelector('.card');
      
      const cardRect = card.getBoundingClientRect();
      const btnRect = btn.getBoundingClientRect();

      // Карточканың ішіндегі шектеулі координаталарды есептеу
      const maxX = cardRect.width - btnRect.width - 20;
      const maxY = cardRect.height - btnRect.height - 20;

      const randomX = Math.floor(Math.random() * maxX);
      const randomY = Math.floor(Math.random() * maxY);

      btn.style.left = randomX + 'px';
      btn.style.top = randomY + 'px';
    }

    // Иә басқанда екінші бетке өту
    function goStep2() {
      document.getElementById('step1').classList.add('hidden');
      document.getElementById('step2').classList.remove('hidden');
    }

    // Тамақтардың адрестері
    const addresses = {
      'Донер': '📍 «SalamBro» немесе сүйікті донерханаң (Абай даңғылы, 45)',
      'Бургер': '📍 «Hardee\'s» / «Burger King» (Жібек Жолы, 100)',
      'Суши': '📍 «Sushimania» (Достық даңғылы, 85)',
      'Плов': '📍 «Rumi» Плов орталығы (Абылай хан даңғылы, 120)',
      'Самса': '📍 «Тандыр Самса» (Сәтбаев көшесі, 15)'
    };

    // Тамақ таңдалғанда адрес шығару
    function selectFood(food) {
      document.getElementById('step2').classList.add('hidden');
      document.getElementById('step3').classList.remove('hidden');

      document.getElementById('resultTitle').innerText = food + " жеуге келістік! 😋";
      document.getElementById('addressText').innerText = addresses[food];
    }
  </script>
</body>
</html>
