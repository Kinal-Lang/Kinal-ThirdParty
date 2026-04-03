# Kinal - CivetWeb 依赖仓库

## [English version](README.md)

# CivetWeb 依赖布局

这个目录用于保存 Kinal `IO.Web` 所依赖的 CivetWeb 源码和头文件。

它更适合保存：

- `include/` 中的固定公共头文件
- `src/` 中的固定版本源码
- `manifests/` 中的小型元数据文件

它不适合长期把按目标平台生成的对象文件或机器本地构建产物当成稳定仓库结构的一部分。

## 目录结构

- `include/`
  - Kinal runtime 和原生桥接使用的公共 CivetWeb 头文件
- `src/`
  - 固定版本的上游 CivetWeb 源码树
- `manifests/`
  - 版本锁定、说明，以及未来的原生构建元数据

## Kinal 如何使用这里

主仓库会把本目录当成同级依赖仓库来寻找：

- `../Kinal-ThirdParty/civetweb`

然后从这里读取：

- `include/` 下的公共头文件
- `src/` 下的原生重建输入
- `manifests/` 下的小型元数据和版本说明

## 构建意图

Kinal 更适合在需要时从源码构建 CivetWeb 原生产物，而不是把长期存在的预编译输出保留在这个仓库里。

这样可以避免把下面这些东西混在一起：

- 上游源码
- 构建生成物
- 机器本地产物

## 说明

- `VERSION.txt` 是上游版本或提交的固定参考
- `LICENSE.md` 和 `SECURITY.md` 作为第三方依赖元数据继续保留
- 如果以后需要构建缓存，更适合放在被忽略的工作目录里，而不是作为已提交结构长期保留
