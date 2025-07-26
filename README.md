name: Notify When Stock Changes Over 3%

on:
  schedule:
    - cron: '0 1 * * *'  # 台灣時間 09:00，每日執行一次
  workflow_dispatch:

jobs:
  notify:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install requests

      - name: Run notifier
        env:
          FINMIND_API_TOKEN: ${{ secrets.FINMIND_API_TOKEN }}
          TELEGRAM_API: ${{ secrets.TELEGRAM_API }}
          TELEGRAM_CHAT_ID: ${{ secrets.TELEGRAM_CHAT_ID }}
        run: |
          python3 script.py
