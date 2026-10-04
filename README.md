# BlueprintReview sample project

A tiny Unreal Engine 5.8 project, a coin collector, made for the
[BlueprintReview user guide](https://blueprintreview.efenggamedev.com/docs/). Its Blueprints and its git history
are what the guide's steps and screenshots use, so you can follow every page with the same files.

## Get it

You need [Git LFS](https://git-lfs.com/): the `.uasset` files are stored with it.

```sh
git lfs install
git clone https://github.com/blueprintreview/sample-project.git
cd sample-project
git fetch origin feature/double-points:feature/double-points
blueprintreview git-setup
```

`blueprintreview git-setup` sets up `git difftool` and `git diff` for Blueprints in this clone. The guide's
[Get the sample](https://blueprintreview.efenggamedev.com/docs/get-the-sample/) page explains each step.

To open it in Unreal, double-click `BlueprintReviewSample.uproject` (UE 5.8). You don't need it in Unreal to follow
the guide: BlueprintReview reads the files without the editor.

## What's in it

All in `Content/Sample/`:

| Asset | What it is |
|---|---|
| `BP_Coin` | A spinning coin. Its `GetPoints` function picks the points by `CoinType`; overlapping it scores them and removes the coin |
| `BP_CoinSpawner` | Spawns a `BP_Coin` every `Interval` seconds, `SpawnRadius` away |
| `BP_ScoreGameMode` | Keeps `TotalScore`; `AddScore` adds to it and calls `OnScoreChanged` |
| `Data/E_CoinType` | The coin types: Bronze, Silver, Gold, Platinum |
| `Data/S_CoinReward` | A reward: points, a label and a pick-up sound |
| `Data/DT_CoinRewards` | The rewards, one row per coin type |

## The history

Each commit makes one kind of change, so each guide has one to look at:

| Commit | Shows |
|---|---|
| Add the coin collector | the starting point |
| Spawner: SpawnRadius setting | a variable added, a default value, a new wire |
| Coin: Silver coins; GetPoints selects the points by coin type | nodes replaced, an enum entry added |
| Coin: spin with a RotatingMovement component | components added and changed |
| Coin: tidy the pick-up graph | nodes moved only: no real change |
| Spawner: route the transform wire through a reroute node | a re-routed wire: no real change |
| Game mode: rename Score to TotalScore | a renamed variable and the nodes that use it |
| Rewards: rebalance the points, add the Silver row | data table rows |
| Add the Platinum coin | an enum, a data table and a Blueprint changed together |
| Rewards: a pick-up sound per reward | a struct field |
| Coin: move the scoring into a ScoreCoin function | nodes collapsed into a function |
| Spawner: comment the timer and the spawn position | comments |
| Spawner: spawn every 1.5 s, up to 800 units away | class defaults |

The `feature/double-points` branch adds two more, for comparing a branch and reviewing a pull request.

## How it was made

Every change was made by an edit plan applied with BlueprintReview's *Blueprint Edit Automation* plugin, without
opening the editor. Each commit adds the plans that made it to `EditPlans/` (the `a`, `b` parts of one number go in
one commit), and the [edit plans tutorial](https://blueprintreview.efenggamedev.com/docs/edit-tutorial/) walks
through one.

The `Plugins/` folder is ignored: install the plugins yourself if you want to apply plans
([the UE plugin](https://blueprintreview.efenggamedev.com/docs/plugin/)).

## License

[MIT](LICENSE). The project uses only engine content (`/Engine/BasicShapes`) besides its own assets.
