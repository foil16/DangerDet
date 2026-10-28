# Detection backend

A Flask API that runs a YOLOv3 model over webcam frames and reports whether it sees a gun, a rifle or fire.

## Credit

The model and `yolo.py` come from [atulyakumar97/fire-and-gun-detection](https://github.com/atulyakumar97/fire-and-gun-detection) (MIT license, see `LICENSE`):
- **Trained on:** the [fire and gun dataset](https://www.kaggle.com/atulyakumar98/fire-and-gun-dataset).
- **Paper:** [Fire and Gun Violence based Anomaly Detection System Using Deep Neural Networks](https://ieeexplore.ieee.org/document/9155625), ICESCS 2020.

During the hackathon we added `app.py`, which serves the model over HTTP for the React frontend.

## API

`POST /process_image`
- **Request:** multipart form with a `frame` image field.
- **Response:** the annotated JPEG, plus a `type` header holding the first detected label (`Gun`, `Rifle`, `Fire`) or `Nothing`.

## Setup

1. Download the pre-trained `yolov3.weights` from the [upstream project's link](https://1drv.ms/u/s!Aj0l1DM1G5wOm0Vg2n7RI5Q4_ZOq?e=gGvvMy).
2. Put it in this folder. It's gitignored.
3. Then:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py        # serves on http://127.0.0.1:5001
```
