# BeeBot: DFS vs A* Pathfinding

A project from my postgraduate course *AI for Autonomous Systems*, exploring how **Depth-First Search (DFS)** and **A\*** compare when navigating a "BeeBot" agent through a randomly generated grid map from a start cell to a goal cell.

The full implementation, walkthrough, and analysis live in [`BeeBot.ipynb`](./BeeBot.ipynb). This README summarizes the approach and findings.

## Problem Formalism

**State** — a 1D array `[bee_row, bee_col, bee_direction]`
- `bee_direction`: `0` = North, `1` = East, `2` = South, `3` = West
- Initial state is randomly placed on an empty cell; goal is reached when `map[bee_row][bee_col] == 2`

**Map** — a 2D `m x n` array
| Value | Meaning |
|---|---|
| `0` | Empty cell |
| `-1` | Obstacle |
| `1` | BeeBot |
| `2` | Goal |

**Actions** — the BeeBot can move forward, move backward, turn left 90°, or turn right 90°, relative to its *own* facing direction (not fixed map cardinal directions). For DFS, actions are ordered `[step back, turn left, turn right, step forward]` to prioritize stepping forward, since DFS explores in LIFO order.

## Algorithms

- **DFS** — explores paths depth-first with no notion of path cost, so it can waste time fully exploring suboptimal branches.
- **A\*** — uses Manhattan distance as the heuristic, which is admissible (never overestimates true cost), guiding the search toward the goal more directly.

## Evaluation

DFS and A* were compared across 5 map sizes (11x11, 21x21, 31x31, 41x41, 51x51), with 20 randomly generated maps per size, measuring:
- **Speed** — execution time
- **Efficiency** — number of actions in the path found

## Results

**Speed**
- On small maps, DFS and A* perform similarly.
- DFS scales poorly on larger maps, since it can exhaust suboptimal branches to full depth rather than moving toward the goal.

**Efficiency**
- A* consistently finds the optimal (shortest) path, since its admissible heuristic guarantees this.
- DFS finds *a* path, not necessarily the shortest one.

## Running it

```bash
pip install numpy matplotlib
jupyter notebook BeeBot.ipynb
```
