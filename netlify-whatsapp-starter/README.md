# Netlify WhatsApp Order Starter

A free, static website that lets customers fill an order form and, on checkout, opens WhatsApp with the order pre-filled. Perfect for small F&B businesses.

## 1) Edit your WhatsApp number
Open `script.js` and change:
```js
const WHATSAPP_NUMBER = '673XXXXXXXX'; // your full number, digits only (no + or spaces)
```

**Examples**
- Brunei: `6738XXXXXXX`
- Malaysia: `60XXXXXXXXXX`
- Singapore: `65XXXXXXXX`

> Use digits only. WhatsApp uses the `https://wa.me/<number>` format.

## 2) Test locally
Just open `index.html` in your browser and submit a test order. It should open WhatsApp Web/App.

## 3) Deploy to Netlify (no Git required)
1. Go to Netlify → **Add new site** → **Deploy manually**.
2. Drag the whole folder into the upload area (or zip it and upload).
3. Wait for deploy, then click the generated URL (e.g., `yourname.netlify.app`).

## 4) (Optional) Deploy via GitHub
1. Create a new GitHub repo and push this folder.
2. In Netlify: **Add new site** → **Import an existing project** → Choose GitHub repo.
3. Build command: none (static site). Publish directory: the repo root.

## 5) Rename your free subdomain
- Netlify → **Site Settings** → **Site details** → **Change site name**.
- Example: `ramlee-bbq.netlify.app`.

## 6) Customize the form
- Update labels/placeholders in `index.html`.
- Add or remove fields (just ensure they’re included in `buildMessage` in `script.js`).
- Styling is in `styles.css`.

## 7) Common tips
- If nothing happens on submit, your browser may block popups. We use `location.href` to avoid this.
- If WhatsApp doesn’t open on desktop, ensure WhatsApp Web is set up or test on mobile.
- Keep your number in international format, digits only.

---

Enjoy! 🍗
