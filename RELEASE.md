# Quick Charge v3.1.16 (Shell)

基于上游 `XiaohaoQvQ/QuickCharge` 增强的 Shell 版发布包，更新通道 `shell`（`versionCode: 3011601`）。

## 主要变更

- **修复未插电悬空噪声放大与日志刷屏**：在 `usb/voltage_max`（或 `current_max`）为 `µV`/`µA` 量级且处于未插电（`online=0` 或未充电）状态时，不再对 `1~20mV` 悬空读数执行千倍放大；未充电时判重签名忽略负载波动与悬空 `vusb`，消除待机每 30 秒刷屏。
- **双电芯电池功率修正**：`sd_chg_line_fill` 计算 `pb` 与中值功率档位时，对双电芯且 `voltage_now` 报单芯电压（`2.5–5.0V`）的机型按双芯包电压折算，避免功率减半。
- **输入电流符号兼容**：`sd_chg_input_v` 先取绝对值再做单位归一，兼容负号输入电流读数。
- **继承 v3.1.15 Fork 增强**：包含可选 `hot_cutoff`（`42–55℃`）物理高温断开兜底、拔线清理 `scr.fail` 并保留 `fcc.norm`，以及无弹窗静默安装。

## 发布产物

- `QuickCharge-v3.1.16.zip`：Magisk / KernelSU / APatch 可刷入模块包
- `update.json`：模块在线更新元数据
- `RELEASE.md`：本版本更新说明
