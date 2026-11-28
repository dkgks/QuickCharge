# Quick Charge (Shell)

适用于 OPPO / 一加 / realme（ColorOS / RealmeUI）的温控伪装与快充解锁模块，支持 **Magisk / KernelSU / APatch**。

> 本仓库 Fork 自 [XiaohaoQvQ/QuickCharge](https://github.com/XiaohaoQvQ/QuickCharge)，并针对稳定性、高温兜底与 CI 构建做了增强。若追求更低资源占用，可选用原生 C 守护进程版：[dkgks/QuickCharge-C](https://github.com/dkgks/QuickCharge-C)。

## 核心特性

- **壳温伪装与动态曲线**：支持 `charge`（默认，基准 `30℃` + 亮屏补偿，可调 `20–33℃`）、`static`、`off` 三种模式。
- **物理高温断开兜底（Fork 新增）**：可选 `hot_cutoff`（`off` 或 `42–55℃`），达到阈值后主动恢复真实温控，降温 `3℃` 滞回后自动重接。
- **快充路径解锁与核温伪装**：支持开启核温（`core` / `noncore` `20–100℃`）、电池温度伪装（`batt` `20–45℃`）及快充电流限制解除（`unlock`）。
- **高刷刷新率锁定**：支持全局锁定 `90–185Hz`（`soft` / `hard` 模式）与后台掉刷守护（`hzguard`）。
- **WebUI 与命令行双控制**：支持 KernelSU / APatch WebUI 可视化面板及 `action.sh` CLI。
- **无弹窗静默安装与稳健状态恢复**：移除安装期额外弹窗；亮/灭屏写失败（`scr.fail`）仅在拔线时清理并保留已校准的 `fcc.norm`。

## 快速上手

1. 前往 [Releases](https://github.com/dkgks/QuickCharge/releases/latest) 下载 `QuickCharge-v3.1.17.zip`。
2. 在 Magisk / KernelSU / APatch 中刷入模块并重启。
3. 通过模块 **WebUI** 或终端执行控制脚本即可调整参数。

### 默认配置

| 配置项 | 默认值 | 可调范围 / 说明 |
| --- | --- | --- |
| 壳温模式 (`temp_mode`) | `charge` | `off` / `static` / `charge` |
| 基准壳温 (`shell_temp`) | `30℃` | `20–33℃`（外加动态曲线偏移 `+12℃`） |
| 物理高温断开 (`hot_cutoff`) | `off` | `off` / `42–55℃`（降温 `3℃` 自动恢复） |
| 电池/核温伪装 | `off` | 电池 `20–45℃`，核心/非核心 `20–100℃` |
| 快充解锁 (`chg_unlock`) | `0`（关） | `on` / `off` |
| 轮询周期 (`tick`) | `15s` | 守护进程刷新间隔 |

## 常用 CLI 命令

可在 root 终端调用模块目录下的 `action.sh`：

```sh
# 温控模式与温度设置
sh action.sh temp charge          # 启用充电动态温控（可选传入目标温度）
sh action.sh base 29              # 设置基准壳温 (20-33)
sh action.sh cutoff 48            # 设置物理高温断开阈值 (42-55 或 off)
sh action.sh batt 32              # 设置电池伪装温度 (20-45 或 off)
sh action.sh core 55              # 设置核心温控伪装 (20-100 或 off)
sh action.sh noncore 55           # 设置非核心温控伪装 (20-100 或 off)
sh action.sh unlock on            # 开启快充电流解锁 (on / off)

# 刷新率与显示策略
sh action.sh hz 120 soft          # 锁定刷新率 (90-185 [soft|hard] 或 off)
sh action.sh hzguard on           # 刷新率守护开关 (on / off)
sh action.sh overrides on         # 覆盖层开关 (on / off)

# 状态排查与维护
sh action.sh status               # 查看运行状态与当前伪装参数
sh action.sh chg                  # 查看充电器与电池实时状态
sh action.sh tiers                # 查看温控档位信息
sh action.sh zones                # 查看已识别的 thermal_zone
sh action.sh logs daemon 50       # 查看日志 (i|w|e|boot|daemon)
sh action.sh level 1              # 设置日志级别 (0-4)
sh action.sh rebuild              # 重建温控节点映射
sh action.sh restart              # 重启守护进程
sh action.sh reset                # 重置全部配置为默认值
```

## 分支与构建

- 本分支包含基于 GitHub Actions 的单元测试（`chg-unit`、`cool-unit`、`mount-unit`、`zone-rank`、`state-unit`）与自动打包 Release 流程。
- 上游致谢：[XiaohaoQvQ/QuickCharge](https://github.com/XiaohaoQvQ/QuickCharge)
