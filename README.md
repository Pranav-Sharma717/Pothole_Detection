# 🛣️ AI-Powered Pothole Detection & Visualization System (EPICS Phase-II)

An intelligent road infrastructure monitoring solution that automates the identification, geo-tagging, and severity assessment of road potholes from dashcam or smartphone-recorded video footage. Developed as part of Vellore Institute of Technology (VIT) Bhopal University **EPICS (Engineering Projects in Community Service)** course.

## 🚀 Live Demo
This dashboard is built using a client-side architecture that allows it to be hosted directly on **GitHub Pages** or **Vercel** with zero server-side configurations!
- **Run Locally:** Open [index.html](file:///c:/Users/gvpra/Downloads/Github%20cleanup/Pothole_Detection/index.html) in any web browser.

---

## ⚙️ How It Works (The Modular Pipeline)

The system is designed around a modular pipeline architecture:
1.  **GPS Metadata Extractor:** Extracts GPS coordinates directly from video metadata using ExifTool or FFprobe and normalizes them into decimal degrees.
2.  **Pothole Detector:** Invokes YOLOv8 (and YOLOv4-tiny fallback) to process frames dynamically (configurable sampling rate) and identify pothole coordinate locations.
3.  **Detection Aggregator:** Combines frame detections and computes a composite severity index.
4.  **Excel Data Logger:** Logs all processed incident metadata into a structured `.xlsx` spreadsheet schema.
5.  **Folium Map Visualizer:** Generates interactive geographic HTML maps using color-coded severity markers.
6.  **Interactive Dashboard:** Streamlit web interface for dispatch officers to review statistics, verify video detections, and close out tickets.

---

## 📐 Severity Classification Mathematical Model

Rather than treating all potholes equally, the system applies a weighted scoring algorithm:

$$\text{Severity Score} = \text{mean}( \text{Area Ratio}_i \times \text{Confidence}_i ) \quad \text{for all detections } i$$

*   **Area Ratio:** $\frac{\text{Bounding Box Width} \times \text{Bounding Box Height}}{\text{Frame Width} \times \text{Frame Height}}$
*   **Confidence:** YOLO model probabilistic certainty score (range `0.0` to `1.0`).
*   **Threshold Classifications:**
    *   $\text{Score} < 0.05$: **LOW** (Minor road damage, routine maintenance recommended)
    *   $0.05 \le \text{Score} < 0.15$: **MEDIUM** (Moderate road damage, schedule repair within 30-60 days)
    *   $\text{Score} \ge 0.15$: **HIGH** (Severe "rim-breaker" hazard, emergency repair within 72 hours)

---

## 📂 Project Output Artifacts

*   **Annotated Video:** Playable `.mp4` video with YOLO bounding box overlays.
*   **GPS Coordinate Logs:** `.txt` files containing latitude/longitude pairs.
*   **Excel Detection Log:** `.xlsx` spreadsheet logging metadata (`Video_Name`, `Latitude`, `Longitude`, `GPS_Status`, `Pothole_Count`, `Severity`, `Avg_Confidence`, etc.).
*   **Interactive Map:** folium Leaflet map (`outputs/pothole_map.html`).

---

## 👥 Project Team (VIT Bhopal University - March 2026)
*   Lucky Kumar (23BCG10089)
*   Nitin Kumar Singh (23BAI10744)
*   Utkarsh Singh Yadav (23BAI10609)
*   Rishabh Mishra (23BAI11016)
*   Kartik Kumar Singh (23BCE11103)
*   GV Pranav Sharma (23BEY10032)
