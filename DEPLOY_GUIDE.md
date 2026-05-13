# Sajawal Store — Deploy Karne Ka Tareeqa

## Step 1: Vercel Pe Free Hosting

1. **vercel.com** pe jaein aur free account banao
2. "New Project" click karein
3. `index.html` file upload karein
4. Deploy button dabao
5. Aapko ek link milega jaise: `https://sajawal-store.vercel.app`

---

## Step 2: Telegram Bot Banao

1. Telegram mein **@BotFather** ko open karein
2. `/newbot` type karein
3. Bot ka naam dein: `Sajawal Store`
4. Bot username dein: `sajawalstore_bot`
5. **API Token** save kar lo (secret rakhein!)

---

## Step 3: Mini App Link Karo

BotFather mein:
```
/newapp
→ Bot chunein: @sajawalstore_bot
→ App title: Sajawal Store
→ Description: Stars & Premium USDT se khareedein
→ URL: https://sajawal-store.vercel.app
```

---

## Step 4: App Ko Share Karein

Telegram mein yeh link share karein:
```
https://t.me/sajawalstore_bot/app
```

Ya direct button ke saath:
```
https://t.me/sajawalstore_bot?startapp
```

---

## Real Blockchain Verification (Advanced)

Production ke liye is code ko backend mein lagao:

```javascript
// Node.js backend — TronGrid API
const axios = require('axios');

async function verifyTronTx(txid, expectedAmount, toAddress) {
  const url = `https://api.trongrid.io/v1/transactions/${txid}`;
  const res = await axios.get(url, {
    headers: { 'TRON-PRO-API-KEY': 'AAPKI_API_KEY' }
  });
  
  const tx = res.data.data[0];
  if (!tx) return { valid: false, reason: 'Transaction nahi mili' };
  
  const contract = tx.raw_data.contract[0].parameter.value;
  const amount = contract.amount / 1_000_000; // TRC-20 decimals
  const to = contract.to_address;
  
  if (to !== toAddress) return { valid: false, reason: 'Galat wallet' };
  if (amount < expectedAmount) return { valid: false, reason: 'Kam amount' };
  
  return { valid: true, amount };
}
```

TronGrid free API key: **trongrid.io** pe sign up karein.

---

## Admin Notifications (Telegram Bot)

Jab order aaye to apne bot se message receive karne ke liye:

```javascript
// Backend mein order save hone par:
const ADMIN_CHAT_ID = '123456789'; // Apna Telegram ID
const BOT_TOKEN = 'AAPKA_BOT_TOKEN';

async function notifyAdmin(order) {
  const msg = `🆕 Naya Order!\n\nPackage: ${order.pkg}\nUser: ${order.user}\nAmount: ${order.price} USDT\nTxID: ${order.txid}\nOrder ID: ${order.id}`;
  await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ chat_id: ADMIN_CHAT_ID, text: msg })
  });
}
```

Apna Telegram ID janye ke liye: **@userinfobot** ko message karein.

---

## Prices Update Karna

`index.html` file mein yeh section dhundein:

```html
<!-- STARS PACKAGES -->
<div class="pkg" onclick="selectPkg(this,'50 Stars','0.50','stars')">
```

`'0.50'` ko jo bhi naya price ho us se replace karein.

---

## Support

Koi masla ho to: @sajawalbudhana3
