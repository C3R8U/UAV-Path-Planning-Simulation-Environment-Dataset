# UAV-Path-Planning-Simulation-Environment-Dataset
## Overview

This dataset contains synthetic simulation environment inputs for UAV path planning in static and dynamically changing obstacle environments. It follows the scenario configurations presented in the manuscript *Holographic Counterpart-Based UAVs Localization Search Strategy Driven by IBB-DQN on Consumer Electronic Devices*. The files describe planning environments and environmental changes, rather than outputs of a path-planning algorithm.

## Dataset Files

- `trial_scenarios_zh.csv`: Defines each simulation trial, its random seed, map dimensions, obstacle density, obstacle block count, and UAV start and target coordinates.
- `trial_grid_blocks_zh.csv`: Records the initial occupancy state of each grid block for every trial.
- `trial_environment_changes_zh.csv`: Records time-stepped obstacle appearance events and the updated occupancy state of the affected block for each trial.

The CSV files have Chinese column headers and are encoded in UTF-8.

## Simulation Environment Configuration

| Parameter | Setting |
| --- | --- |
| Planning environment | Two-dimensional grid-based simulation |
| Map size | 100 m × 100 m |
| Obstacle block size | 10 m × 10 m |
| Grid layout | 10 columns × 10 rows |
| Obstacle density levels | 10%, 30%, 50% |
| Initial occupied blocks per density level | 10, 30, 50, respectively |
| Start location at 10% density | (10 m, 10 m) |
| Start location at 30% density | (20 m, 20 m) |
| Start location at 50% density | (30 m, 30 m) |
| Target location | Randomly assigned per trial |
| Trials | 100 per density level; 300 in total |

The three density levels correspond to the low-, medium-, and high-density scenarios in the manuscript's experimental environment settings.

## File Structure and Interpretation

### trial_scenarios_zh.csv

Each row identifies one trial (`试验编号`) and stores its random seed (`随机种子`), map width and height (`地图宽度米`, `地图高度米`), obstacle block side length (`障碍块边长米`), occupied-area proportion (`障碍占比`), occupied block count (`障碍块数量`), start coordinates (`起点横坐标米`, `起点纵坐标米`) and target coordinates (`终点横坐标米`, `终点纵坐标米`). Coordinates are in metres.

### trial_grid_blocks_zh.csv

Each row describes one block in the trial's initial 10 × 10 occupancy grid. `障碍块列编号` and `障碍块行编号` are zero-based column and row indices (0–9). `是否占用` is 1 for an occupied block and 0 for a free block. There are 100 block records per trial.

### trial_environment_changes_zh.csv

Each row identifies a trial (`试验编号`), event number (`事件序号`), simulation time step (`事件时间步`), event type (`事件类型`), modified grid column and row (`变化块列编号`, `变化块行编号`) and its occupancy after the event (`变化后是否占用`). Events occur at simulation steps 10, 20 and 30; `obstacle_appears` sets the specified block's occupancy to 1. The dataset contains three events per trial.

## Data Relationships

Join the files using `试验编号` (trial ID). Begin with the initial 10 × 10 grid from `trial_grid_blocks_zh.csv`, read the start and target coordinates from `trial_scenarios_zh.csv`, and apply `trial_environment_changes_zh.csv` in ascending `事件时间步` and `事件序号` order to update the grid. The grid indices denote block positions; the physical side length of each block is 10 m.
