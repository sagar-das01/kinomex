# Kinomex

**Kinomex** is a centralized Command & Control Fleet Management Platform for Autonomous Mobile Robots (AMRs). The system bridges high-level web orchestration with on-board edge intelligence, allowing operators to track telemetric states, dispatch missions, and log AI-driven vision alerts in real time.

## 🏗️ System Architecture

- **`kinomex_server/`**: The central command deck built on Python and Django. Manages the fleet registry, relational logs, multi-user operator access, and real-time WebSocket communication pipelines.
- **`kinomex_edge/`**: The lightweight client software executing directly on the robot chassis (or simulation software), handling locomotion layers and computer vision inference.

## 🛠️ Tech Stack

- **Backend Framework:** Django, Django REST Framework (DRF)
- **Real-Time Layer:** Django Channels (WebSockets), Redis
- **Database:** PostgreSQL / SQLite
- **Edge AI & Robotics:** Python, OpenCV, PyTorch / YOLOv8, ROS2 (Optional/Simulated)

## 🚀 Quick Start (Server)

1. Clone the repository:
   ```bash
   git clone https://github.com
   cd kinomex
   ```

2. Set up a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Run migrations and start the server:
   ```bash
   cd kinomex_server
   python manage.py migrate
   python manage.py runserver
   ```
