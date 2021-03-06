# IPC 简介

在学习 Cocos Creator 的插件编写之前，我们先要理解 Cocos Creator 插件开发中的重要一环，进程间通信（IPC）。Cocos Creator 的编辑器是基于 GitHub 开发的 [Electron](https://github.com/atom/electron) 内核。Electron 是一个集成了 Node.js 和 Chromimu 的跨平台开发框架。

在 Electron 的架构中，一份应用程序由主进程和渲染进程组成，其主进程负责管理平台相关的调度，如窗口的开启关闭，菜单选项，基础对话框等等。而每一个新开启的窗口就是一个独立的渲染进程。在 Electron 中，每个进程独立享有自己的 JavaScript 内容，彼此之间无法直接访问。当我们需要在进程之间传递数据时，就需要使用进程间通信（IPC）。 你可以通过阅读 [Electron's introduction document](https://github.com/atom/electron/blob/master/docs/tutorial/quick-start.md) 更深入的理解 Electron 中的主进程和渲染进程的关系。简单点说，Electron 的主进程相当于一个 Node.js 服务端程序，而每一个窗口（渲染进程）则相当于一份客户端界面程序。

Cocos Creator 沿用了 Electron 的主进程和渲染进程的设计结构，在 Creator 启动前，我们将许多服务如：资源数据库，脚本编译器，预览服务器，打包工具等在主进程中开启，之后我们在主窗口也就是渲染进程中启动编辑器的界面操作部分。当界面操作需要使用主进程的模块时，我们就会进行进程间的通信（IPC）来完成请求。

## 进程间通信（IPC）

前面我们已经说到了两个进程之间的 JavaScript 内容是相互独立的，必须靠进程间通信的方式来交换数据。进程间通信实际上就是在一个进程中发消息，然后在另外一个进程中监听消息的过程。 Electron 为我们提供了进程间通信对应的模块 [ipcMain ](https://github.com/atom/electron/blob/master/docs/api/ipc-main.md) 和 [ipcRenderer](https://github.com/atom/electron/blob/master/docs/api/ipc-renderer.md) 来帮助我们完成这个任务。由于这两个模块仅完成了非常基本的通信功能，并不能满足编辑器，插件面板与主进程之间的通信需求，所以 Cocos Creator 在这之上又进行了封装，扩展了进程间消息收发的方法，方便插件开发者和编辑器开发者制作更多复杂情景。

## IPC 消息命名规范

IPC 的消息名就是一个字符串，对于消息的发送者，可以非常随意地进行消息的命名。但是我们希望开发人员在 Cocos Creator 中定制消息时遵守一定的规范。 消息的命名规范为：

```javascript
'module-name:action-name'
// or
'package-name:action-name'
```

## 扩展包中的进程关系

Cocos Creator 的扩展包也分为主进程和渲染进程两个部分。我们在上一篇文章中已经介绍了扩展包的入口程序，它是一份跑在主进程的脚本程序。倘若我们在入口程序中新开了一份窗口，则这份窗口将会运行在渲染进程中。
