# 💌 The Date Invitation

A playful, single-file interactive web page for asking someone out on a date. She can't actually say "no" (the No button runs away), then she walks through picking a day, time, activity, and a few fun extras — and you get an email the moment she's done.

Built as one self-contained `index.html` — no build tools, no dependencies, no backend required.

---

## ✨ What it does

1. **The question** — "Will you go out on a date with me?" The "No" button flees the cursor/finger anywhere on screen the moment it gets close. "Yes" is the only real option.
2. **Pick a day & time** — an interactive calendar (today + next 30 days) plus a time picker (quick chips or a custom time).
3. **What should we do?** — Coffee, Food, Arcade, Bowling, Movie, Picnic, Walk, Viewpoint, Fun Questions, or Other — each with its own follow-up options (or a free-text box).
4. **Fun Questions** *(optional)* — a 10-question mini quiz (Spider-Man, Harry Potter, Marvel, pizza toppings, etc.) that doesn't block progress.
5. **Flowers** — pick a favorite type or type in her own.
6. **Anything I should know?** — an optional free-text note (allergies, preferences, anything).
7. **Her name** — the last step, required.
8. **The big finish** — an animated "It's official!" screen with blooming flowers, plus an automatic email to you with everything she picked.

---

## 📁 Files

```
index.html   ← the entire site (HTML + CSS + JS in one file)
README.md    ← this file
```

---

## ⚙️ Setup

All configuration lives near the top of the `<script>` block at the bottom of `index.html`.

### 1. Your details — `PLAN`

```js
const PLAN = {
  asker: "Sam",                     // your name, shown on the final screen
  email: "vasudevsumanth@gmail.com", // where results get emailed
  maxDaysAhead: 29                  // selectable date range = today + 0..29 (30 days)
};
```

### 2. Automatic email — `EMAILJS_CONFIG`

The page uses [EmailJS](https://www.emailjs.com) (free tier, 200 emails/month) to send you an email automatically the instant she finishes — no action needed from her beyond the final "Send it 💌" button.

```js
const EMAILJS_CONFIG = {
  publicKey:  "YOUR_PUBLIC_KEY",
  serviceID:  "YOUR_SERVICE_ID",
  templateID: "YOUR_TEMPLATE_ID"
};
```

**To get these values:**
1. Create a free account at [emailjs.com](https://www.emailjs.com)
2. **Email Services** → Add a service (connect your Gmail) → copy the **Service ID**
3. **Email Templates** → create a new template → copy the **Template ID**
4. **Account → General** → copy your **Public Key**
5. Paste all three into `EMAILJS_CONFIG`

**Template variables available:**

| Variable | Description |
|---|---|
| `{{her_name}}` | Her name |
| `{{day}}`, `{{date}}`, `{{time}}` | Selected day/date/time |
| `{{activity}}`, `{{choice}}` | Chosen activity and sub-choice |
| `{{flower}}` | Preferred flower |
| `{{note}}` | Optional note |
| `{{fun_spiderman}}`, `{{fun_hp}}`, `{{fun_marvel}}`, `{{fun_movie_night}}`, `{{fun_pet}}`, `{{fun_drink}}`, `{{fun_getaway}}`, `{{fun_schedule}}`, `{{fun_game_night}}`, `{{fun_pizza}}` | Fun Questions answers (only filled if she picks "Fun Questions") |

If EmailJS isn't configured (or a send fails), she still sees a **"📧 Email me a copy of this"** link that opens her email client with everything pre-filled to your address — so nothing is ever lost.

---

## 🚀 Hosting

This is a static page — no server needed. Easiest options:

**GitHub Pages**
1. Push this repo to GitHub (public)
2. Rename `index.html`... already named correctly ✅
3. Repo **Settings → Pages** → Source: `main` branch, `/ (root)` → Save
4. Live at `https://yourusername.github.io/your-repo-name/`

**Netlify Drop**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag `index.html` onto the page
3. Get an instant live link

Serving it over `https://` (rather than opening the file locally) is recommended — EmailJS behaves more reliably that way.

---

## 🎨 Customizing

Everything is editable directly in `index.html`:

- **Colors / fonts** — CSS variables at the top of `<style>` (`--rose`, `--blush`, `--gold`, etc.)
- **Activity options** — edit the buttons inside `#screen-activity` and each `#screen-<activity>` section
- **Fun Questions** — add/remove question blocks inside `#screen-fun`, then update `STATE.fun` and the EmailJS params to match
- **Flower choices** — edit `#flower-grid`
- **Dodge sensitivity** — `DANGER_RADIUS` and `DODGE_COOLDOWN` constants near the bottom of the script

---

## 🛠️ Tech

Plain HTML, CSS, and vanilla JavaScript. Fonts via Google Fonts (Fraunces, Plus Jakarta Sans, Caveat). Email via [EmailJS](https://www.emailjs.com) (loaded from jsDelivr CDN). No frameworks, no build step.
