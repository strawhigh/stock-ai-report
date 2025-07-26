# stock-ai-report
<body>
  <h1>Plan D 股票報告</h1>
  <div id="stock-info"></div>

  <script>
    const stockSymbol = 'AAPL'; // 你可以改成 'TSLA', 'MSFT' 等
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
</body>v.innerHTML += `<p>${symbol}: $${data.price}</p>`;
        } catch (err) {
          stockInfoDiv.innerHTML += `<p>${symbol}: 讀取失敗</p>`;
        }
      }
    }

    fetchStockData();
  </script>
</body>
</html>