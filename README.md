# F1 Data Visualizations

A set of Formula 1 data visualization scripts built with FastF1 and Matplotlib. Each script pulls real telemetry and timing data to generate accurate, race-specific plots.

---

## Visualizations

### 1. Circuit Map
> `draw_circuit.py`

Generates an annotated map of a circuit using GPS position data from the fastest lap. Corner numbers and labels are projected outward from the track using offset vectors, matching the circuit's official orientation.

**Output**
- Track outline from real onboard position data
- All corners labeled with official number and letter (e.g. `1`, `6A`, `6B`)
- Leader lines from each corner marker to its position on track
- Circuit location as the plot title

**How It Works**
1. Loads race session data using FastF1
2. Picks the fastest lap from the session
3. Extracts `X` / `Y` telemetry coordinates as a NumPy array
4. Retrieves circuit rotation angle and corner metadata
5. Applies a 2D rotation matrix to align the track upright
6. Projects corner labels outward using angular offset vectors

---

### 2. Race Position Chart
> `driver_standings.py`

Plots every driver's position across all race laps on a single chart. Each driver is rendered in their official team color with distinct line styles to avoid overlap.

**Output**
- One line per driver across all race laps
- Official team colors and line styles via `fastf1.plotting`
- Y-axis inverted so P1 appears at the top
- Driver abbreviation legend positioned outside the plot area

**How It Works**
1. Loads race session lap data using FastF1
2. Iterates over all drivers in the session
3. Retrieves each driver's official color and line style
4. Plots lap number vs. position for each driver
5. Formats axes and adds a legend

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.x | Core language |
| FastF1 | F1 session, telemetry, and timing data |
| NumPy | Rotation matrix and coordinate operations |
| Matplotlib | All plotting and visualization |

---

## Changing the Race

Both scripts can be pointed at any F1 session by updating a single line:

```python
# track_map.py
session = fastf1.get_session(2021, 'French Grand Prix', 'R')

# position_changes.py
session = fastf1.get_session(2023, 'Japanese Grand Prix', 'R')
```

| Parameter | Options |
|---|---|
| Year | Any season from 2018 onwards |
| Event | Full Grand Prix name (e.g. `'Monaco Grand Prix'`) |
| Session | `'R'` Race · `'Q'` Qualifying · `'FP1'` `'FP2'` `'FP3'` |
