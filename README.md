# -AI-Powered-Maritime-Navigation-System
# 🌊 AI-Powered Maritime Navigation System
## Overview
An intelligent maritime fleet routing and autonomous risk-aware navigation system that uses AI to plan optimal ocean routes while actively avoiding detected hazards through collision avoidance algorithms.

## ✨ Key Features

### 1. **Intelligent Route Planning**
- Graph-based A* pathfinding algorithm for ocean-only navigation
- Ensures routes stay in navigable waters (no land crossing)
- Calculates optimal paths between major global ports

### 2. **Object Detection & Hazard Avoidance** ⚡
- **Trigger-based object detection** (simulates real-time hazard detection)
- Detects maritime hazards:
  - 🧊 Icebergs
  - ❄️ Glaciers
  - 🔴 Navigation Buoys
  - 🌊 Ocean Debris
- **Active collision avoidance**: Routes automatically deviate around detected objects
- Configurable hazard buffer zones (default: 100 km)

### 3. **Fleet Monitoring**
- Real-time tracking of multiple vessels
- Ship position, speed, heading, and priority monitoring
- Route assignment and status tracking

### 4. **Interactive Web Interface**
- Live map visualization with Leaflet.js
- Port selection and route planning
- **Object detection trigger button** for simulating hazard detection
- Real-time route deviation visualization
- Fleet status dashboard
- **Visual Analytics Dashboard**: Real-time charts for hazard distribution, fleet composition, and safety performance
- **Reporting System**: Automated generation of PDF-ready analytics reports

## 📁 Project Structure

```
AI_marine/
├── app.py                      # Flask web application
├── navigation_system.py        # Main navigation system with collision avoidance
├── routing_engine.py           # A* pathfinding algorithm
├── object_detector.py          # Object detection and hazard management
├── init_data.py               # Dataset initialization
├── data/                      # CSV datasets
│   ├── ports.csv              # Global port locations
│   ├── ocean_nodes.csv        # Ocean waypoint graph
│   ├── ships.csv              # Fleet vessel data
│   ├── routes.csv             # Assigned routes
│   └── detected_objects.csv   # Detected maritime hazards
├── object_detection/
│   ├── images/                # Maritime hazard images
│   │   ├── iceberg.png        # Iceberg reference image
│   │   ├── glacier.jpg        # Glacier reference image
│   │   └── buoy.jpg           # Navigation buoy image
│   └── IMAGE_GUIDE.md         # Image requirements guide
├── analytics_generator.py      # Analytics report and graph generator
├── analytics/                  # Generated performance graphs (PNG)
├── templates/
│   └── index.html             # Web interface with integrated Chart.js dashboard
└── ANALYTICS_REPORT.md         # Comprehensive operational report

```

## 🚀 Installation & Setup

### Prerequisites
- Python 3.8+
- pip package manager

### Step 1: Install Dependencies
```bash
pip install pandas numpy opencv-python flask flask-cors
```

### Step 2: Initialize Datasets
```bash
python init_data.py
```

This creates all necessary CSV files with:
- 10 major global ports
- Ocean navigation nodes
- 4 active vessels
- Initial detected hazards

### Step 3: Run the Web Application
```bash
python app.py
```

The server will start at: **http://localhost:5000**

## 🎮 How to Use

### Web Interface

1. **Open your browser** and navigate to `http://localhost:5000`

2. **Select Route**:
   - Choose a start port (e.g., Chennai)
   - Choose an end port (e.g., Singapore)
   - Set hazard buffer distance (default: 100 km)

3. **Trigger Object Detection** ⚡:
   - Click the **"⚡ Trigger Object Detection"** button
   - This simulates detecting maritime hazards in the ocean
   - New icebergs, glaciers, and buoys will appear on the map

4. **Calculate Safe Route**:
   - Click **"🧭 Calculate Safe Route"**
   - The system will:
     - Calculate initial route
     - Scan for hazards along the route
     - **Automatically deviate** if hazards are detected
     - Display the safe route on the map

5. **View Results**:
   - Route status: DIRECT or DEVIATED
   - Total distance and ETA
   - Number of hazards avoided
   - Additional distance due to deviation

### Command Line Interface

Run individual components:

```bash
# Test object detection
python object_detector.py

# Test navigation system
python navigation_system.py

# Test routing engine
python routing_engine.py
```

## 🔍 How Collision Avoidance Works

1. **Initial Route Calculation**: A* algorithm finds shortest ocean path
2. **Hazard Scanning**: System checks for detected objects within buffer zone
3. **Hazard Detection**: If objects found, collision avoidance activates
4. **Route Recalculation**: 
   - Marks hazard zones as obstacles
   - Filters out unsafe ocean nodes
   - Recalculates path avoiding hazard zones
5. **Route Deviation**: New route bypasses all detected hazards
6. **Distance Adjustment**: Calculates additional distance traveled

## 📊 Available Ports

1. Singapore (1.29°N, 103.85°E)
2. Shanghai (31.23°N, 121.47°E)
3. Rotterdam (51.92°N, 4.48°E)
4. Jebel Ali (25.01°N, 55.06°E)
5. Los Angeles (33.74°N, -118.24°W)
6. Chennai (13.08°N, 80.27°E)
7. Colombo (6.93°N, 79.86°E)
8. Suez Canal (North) (31.26°N, 32.30°E)
9. Panama Canal (East) (9.35°N, -79.90°W)
10. Hamburg (53.55°N, 9.99°E)

## 🛠️ Technical Details

### Algorithms
- **Pathfinding**: A* algorithm with Haversine distance heuristic
- **Collision Avoidance**: Dynamic obstacle exclusion with route recalculation
- **Distance Calculation**: Great circle distance (Haversine formula)

### Data Structures
- Graph-based ocean waypoint network
- CSV-based data storage for portability
- Real-time hazard database updates

### Technologies
- **Backend**: Python, Flask
- **Frontend**: HTML5, CSS3, JavaScript
- **Mapping**: Leaflet.js with OpenStreetMap
- **Data Processing**: Pandas, NumPy
- **Image Processing**: OpenCV

## 📝 API Endpoints

- `GET /api/ports` - List all available ports
- `GET /api/ships` - Get fleet status
- `GET /api/detected_objects` - Get all detected hazards
- `POST /api/trigger_detection` - Trigger object detection simulation
- `POST /api/calculate_route` - Calculate route with collision avoidance
- `GET /api/fleet_status` - Get comprehensive fleet status

## 🎯 Example Usage

### Calculate Route from Chennai to Singapore

**Request:**
```json
POST /api/calculate_route
{
  "start_port": "Chennai",
  "end_port": "Singapore",
  "hazard_buffer": 100
}
```

**Response:**
```json
{
  "success": true,
  "deviated": true,
  "distance_km": 3942.6,
  "eta_hours": 141.9,
  "route": [[13.08, 80.27], [12.5, 82.5], ...],
  "hazards": [
    {"type": "buoy", "lat": 13.15, "lon": 80.8}
  ]
}
```

## 🔧 Configuration

### Hazard Buffer Distance
Adjust in the web interface or API call (10-500 km recommended)

### Ocean Node Density
Modify `init_data.py` to add more waypoints for finer route granularity

### Detection Simulation Region
Edit `object_detector.py` to change detection area coordinates

## 🌟 Future Enhancements

- Real-time weather integration
- Machine learning-based object detection (YOLO/Faster R-CNN)
- Multi-ship collision avoidance
- Fuel optimization algorithms
- AIS (Automatic Identification System) integration
- Real-time satellite imagery processing

## 📄 License

This project is for educational and demonstration purposes.

## 👨‍💻 Author

AI Maritime Navigation System
Developed with advanced pathfinding and collision avoidance algorithms

---

**🚢 Safe Navigation! 🌊**
