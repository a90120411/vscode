## Theia 调研
---
### 架构
Theia 旨在作为本地桌面应用程序以及在浏览器和远程服务器的上下文中工作。为了使用单一来源支持这两种情况，**Theia 在两个独立的进程中运行**。这些进程分别称为前端和后端，它们通过基于 `WebSocket` 的 `JSON-RPC` 消息或基于 `HTTP` 的 `REST API` 进行通信。在 Electron 的情况下，后端和前端都在本地运行，而在远程上下文中，后端将在远程主机上运行。

前端和后端进程都有它们的依赖项注入 (DI) 容器（见下文），扩展可以为之做出贡献。


* Theia 没有使用 VSCode 的 依赖注入实现？
  用了一个第三方的 `InversifyJS` 框架（依赖注入）。
---
**Theia 有三种插件实现方式：**

* VSCode Extensions 与 VSCode相同（可能版本滞后），可以复用 VSCode的插件；
* Theia Extensions 在编译时安装的，属于内部扩展，访问权限较高。
* Theia Plugins 借鉴VSCodeExtension的，换了个名字。只能适用于Theia。
---

