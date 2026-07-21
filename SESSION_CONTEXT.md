Project: Gemini Notebook Use Case PortalLast Updated: [Current Date]File Delivered: index.html (Single-file SPA architecture)

1. Core Architecture Decisions
Zero Backend / Edge Computing: The app runs 100% in the browser. There is no Node.js, Python, or external database.
Dual-Storage Engine (Crucial):
localStorage: Stores the JSON state object (titles, text, settings). It is synchronous and fast, but has a ~5MB limit.
IndexedDB (Database: NotebookPortalDB, Store: media): Stores image blobs (Base64). It is asynchronous and handles gigabytes of data. We had to split these because putting images in localStorage was crashing the browser.
Smart Video Iframe Parser (getEmbedUrl): Browsers block standard youtube.com/watch?v= links in iframes. We built a regex parser to auto-convert YouTube and Loom links into their /embed/ equivalents on the fly.
2. Routing Logic (Single File Workaround)
Because everything is in index.html, we simulated a router:

Home/Creator View: Default state (index.html).
Feature View (New Tab): Uses Query Parameters (index.html?id=1690000000000). Fetches text from state, fetches images from IndexedDB.
View All / Admin: Uses Hash Routing (index.html#view-all, index.html#admin).
Note: The hashchange event listener was explicitly added to fix a bug where opening these in new tabs didn't trigger the UI update.
3. State Management Shape
The state object in localStorage looks exactly like this:

{  "isDark": false,  "password": "admin123",  "adminEmail": "admin@yourcompany.com",  "portalTitle": "Gemini Notebook Use Case",  "features": [    {      "id": "1690000000000",      "title": "Mind Map",      "details": "Text...",      "usecase": "Text...",      "refUrl": "https://...",      "media": [{ "type": "video", "url": "https://..." }]       // Note: Images are NOT here. They are in IndexedDB under the key "1690000000000"    }  ]}
4. Current Constraints & Quirks
Cross-Device Sync: Because there is no backend, data lives on the local machine. We added an Export/Import JSON feature to manually move data between computers.
EmailJS: The feedback form is wired up to log to the console by default. To actually send emails, the 3 variables at the top of the <script> tag (EMAILJS_SERVICE_ID, etc.) must be populated with valid EmailJS credentials.
Theme Persistence: Fixed a bug where dark mode was resetting in new tabs. applyTheme() now runs strictly before handleRoute() on DOM load to prevent "flash of white screen".
5. What Was Built So Far
 Gemini branded, high-fidelity UI (Dark/Light mode).
 Creator Form (Text, Details, Usecase, Ref URL, Images, Videos).
 Left Sidebar with live published list.
 "View All" Grid page with thumbnails.
 Split-Screen Feature Reader (Text scrolls left, Media is sticky right).
 Admin Panel (Password gate, Edit/Update/Delete features).
 Cross-tab Dark Mode consistency.
 Auto-resizing of uploaded images (object-contain).
 Export/Import Database functionality.
 Feedback Modal (UI complete, awaiting EmailJS keys).
6. Logical Next Steps (If requested later)
Search/Filter: Add a search bar in the sidebar to filter features by title.
Drag-and-Drop Reordering: Allow admins to change the order of features in the sidebar.
Markdown Support: Integrate a library like marked.js so users can use bold and code blocks in the Details/Usecase textareas instead of just plain text.
PWA (Progressive Web App): Add a manifest.json and Service Worker so stakeholders can "Install" this web app to their desktop like a native application.


To ensure you can seamlessly continue building this application in the future—whether with me in a new chat session or with another developer—I have generated a **Session Context Document**. 

This file captures the hidden architectural decisions, the specific workarounds we built (like the IndexedDB fix), and the exact current state of the app.

### 📋 Instructions:
Save the text below as `SESSION_CONTEXT.md` in your GitHub repository next to the `README.md` and `index.html` files. 

Next time you want to add a feature, simply open a new AI chat and say: *"I want to add [New Feature] to my app. Here is my session context: [Paste this file]."*

***

```markdown
# 🧠 Session Context & Architecture Log
**Project:** Gemini Notebook Use Case Portal
**Last Updated:** [Current Date]
**File Delivered:** `index.html` (Single-file SPA architecture)

## 1. Core Architecture Decisions
* **Zero Backend / Edge Computing:** The app runs 100% in the browser. There is no Node.js, Python, or external database.
* **Dual-Storage Engine (Crucial):** 
  * `localStorage`: Stores the JSON `state` object (titles, text, settings). It is synchronous and fast, but has a ~5MB limit.
  * `IndexedDB` (Database: `NotebookPortalDB`, Store: `media`): Stores image blobs (Base64). It is asynchronous and handles gigabytes of data. *We had to split these because putting images in localStorage was crashing the browser.*
* **Smart Video Iframe Parser (`getEmbedUrl`):** Browsers block standard `youtube.com/watch?v=` links in iframes. We built a regex parser to auto-convert YouTube and Loom links into their `/embed/` equivalents on the fly.

## 2. Routing Logic (Single File Workaround)
Because everything is in `index.html`, we simulated a router:
* **Home/Creator View:** Default state (`index.html`).
* **Feature View (New Tab):** Uses Query Parameters (`index.html?id=1690000000000`). Fetches text from `state`, fetches images from `IndexedDB`.
* **View All / Admin:** Uses Hash Routing (`index.html#view-all`, `index.html#admin`). 
* *Note:* The `hashchange` event listener was explicitly added to fix a bug where opening these in new tabs didn't trigger the UI update.

## 3. State Management Shape
The `state` object in localStorage looks exactly like this:
```json
{
  "isDark": false,
  "password": "admin123",
  "adminEmail": "admin@yourcompany.com",
  "portalTitle": "Gemini Notebook Use Case",
  "features": [
    {
      "id": "1690000000000",
      "title": "Mind Map",
      "details": "Text...",
      "usecase": "Text...",
      "refUrl": "https://...",
      "media": [{ "type": "video", "url": "https://..." }] 
      // Note: Images are NOT here. They are in IndexedDB under the key "1690000000000"
    }
  ]
}
```

## 4. Current Constraints & Quirks
* **Cross-Device Sync:** Because there is no backend, data lives on the local machine. We added an **Export/Import** JSON feature to manually move data between computers.
* **EmailJS:** The feedback form is wired up to log to the console by default. To actually send emails, the 3 variables at the top of the `<script>` tag (`EMAILJS_SERVICE_ID`, etc.) must be populated with valid EmailJS credentials.
* **Theme Persistence:** Fixed a bug where dark mode was resetting in new tabs. `applyTheme()` now runs strictly before `handleRoute()` on DOM load to prevent "flash of white screen".

## 5. What Was Built So Far
- [x] Gemini branded, high-fidelity UI (Dark/Light mode).
- [x] Creator Form (Text, Details, Usecase, Ref URL, Images, Videos).
- [x] Left Sidebar with live published list.
- [x] "View All" Grid page with thumbnails.
- [x] Split-Screen Feature Reader (Text scrolls left, Media is sticky right).
- [x] Admin Panel (Password gate, Edit/Update/Delete features).
- [x] Cross-tab Dark Mode consistency.
- [x] Auto-resizing of uploaded images (`object-contain`).
- [x] Export/Import Database functionality.
- [x] Feedback Modal (UI complete, awaiting EmailJS keys).

## 6. Logical Next Steps (If requested later)
1. **Search/Filter:** Add a search bar in the sidebar to filter features by title.
2. **Drag-and-Drop Reordering:** Allow admins to change the order of features in the sidebar.
3. **Markdown Support:** Integrate a library like `marked.js` so users can use **bold** and `code blocks` in the Details/Usecase textareas instead of just plain text.
4. **PWA (Progressive Web App):** Add a `manifest.json` and Service Worker so stakeholders can "Install" this web app to their desktop like a native application.
```

*** 

*You now have a complete, stakeholder-ready repository containing:*
1. **`index.html`** (The fully working, bug-tested application)
2. **`README.md`** (The marketing/overview documentation)
3. **`SESSION_CONTEXT.md`** (The deep technical blueprint for future development)



