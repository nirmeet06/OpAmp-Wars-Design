## Team Name
<Op-amp paglu>

## Topology
Two-Stage Miller-Compensated Operational Amplifier

## Files Included
- `opamp.asc` — main LTspice schematic including the amplifier subcircuit and the contest harness.
- `twostage` subcircuit — defined inside the schematic via SPICE directives.
- `README.md` — this document.

## Declared Performance Bucket
Minimal Complexity  
(Uses simple two-stage architecture, ideal bias currents, passive loads, no OTA fancy techniques.)

## Requirements Checklist
- Closed-loop gain ≈ 40 dB 
- Bandwidth ≥ 100 kHz 
- Phase margin ≥ 45° 
- Slew rate ≥ 5 V/µs 
- Monte Carlo (20 runs) median Vos within required bounds
- Stable into 10 kΩ load 

## Design Diary (≥3 iterations, timestamped)
- **2025-11-09 13:00** — Inserted baseline two-stage Miller op-amp with `Itail = 200µA` and `Cc = 2pF`. AC gain achieved but PM marginal.
- **2025-11-09 14:30** — Increased load resistors (`RRL1`, `RRL2`) to improve open-loop gain. Observed slight bandwidth reduction.
- **2025-11-09 15:10** — Increased compensation capacitor (`Cc = 3pF`) to improve phase margin above 45°. Slew rate still comfortably above spec.
- **2025-11-09 15:45** — Ran 20 Monte Carlo Vos tests with `mc(seed, 0.01)` on resistors. Observed acceptable median offset.

(Optional extra entries can be added depending on your tweaks.)

## How to Re-Run Simulations
1. Open `yourteam.asc` in LTspice.
2. Run `.op` for DC bias sanity check.
3. Run `.ac` to view gain/phase and extract −3 dB frequency.
4. Run `.tran` to view large-signal step and measure slew rate (cursor slope).
5. Run `.step param seed 1 20 1` + `.op` to collect Monte Carlo Vos values.

## Amplifier Architecture Notes
- Differential NMOS input pair
- Resistive loads to VCC (simple active-load approximation)
- Common-source second stage
- Miller compensation capacitor between first internal node and output
- Ideal tail current source biasing (permitted and keeps design simple)

## Creative Note
A compact two-stage amplifier using classic Miller compensation — simple enough to tune quickly, yet stable and reliable under load. Designed with contest efficiency and clarity in mind.

## License / Citation
Designed by <Op-amp paglu> for Op-Amp Wars contest.
No external libraries or proprietary models used beyond LTspice built-ins.
