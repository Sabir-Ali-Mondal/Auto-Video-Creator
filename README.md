# AI Video Creator Pro - Unified Suite

**AI Video Creator Pro** is a powerful, browser-based application that transforms structured JSON data into engaging, narrated videos. It offers a unique dual-engine approach, allowing users to create either data-driven graph presentations or visually rich creative showcases from a single, intuitive script format.

This project bridges the gap between data and storytelling, enabling developers, marketers, and analysts to produce programmatic videos without complex editing software.



---

## What is the Goal of this Website?

The primary goal of **AI Video Creator Pro** is to **democratize video creation through code**. It provides a declarative, script-based workflow to generate dynamic visual content. Instead of manually manipulating timelines and assets in a traditional video editor, users define the video's structure, content, and narration in a simple JSON file.

### Key Objectives:

1.  **Efficiency:** To enable rapid creation of videos for recurring needs like weekly reports, product explainers, or educational content. Change the data in the JSON, and the video is instantly updated.
2.  **Flexibility:** To offer two distinct visual styles from a unified framework:
    *   **Graph Presentation Mode:** For professional, clear, and data-heavy content (e.g., business intelligence, financial reports, scientific analysis).
    *   **Creative Video Mode:** For marketing, artistic showcases, and engaging educational content with custom graphics, quizzes, and effects.
3.  **Accessibility:** To lower the barrier to video creation. Anyone comfortable with JSON can create a polished video, complete with animations and voiceover, directly in their browser.
4.  **Automation:** To serve as a powerful rendering engine in an automated pipeline. A server could generate JSON scripts from a database or API, and this tool could be used to render the final video content.

---

## How it Works: The Core Concept

The application is built around a central idea: **JSON as a Video Timeline**. The user provides a JSON script that defines a series of "scenes." Each scene has a `type` (e.g., `title`, `chart`, `p5_js_3d`, `quiz`) and `content` (text, data, narration).

The application parses this JSON and passes it to one of two rendering engines:

1.  **GraphPresenter:** Uses **Chart.js** to render animated, interactive charts and graphs. The narration is tightly synchronized with data point highlights, creating a dynamic presentation.
2.  **CreativeVideoRenderer:** Uses a **p5.js**-powered engine to draw custom graphics, tables, quizzes, and even 3D sketches on an HTML5 canvas. It focuses on cinematic transitions and visual flair.

Both engines leverage the browser's **Web Speech API** for text-to-speech narration, bringing the scripts to life.

---

## How I Will Enhance This Project

The current implementation is a robust and feature-rich prototype. The following enhancements will elevate it to a production-ready, extensible, and maintainable application.

### 1. Architecture & Code Quality

The current single-file structure is great for a demo but needs to be modularized for future growth.

-   **Refactor into ES Modules:** Break down the monolithic `<script>` tag into separate modules (`main.js`, `ui.js`, `graphPlayer.js`, `creativePlayer.js`, `utils.js`). This improves organization, maintainability, and enables code-splitting.
-   **Introduce a Build Step:** Use a modern build tool like **Vite** or **Webpack**. This will provide benefits like:
    -   Hot Module Replacement (HMR) for a better development experience.
    -   JavaScript bundling and minification for production performance.
    -   Easy integration of CSS pre-processors (like SASS) if needed.
-   **Migrate to TypeScript:** Convert the codebase to TypeScript. This will introduce static typing, reducing runtime errors, improving developer tooling (autocomplete, refactoring), and making the player APIs explicit and self-documenting.
-   **Formal State Management:** Replace the simple `globalState` object with a more robust solution like **Pinia** or **Zustand** if the application complexity grows, especially for managing UI state and player state cohesively.

### 2. Core Feature Enhancements

The most critical missing piece is the ability to save the created video.

-   **Implement Video Export:**
    -   **Short-Term:** Use the `MediaRecorder` API to record the canvas element and the synthesized speech into a WebM video file. This is a client-side, real-time recording solution.
    -   **Long-Term/Advanced:** Integrate **FFmpeg.wasm** to allow for more complex client-side rendering. This would enable frame-by-frame rendering (non-real-time), which produces higher quality output and is not dependent on the machine's performance during recording. It also allows for adding separate audio tracks and exporting to MP4.
-   **Timeline & Interactive Editing:**
    -   Add a visual timeline UI below the player that shows scene divisions and narration markers.
    -   Allow users to drag-and-drop to reorder scenes, visually updating the JSON script in the editor.
-   **Audio & Music:**
    -   Add support for a background music track (`"audio": { "backgroundMusic": "url/to/music.mp3" }`).
    -   Implement volume controls and automatic "ducking" (lowering music volume) during narration.

### 3. Player & Scene Enhancements

Expand the creative possibilities by adding more scene types and options.

-   **New Scene Types:**
    -   `image`: A scene to display an image with Ken Burns (pan/zoom) effects.
    -   `videoClip`: A scene to play a short, externally hosted video clip.
    -   `code`: A scene that displays a block of code with syntax highlighting and line-by-line animation.
    -   `map`: A scene that uses a library like Leaflet.js to show and animate map data.
-   **Advanced Theming:**
    -   Allow the JSON to specify a full theme (colors, fonts) that applies globally.
    -   Create a simple UI for users to pick colors and fonts, which then generates the theme JSON.
-   **Customizable Narration:**
    -   Allow the JSON to specify which voice (`voiceURI`) to use for narration on a per-scene basis.
    -   Add controls for `pitch` and `rate` in the JSON script.

### 4. Developer Experience & Ecosystem

Improve the project for contributors and future development.

-   **Dependency Management:** Move all CDN dependencies (Chart.js, p5.js) to a `package.json` file and manage them with **npm** or **yarn**.
-   **Testing:** Introduce a testing framework like **Vitest** or **Jest**.
    -   Write unit tests for the `JsonFilter` and other utility functions.
    -   Write component/integration tests for the player classes to ensure scenes render correctly.
-   **Linting and Formatting:** Set up **ESLint** and **Prettier** to enforce a consistent code style across the project, making contributions easier to review.
-   **CI/CD Pipeline:** Create a GitHub Actions workflow to automatically run tests, lint the code, and deploy the application to a hosting service like GitHub Pages or Vercel upon pushes to the `main` branch.

By implementing these enhancements, the **AI Video Creator Pro** can evolve from an impressive proof-of-concept into a truly powerful and versatile tool for automated video creation.
