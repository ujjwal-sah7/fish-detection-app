# 🐟 AquaDetect — AI Fish Detection Web App

A complete, production-ready web application for detecting fish in images using a custom YOLO model.
🌐 Live Demo

Try the live application: https://fish-detection-app-3.onrender.com
---

## 📁 Project Structure

```
fish-detection-app/
├── backend/
│   ├── main.py             ← FastAPI server (API routes)
│   ├── model_loader.py     ← YOLO model loader
│   ├── detector.py         ← Detection logic & smart messages
│   ├── requirements.txt    ← Python dependencies
│   └── best.pt             ← ⚠️ PLACE YOUR MODEL HERE
│
├── frontend/
│   ├── index.html          ← Main UI
│   ├── css/
│   │   └── style.css       ← Ocean-themed stylesheet
│   ├── js/
│   │   └── script.js       ← Frontend logic (uploads, charts, history)
│   └── assets/
│       ├── videos/
│       │   └── background_ocean.mp4   ← ⚠️ PLACE YOUR VIDEO HERE
│       └── images/
│
└── README.md
```

---

## ⚙️ Requirements

- **Python 3.9+**
- **pip**
- A modern web browser (Chrome, Firefox, Edge)

---

## 🚀 Installation & Setup

### Step 1 — Add Your Model

Copy your trained YOLO model into the backend folder:

```
fish-detection-app/backend/best.pt
```

### Step 2 — Install Python Dependencies

```bash
cd fish-detection-app/backend
pip install -r requirements.txt
```

### Step 3 — Start the FastAPI Server

```bash
cd fish-detection-app/backend
python main.py
```

The server will start at:
```
http://localhost:8000
```

You can verify it's running by visiting:
```
http://localhost:8000/docs
```
This opens the auto-generated Swagger API documentation.

### Step 4 — Open the Web Interface

Simply open the frontend HTML file in your browser:

```
fish-detection-app/frontend/index.html
```

> **Note:** Open the file directly in your browser or serve it with any static file server.
> The frontend connects to the backend at `http://localhost:8000`.

---

## 🌊 Adding the Ocean Animation Video

To enable the underwater video background:

1. Obtain or create an ocean animation video (MP4 format)
2. Name it: `background_ocean.mp4`
3. Place it in:

```
fish-detection-app/frontend/assets/videos/background_ocean.mp4
```

If the video file is missing, the UI will still work normally using a CSS gradient fallback — no errors will appear.

---

## 🔌 API Endpoints

| Method | Route       | Description                          |
|--------|-------------|--------------------------------------|
| GET    | `/`         | Health check                         |
| POST   | `/detect`   | Upload an image → get detection JSON |
| GET    | `/history`  | Get detection history grouped by date|
| GET    | `/stats`    | Get dashboard statistics             |
| DELETE | `/history`  | Clear all history                    |

### POST /detect — Example Response

```json
{
  "status": "fish_detected",
  "message": "Fish detected: Tuna.",
  "detections": [
    {
      "label": "Tuna",
      "confidence": 0.9247,
      "bbox": [120, 80, 440, 300],
      "type": "fish",
      "is_fish": true
    }
  ],
  "filename": "ocean_photo.jpg",
  "timestamp": "2024-01-15T14:30:22.123456",
  "annotated_image_url": "/outputs/<uuid>_annotated.jpg"
}
```

---

## 🧠 Detection Logic

| Scenario | Status Code | Message |
|---|---|---|
| Known fish found | `fish_detected` | Fish detected: {name} |
| Unknown fish-like object | `unknown_fish` | Unknown fish detected. This species is not in the model. |
| Human / everyday object | `non_marine` | This application detects marine life only. |
| Nothing found | `no_detection` | No fish detected in the image. |

---

## 🎨 Themes

The UI comes with 3 built-in themes accessible from the sidebar:

- 🌊 **Ocean** — Deep teal/cyan (default)
- 🌑 **Dark** — Indigo/purple deep dark
- 🐋 **Abyss** — Ultra dark navy

---

## 🛠️ Troubleshooting

**Backend won't start?**
- Check Python version: `python --version` (needs 3.9+)
- Check that `best.pt` exists in the `backend/` folder
- Re-run `pip install -r requirements.txt`

**API offline indicator in UI?**
- Make sure `python main.py` is running
- Check that port 8000 is not blocked by a firewall

**Images not showing in results?**
- Backend must be running so it can serve `/outputs/` images
- Check browser console for CORS or network errors

---

## 📄 License

This project is built for demonstration and educational purposes.
YOLO is provided by [Ultralytics](https://ultralytics.com).
