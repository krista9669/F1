# F1 Track Map Visualizer

Generates an annotated circuit map for any Formula 1 race session using real telemetry data. Corner numbers, labels, and track geometry are rendered from actual car position data — not static images.

---

## Output

Produces a scaled, rotated map of the circuit with:
- Track outline drawn from the fastest lap's GPS position data
- All corners labeled with their official number and letter (e.g. `1`, `6A`, `6B`)
- Leader lines connecting corner markers to their position on track
- Circuit name as the plot title

---

## How It Works

1. Loads race session data for the 2021 French Grand Prix using FastF1
2. Picks the fastest lap from the session
3. Extracts `X` and `Y` position coordinates from onboard telemetry
4. Retrieves the circuit's rotation angle and corner metadata
5. Applies a 2D rotation matrix to align the track upright
6. Plots the track outline and projects corner labels outward using offset vectors

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.x | Core language |
| FastF1 | F1 session and telemetry data |
| NumPy | Rotation matrix and array operations |
| Matplotlib | Track and corner visualization |

---

## Installation

```bash
pip install fastf1 numpy matplotlib
```

---

## Usage

```bash
python track_map.py
```

On first run, session data is fetched from the F1 API and written to a local `cache/` folder. Subsequent runs load from cache and execute significantly faster.

To visualize a different race, update these parameters in the script:

```python
session = fastf1.get_session(2021, 'French Grand Prix', 'R')
#                             year   event name          session type
#                                                        'R' = Race
#                                                        'Q' = Qualifying
#                                                        'FP1' / 'FP2' / 'FP3'
```

---

## Notes

- A `cache/` directory is created automatically on first run
- Requires an active internet connection on first run to fetch session data
- Position data is sourced from the fastest lap, which best represents the full track layout
- The rotation transformation ensures the circuit is displayed in its conventional orientation

---

## License

This project is licensed under the [MIT License](LICENSE).
