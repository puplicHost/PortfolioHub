# PortfolioHub

A modern, responsive portfolio showcase built with **Vue 3** + **Vite** + **Tailwind CSS v4**.

## Features

- Premium dark theme with animated gradient hero
- Search + category filter for projects (All / Portfolios / Business / E-Commerce)
- Responsive project grid (2 cols mobile · 2 cols tablet · 3 cols desktop)
- Glassmorphism cards with smooth hover animations
- Floating WhatsApp button + Back-to-top
- Lazy-loaded images, scroll-reveal animations
- SEO-ready meta tags

## Tech Stack

- Vue 3 (Composition API)
- Vite
- Tailwind CSS v4
- Lucide / Heroicons (inline SVGs)

## Project Structure

```
src/
├── assets/images/      # logo & hero background
├── components/         # Vue components
├── config/config.js    # Site config (name, social links, WhatsApp)
├── data/projects.js    # Project list
├── App.vue
├── main.js
└── style.css
```

## Setup

```bash
npm install
npm run dev      # start dev server
npm run build    # production build
npm run preview  # preview production build
```

## Configuration

Edit `src/config/config.js` to change:
- Site name & description
- WhatsApp number
- Email
- Social links
- Logo & hero background images

Edit `src/data/projects.js` to add or remove projects.
