# ygopro-ftd

游戏王各端「先攻抽卡（FTD，First Turn Draw）」补丁方案与维护手册。

## 这是什么

FTD 补丁让游戏王对战各端支持「**先攻第一回合也抽卡**」（起手 6 张，而非标准 OCG 规则的 5 张）。本质是给 ocgcore 引擎加一个 `0x200` 选项位，并让服务端 / 客户端各端识别。

## 文件说明

| 文件 | 说明 |
|---|---|
| `FTD先攻抽卡-全端修改与维护手册.md` | **主文档**（单文件自足，含全部补丁内容和完整 build.yml） |
| `ocgcore-ftd-0x200.patch` | ocgcore 通用三处补丁（所有端共用） |
| `srvpro2-ftd-0x200.patch` | srvpro2 的 `calculate-duel-options.ts` 补丁 |
| `srvpro-ocgcore-ftd-0x200.patch` | srvpro 的 ocgcore 三处补丁 |
| `srvpro-ygopro-ftd-0x200.patch` | srvpro 的 ygopro 主程序补丁 |
| `ygopro-build.yml` | ygopro 客户端改好的完整 build.yml |

## 各端支持状态

| 端 | 状态 |
|---|---|
| srvpro2 服务器 | ✅ 已测试可用 |
| ygopro / ygopro2 / MDPro3（Windows 客户端） | ✅ 已测试可用 |
| srvpro 服务器 | ⚠️ 有方案，**未测试** |
| 安卓版（YGOMobile / MDPro3 安卓） | ⚠️ 有方案，**未测试** |

## 快速开始

1. 打开主文档 `FTD先攻抽卡-全端修改与维护手册.md`
2. 按要改的端跳到对应章节：
   - **srvpro2 服务器** → 第三章
   - **srvpro 服务器** → 第四章
   - **客户端**（MDPro3 / ygopro / ygopro2）→ 第五章
   - **安卓版** → 5.5 节
3. 补丁文件和 build.yml 都已放在本仓库，可直接 `git apply` 使用

## 关键提醒（接手者必读）

- **服务端和客户端的 ocgcore 必须打同一份补丁**，否则录像重放对不上（客户端报错/数据错乱）
- **两个服务端的环境变量不同**：srvpro2 用 `FIRST_TURN_DRAW=1`，srvpro 用 `YGO_FIRST_TURN_DRAW=1`（多了 `YGO_` 前缀）
- **srvpro2 的 wasm 必须用 emscripten 3.1.6 编译**，用其他版本会 ABI 不匹配、对局崩溃

## 上游更新后的维护

上游项目（ocgcore / ygopro / 客户端）更新后，补丁可能失效。维护方法见主文档**第六章**（含重新定位补丁的 grep 命令）。

## 说明

本仓库内容由 AI 协助生成，其中服务端 srvpro2 与 Windows 客户端（ygopro / ygopro2 / MDPro3）已经过实测，其余端为源码核验后的方案、待实测。
