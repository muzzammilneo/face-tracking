Build a single-file real-time face detection and mood/emotion recognition 
web app using HTML, CSS, and JavaScript.

---

### TECH STACK

- **Face Detection & Emotion AI**: Use the `face-api.js` library
  (CDN: https://cdn.jsdelivr.net/npm/face-api.js@0.22.2/dist/face-api.min.js)
- **Models to load** (from the jsDelivr CDN path 
  https://cdn.jsdelivr.net/npm/face-api.js@0.22.2/weights):
    - `tinyFaceDetector` — fast real-time face detection
    - `faceExpressionNet` — detects expressions/emotions
    - `faceLandmark68TinyNet` — lightweight facial landmarks
- **Camera**: HTML5 `getUserMedia` API via `<video>` element
- **Rendering**: HTML5 `<canvas>` overlaid on the video feed

---

### FEATURES

1. **Live Camera Feed**
   - Auto-start webcam on page load (ask permission gracefully)
   - Mirror the video horizontally (selfie-style)
   - Show a loading state while models are downloading

2. **Real-Time Face Detection**
   - Draw bounding boxes around detected faces
   - Support multiple faces simultaneously

3. **Emotion Recognition & Display**
   - Detect and display these emotions with confidence %:
     happy, sad, angry, disgusted, fearful, surprised, neutral
   - Map emotions to expressive emoji: 😊 😢 😠 🤢 😨 😲 😐
   - Highlight the **dominant emotion** (highest confidence score)
   - Show a mini bar chart of all emotion scores below the face

4. **Mood Interpretation Labels**
   - happy/surprised → "You look joyful! 🌟"
   - sad/fearful → "Seems like a tough moment 💙"
   - angry/disgusted → "Feeling intense? 🔥"
   - neutral → "Calm and composed 🧘"

5. **Detection Stats Panel** (sidebar or bottom panel)
   - Number of faces detected
   - Dominant emotion name + emoji
   - Confidence percentage of dominant emotion
   - Real-time FPS counter
   - A live updating emotion history log (last 5 moods detected)

6. **Controls**
   - Toggle detection ON/OFF button
   - Toggle landmark points visibility
   - Snapshot button → captures current frame + overlays as PNG download
   - Fullscreen toggle

---

### UI / DESIGN DIRECTION

- **Aesthetic**: Dark, sleek, sci-fi / biometric scanner feel
- **Color palette**: Deep navy/charcoal background (#0d0f1a), 
  electric cyan (#00f5ff) for accents, warm amber (#ffb347) for 
  emotion highlights
- **Font**: Use `Space Mono` (Google Fonts) for a techy monospace feel
- **Canvas overlay**: Draw bounding boxes and landmark dots in cyan
- **Emotion bars**: Neon-colored horizontal bars per emotion, 
  animate width transitions smoothly
- **Glassmorphism** panel for stats (backdrop-filter: blur)
- **Scanning animation**: A slow horizontal scan line sweeping over 
  the video to reinforce the "biometric" feel
- **Responsive**: Works on desktop; graceful fallback on mobile 
  (portrait layout)

---

### CODE STRUCTURE (single HTML file)

```
<html>
  <head> — fonts, CSS variables, all styles </head>
  <body>
    <!-- Camera section: video + canvas overlay -->
    <!-- Stats panel: dominant emotion, face count, FPS, history -->
    <!-- Controls bar: toggle, snapshot, fullscreen -->
    <script>
      // 1. Load face-api.js models from CDN
      // 2. Start webcam stream
      // 3. Detection loop using requestAnimationFrame
      // 4. Draw detections + expressions on canvas
      // 5. Update UI panels reactively
      // 6. Handle controls (pause, snapshot, fullscreen)
    </script>
  </body>
</html>
```

### ERROR HANDLING

If webcam permission is denied → show a clear message with
instructions to enable camera
If models fail to load → show retry button
If no face detected for >3 seconds → show "No face detected" hint
Wrap all async calls in try/catch


### PERFORMANCE

Use TinyFaceDetector (not SSD MobileNet) for best FPS
Run detection every animation frame but debounce UI text updates
to every 300ms to avoid flicker
Use canvas.getContext('2d') — clear and redraw each frame

**Note:**
- Deliver this as a single self-contained index.html file.
- All styles inline in <style>, all logic inline in <script>.
- No build tools, no npm — runs by opening the file in a browser.