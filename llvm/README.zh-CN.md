# Kinal - LLVM 依赖仓库

## [English version](README.md)

# LLVM 依赖布局

这个目录存放 Kinal 使用的 LLVM 依赖。

之所以把它放在 `Kinal-ThirdParty`，而不是主仓库 `Kinal`，主要是因为：

- 解压后的 LLVM 源码树非常大
- LLVM 预编译包体积大，不适合进入主仓库历史
- 如果把完整 LLVM 混进语言仓库，代码搜索和仓库索引体验都会明显变差

## 目录结构

- `src/`
  - LLVM 源码快照或解压后的源码树
  - 当前默认结构：`src/llvm-project/...`
- `manifests/`
  - 版本固定、下载元数据和自举说明

## Kinal 如何使用这里

主仓库会把本目录当成同级仓库来寻找：

- `../Kinal-ThirdParty/llvm`

然后从这里读取：

- `src/` 下的源码树
- `manifests/` 下的元数据和版本信息

## 自举入口

请使用主仓库中的辅助脚本：

```powershell
python ..\Kinal\infra\toolchains\setup_llvm.py --help
```

常用示例：

```powershell
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-prebuilt
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-src
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-prebuilt --fetch-src
```