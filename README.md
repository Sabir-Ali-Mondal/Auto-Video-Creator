# AI Video Creator Pro - Unified Suite

**AI Video Creator Pro** is a powerful, browser-based application that transforms structured JSON data into engaging, narrated videos. It offers a unique dual-engine approach, allowing users to create either data-driven graph presentations or visually rich creative showcases from a single, intuitive script format.

This project bridges the gap between data and storytelling, enabling developers, marketers, and analysts to produce programmatic videos without complex editing software.



---

## What is the Goal of this Website?

The primary goal of **AI Video Creator Pro** is to **democratize video creation through code**. It provides a declarative, script-based workflow to generate dynamic visual content. Instead of manually manipulating timelines and assets in a traditional video editor, users define the video's structure, content, and narration in a simple JSON file.

AI Video Creator Pro
Choose your creation style. Generate a data-driven presentation, a creative video, a mindmap, or a chemical reaction from an AI-generated JSON script.

Graph Presentation
Ideal for business reviews and data analysis. Uses Chart.js for crisp, animated, and narrated data visualizations.

Creative Video
Perfect for marketing and explainers. Renders custom graphics, tables, quizzes, and even 3D sketches with p5.js.

MindVoice Map
Turn your ideas into a clear and engaging mindmap with guided audio narration.

Chem Mechanism
Explore chemical reactions step by step through easy, visual storytelling.

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


