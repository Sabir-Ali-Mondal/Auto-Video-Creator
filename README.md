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





#### The Complete AI Prompts

I will integrate these full prompts into the JavaScript. They are designed to be copied directly and pasted into an AI like GPT-4, Claude, or Perplexity to get a valid JSON response.

**1.1. Prompt for "Graph Presentation" Mode**

*   **Goal:** To generate a data-centric presentation with narrated charts. This prompt emphasizes structured data and a logical sequence.

```text
Generate a video script JSON for the topic: "The Global Shift to Electric Vehicles (EVs) by 2030".

STRICTLY follow this exact JSON structure. Only change the text, narration, and data values to fit the topic. Use plausible but illustrative data. Do not add any new keys or change the scene types.

OUTPUT ONLY THE RAW JSON. NO MARKDOWN, NO EXPLANATIONS.

TEMPLATE:
{
  "theme": {
    "--bg-color": "#0f0a19",
    "--surface-color": "#1a1625",
    "--border-color": "#2d2438",
    "--primary-color": "#8b5cf6",
    "--text-color": "#f3f4f6",
    "--glass-bg": "rgba(139, 92, 246, 0.15)",
    "--glass-hover-bg": "rgba(139, 92, 246, 0.25)",
    "--highlight-primary": "#a855f7",
    "--highlight-secondary": "#06b6d4",
    "--highlight-accent": "#f59e0b"
  },
  "sceneOrder": ["intro", "market_growth", "charging_infra", "manufacturer_share", "conclusion"],
  "scenes": {
    "intro": {
      "id": "intro",
      "type": "title",
      "content": {
        "title": "The EV Revolution",
        "narration": "Welcome. Today we will explore the exponential growth of the electric vehicle market and the key trends shaping our automotive future towards 2030.",
        "duration": 3000
      }
    },
    "market_growth": {
      "id": "market_growth",
      "type": "scripted_chart",
      "content": {
        "title": "Global EV Sales Growth",
        "intro_narration": "First, let's look at the projected global sales. The growth is staggering.",
        "chartConfig": {
          "type": "line",
          "data": {
            "labels": ["2022", "2024", "2026", "2028", "2030"],
            "datasets": [{
              "label": "EV Sales (Millions)",
              "data": [10.5, 21, 40.5, 62, 75],
              "borderColor": "#8b5cf6", "tension": 0.4
            }]
          }
        },
        "script_steps": [
          {"step": 1, "narration": "In 2022, global sales stood at a strong 10.5 million units.", "highlight": {"datasetIndex": 0, "dataIndex": 0}},
          {"step": 2, "narration": "By 2030, this number is projected to surge to 75 million vehicles sold annually.", "highlight": {"datasetIndex": 0, "dataIndex": 4}}
        ]
      }
    },
    "charging_infra": {
      "id": "charging_infra",
      "type": "scripted_chart",
      "content": {
        "title": "Public Charging Infrastructure",
        "intro_narration": "This growth is supported by a massive expansion in charging infrastructure.",
        "chartConfig": {
          "type": "bar",
          "data": {
            "labels": ["USA", "Europe", "China"],
            "datasets": [{
              "label": "Public Chargers (Millions)", "data": [0.5, 2.9, 7.6], "backgroundColor": ["#8b5cf6", "#06b6d4", "#f59e0b"]
            }]
          }
        },
        "script_steps": [
          {"step": 1, "narration": "China is leading the way with a projected 7.6 million public chargers.", "highlight": {"datasetIndex": 0, "dataIndex": 2}},
          {"step": 2, "narration": "Europe is also investing heavily, aiming for nearly 3 million chargers.", "highlight": {"datasetIndex": 0, "dataIndex": 1}}
        ]
      }
    },
    "manufacturer_share": {
      "id": "manufacturer_share",
      "type": "scripted_chart",
      "content": {
        "title": "Projected Market Share by 2030",
        "intro_narration": "Finally, let's see how the market share is expected to look.",
        "chartConfig": {
          "type": "doughnut",
          "data": {
            "labels": ["Tesla", "BYD", "VW Group", "Others"],
            "datasets": [{"data": [20, 18, 15, 47], "backgroundColor": ["#ef4444", "#8b5cf6", "#3b82f6", "#e2e8f0"]}]
          }
        },
        "script_steps": [
          {"step": 1, "narration": "Tesla is expected to hold a dominant 20% of the market.", "highlight": {"datasetIndex": 0, "dataIndex": 0}},
          {"step": 2, "narration": "However, competitors like BYD are closing the gap, with a projected 18% share.", "highlight": {"datasetIndex": 0, "dataIndex": 1}}
        ]
      }
    },
    "conclusion": {
      "id": "conclusion",
      "type": "end",
      "content": {
        "title": "An Electric Future",
        "narration": "The path is clear. The automotive industry is rapidly and irreversibly shifting to an electric future, driven by innovation, policy, and consumer demand.",
        "duration": 4000
      }
    }
  }
}
```

**1.2. Prompt for "Creative Video" Mode**

*   **Goal:** To generate a visually rich, marketing-style video. This prompt asks for Unsplash URLs and varied scene types to showcase the renderer's capabilities.

```text
Generate a video script JSON for the topic: "The Power of Storytelling in Marketing".

STRICTLY follow this exact JSON structure. Only change the text, narration, and data values to fit the topic. For all "bgUrl" keys, provide real, working image URLs from images.unsplash.com.

OUTPUT ONLY THE RAW JSON. NO MARKDOWN, NO EXPLANATIONS.

TEMPLATE:
{
  "width": 1280, "height": 720,
  "scenes": [
    {
      "id": "title", "type": "title", "text": "Beyond the Product",
      "narration": "In a crowded market, features are not enough. The brands that win are the ones that tell the best stories.",
      "voiceGender": "female"
    },
    {
      "id": "paragraph", "type": "paragraph", "text": "Connecting Emotionally",
      "narration": "Storytelling builds an emotional bridge between a brand and its audience, fostering loyalty that transcends price.",
      "bgUrl": "https://images.unsplash.com/photo-1528716321680-815a8cdb8cbe?w=1280&auto=format&fit=crop&q=80",
      "voiceGender": "male"
    },
    {
      "id": "bullet_points", "type": "bullet_points", "text": "Key Story Elements",
      "narration": "A great brand story has a few key ingredients: a relatable hero, a clear conflict, and a satisfying resolution.",
      "points": ["The Hero (Your Customer)", "The Conflict (Their Problem)", "The Resolution (Your Solution)", "The Transformation"],
      "bgUrl": "https://images.unsplash.com/photo-1455390582262-044cdead277a?w=1280&auto=format&fit=crop&q=80",
      "voiceGender": "female"
    },
    {
      "id": "chart_scene", "type": "chart", "text": "Impact on Engagement",
      "narration": "The data is clear. Story-driven campaigns see significantly higher engagement and recall rates.",
      "chartData": [{"label": "Traditional Ad", "value": 35}, {"label": "Feature List", "value": 45}, {"label": "Brand Story Ad", "value": 85}],
      "bgUrl": "https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=1280&auto=format&fit=crop&q=80",
      "voiceGender": "male"
    },
    {
      "id": "quiz", "type": "quiz",
      "narration": "Let's test your knowledge. In a brand story, who should always be the main character or 'hero'?",
      "question": "Who is the hero of a brand story?",
      "options": ["The CEO", "The Product", "The Customer", "The Brand"],
      "correctAnswer": 2, "answerText": "The Customer",
      "voiceGender": "female"
    },
    {
      "id": "end", "type": "end", "text": "Tell Your Story",
      "narration": "Your audience is waiting for a story to believe in. It's time to tell yours. Thank you.",
      "bgUrl": "https://images.unsplash.com/photo-1481018085669-2bc6e4f00994?w=1280&auto=format&fit=crop&q=80",
      "voiceGender": "male"
    }
  ]
}
```

**1.3. Prompt for "MindVoice" Mode**

*   **Goal:** To generate a hierarchical mindmap with educational, podcast-style narration scripts for each node.

```text
Create a comprehensive, educational mindmap as a JSON object on the topic: "The Process of Photosynthesis".

STRICTLY follow this exact JSON structure. Ensure the 'script' fields contain engaging, conversational narration (2-3 sentences). The map should have at least 3 levels of hierarchy where appropriate.

OUTPUT ONLY THE RAW JSON. NO MARKDOWN, NO EXPLANATIONS.

TEMPLATE:
{
  "id": "root_node",
  "title": "Photosynthesis",
  "notes": "The process used by plants, algae, and some bacteria to convert light energy into chemical energy.",
  "script": "Let's dive into Photosynthesis, the incredible natural process that powers most life on Earth by turning sunlight into food.",
  "children": [
    {
      "id": "inputs", "title": "Key Ingredients", "notes": "Requires sunlight, water, and carbon dioxide.", "script": "To start, photosynthesis needs three key ingredients: sunlight for energy, water absorbed through the roots, and carbon dioxide from the air.",
      "children": []
    },
    {
      "id": "stages", "title": "Two Main Stages", "notes": "Consists of Light-Dependent Reactions and the Calvin Cycle.", "script": "The process happens in two main stages. First, the light-dependent reactions capture solar energy, and then the Calvin Cycle uses that energy to create sugar.",
      "children": [
        {
          "id": "light_reactions", "title": "Light-Dependent Reactions", "notes": "Occur in the thylakoid membranes. Water is split to release oxygen.", "script": "In the light-dependent reactions, chlorophyll absorbs sunlight, splitting water molecules. This is the step that releases the oxygen we breathe into the atmosphere."
        },
        {
          "id": "calvin_cycle", "title": "Calvin Cycle", "notes": "Occurs in the stroma. CO2 is converted into glucose (sugar).", "script": "Next, in the Calvin Cycle, the captured energy is used to convert carbon dioxide into glucose. This sugar is the plant's food, providing energy for growth."
        }
      ]
    },
    {
      "id": "outputs", "title": "Essential Outputs", "notes": "Produces glucose for energy and oxygen as a byproduct.", "script": "So, the two critical products of this entire process are glucose, which fuels the plant, and oxygen, which is essential for animal life.",
      "children": []
    }
  ]
}
```

**1.4. Prompt for "Chem Mechanism" Mode**

*   **Goal:** To generate a step-by-step chemical reaction with atom/bond coordinates and animation actions. This is the most technical prompt.

```text
Generate a comprehensive JSON for visualizing the mechanism of a: "Friedel-Crafts Acylation of Benzene".

STRICTLY follow this exact JSON structure. Ensure all 'position' coordinates create a chemically plausible 2D representation. The 'from' and 'to' in actions must correctly reference molecule and atom/bond IDs.

OUTPUT ONLY THE RAW JSON. NO MARKDOWN, NO EXPLANATIONS.

TEMPLATE:
{
  "meta": {"reactionName": "Friedel-Crafts Acylation"},
  "molecules": {
    "acyl_chloride": {
      "position": {"x": -250, "y": -50},
      "atoms": [
        {"id": "c1", "element": "C", "position": {"x": 0, "y": 0}},
        {"id": "o1", "element": "O", "position": {"x": 0, "y": -50}},
        {"id": "cl1", "element": "Cl", "position": {"x": 50, "y": 0}},
        {"id": "c2", "element": "C", "position": {"x": -50, "y": 25}}
      ],
      "bonds": [
        {"id": "b_co", "from": "c1", "to": "o1", "type": "double"},
        {"id": "b_ccl", "from": "c1", "to": "cl1", "type": "single"},
        {"id": "b_cc", "from": "c1", "to": "c2", "type": "single"}
      ]
    },
    "lewis_acid": {
      "position": {"x": -150, "y": 100},
      "atoms": [
        {"id": "al1", "element": "Al", "position": {"x": 0, "y": 0}},
        {"id": "cl2", "element": "Cl", "position": {"x": -40, "y": -30}},
        {"id": "cl3", "element": "Cl", "position": {"x": 40, "y": -30}},
        {"id": "cl4", "element": "Cl", "position": {"x": 0, "y": 50}}
      ]
    },
    "benzene": {
      "position": {"x": 150, "y": 0},
      "atoms": [
        {"id": "c3", "element": "C", "position": {"x": 0, "y": -60}},
        {"id": "c4", "element": "C", "position": {"x": 52, "y": -30}},
        {"id": "c5", "element": "C", "position": {"x": 52, "y": 30}},
        {"id": "c6", "element": "C", "position": {"x": 0, "y": 60}},
        {"id": "c7", "element": "C", "position": {"x": -52, "y": 30}},
        {"id": "c8", "element": "C", "position": {"x": -52, "y": -30}}
      ],
      "bonds": [
        {"id": "b_pi1", "from": "c3", "to": "c4", "type": "double"},
        {"id": "b_pi2", "from": "c5", "to": "c6", "type": "double"},
        {"id": "b_pi3", "from": "c7", "to": "c8", "type": "double"}
      ]
    }
  },
  "mechanism": [
    {
      "step": 1, "title": "Formation of Acylium Ion", "narration": "The Lewis acid catalyst, aluminum trichloride, coordinates with the chlorine atom of the acyl chloride.",
      "displayMolecules": ["acyl_chloride", "lewis_acid"],
      "actions": [
        {"type": "ELECTRON_ARROW", "from": "acyl_chloride.cl1", "to": "lewis_acid.al1", "duration": 2000, "delay": 500}
      ]
    },
    {
      "step": 2, "title": "Cleavage to form Electrophile", "narration": "This coordination weakens the carbon-chlorine bond, which then breaks to form a highly reactive, resonance-stabilized acylium ion.",
      "displayMolecules": ["acyl_chloride", "lewis_acid"],
      "actions": [
        {"type": "BOND_ANIMATION", "target": "acyl_chloride.b_ccl", "animationType": "breaking", "duration": 1500, "delay": 0}
      ]
    },
    {
      "step": 3, "title": "Electrophilic Attack", "narration": "The pi electrons of the benzene ring act as a nucleophile, attacking the electrophilic carbon of the acylium ion.",
      "displayMolecules": ["acyl_chloride", "benzene"],
      "actions": [
        {"type": "ELECTRON_ARROW", "from": "benzene.b_pi1", "to": "acyl_chloride.c1", "duration": 2000, "delay": 500}
      ]
    },
    {
      "step": 4, "title": "Restoration of Aromaticity", "narration": "Finally, a chloride ion from the catalyst complex removes a proton from the ring, restoring the stable aromatic system and regenerating the catalyst.",
      "displayMolecules": ["benzene", "acyl_chloride"],
      "actions": []
    }
  ]
}
```


