---

# 📘 **README.md (English Version — Clean & Professional)**

````md
# Vue 3 + Vite + TypeScript + SCSS Starter

A clean and modern starter template built with **Vue 3**, **Vite**, **TypeScript**, **SCSS**, and **PostCSS**.  
Ideal for learning Vue fundamentals while following best practices for structure and scalability.

---

## 🚀 Tech Stack

- **Vue 3** — Composition API
- **Vite** — Next-generation frontend tooling
- **TypeScript** — Type safety and better DX
- **Sass (SCSS)** — Styling preprocessor
- **PostCSS** — Autoprefixing & nested rules support

---

## 📦 Installation

Create a new Vite + Vue + TypeScript project:

```bash
npm create vite@latest my-app -- --template vue-ts
```

Go to the project directory:

```bash
cd my-app
```

Install dependencies:

```bash
npm install
```

---

## 🎨 Add SCSS Support

Install Sass:

```bash
npm install -D sass
```

You can now use SCSS inside Vue components:

```vue
<style lang="scss">
.container {
  padding: 16px;
}
</style>
```

---

## 🛠 Add PostCSS

Install PostCSS and recommended plugins:

```bash
npm install -D postcss postcss-nested autoprefixer
```

Create `postcss.config.js`:

```js
export default {
  plugins: {
    "postcss-nested": {},
    autoprefixer: {},
  },
};
```

---

## 📁 Recommended Project Structure

```
src/
  components/
  composables/
  styles/
    main.scss
    variables.scss
    mixins.scss
  views/
  router/
  App.vue
  main.ts
```

Import global styles in `main.ts`:

```ts
import "./styles/main.scss";
```

---

## ▶️ Development

Start the development server:

```bash
npm run dev
```

---

## 📦 Production Build

```bash
npm run build
```

---

## 🔧 Preview Production Build

```bash
npm run preview
```

---

## 📄 License

MIT © 2025
