---
title: 使用 Node.js 创建 Vue.js 应用
description: 可以使用 Vue.js 框架在 Visual Studio 中创建 Node.js 应用程序
ms.custom: seodec18
ms.date: 07/06/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: a83e19f808a3f3ab7e1bf9f4fb58f5ddd7a218b7
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033139"
---
# <a name="create-a-vuejs-application-using-nodejs-tools-for-visual-studio"></a>使用针对 Visual Studio 的 Node.js 工具创建 Vue.js 应用程序

Visual Studio 支持通过 JavaScript 或 TypeScript 使用 [Vue.js](https://vuejs.org/) 框架开发应用。

Visual Studio 中有以下新功能支持 Vue.js 应用程序开发：

* 对 .vue 文件中的脚本、样式和模板块的支持 
* 在 .vue 文件上识别 `lang` 属性 
* Vue.js 项目和文件模板

## <a name="prerequisites"></a>系统必备

* 必须安装 Visual Studio 2017 版本 15.8 或更高版本，且有“Node.js 开发”工作负载  。

    > [!IMPORTANT]
    > 本文需要的功能仅从 Visual Studio 2017 版本 15.8 开始提供。

    ::: moniker range=">=vs-2019"
    如果尚未安装所需版本，请安装 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“Node.js 开发”工作负载，然后选择“修改”   。

* 若要创建 ASP.NET Core 项目，必须有 ASP.NET 且安装 Web 开发和 .NET Core 跨平台开发工作负载。

* 须安装 Node.js 运行时。

    如果未安装，请从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。 一般情况下，Visual Studio 会自动检测已安装的 Node.js 运行时。 如果没有检测到已安装的运行时，则可在“属性”页配置项目以引用已安装的运行时。 （创建项目后，右键单击项目节点并选择“属性”  ）。

## <a name="create-a-vuejs-project-using-a-template"></a>使用模板创建 Vue.js 项目

可以使用新的 Vue.js 模板创建新的项目。 使用模板是最简单的入门方法。 有关详细步骤，请参阅[使用 Visual Studio 创建第一个 Vue.js 应用](../javascript/quickstart-vuejs-with-nodejs.md)。

## <a name="create-a-vuejs-project-with-aspnet-core-and-the-vue-cli"></a>使用 ASP.NET Core 和 Vue CLI 创建 Vue.js 项目

Vue.js 提供官方 CLI，快速搭建项目基架。 如果想要使用 CLI 创建应用程序，请按照本文步骤设置开发环境。

> [!IMPORTANT]
> 这些步骤假定你已有一些 Vue.js 框架经验。 如果没有，请访问 [Vue.js](https://vuejs.org/) 了解有关框架的详细信息。

### <a name="create-a-new-aspnet-core-project"></a>创建新的 ASP.NET Core 项目

在此示例中，使用空的 ASP.NET Core 应用程序 (C#)。 但是，可以选择不同的项目和编程语言。

#### <a name="create-an-empty-project"></a>创建一个空项目

1. 打开 Visual Studio 并创建一个新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q 以打开搜索框，键入“asp.net”，然后选择“创建新的 ASP.NET Core Web 应用程序”    。 在出现的对话框中，键入名称“client-app”，然后选择“创建”   。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左侧窗格中，展开“Visual C#”，然后选择“Web”    。 在中间窗格中，选择“ASP.NET Core Web 应用程序”，键入名称“client-app”，然后选择“确定”    。
    ::: moniker-end

    如果没有看到“ASP.NET Core Web 应用程序”项目模板，则必须先安装“ASP.NET 和 Web 开发”工作负载和“.NET Core”开发工作负载    。 若要安装工作负载，单击“新建项目”对话框左窗格中的“打开 Visual Studio 安装程序”链接（选择“文件” > “新建” > “项目”）      。 Visual Studio 安装程序启动。 选择所需工作负载。

1. 选择“空”，然后单击“确定”   。

    Visual Studio 创建项目，该项目将在解决方案资源管理器（右窗格）中打开。

#### <a name="configure-the-project-startup-file"></a>配置项目启动文件

* 打开文件 ./Startup.cs，并将以下行添加到配置方法  ：

    ```csharp
    app.UseDefaultFiles(); // Enables default file mapping on the web root.
    app.UseStaticFiles(); // Marks files on the web root as servable.
    ```

### <a name="install-the-vue-cli"></a>安装 vue CLI

若要安装 vue-cli npm 模块，请打开命令提示符并键入适用于版本 3.0（目前为 beta 版本）的 `npm install --g vue-cli` 或 `npm install -g @vue/cli`。

### <a name="scaffold-a-new-client-application-using-the-vue-cli"></a>使用 vue CLI 搭建新客户端应用程序基架

1. 转到命令提示符，并将当前目录更改为项目根文件夹。

1. 系统提示回答其他问题时，请键入 `vue init webpack client-app` 并按照步骤执行操作。

    > [!NOTE]
    > 对于 .vue  文件，需要使用 WebPack 或具有加载程序的类似框架来执行转换。 TypeScript 和 Visual Studio 不知道如何编译 .vue  文件。 对于捆绑，情况也是如此；TypeScript 不知道如何将 ES2015 模块（即，`import` 和 `export` 语句）转换为要在浏览器中加载的单个最终 .js  文件。 同样，WebPack 是最佳选择。 若要在 Visual Studio 中使用 MSBuild 推动此过程，需要从 Visual Studio 模板开始。 目前，没有现成的 ASP.NET 模板用于 Vue.js 开发。

#### <a name="modify-the-webpack-configuration-to-output-the-built-files-to-wwwroot"></a>修改 webpack 配置将生成的文件输出到 wwwroot

* 打开文件 ./client-app/config/index.js，并将 `build.index` 和 `build.assetsRoot` 更改为 wwwroot 路径  ：

    ```js
    // Template for index.html
    index: path.resolve(__dirname, '../../wwwroot/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../../wwwroot'),
    ```

#### <a name="indicate-the-project-to-build-the-client-app-each-time-that-a-build-is-triggered"></a>每次触发生成时，指示项目生成客户端应用

1. 在 Visual Studio 中，转到“项目” > “属性” > “生成事件”    。

1. 在“预生成事件命令行”上，键入 `npm --prefix ./client-app run build`  。

#### <a name="configure-webpacks-output-module-names"></a>配置 webpack 的输出模块名称

* 打开文件 ./client-app/build/webpack.base.conf.js，并将以下属性添加到输出属性  ：

    ```js
    devtoolModuleFilenameTemplate: '[absolute-resource-path]',
    devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
    ```

### <a name="add-typescript-support-with-the-vue-cli"></a>使用 Vue CLI 添加 TypeScript 支持

这些步骤需要当前仍处于 beta 版本的 vue-cli 3.0。

1. 转到命令提示符，并将当前目录更改为项目根文件夹。

1. 键入 `vue create client-app`，然后选择“手动选择功能”  。

1. 选择“Typescript”，然后选择其他所需的选项  。

1. 执行剩余步骤并对问题做出响应。

#### <a name="configure-a-vuejs-project-for-typescript"></a>为 TypeScript 配置 Vue.js 项目

1. 打开文件 ./client-app/tsconfig.json，并将 `noEmit:true` 添加到编译器选项  。

    通过设置此选项，可以避免每次在 Visual Studio 中生成时干扰项目。

1. 接下来，在 ./client-app/ 中创建 vue.config.js 文件，并添加以下代码   。

    ```js
    module.exports = {
        outputDir: '../wwwroot',

        configureWebpack: {
            output: {
                devtoolModuleFilenameTemplate: '[absolute-resource-path]',
                devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
            }
        }
    };
    ```

    前面的代码配置 webpack 并设置 wwwroot 文件夹。

#### <a name="build-with-vue-cli-30"></a>使用 vue-cli 3.0 生成

vue-cli 3.0 可能出现未知问题阻止自动执行生成过程。 每次尝试刷新 wwwroot 文件夹时，需要在 client-app 文件夹上运行命令 `npm run build`。

或者，可以使用 ASP.NET 项目属性将 vue-cli 3.0 项目生成为预生成事件。 右键单击项目，选择“属性”，并包含“预生成事件命令行”文本框中“生成”选项卡中的以下命令    。

``` cmd
cd ./client-app
npm run build
cd ../
```

## <a name="limitations"></a>限制

* `lang` 属性仅支持 JavaScript 和 TypeScript 语言。 接受的值为：js、jsx、ts 和 tsx。
* `lang` 属性不适用于模板或样式标记。
* 因其预处理的特性，所以不支持在 .vue 文件中调试脚本块  。
* TypeScript 不会将 .vue 文件识别为模块  。 需要一个包含如下所示代码的文件，告知 TypeScript .vue 文件的外观（vue-cli 3.0 模板已包括此文件）  。

    ```js
    // ./client-app/vue-shims.d.ts
    declare module "*.vue" {
        import Vue from "vue";
        export default Vue;
    }
    ```

* 使用 vue-cli 3.0 时，无法在项目属性上将命令 `npm run build` 作为预生成的事件运行。

## <a name="see-also"></a>请参阅

- [Vue 入门指南](https://vuejs.org/v2/guide)。
- [Vue CLI 项目](https://github.com/vuejs/vue-cli)。
- [Webpack 配置文档](https://webpack.js.org/configuration/)。
