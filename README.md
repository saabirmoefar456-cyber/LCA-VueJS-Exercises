# Cooking Masterclass Catalogue

A responsive Vue.js single-page application for browsing cooking workshops hosted by expert chefs.

---

## Overview

This app allows users to:
- Browse a catalogue of cooking courses displayed as cards
- See course details including chef name, skill level, price, and availability
- Filter courses by availability and skill level
- Save courses to a wishlist (counter shown in the header)
- Clearly see which courses are sold out

Built with **Vue 3** and **Vite** using component-driven design with props, data, and custom events.

---

## Project Structure

```
src/
├── components/
│   ├── AppHeader.vue      # Sticky header with wishlist counter
│   ├── CourseCard.vue     # Individual course card component
│   └── CourseFilter.vue   # Availability and level filter bar
├── data/
│   └── courses.js         # Local course data array
├── App.vue                # Root component — state and layout
└── main.js                # App entry point
```

---

## Installation & Running Locally

**Prerequisites:** Node.js (v18+) installed

```bash
# 1. Clone the repository
git clone https://github.com/your-username/LCA-VueJS-Exercises.git

# 2. Navigate to the project folder
cd LCA-VueJS-Exercises/week9_ex01_vuejs_cooking_catalogue

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

Open your browser at http://localhost:5173

**To build for production:**
```bash
npm run build
```

---

## Features Implemented

- Dynamic course cards (rendered from data array — no hard-coded duplicates)
- Wishlist save/unsave with animated counter in header
- Sold Out badge for unavailable courses
- Filter by availability (all / available only)
- Filter by skill level (All / Beginner / Intermediate / Advanced)
- Animated card transitions when filters change
- Price formatted with South African Rand (R) and thousands separator
- Hover animations on cards and save button
- Responsive layout for desktop and mobile

---

## Screenshot

*(Add a screenshot of the running app here after running npm run dev)*

![Cooking Masterclass Screenshot](screenshot.png)
