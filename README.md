# 🩺 My AI Health Tool
**Free, private, browser-only AI medical intake tool.**  
No server. No storage. No accounts. No exposed API keys.

🔗 **Live:** https://dagrang-repository.github.io/free-ai-medical-tool  
⭐ If this helped you, star the repo — it keeps the tool free.

---

## What it does
1. You describe your health concern in plain language, by voice, or via camera photo
2. AI asks focused, empathetic follow-up questions — like a warm family doctor
3. Generates a structured PDF report with:
   - Patient summary
   - Key symptoms & timeline
   - Concrete final solution
   - Pharmacy card (medication categories, forms, dosage guidance)
   - Risk assessment scores
   - Urgency level
4. All data is permanently purged from your device after download

---

## Features

### 🎙️ Voice input
Speak your symptoms instead of typing. Toggle on/off from the header. Uses the browser's native Speech Recognition API.

### 📷 Camera capture
Take a photo of a visible symptom (rash, wound, etc.) directly from the tool. The image is sent alongside your text to the AI for visual context.

### 🌐 Google Translate
Full Google Translate widget embedded at the bottom of the page — translate the entire UI into any language instantly. Built-in i18n fallback covers EN, FR, ES, DE, PT natively without Google.

### 💾 Auto-save & session restore
Your session is automatically saved to `localStorage` on every keystroke. If you close the tab, restart the browser, or reboot your PC — your progress is still there. On return, a restore banner appears. You can also export your session as a JSON file and re-import it on any device.

### 📊 Live report preview
The AI report updates in real time as you answer questions — visible in a side panel while you type.

### 🔄 Second opinion
Request a fresh AI analysis of your current symptoms with one click — different framing, same data.

### 🤔 What if?
Explore alternative diagnoses or scenarios ("What if it's not X but Y?") without losing your current session.

### 📱 QR code sharing
Generate a QR code for your report. When scanned on another device, it loads the report — auto-purges after 4 hours.

### 🔁 Offline support
Requests are queued when the user loses connection and auto-drained when they reconnect.

---

## Privacy model
- **Zero server storage** — nothing is sent to any server except the Gemini API for AI processing
- **No accounts** — no login, no email required
- **Auto-purge** — after PDF download, localStorage, sessionStorage, IndexedDB, and Service Worker cache are all wiped
- **Client-side PDF** — report is generated entirely in your browser
- **Open source** — you can read every line of code

---

## Architecture

### Single HTML file
No build step. No framework. No npm install. Drop `index.html` anywhere and it works.

### Cloudflare Worker as AI proxy
```
Browser → Cloudflare Worker → Gemini API
```
API keys are stored as encrypted environment variables in the Worker. The frontend never sees a key. GitHub's secret scanner has nothing to flag.

### 5-key rotation with model fallback
If one key hits a rate limit or fails, the Worker automatically tries the next key across multiple models:
- `gemini-2.0-flash`
- `gemini-2.0-flash-lite`
- `gemini-2.5-flash`

### Offline support
Requests are queued when the user loses connection and auto-drained when they reconnect.

### Global error boundary
All unhandled JS errors and promise rejections are caught — user sees a toast, no silent crashes, no data loss.

---

## Tech stack
| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla JS, Tailwind Play CDN |
| PDF generation | jsPDF (client-side) |
| QR generation | qrcode.js (client-side) |
| AI proxy | Cloudflare Workers |
| AI engine | Google Gemini |
| Hosting | GitHub Pages |
| Translation | Google Translate widget + native i18n (EN/FR/ES/DE/PT) |
| Analytics | Google Analytics (anonymous) |

---

## Self-hosting

### Option 1 — GitHub Pages (easiest)
1. Fork this repo
2. Enable GitHub Pages (Settings → Pages → main branch)
3. Done — your own instance is live

### Option 2 — Any static host
Upload `index.html` to Netlify, Vercel, Cloudflare Pages, or your own server. No backend needed.

### Option 3 — Your own Cloudflare Worker
1. Create a Worker at [dash.cloudflare.com](https://dash.cloudflare.com)
2. Paste the Worker code (see `worker.js` or inline in index.html comments)
3. Add your Gemini API keys as `GEMINI_KEYS` environment variable (comma-separated)
4. Update `WORKER_URL` in `index.html` to your Worker URL
5. Get free Gemini API keys at [aistudio.google.com/apikey](https://aistudio.google.com/apikey)

---

## Contributing
PRs welcome. Key areas where help is appreciated:
- Multilingual support (translations)
- Improved red-flag detection logic
- Better PDF layout for edge cases
- Accessibility improvements
- Additional pharmacy card detail

---

## Disclaimer
This tool is AI-generated for informational purposes only. It is **not medical advice, diagnosis, or prescription**. Always consult a qualified healthcare professional. Not a medical device under EU MDR, FDA 21 CFR, or any national healthcare regulation.

---

## Support
If this tool helped you, consider supporting it:  
❤️ [Donate via Stripe](https://buy.stripe.com/fZu00jdsW2O46jm6955ZC07) — keeps it free for everyone

---

Built by [Sang DAGRANG](https://www.letsmeet-here.app) • [LetsMeet-Here](https://www.letsmeet-here.app) • [SecuresVault](https://www.securesvault.com)
