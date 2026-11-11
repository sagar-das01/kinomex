kinomex/
├── .github/
│   └── workflows/
│       └── ci.yml                  # Automated pytest & linting pipeline
├── docker/
│   ├── server/
│   │   └── Dockerfile              # Multi-stage build for Daphne + Celery
│   ├── edge/
│   │   └── Dockerfile              # Containerized simulator for testing
│   └── nginx/
│       └── nginx.conf              # Reverse proxy for HTTPS & WSS routing
│
├── kinomex_server/                 # Core Django Application
│   ├── manage.py
│   ├── kinomex_server/             # Project Configuration Package
│   │   ├── __init__.py             # Exposes Celery app on Django startup
│   │   ├── asgi.py                 # HTTP + WebSocket protocol router
│   │   ├── celery.py               # Celery worker & beat configuration
│   │   ├── urls.py                 # Root API & dashboard URL routing
│   │   └── settings/               # Split settings for environment safety
│   │       ├── __init__.py
│   │       ├── base.py             # Shared settings, installed apps, middleware
│   │       ├── local.py            # Local dev overrides (DEBUG=True)
│   │       └── production.py       # Security headers, S3 storage, strict CORS
│   │
│   ├── apps/                       # Modular Domain Apps
│   │   ├── users/                  # Custom User model, RBAC roles, JWT auth
│   │   ├── fleet/                  # Robot registry, M2M API keys, health states
│   │   ├── missions/               # Waypoint routing, PostGIS geofences, task queues
│   │   ├── telemetry/              # WebSocket consumers, Redis pub/sub, Watchdog tasks
│   │   └── vision/                 # AIInferenceAlert models, S3 snapshot handlers
│   │
│   ├── static/                     # Compiled CSS, JS, map icons
│   ├── templates/                  # Operator Command Dashboard UI
│   └── tests/                      # Pytest integration & WebSocket tests
│
├── kinomex_edge/                   # On-Board / Simulated Robot Client
│   ├── config/
│   │   └── robot_config.yaml       # Hardware thresholds, server endpoints, M2M keys
│   ├── core/
│   │   ├── buffer.py               # Local SQLite offline queue for network drops
│   │   ├── comms.py                # Resilient WebSocket & REST client with auto-retry
│   │   └── safety.py               # Deterministic E-STOP & collision override loop
│   ├── vision/
│   │   ├── detector.py             # ONNX / TensorRT YOLOv8 inference engine
│   │   └── stream.py               # WebRTC low-latency video streamer
│   └── main.py                     # Edge orchestrator entrypoint
│
├── .env.example                    # Template for required environment variables
├── .gitignore                      # Excludes .env, venv, __pycache__, local SQLite DBs
├── docker-compose.yml              # Orchestrates Django, Postgres, Redis, Celery, Nginx
├── requirements/
│   ├── base.txt                    # Core dependencies (Django, DRF, Channels, Celery)
│   ├── local.txt                   # Dev tools (pytest, black, ruff, django-debug-toolbar)
│   └── production.txt              # Prod drivers (gunicorn/daphne, psycopg, sentry-sdk)
└── README.md
