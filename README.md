# VIDEO-LIKE 

**VIDEO-LIKE** is a powerful, browser-based application that transforms structured JSON data into engaging, narrated videos. It offers a unique dual-engine approach, allowing users to create either data-driven graph presentations or visually rich creative showcases from a single, intuitive script format.

This project bridges the gap between data and storytelling, enabling developers, marketers, and analysts to produce programmatic videos without complex editing software.

It will be awesome.


Here is the consolidated list of all 41 scene types discussed, along with a brief technical implementation strategy for each using HTML, CSS (Tailwind), and JavaScript.

**Social Media & Communications**
1. Social Media Post: Use a Flexbox container with a border, padding, and specific gap settings. Use `rounded-full` for avatars and font-weight variations for handles vs. content.
2. Chat Conversation: Use a vertical Flex column. Align "sent" bubbles to `self-end` (right) and "received" bubbles to `self-start` (left) with different background colors and rounded corners.
3. Breaking News: Use a fixed position `bottom-0` container. Implement the scrolling ticker using a CSS `@keyframes` animation translating text from `translateX(100%)` to `translateX(-100%)`.
4. Notification Stack: Use absolute positioning with `z-index` layering. Apply `top` margins incrementally and fade-in animations with delays to simulate stacking.
5. Search Browser: Create an input field container. Use JavaScript `setTimeout` loops to type text into the input value character-by-character, then reveal a dropdown `div` for results.

**Documentary & Journalism**
6. Newspaper: Wrap the container in a `perspective` div. Apply `transform: rotateY(10deg)` to the paper div. Use CSS background patterns for texture and `span` tags with linear-gradient backgrounds for the highlighter effect.
7. Map Points: Use a background image of a map. Place dots using absolute positioning (`top: %`, `left: %`). Use CSS keyframes `scale` and `opacity` to create a pulsing beacon effect.
8. Investigation Board: Use a messy layout with rotated images (`rotate-2`, `-rotate-3`). Use SVG lines (`<line>`) positioned absolutely to draw strings between elements.
9. Kinetic Typography: Use extremely large font sizes (`text-9xl`). Use JavaScript to toggle `display: none` or `opacity` rapidly between words to match the audio timing.
10. Docu-Title: Use a dark background with a `radial-gradient` vignette. Use heavy fonts (Oswald) and `mix-blend-mode: overlay` to blend text with background textures.
11. Spotlight: Create a dark overlay `div` covering the screen. Use CSS `mask-image: radial-gradient` or a large SVG path with a transparent hole to reveal the layer underneath.
12. Film Strip: Create a wide container with a repeating pattern of "film holes" on top/bottom. Animate the `background-position` or `translateX` to slide the strip horizontally.
13. Picture in Picture: Use a small container with `position: absolute`, `bottom-4`, `right-4`, `z-index: 50`. Add a border and shadow to separate it from the background.

**Data Visualization**
14. Chart: Inject a `<canvas>` element. Use `new Chart(ctx, config)` via Chart.js library to render the visual.
15. Chart Split: Use a CSS Grid with 2 columns (`grid-cols-2`). Place text content in the left cell and the Chart.js canvas in the right cell.
16. 3D Plot: Use a `div` container. Pass data to `Plotly.newPlot()` to render WebGL-based 3D interactives.
17. Timeline: Use a horizontal flex container (`overflow-x-auto`). Draw a central line using a `border-bottom` or an absolute `div`. Place nodes at specific intervals.
18. Flowchart: Use Flexbox or Grid to position boxes. Use SVG `<path>` elements with `marker-end="url(#arrow)"` to draw the connectors between boxes.
19. Funnel Chart: Use a Flex column. Create bars with decreasing widths (`w-full`, `w-3/4`, `w-1/2`) or use CSS `clip-path: polygon(...)` to create trapezoid shapes.
20. Table: Use standard HTML `<table>`. Apply Tailwind `divide-y` and `border` classes for styling. Use `bg-gray-100` on alternating rows (zebra striping).
21. Calendar View: Use a 7-column CSS Grid. Generate numbered cells. Use conditional styling to change the background color of specific "active" dates.
22. Number Counter: Use a large text element. Use a JavaScript `requestAnimationFrame` loop to rapidly increment the `innerText` from 0 to the target number over a set duration.

**Comparison & Logic**
23. Comparison: Use a Flex row split 50/50. Apply a border to the right of the first element. Use contrasting text alignments (right-align vs. left-align) for symmetry.
24. Pros and Cons: Use a 2-column Grid. Use green checkmark icons for the left column and red X icons for the right column.
25. Venn Diagram: Use two or three `div` elements with `rounded-full`. Position them to overlap and use `mix-blend-mode: multiply` or `opacity: 0.7` so the intersection is visible.
26. Tier List: Use a Flex column. Each row contains a colored label cell (S, A, B) and a content area. Use `flex-wrap` in the content area to stack items horizontally.
27. Image Slider: Stack two images absolutely. Use `clip-path: inset(0 X% 0 0)` on the top image. Bind a range input slider's value to the X percentage to reveal/hide.

**Layout & Motion**
28. Bento Grid: Use CSS Grid with `grid-template-columns`. Use `col-span-2` or `row-span-2` classes on child elements to create tiles of different sizes.
29. Card Carousel: Use a flex container with `overflow-x-scroll` and `snap-x`. Set child elements to `snap-center` so they lock into place when scrolling.
30. Photo Collage: Use absolute positioning for multiple images. Apply random small rotations via CSS to simulate a scattered pile. Add `box-shadow` for depth.
31. Parallax Scroll: Set a container to `perspective: 10px`. Set children to `transform: translateZ(...)`. As the container scrolls, depth creates different movement speeds.
32. Exploded View: Use a container with `transform-style: preserve-3d`. Apply `transform: translateZ(Npx)` to separate layers of an image or diagram along the Z-axis.

**Technical & Educational**
33. Code Terminal: Create a window-like `div` with a header bar (3 colored dots). Use a `<pre>` tag inside with Prism.js for syntax highlighting.
34. Concept Sketch: Use an SVG `<path>`. Animate the `stroke-dashoffset` property from the path length to 0 to simulate the drawing action.
35. Quiz: Create a grid of `<button>` elements. Use JavaScript onclick events to check the index against the correct answer and apply `.bg-green-500` or `.bg-red-500` classes.
36. Generative Art: Use a dedicated `div` id. Initialize a P5.js sketch in instance mode to draw canvas graphics inside that div.
37. Tree: Use a Flex column structure. Use CSS pseudo-elements `::before` and `::after` with borders to create the connecting "branches" between nodes.

**Standard Presentation**
38. Title: Use Flexbox centering (`items-center justify-center`). Use huge font sizes (`text-6xl`) and letter spacing (`tracking-widest`).
39. Bullets: Use a standard `<ul>`. Set list items `<li>` to `opacity: 0` by default and toggle to `opacity: 1` based on the step index.
40. Image / Video: Use an `<img>` or `<video>` tag. Apply `object-fit: cover` and `w-full h-full` to ensure they fill their containers without distortion.
41. Quote: Use a Flex column. Use a Serif font (`font-serif`) and large quotes (CSS `::before { content: '"' }`) for styling.
