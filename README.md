# football_counter
# Footfall Counter using Computer Vision (OpenCV DNN)

## Objective
Detect, track and count people entering/exiting a region by counting people who cross a virtual line in a video.

## Approach
- Detection: OpenCV DNN using a Darknet model (YOLOv4-tiny recommended).
- Tracking: Simple centroid-based tracker to assign object IDs across frames.
- Counting logic: A horizontal counting line is placed at a configurable relative position. If a tracked object's centroid crosses the line from top→bottom it's counted as **In**, from bottom→top it's counted as **Out**.
- Visualization: Bounding boxes, IDs, and counts are overlaid and can be saved as an output video.

## Files
- `footfall_counter.py` — main script (provided).
- `README.md` — this file.
- Example output video: `output_with_counts.mp4` (create by running the script).

## Dependencies
- Python 3.8+
- OpenCV (with `dnn`): `pip install opencv-python`
- NumPy: `pip install numpy`

Optional (if you want GPU acceleration for DNN):
- OpenCV built with CUDA support (not available via `pip` by default). See OpenCV build docs.

## Model files (you must download)
This script expects a Darknet model (cfg + weights) and a `coco.names` file.

Recommended (YOLOv4-tiny):
- `yolov4-tiny.cfg` (Darknet cfg)
- `yolov4-tiny.weights` (Darknet weights)
- `coco.names` (class labels; person is class `person` with id 0)

You can find these on public repositories; example sources:
- `yolov4-tiny.cfg`: https://raw.githubusercontent.com/AlexeyAB/darknet/master/cfg/yolov4-tiny.cfg
- `yolov4-tiny.weights`: download from the darknet weights links (large file ~ 23MB-25MB for tiny)
- `coco.names`: common COCO names file containing `person` as first line.

> Do **not** commit large weights to your repo. In your submission README include download instructions or a script to fetch these files.

## Running
Example:
```bash
python footfall_counter.py \
  --input people.mp4 \
  --cfg yolov4-tiny.cfg \
  --weights yolov4-tiny.weights \
  --names coco.names \
  --output output_with_counts.mp4
