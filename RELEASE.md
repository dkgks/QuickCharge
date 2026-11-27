# Quick Charge v3.1.15 (Shell)

基于上游 `XiaohaoQvQ/QuickCharge` 增强的 Shell 版发布包，更新通道 `shell`（`versionCode: 3011501`）。

## 主要变更

- **新增物理高温断开兜底 (`hot_cutoff`)**：支持在 `42–55℃` 之间设置硬保护阈值，触发后主动恢复真实温控节点，温度回落 `3℃` 后自动重连，同时同步接入 WebUI 与 CLI (`cutoff`)。
- **优化拔线状态恢复**：亮/灭屏节点写入异常标记 (`scr.fail`) 改为拔出充电器时清理，并完整保留已记录的正常满充基准 (`fcc.norm`)。
- **移除多余安装弹窗**：清理 `customize.sh` 刷入阶段的群聊提示弹窗，实现静默安装。
- **更新源与 CI/CD 适配**：`module.prop` 与 `update.json` 指向 `dkgks/QuickCharge`，已通过全套 Shell 单元测试并由 GitHub Actions 自动构建打包。

## 发布产物

- `QuickCharge-v3.1.15.zip`：Magisk / KernelSU / APatch 可刷入模块包
- `update.json`：模块在线更新元数据
- `RELEASE.md`：本版本更新说明
