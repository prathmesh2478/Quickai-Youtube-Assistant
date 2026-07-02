# QuickAI — YouTube AI Learning Assistant & Dashboard 🚀

[![Watch the Demo Video](https://img.shields.io/badge/Watch-Demo%20Video-red?style=for-the-badge&logo=youtube&logoColor=white)](https://drive.google.com/file/d/1o2GVcFo3v2m6ey0KtP0hEVnd5BepZqMT/view?usp=sharing)

QuickAI is a powerful, production-ready developer platform designed to supercharge your learning workflow on YouTube. Built as a **Modular Monolith Architecture** using the **MERN Stack**, it features a cross-origin synchronized **Chrome Extension (Manifest V3)** and an interactive **Web Dashboard**. 

The platform turns passive video consumption into active learning by combining state-of-the-art Generative AI with advanced data-processing pipelines.

---

## 🌟 Core Features

### 🎬 The YouTube AI Chrome Extension (Core USP)
* **Single-Shot Summarization:** Extracts closed captions or scrapes transcripts directly from the YouTube DOM to generate structured, markdown-formatted summaries instantly.
* **Stateful Conversational Agent:** Injects an interactive chat UI directly onto the YouTube viewing page. Users can hold a persistent, back-and-forth Q&A session with an AI agent trained entirely on the video's context.
* **Intelligent Token-Chunking Pipeline:** Seamlessly bypasses API token limitations for long videos (30+ minutes). A robust backend algorithm splits long transcripts into logical 2-minute segments, processes them iteratively, and compiles extensive, textbook-style notes.
* **Dynamic Flowchart Visualization:** Automatically extracts architectural logic from video notes and dynamically renders structural **Mermaid.js** charts to visualize complex, nested workflows.

### 💻 Web Dashboard & Developer Tooling
* **Cross-Origin Stateful Authentication:** A custom-built, stateless **JWT & bcrypt system** that seamlessly shares authentication states between the React Web Dashboard and the background service workers of the Chrome Extension.
* **AI Resume Reviewer:** Multi-part file handling (**Multer**) allows users to upload PDF resumes securely to Cloudinary, parsing layout text to generate constructive AI analysis and career optimization strategies.
* **Advanced Image Manipulation:** Integrates native **Gemini Image Generation** alongside industry-standard AI pipelines for automated background removal and object erasing.

---

## 🛠️ Tech Stack & Architecture

### Backend (Modular Monolith)
* **Runtime Environment:** Node.js & Express.js (Layered MVC Architecture: Routes ➡️ Controllers ➡️ Services)
* **Database:** MongoDB Atlas (Mongoose ODM tracking analytical user profiles, study sessions, and persistent chat history)
* **Authentication:** Stateless JWT (JSON Web Tokens) + Bcrypt Password Hashing
* **Integrations:** Google Gemini API, Cloudinary SDK, Remove.bg API, Multer, Unpdf

### Chrome Extension (Vite + Vanilla/React Contexts)
* **Manifest Specification:** Manifest V3
* **Build Tool:** Vite + Rollup Optimization
* **DOM Scraping:** Custom MutationObserver tracking YouTube SPA navigation for reliable transcript extraction.
* **UI Injector:** High-isolation CSS scoping preventing YouTube style leaks into the custom overlay layout.

---

## 📂 Project Structure

```text
├── client/                     # React Frontend Web Dashboard
│   ├── public/                 # Static web assets & favicons
│   ├── src/
│   │   ├── assets/             # Frontend UI images and styling graphics
│   │   ├── components/         # Reusable UI components (Navbar, Sidebar, Loaders)
│   │   ├── context/            # React Context API for global state (Auth, UI)
│   │   ├── pages/              # View screens (Dashboard, ResumeReview, NoteView)
│   │   ├── App.jsx             # Main Application component & client router
│   │   └── main.jsx            # React DOM Initialization
│   ├── index.html              # Core single-page entry layout
│   ├── package.json            # Frontend script dependencies
│   └── vite.config.js          # Client Vite compiler config
│
├── extension/                  # Manifest V3 Chrome Extension Monorepo
│   ├── public/                 # Extension manifests, badges, and asset icons
│   ├── src/
│   │   ├── background/         # Service worker tracking API tokens & Auth sync
│   │   ├── content/            # YouTube DOM MutationObserver & custom Chat Overlay UI
│   │   ├── popup/              # Standalone login extension overlay dashboard
│   │   └── utils/              # Platform message brokers & DOM extraction tools
│   ├── build.js                # Custom isolated distribution pipeline script
│   ├── package.json            # Extension development dependencies
│   └── vite.config.js          # Rollup bundling engine properties
│
└── server/                     # Layered Express.js Backend Monolith
    ├── src/
    │   ├── config/             # Connection pooling configurations (MongoDB, Gemini, Cloudinary)
    │   ├── controllers/        # Request controllers (Auth, Document parsing, AI workflows)
    │   ├── middlewares/        # Custom Route interceptors (JWT claims guard & Multer)
    │   ├── models/             # Mongoose schemas (User records, Sessions, Prompt history)
    │   ├── routes/             # Isolated Router mounting layers
    │   └── services/           # Heavy processing core (Token-chunking engine & Gemini logic)
    ├── uploads/                # Volatile memory disk layer for incoming files/resumes
    ├── .env.example            # Blank variables checklist blueprint
    ├── .gitignore              # Local secrets filter mapping
    ├── package.json            # Node backend pipeline dependencies
    └── server.js               # Application Entry point & Express boot listener
