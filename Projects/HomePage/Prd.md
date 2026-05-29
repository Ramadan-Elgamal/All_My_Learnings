Here is the comprehensive Product Requirements Document (PRD) compiling all the established details, mechanics, and structures for your project.
# Product Requirements Document (PRD)
## Project: Ultimate Access Hub (Personal Command Center)
### 1. Project Overview
The Ultimate Access Hub is a highly personalized, blazing-fast web dashboard designed to serve as a custom "New Tab" page in the Brave browser. The primary objective is to eliminate navigational friction by using a heavily keyboard-driven interface. It centralizes routing to frequently used websites, local development environments, AI tools, learning platforms, personal tracking tools, and a built-in Kanban board.
### 2. Technology Stack
 * **Frontend Framework:** React
 * **Language:** TypeScript
 * **State Management:** Zustand (for lightweight, sub-hub view switching)
 * **UI/Styling:** Shadcn UI (combined with Tailwind CSS)
 * **Hosting:** Netlify (Configured as the default browser home page)
 * **Database:** MongoDB (specifically for Kanban board data persistence, likely connected via a lightweight API layer)
### 3. Core Mechanics & User Experience
 * **Keyboard-First Navigation:** The application relies on a two-tier keyboard shortcut system.
   * **Global Shortcuts (Ctrl + [Key]):** Used to navigate from the Core Hub to specific sub-hubs.
   * **Local Shortcuts (Single Key):** Used within a specific sub-hub to immediately launch a target URL in a new background tab (e.g., pressing f inside the Social Hub opens Facebook).
 * **Native Override:** The application utilizes e.preventDefault() to aggressively override Brave's default browser shortcuts (like Ctrl + S or Ctrl + H) to ensure seamless dashboard navigation.
 * **Input Protection:** The shortcut listener automatically disables itself when the user is typing inside an INPUT or TEXTAREA (crucial for adding/editing tasks in the Kanban board).
### 4. Hub Architecture & Shortcut Mapping
The application is structured around a "Core Hub" which branches into distinct, modular "Sub-Hubs".
#### 4.1 Global Navigation Shortcuts
 * Ctrl + S ➔ Social Media Hub
 * Ctrl + F ➔ Freelance Hub
 * Ctrl + H ➔ LocalHosts Hub
 * Ctrl + P ➔ Web Apps Hub
 * Ctrl + A ➔ AI Tools Hub
 * Ctrl + C ➔ Courses Hub
 * Ctrl + K ➔ Kanban Board
 * Ctrl + M ➔ Cinema & Tracking Hub
 * Ctrl + I ➔ Design & Architecture Hub
 * Ctrl + Esc ➔ Return to Core Hub
#### 4.2 Sub-Hub Link Directories
**Social Media Hub**
 * Instagram (i)
 * TikTok (t)
 * Facebook (f)
 * YouTube (y)
 * LinkedIn (l)
**Freelance Hub**
 * Khamsat (k)
 * Upwork (u)
 * Mostaql (m)
 * Freelancer (f)
**LocalHosts Hub**
 * localhost:5000
 * localhost:3000
 * localhost:5173
 * localhost:5678
 * localhost:27017
**Web Apps Hub**
 * PromptCowboy
**AI Tools Hub**
 * Gemini
 * Gemini AI Studio
 * Claude
 * ChatGPT
 * Mistral AI
 * Ollama (o)
**Courses Hub**
 * Udemy Business
 * Scrimba
 * Leetcode
**Cinema & Tracking Hub**
 * Letterboxd (l)
 * TMDB (t)
 * IMDb (i)
 * YouTube Trailers (y)
**Design & Architecture Hub**
 * Shadcn UI Documentation (s)
 * Pinterest (p)
### 5. Future Considerations / Extensibility
 * **API Integration:** The frontend hosted on Netlify will require a backend connection (e.g., Node/Express server or Netlify Serverless Functions) to handle the MongoDB queries for the Kanban board.
 * **Scalability:** The useShortcuts hook and the Zustand HubStore are designed modularly. Adding a new hub requires only defining the shortcut in the main controller and passing the key-value pairs of URLs to the new hub component.
