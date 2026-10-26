# Smart India Hackathon Workshop
# Date: 26.10.2026
## Register Number: 212224040056
## Name: CHITTOOR SARAVANA MRUDHULA
## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations
## Problem Description
Background: Railway stations are complex environments with numerous facilities and locations such as ticket counters, platforms, restrooms, food courts, and waiting areas. Passengers often face difficulties in navigating these spaces, especially in large or unfamiliar stations. Efficient and user-friendly navigation systems are crucial for improving passenger experience, reducing congestion, and ensuring timely travel connections. Description: The problem involves developing a comprehensive navigation solution for railway stations that assists passengers in locating various facilities and destinations within the station premises. This includes creating detailed maps, providing real-time directions, and integrating features such as accessibility options for individuals with disabilities. The solution should be intuitive, easy to use, and accessible via multiple platforms, including mobile devices and digital kiosks. Key challenges include updating navigation information in real-time, ensuring accuracy, and accommodating the diverse needs of all passengers. Expected Solution: The expected solution is a multi-platform navigation system that provides detailed, real-time directions to all facilities and locations within a railway station. This system should include: A mobile application with 3D interactive maps and step-by-step navigation. Digital kiosks located throughout the station with touch-screen interfaces. Voice-guided navigation for visually impaired passengers. Regular updates to reflect changes in station layout and facility locations. Integration with existing railway apps and services for seamless user experience. The solution should enhance the overall passenger experience by reducing confusion, saving time, and improving accessibility within the station.

## Problem Creater's Organization
Ministry of Railway

## Idea

**RailWayfinder** is a single indoor-routing engine that powers every passenger touchpoint: a mobile PWA, touch-screen kiosks and voice guidance.

- **Station as a graph:** every location (platform, ticket counter, lift, restroom) is a node, and every walkway, staircase, lift or ramp is an edge, across multiple levels.
- **Accessibility-first routing:** wheelchair mode uses only lifts and ramps and a slower walking speed for the time estimate. If no step-free path exists, the app says so and directs the user to station staff.
- **Real-time updates:** staff can close a lift or path, and crowd-density data can be fed in. Routes recompute instantly, with no app update needed.
- **Inclusive guidance:** spoken directions and screen-reader support for visually impaired users, in English, Hindi and Tamil.
- **Seamless railway integration:** entering a train number sets the destination to its platform automatically (NTES/UTS integration planned).
- **No install, works offline:** a PWA that opens from a QR code at any pillar and caches the map for weak connectivity.

## Proposed Solution / Architecture Diagram


## Use Cases

| # | Actor | Scenario | Outcome |
|---|-------|----------|---------|
| 1 | First-time traveller | Arrives at a large station and needs Platform 6 | Step-by-step route with map highlight and time estimate |
| 2 | Wheelchair user | Needs a platform without stairs | Step-free route via lifts/ramps, or a clear message to contact staff |
| 3 | Visually impaired passenger | Needs to reach the restroom | Spoken turn-by-turn directions, screen-reader friendly, keyboard navigation |
| 4 | Passenger with a train ticket | Enters train number | Platform is found and navigated to automatically |
| 5 | Elderly / non-English speaker | Prefers Hindi or Tamil | Directions and place names in their language |
| 6 | Kiosk user | Walks up to a touch screen | Starts from the kiosk's fixed location with large, simple controls |
| 7 | Station staff | Lift under maintenance | Marks it closed; all routes update instantly |
| 8 | Station manager | Platform entrance is crowded | Crowd data pushes passengers to alternate paths, easing congestion |
| 9 | Railway planner (future) | Analyses movement patterns | Heatmaps and dwell-time analytics to improve layouts |

## Technology Stack

| Layer | Technology |
|-------|------------|
| Frontend (mobile and kiosk) | HTML5, CSS3, JavaScript (PWA), SVG maps, Service Worker for offline use |
| Voice and accessibility | Web Speech API (text-to-speech), ARIA live regions, keyboard navigation |
| Backend API | Python 3, FastAPI, Uvicorn, Pydantic |
| Routing | Dijkstra's algorithm on a multi-level weighted graph |
| Data | JSON station graphs (prototype); PostgreSQL/PostGIS + Redis (production) |
| Real-time (planned) | WebSockets / Server-Sent Events, Redis pub/sub |
| Positioning (planned) | BLE beacons, Wi-Fi RTT, QR-code anchors |
| 3D maps (planned) | Three.js / Mapbox indoor |
| DevOps | Docker, Docker Compose, GitHub Actions (CI), pytest |

## Dependencies

### Software libraries
- `fastapi`, `uvicorn`, `pydantic` (API server)
- `pytest`, `httpx` (testing)
- Browser APIs: Web Speech API, Service Worker, Fetch (no frontend framework needed)

### Data dependencies
- Station floor plans and facility locations (from Railways/station authorities)
- Lift, escalator and ramp locations, to support step-free routing
- Train and platform data feed (NTES/UTS) for the train-to-platform feature

### Infrastructure and integration
- Station Wi-Fi or mobile internet, with offline caching as a fallback
- Kiosk hardware (touch screen, speaker) and pillar QR codes
- Optional BLE beacons for automatic live positioning
- Access to Indian Railways APIs (NTES, UTS, Rail Madad) for production integration

### Operational dependencies
- Station staff access to the closure and crowd update interface
- Periodic review of map data when the layout changes
