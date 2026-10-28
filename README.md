# DangerDet

A web dashboard that watches a webcam feed and raises an alert when it detects a firearm or fire.

Built at **ConUHacks VIII** (Concordia, January 2024) in about 24 hours, by a team of four.

<!-- TODO: add a screenshot or GIF of an alert here -->

## Tech stack

- **Frontend:** React, browser `getUserMedia` webcam capture, Canvas API
- **Detection backend:** Python, Flask, OpenCV DNN running a YOLOv3 model
  - The pre-trained model comes from [atulyakumar97/fire-and-gun-detection](https://github.com/atulyakumar97/fire-and-gun-detection) (MIT); see [`model/README.md`](model/README.md).

## How it works

1. The React app streams the webcam and, every 5 seconds, draws a frame to a `<canvas>` and POSTs it to the Flask API.
2. The API runs YOLOv3 through OpenCV:
   - It applies a confidence threshold and non-max suppression.
   - It returns the annotated frame, with the detected class (`Gun`, `Rifle`, `Fire` or `Nothing`) in a response header.
3. The frontend watches that label and switches the UI: police lights and a "Firearm Detected" banner for guns and rifles, a fire animation and a "Fire Hazard Detected" banner for fire.

## Running it locally

Requirements: Node.js 18+, Python 3.10+, and the YOLOv3 weights file (see [`model/README.md`](model/README.md)).

**Detection backend** (port 5000):

```bash
cd model
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
# put yolov3.weights in this folder first
python app.py
```

**Frontend** (port 3000), in a second terminal:

```bash
cd app
npm install
npm start
```

Open http://localhost:3000 and allow camera access.
