# QuickAI — YouTube AI Learning Assistant & Dashboard 

QuickAI is a powerful, production-ready developer platform designed to supercharge your learning workflow on YouTube. Built as a **Modular Monolith Architecture** using the **MERN Stack**, it features a cross-origin synchronized **Chrome Extension (Manifest V3)** and an interactive **Web Dashboard**. 

The platform turns passive video consumption into active learning by combining state-of-the-art Generative AI with advanced data-processing pipelines.

---

##  Core Features

###  The YouTube AI Chrome Extension (Core USP)
*   **Single-Shot Summarization:** Extracts closed captions or scrapes transcripts directly from the YouTube DOM to generate structured, markdown-formatted summaries instantly.
*   **Stateful Conversational Agent:** Injects an interactive chat UI directly onto the YouTube viewing page. Users can hold a persistent, back-and-forth Q&A session with an AI agent trained entirely on the video's context.
*   **Intelligent Token-Chunking Pipeline:** Seamlessly bypasses API token limitations for long videos (30+ minutes). A robust backend algorithm splits long transcripts into logical 2-minute segments, processes them iteratively, and compiles extensive, textbook-style notes.
*   **Dynamic Flowchart Visualization:** Automatically extracts architectural logic from video notes and dynamically renders structural **Mermaid.js** charts to visualize complex, nested workflows.

###  Web Dashboard & Developer Tooling
*   **Cross-Origin Stateful Authentication:** A custom-built, stateless **JWT & bcrypt system** that seamlessly shares authentication states between the React Web Dashboard and the background service workers of the Chrome Extension.
*   **AI Resume Reviewer:** Multi-part file handling (**Multer**) allows users to upload PDF resumes securely to Cloudinary, parsing layout text to generate constructive AI analysis and career optimization strategies.
*   **Advanced Image Manipulation:** Integrates native **Gemini Image Generation** alongside industry-standard AI pipelines for automated background removal and object erasing.

---

##  Tech Stack & Architecture

### Backend (Modular Monolith)
*   **Runtime Environment:** Node.js & Express.js (Layered MVC Architecture: Routes ➡️ Controllers ➡️ Services)
*   **Database:** MongoDB Atlas (Mongoose ODM tracking analytical user profiles, study sessions, and persistent chat history)
*   **Authentication:** Stateless JWT (JSON Web Tokens) + Bcrypt Password Hashing
*   **Integrations:** Google Gemini API, Cloudinary SDK, Remove.bg API, Multer, Unpdf

### Chrome Extension (Vite + Vanilla/React Contexts)
*   **Manifest Specification:** Manifest V3
*   **Build Tool:** Vite + Rollup Optimization
*   **DOM Scraping:** Custom MutationObserver tracking YouTube SPA navigation for reliable transcript extraction.
*   **UI Injector:** High-isolation CSS scoping preventing YouTube style leaks into the custom overlay layout.

---

##  Project Structure

```text
├── server/                 # Layered Express.js Backend Monolith
│   ├── src/
│   │   ├── config/         # Database, Gemini, and Cloudinary configurations
│   │   ├── controllers/    # Request handlers (Auth, Document, Image, YouTube)
│   │   ├── middlewares/    # Custom JWT protection & file upload interceptors
│   │   ├── models/         # Mongoose Schemas (User, StudySession, ChatHistory)
│   │   ├── routes/         # Clean REST Endpoints
│   │   └── services/       # Core Business Logic (Chunking pipelines & AI interaction)
│   ├── server.js           # Server Initialization
│   └── package.json
│
└── extension/              # Manifest V3 Chrome Extension Monorepo
    ├── public/             # Extension manifests and asset icons
    ├── src/
    │   ├── background/     # Background service worker (API agent & Token storage)
    │   ├── content/        # YouTube DOM parser, chat injector & style engines
    │   ├── popup/          # UI login and local session management dashboard
    │   └── utils/          # DOM helpers and background communications
    ├── build.js            # Custom production compiling script
    └── vite.config.js       # Rollup engine setup


## Getting Started Locally

1. Clone and Configure the Server
Navigate to the server directory and create your .env file matching this template:
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secure_jwt_secret
GEMINI_API_KEY=your_google_gemini_api_key
REMOVEBG_API_KEY=your_remove_bg_api_key
CLOUDINARY_CLOUD_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_key
CLOUDINARY_API_SECRET=your_cloudinary_secret

Install packages and boot up the development server:
cd server
npm install
npm run server

2. Build and Load the Extension
Navigate to the extension directory to install dependencies and compile the production bundle:
cd extension
npm install
npm run build

To load into your browser:

1. Open Chrome and head to chrome://extensions/.
2. Toggle on Developer mode (top-right corner).
3. Click Load unpacked in the top-left.
4. Select the compiled extension/dist folder.
5. Head to any YouTube video, register/log in via the Extension popup, and start learning!

