# Smart-Fire-Detection-Environmental-Analytics-System
 An end-to-end industrial safety IoT application built on the Arduino Giga R1 WiFi architecture. The system utilizes multi-sensor fusion to track environmental anomalies and instantly stream hazard telemetry data to the cloud.
 
## 📸 System Visual Showcase

### 🛠️ Hardware Prototype Layout
Physical component configuration featuring the Arduino Giga R1 WiFi architecture, an embedded single-bus DHT11 atmospheric sensor, and an infrared flame sensor integrated with a prototyping breadboard matrix.

![Physical Hardware System Layout](Screenshot%202026-05-22%20at%201.38.23%20PM.png)

### ☁️ Cloud Telemetry & Analytics Dashboard
Real-time environmental monitoring interface hosted via ThingSpeak IoT Analytics. The multi-field telemetry pipeline tracks simultaneous data streams for ambient temperature spikes, humidity fluctuations, and discrete infrared flame hazard detections.

![ThingSpeak Cloud Analytics Dashboard](Screenshot%202026-05-22%20at%201.38.43%20PM.png)

---

## 🛠️ Technical Specifications & Tech Stack
- **Hardware Platform:** Arduino Giga R1 WiFi (Dual-Core ARM Cortex M7/M4 architecture)
- **Sensor Array (Sensor Fusion):** Infrared (IR) Flame Sensor & DHT11 Atmospheric Sensor (Temperature/Humidity)
- **Edge Processing:** Local serial diagnostics used to calibrate sensor thresholds against ambient light interference
- **Firmware Environment:** Embedded C++ (Arduino Core)
- **Cloud Infrastructure:** ThingSpeak IoT Analytics REST API Protocol

---

## 📊 Core Features & Engineering Logic
- **Sensor Fusion Processing:** Logic-optimized architecture that cross-references sharp environmental temperature spikes against active infrared readings to effectively minimize false positives in safety tracking.
- **Concurrent Cloud Pipelines:** Custom-built REST API integration pushing distinct, multi-channel telemetry streams simultaneously to remote cloud endpoints.
- **Data Integrity Management:** Implemented non-blocking delay routines using `millis()` to handle sensor polling intervals while matching cloud-side API rate limits, ensuring 0% packet drop rates.

---

## 💾 Firmware Implementation Architecture

```cpp
// --- Environmental Safety Pin Mapping ---
#define FLAME_SENSOR_PIN 2    // Digital input for active flame detection
#define DHT_PIN 3             // Single-bus data line for atmospheric tracking
#define ALARM_BUZZER 6        // Audible hazard notification indicator

// Telemetry Pipeline Controls
unsigned long lastCloudUpload = 0;
const int apiRateLimit = 15000; // 15-second non-blocking cloud synchronization window
