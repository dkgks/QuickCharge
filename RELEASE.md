# Quick Charge v3.1.17 (Shell)

整合上游 `3.1.16–3.2.0` 启动可靠性增强，保留旧版 `state.conf` 兼容性及本分支全部优化（`versionCode: 3011701`）。

## 主要变更

- **吸收上游 `3.1.16–3.2.0` 启动与挂载增强**：
  - `post-fs-data.sh` 新增 `phase.pfs` 阶段落痕与多路径 `MODDIR` 探测；`service.sh` 使用 `/proc/uptime` 单调时钟校验开机新鲜度，异常/中途退出时自动重建补挂，同时尊重 `safe-mode` 安全模式跳过挂载。
  - 删除「内容相同即当已挂载」误判，改查 `/proc/mounts` 与 `/proc/self/mountinfo` 并支持 `yes` / `partial` / `no` 三态判活（`partial` 自动补挂）。
  - `sd_dump_env` 新增 `overrides=N mounts=N nm=bind|nomount alive=...`；`sd_transform` 改写无差异时不生成空耗覆盖层并归类为「无差异」。
  - 平台探测扩展至 `300s` 时间窗并在认对后日志留痕，新增 `*alor*` 识别。
- **保留 v3.1.16 Fork 特性**：无弹窗静默安装、精简 WebUI/README、`hot_cutoff` 高温保护、未插电 `vusb` 噪声防放大与双电芯功率折算、`state.conf` 平滑兼容。

## 发布产物

- `QuickCharge-v3.1.17.zip`：Magisk / KernelSU / APatch 可刷入模块包
- `update.json`：模块在线更新元数据
- `RELEASE.md`：本版本更新说明
