<div align="center">

# EcoGreen — Waste Classification

**An AI-powered web application to classify waste as Organic or Recyclable,  
complete with disposal guidance, an encyclopedia, waste map, and eco badge system.**

[![TensorFlow.js](https://img.shields.io/badge/TensorFlow.js-4.20.0-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/js)
[![MobileNet](https://img.shields.io/badge/MobileNet-v2-blue?logo=google&logoColor=white)](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet)
[![HTML5](https://img.shields.io/badge/HTML5-CSS3-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES2022-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

</div>

---

## About

**EcoGreen** is a browser-based waste classification tool that uses deep learning to help people sort their trash correctly. Simply upload a photo (or use your camera), and the AI instantly determines whether the item is **Organic** or **Recyclable** — then provides specific disposal tips, step-by-step recycling guidance, and interesting environmental facts.

The project also includes:
- A **Trash Encyclopedia** to look up common waste items
- An **Interactive Waste Map** showing nearby trash banks (Bank Sampah)
- An **Eco Badges** system to track your classification history and environmental impact

> **Goal:** Make waste management smarter, easier, and more engaging for everyone.

---

## Features

| Feature | Description |
|---|---|
| **Smart Scanner** | Upload a photo or use the camera to classify waste in real-time |
| **AI Classification** | Powered by TensorFlow.js (MobileNet v2 or custom trained model) |
| **Confidence Score** | Shows organic vs recyclable percentage for each prediction |
| **Disposal Tips** | Step-by-step recycling/composting guidance per waste type |
| **Encyclopedia** | Searchable database of common waste items with categories |
| **Waste Map** | Locate nearby trash banks (Bank Sampah) with addresses & hours |
| **Eco Badges** | Gamified achievement system tracking your environmental contribution |
| **Share Progress** | Share your eco impact to social media or clipboard |
| **Local Persistence** | Classification history saved in browser localStorage |

---

## Application Pages

### 1. Smart Scanner
Upload an image or capture directly from camera. The AI model classifies the waste and shows:
- Waste category (Organic / Recyclable)
- Confidence bars for both categories
- Proper bin color to use
- Hazard level
- Disposal tips & step-by-step recycling guide
- Fun environmental fact

### 2. Trash Encyclopedia
A searchable reference of 12+ common waste items. Each entry shows the item name, description, and whether it is organic or recyclable.

### 3. Interactive Waste Map
Displays nearby **Bank Sampah** (community-based trash banks) on an interactive map. Click a location to see its address and operating hours.

### 4. Eco Badges
Tracks how many items you have classified and unlocks achievement badges as you progress:

| Badge | Goal |
|---|---|
| First Step | 1 item |
| Eco Warrior | 10 items |
| Green Hero | 25 items |
| Eco Master | 50 items |

Also calculates your estimated **CO₂ saved**, **trees equivalent**, and **kg recycled**.

---

## Tech Stack

### Frontend (Website)
| File | Role |
|---|---|
| [`index.html`](website/index.html) | App shell, layout, and all page markup |
| [`Style.css`](website/Style.css) | Full responsive styling (green/teal theme, dark-mode ready) |
| [`model.js`](website/model.js) | TF.js model loader & waste classification logic |
| [`app.js`](website/app.js) | Page navigation, scanner, encyclopedia, badges, storage |

### AI / Machine Learning
| Library | Purpose |
|---|---|
| **TensorFlow.js 4.20.0** | In-browser deep learning inference |
| **MobileNet v2** | Pre-trained image classification (default fallback) |
| **Custom TF.js Model** | Optional: plug in your own trained `model.json` |

### Training Notebooks (`/training`)
Five Jupyter notebooks are included for training or fine-tuning your own waste classifier:

| Notebook | Architecture |
|---|---|
| [`cnn.ipynb`](training/cnn.ipynb) | Custom CNN from scratch |
| [`EfficientNetB0.ipynb`](training/EfficientNetB0.ipynb) | EfficientNet-B0 (transfer learning) |
| [`MobileNetV4_.ipynb`](training/MobileNetV4_.ipynb) | MobileNet V4 (transfer learning) |
| [`RESNET50.ipynb`](training/RESNET50.ipynb) | ResNet-50 (transfer learning) |
| [`yolo_v8.ipynb`](training/yolo_v8.ipynb) | YOLOv8 (object detection) |

---

## Getting Started

### Prerequisites
- A modern web browser (Chrome, Edge, Firefox, Safari)
- No server or installation required — runs entirely in the browser!

### Run Locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/EcoGreen-Waste-Classification.git
   cd EcoGreen-Waste-Classification
   ```

2. **Open the website**

   Navigate to the `website/` folder and open `index.html` directly in your browser:
   ```
   website/index.html
   ```

   > For camera access or local model loading, serve the files via a local HTTP server (see below).

3. **(Optional) Use a local server**
   ```bash
   # Using Python
   cd website
   python -m http.server 8080
   # Then open http://localhost:8080
   ```
   ```bash
   # Using Node.js / npx
   cd website
   npx serve .
   ```

---

## Using a Custom Trained Model

By default the app uses **MobileNet v2** (pre-trained on ImageNet) with a keyword mapping heuristic to categorize waste. To plug in your own TensorFlow.js model:

1. Train a binary classifier (Organic vs Recyclable) using one of the notebooks in `/training`.
2. Export it as a TensorFlow.js **LayersModel** (`model.json` + weight shards).
3. Place the exported files in `website/model/`.
4. In [`model.js`](website/model.js), change:
   ```js
   const USE_CUSTOM_MODEL  = true;          // ← set to true
   const CUSTOM_MODEL_PATH = "./model/model.json";  // ← path to your model
   ```

The app will automatically load your custom model and display **"Custom EcoGreen Model"** in the status bar.

---

## Project Structure

```
EcoGreen-Waste-Classification/
│
├── training/                   # Jupyter notebooks for model training
│   ├── cnn.ipynb               # Custom CNN
│   ├── EfficientNetB0.ipynb    # EfficientNet-B0
│   ├── MobileNetV4_.ipynb      # MobileNet V4
│   ├── RESNET50.ipynb          # ResNet-50
│   └── yolo_v8.ipynb           # YOLOv8
│
└── website/                    # Frontend web application
    ├── index.html              # Main HTML (all pages)
    ├── Style.css               # Stylesheet
    ├── model.js                # TF.js model loader & classifier
    ├── app.js                  # App logic (navigation, scanner, badges, etc.)
    └── model/                  # (Optional) Place custom model files here
        └── model.json
```

---

## Waste Categories

### Organic
Food scraps, fruit peels, vegetable waste, garden cuttings, egg shells, coffee grounds, etc.

- **Bin:** 🟢 Green Bin
- **Disposal:** Composting — reduces methane emissions by up to 70%
- **Fact:** 1 kg of organic waste can produce compost for 2 m² of garden soil!

### Recyclable
Plastic bottles, aluminum cans, cardboard, newspapers, glass jars, steel cans, plastic bags, etc.

- **Bin:** 🟡 Yellow Bin  
- **Disposal:** Bring to Bank Sampah or recycling drop-off point
- **Fact:** Recycling 1 plastic bottle saves enough energy to power a 60W bulb for 6 hours!

---

## Contributing

Contributions are welcome! Here are some ways you can help:

- Train and share a better classification model
- Add more waste items to the Encyclopedia
- Add real Waste Map integration (e.g. Google Maps API)
- Add multilingual support (Bahasa Indonesia, etc.)
- Report bugs or suggest features via [Issues](../../issues)

**To contribute:**
```bash
# 1. Fork the repo
# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Commit your changes
git commit -m "feat: add your feature"

# 4. Push and open a Pull Request
git push origin feature/your-feature-name
```

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- [TensorFlow.js](https://www.tensorflow.org/js) — in-browser ML inference
- [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) — pre-trained image classification
- [Google Fonts — Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) — typography
- Inspired by the global movement for smarter, greener waste management

---

<div align="center">
  <strong>Together for a cleaner planet</strong><br/>
  © 2026 EcoGreen. Making waste management smarter and greener.
</div>
