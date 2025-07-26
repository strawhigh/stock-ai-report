# stock-ai-report
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>Plan D 股票快報</title>
</head>
<body>
  <h1>Plan D 股票快報（美股）</h1>
  <div id="stock-info">載入中...</div>

  <script>
    const apiKey = "你的API_KEY"; // ← 自己註冊 Twelve Data 後取得
    const symbols = ["AAPL", "MSFT", "GOOGL", "TSLA"]; // 自訂你要的股票代碼

    async function fetchStockData() {
      const stockInfoDiv = document.getElementById("stock-info");
      stockInfoDiv.innerHTML = "";

      for (let symbol of symbols) {
        const url = `https://api.twelvedata.com/price?symbol=${symbol}&apikey=${apiKey}`;
        try {
          const res = await fetch(url);
          const data = await res.json();
          stockInfoDiv.innerHTML += `<p>${symbol}: $${data.price}</p>`;
        } catch (err) {
          stockInfoDiv.innerHTML += `<p>${symbol}: 讀取失敗</p>`;
        }
      }
    }

    fetchStockData();
  </script>
</body>
</html>