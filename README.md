
import requests
from datetime import datetime
import os

# FinMind API 設定
api_token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRlIjoiMjAyNS0wNy0yNyAwMDowMTozNiIsInVzZXJfaWQiOiJTdHJhd2hpZ2giLCJpcCI6IjU5LjExNS4xNy4yMCJ9.la5mV6ZY1uqWeuY8kSlqnwyxyldSAp6eA8OKmEBcvjc"
api_url = "https://api.finmindtrade.com/api/v4/data"

# 股票清單（可依需求增減）
stocks = [
    {"name": "世芯-KY", "code": "3661"},
    {"name": "乙盛-KY", "code": "5243"},
    {"name": "弘格", "code": "6696"},
]

# Telegram 設定
telegram_token = os.getenv("TELEGRAM_TOKEN")
chat_id = "7962664337"

def fetch_price(code):
    today = datetime.now().strftime("%Y-%m-%d")
    payload = {
        "dataset": "TaiwanStockPrice",
        "data_id": code,
        "start_date": today,
        "end_date": today,
        "token": api_token
    }
    r = requests.get(api_url, params=payload)
    data = r.json().get("data", [])
    if not data:
        return None
    return float(data[0]["open"]), float(data[0]["close"])

def send_telegram(message):
    url = f"https://api.telegram.org/bot{telegram_token}/sendMessage"
    payload = {"chat_id": chat_id, "text": message}
    requests.post(url, data=payload)

def main():
    for stock in stocks:
        result = fetch_price(stock["code"])
        if result:
            open_price, close_price = result
            pct = (close_price - open_price) / open_price * 100
            if abs(pct) >= 3:
                msg = f"{stock['name']}（{stock['code']}）今日漲跌幅：{pct:.2f}%"
                send_telegram(msg)

if __name__ == "__main__":
    main()
