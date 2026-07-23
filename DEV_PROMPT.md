# 🧠 AI Developer Master Prompt

This file contains the **Master Prompt** designed to instruct an AI coding assistant (like Google's Antigravity or standard Gemini/Claude interfaces) to build the complete **Gemini Notebook Use Case Portal** from scratch or understand its entire architecture instantly.

If you ever lose the source code or want to rebuild this platform in a new environment, simply copy and paste the prompt below to your AI assistant.

---

### **Copy the text below:**

```text
Act as an elite Senior Full-Stack Engineer and UX/UI Designer. Your task is to build a zero-backend, single-file SPA (Single Page Application) called the "Gemini Notebook Use Case Portal". The entire application must be contained within a single `Index.html` file.

### **Core Architecture & Tech Stack:**
1. **Framework:** Pure HTML5, CSS3, and Vanilla JavaScript (ES6+). No React, Vue, or build steps.
2. **Styling:** Tailwind CSS (via Play CDN). Use the `Inter` font for UI and `Fira Code` for prompts.
3. **Dual-Database Persistence:** 
   - Use `localStorage` to synchronously store text-based state (landing page text, JSON arrays of use cases, prompt templates, settings).
   - Use `IndexedDB` to asynchronously store heavy binary media (Base64 screenshots uploaded by users). Ensure `IndexedDB` is cleanly wrapped in Promises.
4. **SPA Routing:** Build a custom router using the `HashChangeEvent` API to show/hide `<main>` sections (e.g., `#home`, `#create`, `#admin`, `#view-all`). Include URL param parsing (e.g., `?id=123`) to open specific feature cards on load.

### **Required Features & UI Components:**
1. **Hero & Global Navigation:** 
   - A sticky header with frosted glassmorphism (`backdrop-blur`) and smooth-scrolling anchor links (Use Cases, Published Usecases, Prompts).
   - A dark/light mode toggle that saves user preference.
   - A Hero section featuring a custom-built SVG logo of "Gemini Notebook" (three nested, gradient blue/purple arches) centered at the top.
2. **Landing Page Sections:**
   - **Overview:** Text block describing Google NotebookLM.
   - **Case Studies (Accordion):** A section highlighting the 7 core use cases for Tableau Technical Support (e.g., Log Investigation, Data Compliance, Mind Maps).
   - **Published Usecases Grid:** A responsive card grid displaying community-submitted features dynamically loaded from `localStorage`.
   - **Expert Prompts:** A section at the bottom containing 4 Tableau-specific prompt templates. Each prompt block must have a "Copy to Clipboard" button utilizing `navigator.clipboard.writeText`.
3. **Content Creator Form:**
   - A `#create` route where users can submit a title, description, URL, and upload multiple screenshots.
   - All textareas must be vertically resizable (`resize-y`).
4. **Split-Screen Reader:**
   - When a user clicks a feature card, load a split-screen view. The left side contains scrolling text (markdown-like bullet lists and paragraphs). The right side is a sticky container displaying the uploaded screenshots and an inline iframe of the reference URL (with a fallback "Open in New Tab" link).
5. **Slack Canvas Generator:**
   - A footer button that opens a `<dialog>` modal. This modal runs a JavaScript function to aggregate the entire portal's state (titles, stats, prompts) into a beautifully formatted text block. Include "Copy to Clipboard" and "Download .txt" buttons.
6. **Admin Dashboard (`#admin`):**
   - Password-protected via a simple client-side check against state.
   - Features full CRUD (Create, Read, Update, Delete) tabs for:
     1. **Landing Page Content:** Edit the Hero text and Case Studies.
     2. **Prompts:** Add, edit, or delete the expert prompt templates.
     3. **Usecases (with Image Cropper):** Edit published features, upload new images, and utilize `Cropper.js` (via CDN) to crop images before saving them to IndexedDB.
     4. **Export/Import:** Export the entire state + IndexedDB images as a `.json` backup file, and import a `.json` file to restore the portal (vital for cross-machine sharing since there is no backend).

### **Design Requirements:**
- Implement "World-Class UX/UI Polish". Use subtle hover micro-animations (`hover:-translate-y-1`), soft drop shadows, rounded corners (`rounded-xl` or `rounded-2xl`), and a "Sophisticated Enterprise" color palette (Deep Slates, Indigo/Blue gradients, Emerald success accents).

Please write the complete `Index.html` file meeting all these requirements.
```
