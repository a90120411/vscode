## VSCode代码研究
---
### 本地编译流程

参考资料：https://github.com/microsoft/vscode/wiki/How-to-Contribute

* **前置条件**
  * git
  * 安装 Yarn1 version >=1.10.1 and <2
  * Python 环境（node-gyp 需要）
  * C/C++编译器工具链
    * Mac: xcode-select --install

* **下载源码**
  * git clone

* **构建**
  ```
  cd vscode
  yarn
  ```
增量构建器将执行初始完整构建，并在初始构建完成后显示一条消息，其中包含短语“Finished compilation”。构建器将监视文件更改并逐步编译这些更改，为您提供快速、迭代的编码体验。

* 增量编译，在开发时需要一直运行，会持续增量编译。
  ```
  //将在单个终端中同时运行核心监视任务和监视扩展任务
  yarn watch
  ```

* **运行**
  运行Desktop桌面端
**Mac:**
	```
  	./scripts/code.sh
	./scripts/code-cli.sh # for running CLI commands (eg --version)
	```
  运行web端vscode
  除了 `yarn watch` 之外，还需运行 `yarn watch-web` 来为内置扩展构建网络位。
**Mac:**
  构建服务器端
  ```
  ./scripts/code-web.sh
  ```
  运行web端
  ```
  ./scripts/code-server.sh --launch
  ```
---
### Development container 基于容器的开发--暂未使用，后续可以在windows平台实验这种方式
  * 使用Docker
  * 使用Github CodeSpaces

---
### 零碎的知识点

* 目前并未使用最新版的electron，每次更新electron的版本，对团队来说是一个比较严谨的流程，目前使用的版本是：electron@19.1.9
---
* 创建了一个demo工程，使用npm安装同样版本的electron，并与vscode的node_modules文件夹中的electron进行对比，是完全一致的，说明vscode并没有定制electron的公开代码。
---
* npm_modules中前面带@的包名称，表示包别名。@ 符号可以让你在 npm 中安装一个包的时候，给它起一个自己喜欢的名字。比如，你可以这样写：npm install @my-react@npm:react。这样就会安装 react 包，并且把它叫做 @my-react。这样你就可以在你的代码中用 @my-react 来导入 react 包，而不用写 react。
---
* 在软件中，`contrib module` 表示贡献模块。它是由社区成员开发和分享的附加软件模块，通常包含一些实用工具、库、插件或算法等，可以用于增强软件的功能，提升用户体验。`contrib module` 可以是最新的开发版本，也可以是旧的，即已过时的版本。通常情况下，贡献模块都是可选的，用户可以根据自己的需要自由决定是否使用。`contrib module` 对于开源软件的发展和推广具有重要的作用。

---
### Extensions 扩展 待研究
* **Visual Studio Code 由分层和模块化的 core （目录`src/vs` ）组成，可以使用扩展进行扩展。扩展在一个单独的进程中运行，称为 `extension host`. 扩展是通过使用扩展 API 实现的。可以在 `extensions` 文件夹中找到内置扩展。**
* vscode 开源版本不提供 Visual Studio Marketplace。
* 需要研究一下如何自己来实现插件的管理，插件的加载机制，版本管理等。是否可以参考油猴脚本管理器？
* 插件打包后的`.VSIX格式`需要进一步研究
* https://code.visualstudio.com/api/extension-capabilities/overview
* https://code.visualstudio.com/api
* https://github.com/microsoft/vscode/wiki/Extension-API-guidelines
* **开源的市场** [Open VSX Registry](https://open-vsx.org/)
 VS Codium 配置为使用其 Open VSX Registry。该注册表是在 Eclipse Open VSX 项目下开发和维护的。它是供应商中立的，因此它可以与任何技术或工具一起使用。例如：VSCodium、Eclipse Theia、Eclipse Che、Gitpod、Coder 和 SAP Business Application Studio。
 这两个市场都提供 CLI 工具来发布和管理您的扩展，vsce 用于 VS Code，ovsx 用于 Open VSX。它们非常相似。

---
### 测试相关 待研究
* Automated Testing 自动化测试
* Unit Testing 单元测试
* Linting（eslint）
* https://github.com/microsoft/vscode/wiki/Dealing-with-Test-Flakiness
* https://github.com/microsoft/vscode/wiki/Smoke-Test
* https://github.com/microsoft/vscode/wiki/Test---Smoke-Test-Template
---

### Packaging 包装
VS Code 可以为以下平台打包：
* win32-ia32
* win32-x64
* darwin-x64
* darwin-arm64
* linux-ia32
* linux-x64
* linux-arm

这些 gulp 任务可用：
为 [platform] 构建打包版本。
* `vscode-[platform]`: Builds a packaged version for [platform].
* `vscode-[platform]-min`: Builds a packaged and minified version for [platform].

提示：通过 yarn 运行 gulp 以避免潜在的内存不足问题，例如 yarn gulp vscode-linux-x64

---
### 本地化
https://github.com/microsoft/vscode-loc

---
### 更新机制？
https://github.com/microsoft/vscode/wiki/Roadmap#install--update

* VSCodium 的更新机制
https://github.com/VSCodium/update-api

* Theia 的更新机制
  https://www.npmjs.com/package/electron-updater

---
### 编码规范
https://github.com/microsoft/vscode/wiki/Coding-Guidelines

----
### 完成的定义
- [ ] 已创建测试计划项
- [ ] 可使用键盘
- [ ] 屏幕阅读器可访问
- [ ] 适用于不同的主题，包括高对比度主题
- [ ] 遥测事件到位
- [ ] 发行说明已更新

----
### 文件搜索
https://github.com/BurntSushi/ripgrep

----
### VSCode API
https://github.com/microsoft/vscode/wiki/Extension-API-process

----
### 问题自动分类器
https://github.com/microsoft/vscode/wiki/Automated-Issue-Triaging

是否可以基于这个做文件自动分类？

-----
### 设计原则
https://github.com/microsoft/vscode/wiki/%5BWIP%5D-Design-Principles
https://github.com/microsoft/vscode/wiki/%5BWIP%5D-Design-Checklist

----
### Model-View-ViewModel in Monaco
虽然我们在开发的时候并没有采用任何框架，但是Monaco的设计最终变成了MVVM（Model-View-ViewModel）

* View: 用户界面。它向用户显示信息（文本、光标、选择等）并处理用户交互。这里的 View 元素实际上是 HTML DOM 节点。

* Model: 提供业务实体的独立于视图的表示。在摩纳哥，它通常代表您正在编辑的文件。

* ViewModel: View和Model之间的桥梁。它从模型中检索数据并将其处理为视图所需的格式。一个有助于理解 ViewModel 的好例子是 \t 在 Model 中始终是单个字符，而它在 ViewModel 中占用多个列并且由选项 tabSize 确定。

----
* `vscode/src/vs/editor/browser/viewParts` 中定义了不和任何业务功能绑定的原始组件，基于这些原始组件进行组装，来开发复杂的组件。这些组件放在`/vs/editor/contrib/`内，被视为1级（最顶级）扩展来使用。
* View 不能直接访问 Model，而是通过访问 ViewModel 获取数据和事件响应，ViewModel 用来解耦。
* ViewModel 包含对模型的引用、视图的状态、事件处理程序和分发器，以及可以将模型数据转换为视图信息（反之亦然）的转换器。

----
### VSC和开源版的Code-OSS的不同点

* **图标、产品名称（例如“Microsoft Visual Studio Code”）、文档**
* **Visual Studio Marketplace 插件市场**
Visual Studio Marketplace 是我们为 Visual Studio 系列产品（Visual Studio for Windows 和 Mac、Visual Studio Code 和 Azure DevOps，以前称为 Visual Studio Team Services）的用户提供的服务。 Marketplace 不仅提供发现和托管服务，还提供评级、评论、问答、发布者验证、病毒扫描、冲突解决服务、Azure DevOps 扩展的支付服务，以及对发布者的支持。 Marketplace 不是旨在支持任何分发或分发子集的通用商店。对 Marketplace 的访问受 Marketplace 使用条款的约束。
* **Extension Recomendations 扩展建议**
  我们保留了一份精选的“重要”和“一般”扩展建议列表，这些建议随后从 Marketplace 安装，因此我们只将这些包含在发行版中。
* **Remote Development 远程开发**
  部分远程开发扩展用于在专有许可下运行的开发人员服务。虽然这些扩展不需要这些服务来工作，但有足够的代码重用，这些扩展也有专有许可。虽然大部分代码位于扩展和 Code - OSS 存储库中，但 Visual Studio Code 分发版中有一些小的更改。
* **启用专有调试适配器，Visual Studio 代码服务器**
  某些 Microsoft 扩展（例如 C#/.NET 调试器）和 Visual Studio Code Server 是根据限制其在 Visual Studio 系列产品（Visual Studio、Visual Studio Code 或 Visual Studio for Mac）中使用的许可证分发的。
* **Extensions Using Proposed APIs 使用建议的 API 的扩展**
* **Telemetry, Surveys, Crash Reporting 遥测、调查、事故报告**
  Microsoft 收集匿名使用情况统计信息、调查数据和故障转储以帮助提高产品质量。不会收集任何个人身份信息。我们收集的任何数据（例如故障转储）都会按照 GDPR 指南（常见问题解答）进行保存。您可以禁用遥测收集，请参阅我们的常见问题解答了解更多详情。
* **Update Services 更新服务**
  Visual Studio Code 定期检查我们托管的服务，看看是否有更新要安装，或者在极少数情况下回滚。

----
### Eclipse 的 Theia IDE

https://theia-ide.org/
https://github.com/eclipse-theia/theia
基于 VSCode 的代码开发的。

**Flexible Layout 灵活布局，可以任意调整布局位置**
Theia's shell is composed of lightweight modular widgets that provide a solid foundation for draggable dock layouts.

* 基于 Theia 开发的低代码 APP 生成工具
https://smartface.io/
https://github.com/smartface/smartface-native

----
### Atom IDE

----

* 我发现vscode没有用electron的ffmpeg.dll，而是用了一个体积更小的ffmpeg.dll（来自csdn上的文章所述，需要调研）

---
### 项目结构

* Visual Studio Code 由分层和模块化的 core （目录`src/vs` ）组成，可以使用扩展进行扩展。扩展在一个单独的进程中运行，称为 `extension host`. 扩展是通过使用扩展 API 实现的。可以在 `extensions` 文件夹中找到内置扩展。

**项目层级 Layers**

`core` 分为以下几层：

* `base` ：提供可在任何其他层中使用的通用实用程序和用户界面构建块。（基础通用UI组件和工具类）
* `platform` ：定义服务注入支持和跨层共享的 VS Code 基础服务，例如 `workbench` 和 `code` 。不应包含 `editor` 或 `workbench` 特定服务或代码。
* `editor` ：“Monaco” 编辑器可作为单独的可下载组件使用。
* `workbench` ：承载“Monaco”编辑器、笔记本和自定义编辑器，并为资源管理器、状态栏或菜单栏等面板提供框架，利用 Electron 实现 VSCode 桌面端，使用 webAPI 来实现 VSCode Web端。
* `code` ：桌面应用程序的入口点，它将所有内容缝合在一起，例如包括 Electron main file、shared process 共享进程和 CLI。
* `server` ：用于远程开发的服务器应用程序的入口点。

![structure](https://github.com/microsoft/vscode/wiki/images/organization/layers2.png)

**目标环境(运行平台)Target Environments**

VS Code 的 core 完全用 TypeScript 实现。在每一层内，代码由目标运行时环境组织。这确保仅使用特定于运行时的 API。在代码中我们区分了以下目标环境(运行平台):

* `common` : 只使用标准 JavaScript API 并可以在所有环境下运行的源代码
* `browser` : 依赖 [Web API](https://developer.mozilla.org/en-US/docs/Web/API) 的源代码，例如:DOM
  * 可以调用 `common` 中的代码
* `node` : 依赖 [Node.JS API](https://nodejs.org/) 的源代码
* `electron-sandbox` : 依赖 `browser` API 的源代码，例如访问 DOM 和 一小部分 API 用于与 Electron 主进程通信（任何从 src/vs/base/parts/sandbox/electron-sandbox/globals.ts 公开的内容）
  * may use code from: common, browser, electron-sandbox
* [ ⚠️ 已弃用] electron-browser ：Source code that requires the [Electron renderer-process](https://github.com/atom/electron/tree/master/docs#modules-for-the-renderer-process-web-page) APIs
  需要 Electron 渲染器进程 API 的源代码
  * may use code from: common, browser, node

* electron-main: Source code that requires the [Electron main-process](https://github.com/atom/electron/tree/master/docs#modules-for-the-main-process) APIs
  需要 Electron 主进程 API 的源代码
  * may use code from: common, node

![target](https://github.com/microsoft/vscode/wiki/images/organization/environments.png)

---
### 依赖注入

**消费服务 Consuming a service**

The code is organised around services of which most are defined in the platform layer. Services get to its clients via constructor injection.
**代码围绕服务构成**，其中大部分定义在 `platform` 层。服务通过 `constructor injection` 到达其客户。

A service definition is two parts: (1) the interface of a service, and (2) a service identifier - the latter is required because TypeScript doesn't use nominal but structural typing. A service identifier is a decoration (as proposed for ES7) and should have the same name as the service interface.
服务定义由两部分组成：(1) 服务接口 (2) 服务标识符——后者是必需的，因为 TypeScript 不使用名义类型而是结构类型。服务标识符是一种装饰（如 ES7 所建议的那样）并且应该与服务接口同名。

通过向构造函数参数添加相应的修饰来声明服务依赖性。在下面的代码片段中， @IModelService 是服务标识符装饰， IModelService 是此参数的（可选）类型注释。

```ts
class Client {
  constructor(
    @IModelService modelService: IModelService
  ) {
    // use services
  }
}
```
Use the instantiation service to create instances for service consumers, like so instantiationService.createInstance(Client). Usually, this is done for you when being registered as a contribution, like a Viewlet or Language.
使用实例化服务为服务消费者创建实例，例如 `instantiationService.createInstance(Client)` 。通常，这是在注册为贡献时为您完成的，例如 Viewlet 或语言。

---

**Providing a service 提供服务**

The best way to provide a service to others or to your own components is the registerSingleton-function. It takes a service identifier and a service constructor function.
向他人或您自己的组件提供服务的最佳方式是 `registerSingleton` 函数。它需要一个服务标识符和一个服务构造函数。

```ts
registerSingleton(
  ISymbolNavigationService, // identifier
  SymbolNavigationService,  // ctor of an implementation
  InstantiationType.Delayed // delay instantiation of this service until is actually needed
);
```
Add this call into a module-scope so that it is executed during startup. The workbench will then know this service and be able to pass it onto consumers.
将此调用添加到模块范围内，以便它在启动期间执行。工作台然后将知道此服务并能够将其传递给消费者。

------
### VSCode 编辑器部分的源码结构 VSCode Editor source organisation

* `vs/editor` 文件夹不应有任何 `node` 或 `electron-*` 依赖项。

* `vs/editor/common` and `vs/editor/browser` - the code editor core (critical code without which an editor does not make sense).
`vs/editor/common` 和 `vs/editor/browser` 中包含
代码编辑器核心（关键代码，没有它编辑器就没有意义）

* `vs/editor/contrib` - 在 VS Code 和独立编辑器(Monaco)中提供的贡献模块。按照惯例，它们依赖于 `browser` ，并且可以在没有它们的情况下制作编辑器，这会导致引入的功能被删除。

* `vs/editor/standalone` - 仅随独立编辑器一起提供的代码。其它任何模块都不应该建立对 `vs/editor/standalone` 的依赖。

* `vs/workbench/contrib/codeEditor` - 来自于 VSCode 社区的编辑器部分的贡献模块 `contrib modules`。

---
### VSCode Workbench 部分的源码结构 VSCode Workbench source organisation

The VS Code workbench (`vs/workbench`) is composed of many things to provide a rich development experience. Examples include full text search, integrated git and debug. At its core, the workbench does not have direct dependencies to all these contributions. Instead, we use an internal (as opposed to real extension API) mechanism to contribute these contributions to the workbench.
VS Code 工作台 ( `vs/workbench` ) 由许多东西组成，以提供丰富的开发体验。例如：全文搜索、集成 git 和调试等。工作台的核心并不直接依赖于所有这些组件。相反，我们使用一种内部机制（而非真正的扩展 API）来向工作台注入这些组件。换句话说，这些组件通过内部机制被注入到工作台中，以提供相应的功能。

* `vs/workbench/{common|browser|electron-sandbox}`: workbench core that is as minimal as possible.
  尽可能精简的工作台核心部分

* `vs/workbench/api`: the provider of the vscode.d.ts API (both extension host and workbench implementations)
  vscode.d.ts API 的提供者（扩展主机和工作台实现）

* `vs/workbench/services`: workbench core services (should NOT include services that are only used in `vs/workbench/contrib`)
  工作台核心服务（不应包括仅在 `vs/workbench/contrib` 中使用的服务）

* `vs/workbench/contrib`: workbench contributions (this is where most of your code should live, see below)
  工作台贡献（这是你的大部分代码应该存在的地方，见下文）

所有给工作台的贡献都应存放在 `vs/workbench/contrib` 文件夹中，并遵循以下规则：

* there cannot be any dependency from outside `vs/workbench/contrib` into `vs/workbench/contrib`
  不能有任何从 `vs/workbench/contrib` 外部到 `vs/workbench/contrib` 的依赖（仅限包内引用）

* every contribution should have a single `.contribution.ts` file (e.g. `vs/workbench/contrib/search/browser/search.contribution.ts`) to be added to the main entry points for the product (see last paragraph for details)
  每个贡献都应该有一个单独的 `.contribution.ts` 文件（例如 `vs/workbench/contrib/search/browser/search.contribution.ts` ）添加到产品的主要入口点（详见最后一段）

  * if you add a new service which is only used from one contrib and not other components or workbench core, it is recommended to register the service from the contrib entrypoint file
    如果您添加的新服务仅用于一个 contrib 而不是其他组件或工作台核心，建议从 contrib 入口点文件注册该服务

* every contribution should expose its internal API from a single file (e.g. `vs/workbench/contrib/search/common/search.ts`)
  每个贡献都应该从单个文件中公开其内部 API（例如 `vs/workbench/contrib/search/common/search.ts` ）

* a contribution is allowed to depend on the internal API of another contribution (e.g. the git contribution may depend on `vs/workbench/contrib/search/common/search.ts`)
  允许一个贡献依赖于另一个贡献的内部 API（例如 git 贡献可能依赖于 `vs/workbench/contrib/search/common/search.ts` ）

* a contribution should never reach into the internals of another contribution (internal is anything inside a contribution that is not in the single common API file)
  贡献永远不应该进入另一个贡献的内部（不应该调用另一个贡献内的非公开API方法）

* think twice before letting a contribution depend on another contribution: is that really needed and does it make sense? Can the dependency be avoided by using the workbench extensibility story maybe?
  在让一个贡献依赖于另一个贡献之前要三思：这真的需要并且有意义吗？是否可以通过使用工作台可扩展性故事来避免依赖性？
  > 在此处 workbench extensibility story 指的是 Visual Studio Code 工作台提供的一种机制，用于允许开发人员通过扩展来改进工作台。这个机制提供了一些 API（如 Extension API、Language Server Protocol 等），用于编写扩展和定制化设置。因此，当在贡献之间决定是否需要依赖另一个贡献时，需要三思而后行，考虑是否可以通过使用工作台扩展机制避免这种依赖关系。因此在语句中，作者建议在允许贡献之间相互依赖之前，需要认真思考这是否真的需要，是否有意义，是否可以通过使用工作台扩展机制来避免依赖关系。

---
### 桌面端 和 Web端 VSCode for Desktop / VSCode for Web

We ship both to desktop via Electron and to the Web with the goal to share as much code as possible in both environments. Writing code that only runs in the one environment should be the exception, think twice before going down that path. Ideally the same code can run in both environments.
我们通过 Electron 将应用程序发到桌面，同时也发布到Web，目标是在两个环境中尽可能共享代码。编写仅运行在一个环境中的代码应该是例外情况，在采取这种方法之前请三思。理想情况下，相同的代码可以在两个环境中运行。

To distinguish the environments in the product we build, there are entry files that define all the dependencies depending on the environment:
为了区分我们构建的产品中的环境，使用入口文件定义了所有依赖于环境的依赖项：

* `src/vs/workbench/workbench.sandbox.main.ts`: for desktop only dependencies
  仅适用于桌面依赖项
* `src/vs/workbench/workbench.web.main.ts`: for web only dependencies
  仅用于 web 依赖项

Both depend on our core entry file:
两者都取决于我们的核心入口文件：

* `src/vs/workbench/workbench.common.main.ts`: for shared dependencies
  用于共享依赖

Here are some rules that apply:
以下是一些适用的规则：

* 共享的代码应该进入 `workbench.common.main.ts`

* 仅限网络的代码应该进入 `workbench.web.main.ts`

* 只有桌面的代码应该进入 `workbench.desktop.main.ts`

Be careful when introducing a service only for the desktop and not for the web: code that runs in the web that requires the service will fail to execute if you do not provide a related service for web. It is fine to ship two different implementations of a service when you use different strategies depending on the environment.
只为桌面而不是 Web 引入服务时要小心：如果您不为 Web 提供相关服务，则在需要该服务的 Web 中运行的代码将无法执行。当您根据环境使用不同的策略时，可以发布服务的两种不同实现。

Note: Only code that is referenced from the main entry files is loaded into the product. If you have a file that is otherwise not referenced in your code, make sure to add the import to your `.contribution.ts` file.
注意：只有从主条目文件中引用的代码才会加载到产品中。如果您有一个文件未在您的代码中引用，请确保将导入添加到您的 `.contribution.ts` 文件中。

---
### 需要详细了解的内容

* A service definition is two parts: (1) the interface of a service, and (2) a service identifier - the latter is required because TypeScript doesn't use nominal but structural typing. A service identifier is a decoration (as proposed for ES7) and should have the same name as the service interface.
服务定义由两部分组成：(1) 服务接口 (2) 服务标识符——后者是必需的，因为 TypeScript 不使用名义类型而是结构类型。服务标识符是一种装饰（如 ES7 所建议的那样）并且应该与服务接口同名。
**这里所述的名义类型和结构类型是什么？**

* Add this call into a module-scope so that it is executed during startup. The workbench will then know this service and be able to pass it onto consumers.
将此调用添加到模块范围内，以便它在启动期间执行。工作台然后将知道此服务并能够将其传递给消费者。
**这里的模块范围是指？**

* 使用 Theia 的 Task 任务来完成后台任务？
  https://theia-ide.org/docs/tasks/

*
