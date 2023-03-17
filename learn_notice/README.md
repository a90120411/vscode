### VSCode代码研究
---
#### 本地编译流程

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
#### Development container 基于容器的开发--暂未使用，后续可以在windows平台实验这种方式
  * 使用Docker
  * 使用Github CodeSpaces
---
* 目前并未使用最新版的electron，每次更新electron的版本，对团队来说是一个比较严谨的流程，目前使用的版本是：electron@19.1.9
---
* 创建了一个demo工程，使用npm安装同样版本的electron，并与vscode的node_modules文件夹中的electron进行对比，是完全一致的，说明vscode并没有定制electron的公开代码。
---
* npm_modules中前面带@的包名称，表示包别名。@ 符号可以让你在 npm 中安装一个包的时候，给它起一个自己喜欢的名字。比如，你可以这样写：npm install @my-react@npm:react。这样就会安装 react 包，并且把它叫做 @my-react。这样你就可以在你的代码中用 @my-react 来导入 react 包，而不用写 react。
---
#### Extensions 扩展 待研究
* vscode 开源版本不提供 Visual Studio Marketplace。
* 需要研究一下如何自己来实现插件的管理，插件的加载机制，版本管理等。是否可以参考油猴脚本管理器？
* 插件打包后的`.VSIX格式`需要进一步研究
---
#### 测试相关 待研究
* Automated Testing 自动化测试
* Unit Testing 单元测试
* Linting（eslint）
---

