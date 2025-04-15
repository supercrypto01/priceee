import requests
from telegram import Bot
import asyncio

# تنظیمات
TELEGRAM_TOKEN = 'YOUR_TELEGRAM_BOT_TOKEN'  # توکن بات تلگرام
CHAT_ID = 'YOUR_CHAT_ID'  # آیدی چت تلگرام (با @userinfobot بگیر)

async def send_crypto_prices():
    try:
        # گرفتن قیمت از API عمومی کوین‌مارکت‌کپ
        url = "https://api.coingecko.com/api/v3/simple/price?ids=ethereum,zksync&vs_currencies=usd"
        response = requests.get(url)
        data = response.json()
        
        # استخراج قیمت‌ها
        eth_price = data['ethereum']['usd']
        zk_price = data['zksync']['usd']
        
        # ساخت پیام
        message = f"💰 قیمت لحظه‌ای:\nاتریوم: ${eth_price:.2f}\nZKsync: ${zk_price:.4f}"
        
        # ارسال به تلگرام
        bot = Bot(token=TELEGRAM_TOKEN)
        await bot.send_message(chat_id=CHAT_ID, text=message)
        print("پیام فرستاده شد!")
        
    except Exception as e:
        print(f"خطا: {e}")

# اجرا
asyncio.run(send_crypto_prices())# priceee
