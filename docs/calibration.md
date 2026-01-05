# Calibration (quick guide)

This project currently uses fixed thresholds:
- Fall: `accelMag > 18.0`
- No movement: `accelMag < 2.0`
- Tremor: `abs(accelMag - prevAccelMag) > 2.0`
- Pulse detected: `irValue > 5000`

## Recommended calibration steps
1. **Baseline stillness**
   - Wear/hold device in the intended position.
   - Observe `accelMag` values while still for 30–60s.
   - Set `noMovement` threshold slightly above that baseline.

2. **Normal motion**
   - Walk normally, do typical hand motion.
   - Ensure `noMovement` does not trigger falsely.

3. **Tremor detection**
   - Instead of single-step delta, use a sliding window (e.g., 2–3 seconds)
     and evaluate variance or dominant frequency.

4. **Fall detection**
   - Fall detection is tricky; consider a 2-stage rule:
     - Free-fall / low-g spike then impact spike within a time window.

5. **MAX30102**
   - For real vitals, implement proper beat detection and SpO2 computation.

## Suggested next commit
Add a `DEBUG` mode that prints:
- accelMag
- prevAccelMag
- irValue
so you can tune thresholds faster.
