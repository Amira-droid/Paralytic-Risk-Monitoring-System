# Wiring

## ESP32 ↔ I2C (shared bus)
This sketch uses:
- `SDA_PIN = 21`
- `SCL_PIN = 22`

Connect both sensors to the same I2C lines.

## MPU6050
- VCC → 3.3V (recommended)
- GND → GND
- SDA → GPIO 21
- SCL → GPIO 22
- AD0:
  - If you want address **0x68**, tie AD0 to GND
  - If you want address **0x69**, tie AD0 to 3.3V

> The code currently calls `mpu.begin(0x69)` — set AD0 accordingly.

## MAX30102
Breakout boards vary; check the silkscreen.
- VIN / VCC → 3.3V
- GND → GND
- SDA → GPIO 21
- SCL → GPIO 22

## Alert LED
- `LED_PIN = 2` (ESP32 on-board LED on many dev boards)
If your board differs, change `LED_PIN` in the code.

## Common issues
- Power: MAX30102 can be sensitive to noisy power. Prefer stable 3.3V.
- I2C pullups: Most breakouts include pullups; avoid doubling too many.
