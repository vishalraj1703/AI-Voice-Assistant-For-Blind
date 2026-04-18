# 🤖 Advanced AI Vision Assistant

A browser-based accessibility tool that combines real-time object detection, AI-powered scene description, OCR text reading, and voice interaction — designed to help visually impaired users understand their surroundings.

![HTML](https://img.shields.io/badge/built%20with-HTML%2FJS-orange.svg)
![Gemini](https://img.shields.io/badge/AI-Google%20Gemini-blue.svg)
![TensorFlow](https://img.shields.io/badge/ML-TensorFlow.js-FF6F00.svg)

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎯 **Real-Time Object Detection** | Uses TensorFlow.js COCO-SSD to detect 80+ object categories live from your camera |
| 📏 **Distance Estimation** | Estimates approximate distance to detected objects in meters |
| 👁️ **AI Scene Description** | Sends camera frames to Google Gemini for rich, natural-language scene descriptions |
| 📄 **OCR Text Reading** | Reads text from the camera feed using Tesseract.js |
| 💬 **Multi-Turn Voice Chat** | Voice-activated Q&A with full conversation memory across exchanges |
| 🔊 **Text-to-Speech** | All AI responses are spoken aloud via the Web Speech API |
| 🧠 **Conversation Memory** | Retains the last 15 exchanges so follow-up questions have full context |

---

## 🚀 Getting Started

### Prerequisites

- A modern browser (Chrome or Edge recommended for full Web Speech API support)
- A webcam or device camera
- A [Google Gemini API key](https://makersuite.google.com/app/apikey)

### Running Locally

No build step required. Just open the HTML file directly in your browser:

```bash
git clone https://github.com/your-username/advanced-vision-assistant.git
cd advanced-vision-assistant
open index.html   # macOS
# or double-click index.html on Windows/Linux
```

On first load, you'll be prompted to enter your Gemini API key. It's stored in `localStorage` — you won't need to re-enter it on future visits.

---

## 🎤 Voice Commands

| Command | Action |
|---|---|
| `"Start camera"` | Activates the camera |
| `"Stop camera"` | Deactivates the camera |
| `"Describe the scene"` | Requests a full Gemini AI scene description |
| `"Read the text"` | Performs OCR on the current camera frame |
| `"How many people?"` | Counts a specific detected object type |
| `"Is there a [object]?"` | Checks for a specific object |
| `"What is that?"` | Follow-up question using conversation context |
| `"Clear history"` | Resets conversation memory |
| `"Help"` | Lists available commands |

---

## 🧰 Tech Stack

- **[TensorFlow.js + COCO-SSD](https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd)** — in-browser object detection
- **[Google Gemini API](https://ai.google.dev/)** — multimodal scene description and conversational Q&A
- **[Tesseract.js](https://tesseract.projectnaptha.com/)** — OCR text extraction
- **Web Speech API** — voice recognition and text-to-speech
- **[Tailwind CSS](https://tailwindcss.com/)** — styling

---

## 📐 Distance Estimation

Distance is estimated using a simplified pinhole camera model based on the detected bounding box width:

```
distance = (KNOWN_WIDTH × FOCAL_LENGTH) / pixel_width
```

| Constant | Value | Notes |
|---|---|---|
| `KNOWN_WIDTH` | `0.5 m` | Average real-world object width |
| `FOCAL_LENGTH` | `615 px` | Calibrated for typical webcams |

> ⚠️ Distance estimates are approximate and intended as accessibility guidance, not precise measurements.

---

## 🔑 API Key Management

Your Gemini API key is stored in the browser's `localStorage`. To reset it:

1. Open your browser's DevTools (`F12`)
2. Go to **Application → Local Storage**
3. Delete the `GEMINI_API_KEY` entry
4. Refresh the page to enter a new key

---

## ♿ Accessibility Focus

This tool is designed with blind and visually impaired users in mind:

- All AI responses are spoken aloud automatically
- Spatial positioning (left / center / right) is included in descriptions
- Safety notices are triggered when vehicles, people, or stairs are detected
- Follow-up questions retain full conversational context so users don't need to repeat themselves

---

## 📁 Project Structure

```
advanced-vision-assistant/
└── index.html        # Single-file application (HTML + CSS + JS)
```

All dependencies are loaded via CDN — no npm install needed.

---

## ⚙️ Configuration

You can adjust these constants at the top of the `<script>` block in `index.html`:

```js
const KNOWN_WIDTH = 0.5;   // Real-world object width in meters
const FOCAL_LENGTH = 615;  // Calibrate for your camera if needed
```

Conversation memory depth (default: 15 exchanges) can be changed here:

```js
if (conversationHistory.length > 30) {   // 30 = 15 user + 15 model turns
    conversationHistory = conversationHistory.slice(-30);
}
```

---

## 🛡️ Privacy

- **No data is sent to any server except Google's Gemini API** when scene description or Q&A features are used.
- Camera frames are processed locally for object detection and OCR.
- Your API key never leaves your browser.

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

---

