# Coordinates But With Time Per Point

- Your challenge is on how you can visualize this!
- Instead of each point being just `x` and `y`, we also have a `t` or a time component!
    - `t` is in microseconds
    - Means, you'll now be dealing with 3D data

## CSV Information

- Compressed with gzip. You can easily decompress this to a CSV
    - If inside `pandas`: `pandas.read_csv("file.csv.gz")`
    - If in a Linux terminal: `gunzip file.csv.gz`
- Three columns: `x`, `y`, `t`
- Total duration of the stream of coordinate points is just `4.735_154` seconds

## Data Hints

- `t` is the *motion through time* of what the object being pertained to is
- This is the same man riding on a horse you've seen before
- But since there's a time component, the coordinate points themselves may reveal something new
- Major Hint: Consider exporting what the counter looks like every 50 milliseconds, then resetting the whole counter
    - what would a sequence of those snapshots look like?

## Sample Usage

```python
class Coordinate(NamedTuple):
    x: int
    y: int
    t: int

WINDOW_US = 50_000  # 50 milliseconds in microseconds

coordinates: list[Coordinate] = ...  # contains the (x, y, t) triples
counter = CoordinateTimedCounter(width=320, height=320)
frames = []
window_start = coordinates[0].t

for x, y, t in coordinates:
    if ...:  # has enough time passed to export a frame?
        frames.append(counter.export())
        counter.reset()
        window_start = t
    counter.update(x=x, y=y, t=t)
```

## Deliverables

- Create a Jupyter notebook that visualizes the data
    - A heatmap (or a series of heatmaps?), an animation, a video, multiple frames, or something else entirely
