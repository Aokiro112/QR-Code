# ⚡ Digital Compendium

> **Scan a QR code → a clean, structured info page opens instantly.**

A QR-code-powered digital page built with **pure HTML + CSS**. No frameworks, no npm install, no build tools. Just open and it works.

---

## 📖 What Is This Project?

The **Digital Compendium** is a single-page website designed to work hand-in-hand with a QR code. Instead of printing pamphlets or paper brochures, you create one clean digital page, host it online for free, generate a QR code for its URL, and anyone who scans it sees all your content — text, images, videos, and links — in a premium modern interface.

### The Complete Flow

```
1. Customize the page  →  index.html (your content)
2. Deploy for free     →  Netlify / Vercel (drag & drop)
3. Get live URL        →  e.g. https://my-project.netlify.app
4. Open QR Generator   →  Built into the page itself (Section 5)
5. Paste your URL      →  Click Generate
6. Download QR PNG     →  Print it on anything
7. Someone scans it    →  Your digital page opens instantly ✅
```

---

## 📁 Project Structure

```
c:\QR Code\
│
├── index.html          ← The entire webpage (all 6 sections + logic)
├── style.css           ← All styling, animations, layout, colors
├── README.md           ← This file
│
└── images\
    ├── hero_banner.png      ← Hero section background (currently unused in new design)
    ├── project_card1.png    ← Media gallery — Image 1 (tech/circuits)
    └── project_card2.png    ← Media gallery — Image 2 (dashboard UI)
```

### What Each File Does

| File | Purpose |
|---|---|
| `index.html` | Contains all HTML structure, all 6 sections, built-in QR generator, and all JavaScript logic |
| `style.css` | Contains all CSS — layout (Flexbox/Grid), colors, animations, hover effects, responsive rules |
| `images/` | Local images used in the Media Gallery section |

---

## 🚀 Running the Project Locally

You have **two options** to run this project on your computer. Both work perfectly.

---

### ✅ Option 1 — Live Server Extension (Recommended for Development)

**Best for:** Daily development, because it **auto-reloads** the browser every time you save a file.

#### Step 1: Install the Extension
1. Open VS Code
2. Press `Ctrl + Shift + X` to open Extensions panel
3. Search for: **Live Server**
4. Install the one by **Ritwick Dey** (it has millions of downloads)
5. Restart VS Code if prompted

#### Step 2: Run the Project
1. Open the `c:\QR Code` folder in VS Code (`File → Open Folder`)
2. Open `index.html` in the editor
3. Look at the **bottom-right corner** of VS Code — click **"Go Live"**
4. Your browser opens automatically at `http://127.0.0.1:5500`
5. ✅ Done! Every time you save `index.html` or `style.css`, the browser refreshes automatically

#### Step 3: Stop Live Server
- Click **"Port: 5500"** in the bottom-right corner of VS Code, OR
- Press `Ctrl + Shift + P` → type `Live Server: Stop Server` → Enter

#### Why Use This?
| Feature | Live Server |
|---|---|
| Auto-reload on save | ✅ Yes (instant) |
| No terminal needed | ✅ Yes |
| Works offline | ✅ Yes |
| Installation | One-time only |

---

### ✅ Option 2 — `npx serve` Command (Terminal)

**Best for:** Quick testing or sharing with someone on your local network.

#### Run This Command in Terminal:
```bash
npx serve "c:\QR Code" --listen 3000
```

Then open your browser and go to:
```
http://localhost:3000
```

#### Important Notes:
> ⚠️ **If port 3000 is already in use**, `serve` will automatically pick a different port (e.g. `55431`). Check the terminal output — it will tell you the exact URL to open.
> 
> Example terminal output when port is busy:
> ```
> - Local:    http://localhost:55431
> - Network:  http://192.168.1.5:55431
> ```
> Just open whichever URL it shows you.

> 💡 The first time you run `npx serve`, it downloads the package (~30 seconds). After that it runs instantly.

#### To Stop the Server:
Press `Ctrl + C` in the terminal.

#### Comparison: `npx serve` vs Live Server

| Feature | `npx serve` | Live Server Extension |
|---|---|---|
| Auto-reload on save | ❌ No (manual refresh) | ✅ Yes (instant) |
| Terminal needed | ✅ Yes | ❌ No |
| Network access | ✅ Yes (share with phone on same WiFi) | ✅ Yes |
| Best for | Testing / Sharing | Development |

---

## 🧩 How Each Section Works

### Section 1 — Navbar
- **Fixed at top** — stays visible while scrolling
- **Glassmorphism effect** — `backdrop-filter: blur(16px)` makes it frosted-glass
- **Smooth scroll** — clicking nav links scrolls to that section using CSS `scroll-behavior: smooth`
- **Shadow on scroll** — JavaScript adds a drop shadow when you scroll down

### Section 2 — Hero
- **Full-screen** using `min-height: 100vh`
- **Floating cards** — 4 cards (sticky note, page sections checklist, QR Ready, stats pill) float up and down using CSS `@keyframes floatY` animation
- **Dot pattern background** — created with CSS `radial-gradient` on the `body::before` pseudo-element
- **Blue gradient glow** — behind the title using CSS `radial-gradient` on `hero::after`

### Section 3 — About (Features Grid)
- **6 feature cards** in a CSS Grid layout (3 columns)
- **Hover lift effect** — `transform: translateY(-6px)` on hover
- **Icon backgrounds** — colored using custom CSS classes (`fi-blue`, `fi-green`, etc.)
- **Fade-in animations** — triggered by `IntersectionObserver` JavaScript API

### Section 4 — Media Gallery
- **2 image cards** side by side using CSS Grid `grid-template-columns: 1fr 1fr`
- **Image zoom on hover** — `transform: scale(1.04)` on the `<img>` tag
- **Video embed** — standard YouTube `<iframe>` with `aspect-ratio: 16/9`
- **Browser bar UI** — fake browser dots (red/yellow/green) above the video for aesthetic

### Section 5 — Links Grid
- **6 link cards** in a CSS Grid layout (3 columns)
- Each card is a real `<a href="">` tag pointing to a URL
- **Icon lift on hover** — `transform: scale(1.12)` on the icon box
- **Update these links** to point to your actual GitHub, website, email, etc.

### Section 6 — QR Code Generator
- **Input field** — type any URL
- **Generate button** — calls the `generateQR()` JavaScript function
- **QR library** — uses [QRCode.js](https://github.com/davidshimjs/qrcodejs) loaded from CDN (no install needed)
- **Download PNG** — `downloadQR()` creates an `<a>` element and triggers a click to save the image
- **Copy URL** — uses `navigator.clipboard.writeText()` Web API
- **Auto-generates on load** — `window.addEventListener('load', () => generateQR())` runs it instantly

---

## ⚙️ How the JavaScript Works

All JavaScript is at the bottom of `index.html` inside a `<script>` tag. There are 4 parts:

### 1. Scroll Animations (`IntersectionObserver`)
```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
```
- Any HTML element with class `fade-up` starts invisible (`opacity: 0`)
- When it enters the viewport (10% visible), the `visible` class is added
- CSS transitions then animate it into view

### 2. Navbar Scroll Effect
```javascript
window.addEventListener('scroll', () => {
  const nav = document.getElementById('navbar');
  nav.style.boxShadow = window.scrollY > 60 ? '0 4px 24px rgba(0,0,0,0.08)' : 'none';
});
```
- Listens to scroll events
- Adds a shadow to the navbar after scrolling 60px down

### 3. QR Code Generator
```javascript
function generateQR() {
  const url = document.getElementById('qr-url-input').value.trim();
  const canvas = document.getElementById('qr-canvas');
  canvas.innerHTML = '';   // Clear previous QR
  new QRCode(canvas, {
    text: url,
    width: 220, height: 220,
    colorDark: '#2563EB',   // Blue QR dots
    colorLight: '#FFFFFF',   // White background
    correctLevel: QRCode.CorrectLevel.H
  });
}
```
- Reads the URL from the input field
- Clears the previous QR code
- Creates a new QR code with blue color matching the design

### 4. Download & Copy
```javascript
function downloadQR() {
  const img = document.querySelector('#qr-canvas img');
  const link = document.createElement('a');
  link.href = img.src;
  link.download = 'qr-code.png';
  link.click();   // Triggers browser download
}

function copyURL() {
  navigator.clipboard.writeText(url).then(() => {
    btn.textContent = '✅ Copied!';
    setTimeout(() => btn.textContent = '📋 Copy URL', 2000);
  });
}
```

---

## ⚡ How the CSS Works

### Design System (CSS Variables)
All colors, shadows, and sizes are defined at the top of `style.css` as CSS variables:
```css
:root {
  --blue:        #2563EB;    /* Main accent color */
  --blue-light:  #EFF6FF;    /* Light blue backgrounds */
  --blue-dark:   #1d4ed8;    /* Darker blue for hover states */
  --bg:          #F8F9FB;    /* Page background (light gray) */
  --bg-white:    #FFFFFF;    /* Card backgrounds */
  --text-head:   #0F172A;    /* Heading color (near-black) */
  --text-light:  #6B7280;    /* Body text (gray) */
  --shadow-lg:   0 12px 40px rgba(0,0,0,0.1);  /* Large shadow */
}
```
To change the accent color, just update `--blue` to any hex color.

### Dot Pattern Background
```css
body::before {
  background-image: radial-gradient(circle, #E5E7EB 1px, transparent 1px);
  background-size: 28px 28px;
}
```
This creates the subtle dot grid pattern across the entire page background.

### Floating Card Animations
```css
@keyframes floatY {
  from { transform: translateY(0); }
  to   { transform: translateY(-12px); }
}
.float-card {
  animation: floatY 4s ease-in-out infinite alternate;
}
```
Each floating card has a different `animation-delay` so they don't all move in sync.

### Glassmorphism Navbar
```css
.navbar {
  background: rgba(255,255,255,0.85);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
}
```

---

## 🔧 Customization Guide

### Change the Hero Title & Subtitle
Open `index.html`, find the `Hero Section` and update:
```html
<h1 class="hero-title">
    Your Project,<br />
    <span class="accent">One QR Away.</span>   ← Change this
</h1>
<p class="hero-subtitle">
    A premium digital page...   ← Change this description
</p>
```

### Change the About Description
Find the `#about` section and update the `section-desc` paragraph:
```html
<p class="section-desc">
    This is a Digital Compendium...   ← Your project description here
</p>
```

### Change the Gallery Images
1. Add your images to the `images/` folder
2. Update the `src` attributes:
```html
<img src="images/YOUR_IMAGE.png" alt="Your description" />
```

### Change the YouTube Video
Find the `<iframe>` tag in the Media section:
```html
<iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" ...>
```
Replace `dQw4w9WgXcQ` with your YouTube video ID.
> To find the ID: go to your video → the URL is `youtube.com/watch?v=VIDEO_ID` — copy the `VIDEO_ID` part.

### Change the Quick Links
Find the Links section and update each card's `href`:
```html
<a href="https://github.com/YOUR_USERNAME/REPO" ...>    ← GitHub
<a href="https://your-website.com" ...>                 ← Website
<a href="mailto:your@email.com" ...>                    ← Contact
```

### Change the Footer Name
```html
Made with ♥ by <strong>Mayank</strong>.   ← Change Mayank to your name
```

### Change the Accent Color
Open `style.css` and update the `:root` variables:
```css
--blue:      #2563EB;   ← Change to any color (e.g. #7C3AED for purple)
--blue-dark: #1d4ed8;   ← Should be a darker version of above
--blue-light:#EFF6FF;   ← Should be a very light tint of above
```

---

## 🌐 Deploying Online (Free Hosting)

To make the QR code work from anywhere in the world, you need a live URL. Here are the two easiest options:

### Option A — Netlify (Drag & Drop — Easiest)

1. Go to [netlify.com](https://netlify.com) and create a free account
2. Click **"Add new site"** → **"Deploy manually"**
3. Open File Explorer, navigate to `c:\QR Code`
4. **Drag the entire folder** into the Netlify browser window
5. Wait ~10 seconds → you get a live URL like:
   ```
   https://amazing-project-abc123.netlify.app
   ```
6. (Optional) Go to Site Settings → Change site name to something cleaner
7. Copy that URL → paste in the QR Generator → Download PNG 🎉

### Option B — Vercel

1. Go to [vercel.com](https://vercel.com) and sign up (use GitHub)
2. Click **"Add New → Project"**
3. Upload your folder or connect GitHub repo
4. Click Deploy → get your live URL

### Comparison

| Platform | Speed | Custom Domain | Best For |
|---|---|---|---|
| **Netlify** | ⚡ Very fast | ✅ Free | Beginners — drag & drop |
| **Vercel** | ⚡ Very fast | ✅ Free | Developers using GitHub |
| **GitHub Pages** | Fast | ✅ Free | If you use Git |

---

## 📱 QR Code Generator — Built-in Tool

The QR generator is **built directly into the page** — no external service, no data sent anywhere.

| Step | Action |
|---|---|
| 1 | Scroll to the **QR Code** section |
| 2 | Type or paste your live URL in the input field |
| 3 | Click **⚡ Generate** (or press `Enter`) |
| 4 | A blue QR code appears instantly |
| 5 | Click **⬇️ Download PNG** to save it |
| 6 | Print it on posters, cards, brochures |

> **Privacy note:** The QR code is generated entirely in your browser using [QRCode.js](https://github.com/davidshimjs/qrcodejs). No URL or data is sent to any server.

---

## 💡 Real-World Use Cases

| Scenario | How to Use |
|---|---|
| 🎓 **College Project** | Print QR on your title page → anyone scans → sees full project page |
| 🎪 **Events & Fests** | Stick QR on banners → visitors scan → schedule, team info, registration |
| 🍽️ **Restaurant Menu** | QR on tables → customers see digital menu (no printing cost!) |
| 💼 **Portfolio Card** | Print QR on visiting card → recruiters scan → see your full portfolio |
| 📦 **Product Packaging** | QR on box → customers see product details, tutorials, support |
| 📚 **Museum/Library** | QR beside exhibit → visitors read detailed info |

---

## 🛠️ Tech Stack

| Technology | Role | Notes |
|---|---|---|
| **HTML5** | Page structure | Semantic elements, single `index.html` |
| **CSS3** | All styling | Variables, Grid, Flexbox, Animations |
| **Vanilla JavaScript** | Interactivity | Scroll animations, QR generator |
| **Google Fonts (CDN)** | Typography | Inter font — loaded via `@import` in CSS |
| **QRCode.js (CDN)** | QR generation | Loaded via `<script>` tag in HTML |
| **Netlify / Vercel** | Hosting | Free static site hosting |

### Dependencies (No Install Required)

| Library | How It's Loaded | Version |
|---|---|---|
| Google Fonts (Inter) | CSS `@import` URL | Latest |
| QRCode.js | HTML `<script src="...cdnjs...">` | 1.0.0 |

> Everything loads from CDN — **zero npm, zero node_modules, zero build step.**

---

## ❓ Frequently Asked Questions

**Q: The `npx serve` command shows "port 3000 is in use" — what do I do?**
A: Nothing — it automatically picks another port. Just use the URL it shows you in the terminal (e.g. `http://localhost:55431`). This happens when another server from a previous session is still running.

**Q: Why does the QR code not work when I scan it?**
A: If you used `localhost` as the URL, it only works on the device running the server. You need a **live deployed URL** (Netlify/Vercel) for the QR to work from any phone/device.

**Q: I changed the code but the browser is not updating — why?**
A: If using `npx serve`, you need to **manually refresh** the browser (`F5`). If using **Live Server** extension, it auto-refreshes on every save.

**Q: Can I add more sections to the page?**
A: Yes. Copy an existing section block from `index.html`, paste it, change the `id` and content. Add matching styles in `style.css`.

**Q: Can I change the QR color?**
A: Yes. In `index.html`, find the `generateQR()` function and update:
```javascript
colorDark: '#2563EB',   ← Change this to any hex color
```

**Q: How do I use my own images instead of the generated ones?**
A: Add your `.jpg` or `.png` files to the `images/` folder, then update the `src` attributes in `index.html`:
```html
<img src="images/my-photo.jpg" alt="My photo" />
```

**Q: Is this free to use?**
A: Completely free for personal, educational, and non-commercial projects.

---

## 📄 License

Free to use, modify, and deploy for personal and educational purposes.

---

<p align="center">
  <strong>⚡ Digital Compendium</strong><br/>
  <em>Scan. Read. Connect.</em><br/><br/>
  Made with ♥ by <strong>Mayank</strong> · 2025
</p>
#   Q R - C o d e  
 