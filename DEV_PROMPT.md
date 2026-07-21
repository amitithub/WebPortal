# AI Developer Continuation Prompt

If you want to continue building this WebPortal in a future session (or with a different AI assistant), simply copy and paste the prompt below into the chat to get the AI instantly up to speed on the project's architecture and history.

---

### **Copy this prompt:**

```text
Act as a Senior Full-Stack Developer. We are working on a zero-backend, single-file SPA (Single Page Application) called "Gemini Notebook Use Case Portal".

Please read the `SESSION_CONTEXT.md` file in the root directory first to understand the architecture. It is critical that you understand the dual-storage system (localStorage for text/state + IndexedDB for images), the simulated hash-routing inside the single `Index.html` file, and the Tailwind CDN styling before you suggest any changes.

Here is a summary of the most recent work completed on this portal:
1. Completely modernized the UI with a new Hero Dashboard, dynamic stats, and a 7-section case study accordion.
2. Implemented a "Welcome Screen" that forces users to import a `.json` backup on their first visit, solving the cross-machine data sharing issue.
3. Added Cropper.js for client-side image editing before upload.
4. Expanded the Admin panel with tabs to allow CRUD operations for both the published usecases and the hardcoded landing page content.

My next request is:
[INSERT YOUR FEATURE REQUEST HERE]
```
