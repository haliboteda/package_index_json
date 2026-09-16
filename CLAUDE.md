# 开工入口 —— 板卡包索引

**这份文件是给 AI 会话看的。**

这个仓库只有一个文件：`package_openplc_alp_index.json`。Arduino IDE 的「其他开发板管理器地址」指向它的 raw URL，用户点「安装 OpenPLC_Alpha」时，IDE 读的就是这份索引。

> **产品文档在 `OpenPLC_Docs`**（`$PROD`）—— 全部文档和待决的问题，入口它的 `README.md`（本机位置见 `DOCS_REPO`）。

## 它在整条链路上的位置

```
package_openplc_alp_index.json          ← 本仓库
        │ platforms[].url
        ▼
github.com/haliboteda/open_plc_arduino/archive/refs/tags/v<版本>.tar.gz
        │ IDE 解压后
        ▼
$A15/packages/OpenPLC_Alpha/hardware/stm32/<版本>/      ← 文档里的 $CORE_LIVE
```

`tools[]` 里另外挂着 `xpack-arm-none-eabi-gcc`、`xpack-openocd`、`CMSIS`，以及**随包分发的 `STM32Tools`（里面是 `IAPTool`）**。

⚠️ **`STM32Tools` 的版本号和板卡包的版本号是两个独立的号**，不要以为它们该一致。

## 只在发板卡包时才动它

平时不碰。要加一个新版本时，三件事缺一不可：

1. `open_plc_arduino` 上打好 tag，**GitHub 的 tarball 必须真的能下下来**
2. 往 `platforms[]` 里加一条，`url` / `archiveFileName` / `checksum` / `size` 都要对得上那个 tarball
3. **`checksum` 是 `SHA-256:<hex>`，算错了 IDE 只会说"下载失败"**，不会告诉你是校验不过

改完在**一台没装过这个板卡包的机器**上走一遍安装，才算验证过。

## ⚠️ 共享文档不在这个仓库里

| 找什么 | 去哪 |
|---|---|
| 六个仓库怎么分工、需求做到哪一步、跨仓镜像清单、写文档的约定 | `$PROD`，入口 `README.md` |
| 板卡包本身（`$CORE_LIVE` 与 `$CORE_REPO` 的关系、怎么编译） | `open_plc_arduino` 根目录的 `CLAUDE.md` |
| 引脚怎么接 | `Hardware` 仓库的原理图 / netlist，结论记在 `$PROD/docs/hardware/HARDWARE-FACTS.md` |

**这个仓库只管这一份索引 JSON，不存任何产品级事实。**

## 语言

本文件用中文。JSON 里的字段保持原样。
