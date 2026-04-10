<div align="center">

<br/>

<img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" />
<img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" />
<img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" />
<img src="https://img.shields.io/badge/Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white" />

<br/><br/>

# ⚡ Digital Compendium

### *Scan a QR code → a clean, structured info page opens instantly.*

A **QR-code-powered digital page** built with pure HTML + CSS.
No frameworks, no npm install, no build tools. Just open and it works.

<br/>

[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-2563EB?style=for-the-badge)](https://your-project.netlify.app)
[![License](https://img.shields.io/badge/License-Free-10B981?style=for-the-badge)](#)
[![Last Updated](https://img.shields.io/badge/Updated-April_2025-F59E0B?style=for-the-badge)](#)

</div>

---

## 📖 What Is This?

The **Digital Compendium** is a single-page website that works hand-in-hand with a QR code.

> Instead of printing paper brochures — you create one clean digital page, host it free online, generate a QR code, and **anyone who scans it sees all your content instantly**.

```
Customize page → Deploy free → Get URL → Generate QR → Print → Scan → ✅ Done
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 🚀 **Hero Section** | Full-screen with floating UI cards, bold headline, CTA buttons |
| 📝 **About Section** | 6 feature cards with icons, hover effects & scroll animations |
| 🖼️ **Media Gallery** | Image cards + embedded YouTube video with browser-bar UI |
| 🔗 **Links Grid** | 6 quick-access link cards (GitHub, Website, Contact, etc.) |
| 📱 **QR Generator** | Type any URL → instant QR → Download PNG or Copy URL |
| 🌙 **Premium Design** | Light theme, dot pattern bg, glassmorphism navbar, blue accents |
| 📐 **Responsive** | Works on mobile, tablet, and desktop |
| 🎞️ **Animations** | Scroll fade-ins, floating cards, hover lifts, micro-interactions |

---

## 📁 Project Structure

```
QR Code/
│
├── 📄 index.html          → All 6 sections + JavaScript logic
├── 🎨 style.css           → Design system, animations, responsive rules
├── 📘 README.md           → This file
│
└── 📂 images/
    ├── hero_banner.png    → Hero background image
    ├── project_card1.png  → Gallery — Image 1 (tech/circuits)
    └── project_card2.png  → Gallery — Image 2 (dashboard UI)
```

---

## 🚀 Running Locally

You have **two ways** to run this project. Pick the one you prefer.

---

### ✅ Option 1 — Live Server Extension *(Recommended)*

> Best for development — **auto-reloads** the browser every time you save a file.

**Step 1: Install the Extension**
1. Open VS Code
2. Press `Ctrl + Shift + X` → Search **"Live Server"**
3. Install by **Ritwick Dey** → Restart VS Code

**Step 2: Run**
1. Open the `QR Code` folder in VS Code (`File → Open Folder`)
2. Open `index.html`
3. Click **"Go Live"** button in the **bottom-right corner** of VS Code
4. Browser opens at `http://127.0.0.1:5500` ✅

**Step 3: Stop**
- Click **"Port: 5500"** in the bottom-right corner, OR
- `Ctrl + Shift + P` → type `Live Server: Stop Server` → Enter

| Feature | Live Server |
|---|---|
| Auto-reload on save | ✅ Yes — instant |
| No terminal needed | ✅ Yes |
| Works offline | ✅ Yes |

---

### ✅ Option 2 — Terminal (`npx serve`)

> Best for quick testing or sharing on your local network.

```bash
npx serve "c:\QR Code" --listen 3000
```

Then open: **`http://localhost:3000`**

> ⚠️ **If port 3000 is busy**, `serve` auto-picks another port.
> Check the terminal — it shows the exact URL to use.
> ```
> This port was picked because 3000 is in use.
> - Local: http://localhost:55431   ← Use this URL
> ```

To stop: Press `Ctrl + C` in the terminal.

---

### Comparison

| | Live Server | `npx serve` |
|---|---|---|
| Auto-reload on save | ✅ Yes | ❌ No (manual F5) |
| Terminal needed | ❌ No | ✅ Yes |
| LAN sharing | ✅ Yes | ✅ Yes |
| Best for | Development | Testing / Sharing |

---

## 🧩 How Each Section Works

<details>
<summary><b>🌟 Navbar</b></summary>

- Fixed at top using `position: fixed`
- Glassmorphism effect: `backdrop-filter: blur(16px)` — frosted glass look
- Smooth scroll to sections: CSS `scroll-behavior: smooth`
- Shadow on scroll: JavaScript adds `box-shadow` after scrolling 60px

</details>

<details>
<summary><b>🚀 Hero + Floating Cards</b></summary>

- Full-screen using `min-height: 100vh`
- 4 floating UI cards (sticky note, checklist, QR ready, stats) float using CSS `@keyframes floatY`
- Each card has different `animation-delay` so they don't sync
- Dot grid background: CSS `radial-gradient` on `body::before`
- Blue glow: CSS `radial-gradient` on `.hero::after`

</details>

<details>
<summary><b>📝 About / Features Grid</b></summary>

- 6 cards in `CSS Grid` (3 columns, auto 2 on tablet, 1 on mobile)
- Hover lift: `transform: translateY(-6px)` with `box-shadow`
- Scroll animations: `IntersectionObserver` API adds `.visible` class when in viewport

</details>

<details>
<summary><b>🖼️ Media Gallery</b></summary>

- 2 image cards in `grid-template-columns: 1fr 1fr`
- Image zoom: `transform: scale(1.04)` on hover
- YouTube embed: standard `<iframe>` with `aspect-ratio: 16/9`
- Browser bar (red/yellow/green dots) above video — pure CSS aesthetic

</details>

<details>
<summary><b>📱 QR Code Generator</b></summary>

- Uses [QRCode.js](https://github.com/davidshimjs/qrcodejs) loaded from CDN
- Auto-generates on page load with default URL
- Press `Enter` or click Generate to create QR
- Download: creates a hidden `<a>` tag and triggers `.click()`
- Copy: uses `navigator.clipboard.writeText()` Web API

</details>

---

## ⚙️ JavaScript Explained

All JS is in a `<script>` tag at the bottom of `index.html`:

```javascript
// 1. Scroll Animations
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.add('visible');
  });
}, { threshold: 0.1 });
document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));

// 2. QR Generator
function generateQR() {
  const url = document.getElementById('qr-url-input').value.trim();
  document.getElementById('qr-canvas').innerHTML = '';
  new QRCode(document.getElementById('qr-canvas'), {
    text: url,
    width: 220, height: 220,
    colorDark: '#2563EB',    // Blue dots
    colorLight: '#FFFFFF',   // White background
  });
}

// 3. Download QR
function downloadQR() {
  const img = document.querySelector('#qr-canvas img');
  const link = document.createElement('a');
  link.href = img.src;
  link.download = 'qr-code.png';
  link.click();
}

// 4. Copy URL
function copyURL() {
  navigator.clipboard.writeText(url).then(() => {
    btn.textContent = '✅ Copied!';
    setTimeout(() => btn.textContent = '📋 Copy URL', 2000);
  });
}
```

---

## 🔧 Customization Guide

| What to Change | File | Where to Look |
|---|---|---|
| Page title & tagline | `index.html` | Hero section — `<h1>` and `<p>` |
| About description | `index.html` | `#about` → `.section-desc` |
| YouTube video | `index.html` | `<iframe src="...embed/VIDEO_ID">` |
| Links (GitHub, Website, etc.) | `index.html` | `#links` → each `<a href="">` |
| Gallery images | `images/` folder + `index.html` | Replace files, update `src=""` |
| Footer name | `index.html` | Bottom — `Made with ♥ by Mayank` |
| Accent color | `style.css` | `:root { --blue: #2563EB; }` |

### Change QR Color
In `index.html` → `generateQR()` function:
```javascript
colorDark: '#2563EB',   // ← Change to any hex (e.g. #7C3AED for purple)
```

### Change Accent Color
In `style.css` → `:root`:
```css
--blue:        #2563EB;   /* ← Change this */
--blue-dark:   #1d4ed8;   /* ← Slightly darker version */
--blue-light:  #EFF6FF;   /* ← Very light tint */
```

---

## 🌐 Deploying Free Online

### 🥇 Netlify — Drag & Drop (Easiest)

1. Go to [netlify.com](https://netlify.com) → Create free account
2. Click **"Add new site"** → **"Deploy manually"**
3. Open File Explorer → Navigate to `c:\QR Code`
4. **Drag the entire folder** into the Netlify browser window
5. Wait ~10 sec → get your live URL:
   ```
   https://your-project-abc123.netlify.app
   ```
6. Paste that URL in the **QR Generator** → Download PNG → Print! 🎉

### 🥈 Vercel

1. Go to [vercel.com](https://vercel.com) → Sign up with GitHub
2. Click **"Add New → Project"** → Upload folder or connect repo
3. Deploy → Get live URL

---

## 💡 Use Cases

| 🎓 College Projects | Print QR on title page → anyone scans → full project page |
|---|---|
| 🎪 Events & Fests | QR on banner → visitors see schedule, links, registration |
| 🍽️ Restaurant Menu | QR on table → customers see digital menu |
| 💼 Portfolio Card | QR on visiting card → recruiters scan → your portfolio |
| 📦 Product Page | QR on packaging → customers see details & support |

---

## 🛠️ Tech Stack

| Technology | Purpose | Notes |
|---|---|---|
| **HTML5** | Page structure | Single `index.html` file |
| **CSS3** | All styling | Grid, Flexbox, Variables, Animations |
| **Vanilla JS** | Interactivity | IntersectionObserver, Clipboard API |
| **Google Fonts** | Typography | Inter — loaded via CSS `@import` |
| **QRCode.js** | QR generation | Loaded via CDN `<script>` tag |
| **Netlify/Vercel** | Hosting | Free static site hosting |

> **Zero npm. Zero node_modules. Zero build step.** Just HTML, CSS, JS.

---

## ❓ FAQ

**Q: QR code doesn't work when I scan it?**
> You used `localhost` as the URL — it only works on your device. Use a deployed Netlify/Vercel URL for QR to work globally.

**Q: Browser not updating after code change?**
> Using `npx serve`? Press `F5` to manually refresh. Use **Live Server** extension for auto-reload.

**Q: Port 3000 is already in use?**
> `serve` auto-picks another port. Check the terminal output for the exact URL (e.g. `http://localhost:55431`).

**Q: Can I use my own photos?**
> Yes! Put them in the `images/` folder and update `src=""` in `index.html`.

---

<div align="center">

<br/>

**⚡ Digital Compendium**

*Scan. Read. Connect.*

<br/>

Made with ♥ by **Mayank** · 2025

</div>