[![make.fun](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)
[![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/sofyanadirs-sketch/sokoban-solver-01-run-20261121/rank.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)
[![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/sofyanadirs-sketch/sokoban-solver-01-run-20261121/reward.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)

# Sokoban Solver — make.fun bounty `sokoban-solver-01-run-20261121`

A push-optimal Sokoban solver for [the make.fun bounty](https://make.fun/bounty/sokoban-solver-01-run-20261121): one program answers all 5 instances of a set in a single run, writing each instance's player moves (u/d/l/r) to `/output/<id>/solution.txt`.

## How it works

Each level is a hallway with independent rooms off it, and a level's push-optimal count is the sum of its rooms' optima — so the solver splits the level into its rooms, solves every room push-optimally on its own, and stitches the rooms together with plain walks through the hallway (walks cost no pushes, only pushes count towards the score).

Each room is solved with a push-based A*: a state is the sorted box squares plus the player's reachable region, the estimate is the cheapest assignment of boxes to goals by box-travel distance, and the search prunes simple deadlocks (a box on a square no goal can be reached from) and frozen 2x2 blocks. Search budgets count expanded states, never wall time, so two runs write the same bytes.

Practice-set result: **1,000,000 / 1,000,000** — all 5 instances solved in exactly P* pushes (13, 16, 29, 47, 60), in about 0.5 s for the whole set. The same score held on 50 freshly drawn sets (250 instances) from the kit's own generator.

## Run

```sh
# Local run on the practice set (from the unpacked kit):
MAKEFUN_INPUT_DIR=practice/input MAKEFUN_OUTPUT_DIR=out node main.ts

# The grader runs it as:
node /bot/main.ts
```

Node 22.18+ (type stripping) or later, no dependencies, no network. `main.ts` is the entrypoint at the repository root.

## Referral

make.fun referral code: **h9b99srf** — https://make.fun/r/h9b99srf

## License

MIT — see [LICENSE](LICENSE).
