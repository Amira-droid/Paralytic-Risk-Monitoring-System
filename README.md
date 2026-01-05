# Paralytic Risk Monitoring System (ESP32 + MAX30102 + MPU6050)

An ESP32-based prototype that reads motion + vitals and raises an alert if **pulse is not detected**, **movement is absent**, a **fall** is detected, or **tremor-like shaking** is detected.

## What’s inside
- **ESP32** (tested with default I2C pins set explicitly to SDA=21, SCL=22)
- **MAX30102 / MAX30105 library (SparkFun MAX3010x)** for IR readings
- **MPU6050 (Adafruit library)** for accel/gyro motion detection
- **On-board / external LED** (GPIO 2) indicates alert condition

## Repo structure
```
paralytic-risk-monitor-esp32/
  ParalyticRiskMonitor/
    ParalyticRiskMonitor.ino
  docs/
    wiring.md
    calibration.md
  .gitignore
  LICENSE
```

## Setup (Arduino IDE)
1. Install **ESP32 board support** in Arduino IDE:
   - *Boards Manager* → search **esp32** → install “ESP32 by Espressif Systems”.
2. Install libraries (Library Manager):
   - **Adafruit MPU6050**
   - **Adafruit Unified Sensor**
   - **SparkFun MAX3010x Sensor Library** (provides `MAX30105.h` used in the sketch)
3. Open `ParalyticRiskMonitor/ParalyticRiskMonitor.ino`
4. Select your board (e.g., *ESP32 Dev Module*) and correct COM port.
5. Upload.

## Serial Monitor
- Baud rate: **115200**
- You will see a UI-friendly output every second.

## Alert logic (current)
The sketch sets **ALERT** if any is true:
- Pulse not detected (IR below threshold)
- No movement (accel magnitude below threshold)
- Fall detected (accel magnitude above threshold)
- Tremor detected (large delta vs previous accel magnitude)

> Note: HR/SpO2 in this prototype are **rough estimates** derived from IR intensity, for demonstration only.

## Next improvements (recommended)
- Proper HR and SpO2 computation (peak detection + ratio-of-ratios)
- Adaptive thresholds per user/session (calibration step)
- Sliding-window tremor detection (frequency-domain)
- Add buzzer / notification (BLE / Wi‑Fi)

See `docs/calibration.md`.

---
**Disclaimer:** This is a research/prototype project and not a medical device.
