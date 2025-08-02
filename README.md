# Footfall-Dwell Tracker

*A Footfall Tracker that detects and tracks people in a video, measures how long they remain within a specified polygonal region, and generates a visual heatmap of high-engagement zones.*  
**Output**: Annotated video highlighting live counts and dwell-time hotspots—ideal for retail analytics, security monitoring, and facility management.

---

## Key Features

- **Real-Time Person Detection & Tracking**  
  Utilizes YOLOv8’s `track()` API for fast, accurate detection with persistent person IDs.

- **Footfall Counting**  
  Live tally of people entering and exiting your target zone.

- **Dwell-Time Heatmap**  
  Highlights regions where individuals linger beyond a set threshold (e.g., >5 seconds).

- **Zone Annotation**  
  Easily draw custom polygonal analysis areas—for aisles, entryways, or high-security spaces.

- **Video Output**  
  Automatically saves a new video with bounding boxes, zone outlines, live counts, and dwell-time heatmap overlays.

---

## Prerequisites

- Python 3.8+
- NVIDIA GPU (**recommended** for 30+ FPS processing)
- Python libraries: `ultralytics`, `opencv-python`, `numpy`, `supervision`, `matplotlib`

---
## Configuration

- **Zone Coordinates**:  
  In `processing.py`, set your region’s polygon:
polygon = np.array([[x1, y1], [x2, y2], [x3, y3], [x4, y4]])

text

- **Dwell Threshold**:  
Adjust how long someone must linger to mark as a hotspot:
dwell_time > <seconds>

text

- **Visualization Settings**:  
Tune `cv2.circle()` (radius, color) to fit your brand or analytic requirements.

---

## Usage

You'll be prompted:
Enter path to input video: ./data/shopping_mall.mp4
Enter path to save output video: ./output/annotated_mall.mp4

After processing, the script displays the last video frame with the heatmap (using Matplotlib).

---

## Code Workflow Overview

1. **Initialize YOLOv8**, polygon zone, and annotators.
2. **Read video frames**.
3. **Detect & Track people**; assign unique IDs.
4. **Count entries/exits** by detecting centroids crossing the zone boundary.
5. **Measure dwell time** for each ID inside the zone.
6. **Build heatmap**: Accumulate intensity for prolonged stays.
7. **Annotate & blend**: Draw boxes, zone, count, and overlay heatmap.
8. **Save annotated video**; return the final frame for display.

---

## Real-World Applications

- **Retail Analytics**: Discover high-engagement aisles or displays.
- **Transportation Hubs**: Monitor crowd build-up at ticket counters/gates.
- **Security**: Detect loitering near ATMs or restricted regions.
- **Smart Facilities**: Optimize space and flow using dwell/footfall patterns.

---

## Future Enhancements

- **Multiple Zones**: Analyze several regions per frame.
- **Dynamic Thresholds**: Adjust dwell time based on crowd/time-of-day.
- **Live Dashboard**: Real-time web UI with streaming video and analytics.
- **Edge Deployment**: Containerize for Jetson, NUC, or IoT-edge devices.
- **Privacy Filters**: Face blurring or silhouette mode (GDPR compliance).

---

**Clone the repo:**
