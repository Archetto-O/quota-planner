# Quota Planner

一个用于规划codex固定额度窗口与每日工作时间的纯前端网页工具。  
A browser-based tool for planning codex recurring quota windows around your daily work schedule.

---

## 中文说明

### 功能

- 使用 24 小时时间轴设置每天的工作时间。
- 时间轴从 **04:00** 开始，到次日 **04:00** 结束。
- 支持多个互不连续的工作时间段。
- 默认工作时间为：
  - 09:00–12:00
  - 14:00–17:00
  - 20:00–22:00
- 额度窗口长度可自由调整，并可选择：
  - 小时
  - 分钟
- 时间轴精度可选：
  - 5 分钟
  - 10 分钟（默认）
  - 30 分钟
  - 1 小时
- 可设置“每个额度池至少覆盖的工作时间”。
  - 分钟部分以 5 分钟为单位调整。
- “要求循环”默认勾选。
  - 勾选后，方案必须能够每天按照同一组触发时间重复。
  - 取消勾选后，仅优化当前 24 小时，可以考虑无法长期循环的单日方案。
- “触发可以在非工作时间内”默认勾选。
  - 允许通过一个极小任务在非工作时间启动新的额度窗口。
  - 如果最优方案包含非工作时间触发，网页会自动生成一段可编辑、可复制的提示词，并自动填入需要触发的时间。
- 自动给出最优触发时间、额度恢复时间、覆盖的工作时长以及等待下一额度窗口的时间。

### 默认假设

工具按照以下额度机制进行计算：

1. 一个额度池在首次使用时开始计时。
2. 达到设定的额度窗口长度后，额度恢复。
3. 恢复后可以等待到任意时刻再首次使用下一额度池。
4. 如果启用“要求循环”，则每天使用同一组触发时间，并保证方案可以长期重复。

### 优化目标

方案按以下顺序进行比较：

1. 最大化可使用的额度池数量。
2. 在额度池数量相同时，最大化所有额度池覆盖的总工作时间。
3. 在前两项相同时，尽量减少发生在工作时间外的触发次数。

### 时间轴与计算精度

工作时间在内部按分钟保存，因此修改时间轴精度不会破坏已经设置的工作区间。

时间轴精度决定：

- 鼠标拖动时的时间吸附粒度。
- 优化器允许选择的候选触发时间。

例如，当精度设置为 30 分钟时，候选触发时间会出现在：

```text
04:00
04:30
05:00
05:30
...
```

### 使用方法

1. 在时间轴上拖动鼠标设置工作时间。
2. 从空白区域开始拖动可添加工作时间。
3. 从已经设置的工作区域开始拖动可擦除工作时间。
4. 设置额度窗口长度。
5. 设置时间轴精度。
6. 设置每个额度池至少需要覆盖的工作时间。
7. 根据需要选择是否要求循环，以及是否允许非工作时间触发。
8. 点击 **“计算最优方案”**。
9. 查看推荐的触发时间和额度窗口安排。
10. 如果存在非工作时间触发，可以直接复制网页自动生成的提示词。

### 默认工作时间

点击 **“载入默认工作时间”** 后，会自动设置：

```text
09:00–12:00
14:00–17:00
20:00–22:00
```
---

## English

### Features

- Set your daily working hours on a 24-hour timeline.
- The timeline starts at **04:00** and ends at **04:00 the next day**.
- Multiple separated working periods are supported.
- Default working hours:
  - 09:00–12:00
  - 14:00–17:00
  - 20:00–22:00
- The quota window length is configurable in:
  - Hours
  - Minutes
- Timeline precision can be set to:
  - 5 minutes
  - 10 minutes (default)
  - 30 minutes
  - 1 hour
- You can specify the minimum amount of working time that each quota window must cover.
  - The minute value is adjusted in 5-minute increments.
- **Require recurring schedule** is enabled by default.
  - When enabled, the same trigger schedule must be repeatable every day.
  - When disabled, the optimizer only considers the current 24-hour period and may return a one-day schedule that cannot be repeated indefinitely.
- **Allow triggers outside working hours** is enabled by default.
  - This allows a very small task to start a quota window outside your normal working hours.
  - If the optimal schedule contains such triggers, the page automatically generates an editable and copyable prompt with the calculated trigger times.
- The optimizer reports recommended trigger times, quota reset times, covered working time, and waiting time before the next quota window.

### Assumptions

The planner uses the following quota model:

1. A quota window starts when the quota pool is first used.
2. The quota is restored after the configured window length.
3. After restoration, the next quota window does not need to start immediately. It can wait until the next actual use.
4. If **Require recurring schedule** is enabled, the same set of trigger times must remain repeatable every day.

### Optimization Objective

Schedules are ranked in the following order:

1. Maximize the number of usable quota windows.
2. If the number of windows is the same, maximize the total amount of working time covered by all quota windows.
3. If the first two objectives are tied, minimize the number of triggers that occur outside working hours.

### Timeline and Precision

Working periods are stored internally at minute-level resolution, so changing the visible timeline precision does not destroy previously selected working periods.

The selected timeline precision controls:

- The snapping interval when dragging on the timeline.
- The candidate trigger times considered by the optimizer.

For example, with 30-minute precision, candidate trigger times include:

```text
04:00
04:30
05:00
05:30
...
```

### How to Use

1. Drag on the timeline to select your working hours.
2. Start dragging from an empty area to add working time.
3. Start dragging from an existing working block to erase working time.
4. Set the quota window length.
5. Select the timeline precision.
6. Set the minimum working time required for each quota window.
7. Choose whether the schedule must repeat every day and whether triggers outside working hours are allowed.
8. Click **Calculate Optimal Schedule**.
9. Review the recommended trigger times and quota windows.
10. If off-hours triggers are required, copy or edit the automatically generated prompt.

### Default Working Hours

Clicking **Load Default Working Hours** sets:

```text
09:00–12:00
14:00–17:00
20:00–22:00
```

---
