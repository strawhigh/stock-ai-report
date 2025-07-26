# stock-ai-report
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>Plan D 股票快報</title>
</head>
<body>
  <h1>Plan D 股票快報（美股）</h1>
  <div id="stock-info"></div>

  <script>
    const stockSymbol = 'AAPL'; // 想查哪支股就改成代號，支援台美股
    const apiKey = '5cf6536c709248709723a7a9c13648d8';

    async function fetchStockPrice() {
      const url = `https://api.twelvedata.com/price?symbol=${stockSymbol}&apikey=${apiKey}`;

      try {
        const response = await fetch(url);
        const data = await response.json();
        if (data.price) {
          document.getElementById('stock-info').innerText =
            `${stockSymbol} 現價：$${data.price}`;
        } else {
          document.getElementById('stock-info').innerText =
            `錯誤：${JSON.stringify(data)}`;
        }
      } catch (error) {
        document.getElementById('stock-info').innerText =
          '資料載入失敗';
      }
    }

    fetchStockPrice();
  </script>
</body>
</html>
