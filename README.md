# stock-ai-report
fetch('stocks.json')
  .then(response => response.json())
  .then(data => {
    const container = document.getElementById('stock-list');
    container.innerHTML = '';
    data.forEach(stock => {
      const item = document.createElement('div');
      item.innerHTML = `<strong>${stock.name}</strong> (${stock.code}): ${stock.analysis}`;
      container.appendChild(item);
    });
  })
  .catch(error => {
    document.getElementById('stock-list').innerText = '讀取失敗：' + error;
  });
