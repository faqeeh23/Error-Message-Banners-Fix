# 🚀 Submitty UI Redesign: System Alert Banners

[![Vue 3](https://img.shields.io/badge/Vue.js-3.0-4FC08D?style=for-the-badge&logo=vue.js)](https://vuejs.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_v4-38B2AC?style=for-the-badge&logo=tailwind-css)](https://tailwindcss.com/)
[![Accessibility: WCAG AA](https://img.shields.io/badge/Accessibility-WCAG_AA-blue?style=for-the-badge)](https://www.w3.org/WAI/standards-guidelines/wcag/)

> A modern, componentized, and highly accessible architectural proposal designed specifically to resolve Submitty **Issue #12431**.

---

### 🌟 [**Click Here to View the Interactive Live Demo!**](https://faqeeh23.github.io/Error-Message-Banners-Fix/) 🌟

---

## 🎯 Overview

Submitty relies heavily on system message banners (Warnings, Errors, Success, Info) to communicate critical information to students and instructors. Historically, these banners have lacked a standardized style, often relying on purely colored hardcoded containers that are inconsistent across pages.

This repository serves as a **Proof of Concept (PoC)** demonstrating how Submitty can seamlessly migrate these banners to a unified, reusable **Vue.js** component while strictly adhering to the requested global CSS architecture. 

## ✨ Key Features & Enhancements

### 1. 🧩 100% Reusable Vue Component (`SubmittyAlert.vue`)
At the core of this redesign is a flexible, highly reusable component. 
- **Dynamic Types**: By simply passing a `type="error" | "warning" | "success" | "info"` prop, the component instantly adapts its layout, borders, and semantic iconography.
- **Content Agnostic**: Utilizing Vue `<slot>...</slot>`, the banner can encapsulate anything from a single sentence to a complex interactive form.
- **Emitted Closures**: Close buttons handle logical events (`@close`), decoupling the UI from the backend business logic.

### 2. 🏗️ Seamless Submitty Architecture Integration
The styling approach was engineered specifically to answer the architectural constraints requested by Submitty maintainers:
- **`colors.css`**: All layout colors (backgrounds, borders, text, glows) are strictly defined via CSS variables in the globally available `colors.css` file. It fully supports immediate Light/Dark Mode switching.
- **`server.css`**: All structural classes (padding, flexbox layouts, borders) have been extracted entirely from the Vue component into the global `server.css`.
*(You can literally copy-paste the Vue HTML and those two CSS files into Submitty today, and it will work natively!)*

### 3. 👁️‍🗨️ Extreme Accessibility & Colorblind Support
Accessibility is not an afterthought; it is built into the foundation:
- **Okabe-Ito Color Palette**: Colors have been heavily tuned to the scientifically backed Okabe-Ito palette. Errors use a deep dark red (`red-800/900`) and Warnings use high-contrast golden-oranges, ensuring immediate recognition for users with Protanopia, Deuteranopia, or Tritanopia.
- **Explicit Warning Labels**: Banners no longer rely purely on color. Explicit text tags (e.g., `ERROR`, `WARNING`) and high-contrast circular iconography immediately indicate the context to all users.
- **Screen Reader Support**: Hidden `sr-only` aria labels and `aria-live="polite"` rules announce message significance cleanly to assistive devices.
- **WCAG AA Contrast**: Deeply saturated dark text guarantees readability against the tinted glassy backgrounds in light mode.

### 4. 💎 Premium UI / UX "Wow Factor"
- **Glassmorphism**: Banners utilize a sophisticated `backdrop-blur` effectively turning the background into frosted glass.
- **Micro-interactions**: Subtle hover elevations and smooth entry transitions breathe life into the formerly static UI.

---

## 🛠️ How to View the Demo locally

This repository includes an interactive **Side-by-Side Comparison** App showing the legacy hardcoded UI directly contrasted against the newly proposed component system!

1. Clone this repository and navigate to the `client` directory:
   ```bash
   cd client
   ```
2. Install the necessary dependencies (Vue, Tailwind v4, Lucide Icons):
   ```bash
   npm install
   ```
3. Boot up the Vite Development Server:
   ```bash
   npm run dev
   ```
4. Open the provided `localhost` link in your browser! Make sure to test the **Light/Dark Mode toggle** button located at the top right of the page.

---
*Built as a dedicated engineering proposal for the Submitty Open Source Ecosystem.*
