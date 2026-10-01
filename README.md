# Inbox Copilot

> A smart, full-stack browser extension that embeds directly into **Gmail** to draft, tone-match, and generate instant context-aware replies powered by **Spring Boot**, **Google Gemini 3.8 Flash**, and **React (Vite)**.

## 📸 Overview

**Inbox Copilot** seamlessly integrates into the native Gmail compose and reply interface. Instead of switching back and forth between external AI tools and your inbox, users can select a desired tone (e.g., Professional, Casual, Direct, Empathetic) and let the AI analyze incoming context to generate polished email drafts or quick responses directly inside Gmail in seconds.

## ✨ Features

* **Native Gmail Integration:** Injects seamless action buttons and controls directly into Gmail's compose and reply toolbars.
* **Tone-Adjustable Replies:** Generates context-aware replies tailored to specific communication styles and tones.
* **Ultra-Fast Generation:** Powered by Gemini 3.8 Flash for instant draft creation and low latency.
* **Direct DOM Insertion:** Automatically populates email bodies and subject lines right inside your active Gmail window.
* **Custom Tone & Prompt Tuning:** Adjust tone settings on the fly before inserting text into your email draft.

## 🛠️ Tech Stack

### **Frontend / Browser Extension**
* **Framework:** React (via [Vite](https://vitejs.dev/) running locally on port `5174`)
* **Extension Standard:** Chrome Extension Manifest v3 / Content Scripts
* **Styling & UI:** Tailwind CSS / Modern CSS Components
* **HTTP Client:** Axios / Fetch API

### **Backend Service**
* **Framework:** Java / Spring Boot 3.x (running on port `8080`)
* **Build Tool:** Maven / Gradle
* **AI Provider:** Google Gemini 3.8 Flash API
* **Security:** Spring Security & CORS configured for extension requests

## 🚀 Getting Started

### **Prerequisites**

* [Java Development Kit (JDK 17+)](https://www.oracle.com/java/technologies/downloads/)
* [Node.js (v18+) & npm](https://nodejs.org/)
* Google Chrome or any Chromium-based browser
* Google Gemini API Key

### 📦 Installation & Setup

#### **1. Clone the Repository**

```bash
git clone https://github.com/your-username/inbox-copilot.git
cd inbox-copilot
```

#### **2. Backend Setup (Spring Boot)**

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Configure your `src/main/resources/application.properties` (or `application.yml`):
   ```properties
   server.port=8080
   
   # Gemini API Settings
   gemini.api.key=YOUR_GEMINI_API_KEY
   gemini.api.model=gemini-3.8-flash
   ```

3. Run the Spring Boot server:
   ```bash
   ./mvnw spring-boot:run
   ```
   *The backend will start at `http://localhost:8080`.*

#### **3. Frontend & Chrome Extension Setup (React + Vite)**

1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Run Vite dev server (Optional for UI debugging at `http://localhost:5174`):
   ```bash
   npm run dev -- --port 5174
   ```

4. Build the Chrome extension bundle:
   ```bash
   npm run build
   ```
   *This creates a `dist/` build directory containing the extension files.*

#### **4. Load Extension into Chrome**

1. Open Google Chrome and navigate to `chrome://extensions/`.
2. Enable **Developer mode** (toggle switch in the upper-right corner).
3. Click **Load unpacked** and select the `frontend/dist` directory.
4. Open [Gmail](https://mail.google.com/) and open any email or compose box to see **Inbox Copilot** integrated into your toolbar.

## 🔌 API Endpoints (Backend)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/email/reply` | Processes incoming email content & chosen tone; returns a context-aware response draft. |
| `POST` | `/api/email/generate` | Generates a new email draft based on user prompts and tone parameters. |

## 🎨 Project Architecture

```text
inbox-copilot/
├── backend/                  # Spring Boot REST API (Port 8080)
│   ├── src/main/java/        # Controllers, Services, & Gemini Integration
│   └── src/main/resources/   # App Configuration & API Keys
└── frontend/                 # React + Vite Chrome Extension (Port 5174)
    ├── public/               # Manifest v3 JSON & Extension Icons
    └── src/
        ├── content/          # Content scripts injected into Gmail DOM
        ├── components/       # Toolbar UI & Tone Selector components
        └── services/         # API Service client for backend communication
```

## 📜 License

Distributed under the **MIT License**. See `LICENSE` for details.
