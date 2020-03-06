---
title: 快速入门：创建第一个 Vue.js 应用
description: 在此快速入门中，将使用针对 Visual Studio 的 Node.js 工具在 Visual Studio 中创建 Vue.js 应用
ms.custom: ''
ms.date: 10/31/2019
ms.topic: quickstart
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: a1995353d00f9e48811f388e1d853c93850b85f4
ms.sourcegitcommit: 9eff8371b7a79a637ebb6850f775dd3eed343d8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2020
ms.locfileid: "78235101"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-vuejs-app"></a>快速入门：使用 Visual Studio 创建第一个 Vue.js 应用

在这个对 Visual Studio 集成开发环境 (IDE) 的 5-10 分钟简介中，可以创建并运行简单的 Vue.js Web 应用程序。

> [!IMPORTANT]
> 本文需要从 Visual Studio 2017 版本 15.8 开始提供的 Vue.js 模板。

## <a name="prerequisites"></a>先决条件

* 须安装 Visual Studio 且具有 Node.js 开发工作负载。

    ::: moniker range=">=vs-2019"
    如果尚未安装 Visual Studio 2019，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio 2017，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“Node.js 开发”工作负载，然后选择“修改”   。

    ![VS 安装程序中的 Node.js 工作负载](../ide/media/quickstart-nodejs-workload.png)

* 须安装 Node.js 运行时。

    如果尚未安装，我们建议从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本，以实现与外部框架和库的最佳兼容性。 Node.js 是为 32 位和 64 位体系结构构建的。 Visual Studio 中的 Node.js 工具（包含在 Node.js 工作负载中）支持这两个版本。 只有一个版本是必需的，并且 Node.js 安装程序一次只支持安装一个版本。
    
    一般情况下，Visual Studio 会自动检测已安装的 Node.js 运行时。 如果系统未检测到已安装运行时，则可以将项目配置为引用属性页中已安装的运行时（创建项目后，右键单击项目节点，选择“属性”  ，并设置“Node.exe 路径”  ）。 可以使用 Node.js 的全局安装，或者可以在每个 Node.js 项目中指定本地解释器的路径。 

## <a name="create-a-project"></a>创建项目

首先，创建 Vue.js Web 应用程序项目。

1. 如果尚未安装 Node.js 运行时，请从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。

    有关详细信息，请参阅先决条件。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q  以打开搜索框，键入“基本 Vue.js”  ，然后选择“基本 Vue.js Web 应用程序”  （JavaScript 或 TypeScript）。 在出现的对话框中，键入名称“basic-vuejs”，然后选择“创建”   。

    ![Vue.js 模板](../javascript/media/vs-2019/vuejs-template.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，展开“JavaScript”或“TypeScript”，然后选择“Node.js”     。 在中间窗格中，选择“基本 Vue.js Web 应用程序”，键入名称“basic-vuejs”，然后选择“确定”    。

    ![Vue.js 模板](../javascript/media/vuejs-template.png)
    ::: moniker-end
    如果未看到“基本 Vue.js Web 应用程序”  项目模板，必须先添加 Node.js 开发工作负载  。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 随即创建新项目。 新项目在“解决方案资源管理器”（右窗格）中打开。

1. 选中输出窗口（下方窗格），查看安装应用程序所需的 npm 包的进度。

1. 打开“解决方案资源管理器”中的“npm”节点，确保其中已安装所有列出的 npm 包  。

    如果缺少任何包（感叹号图标），可右键单击“npm”节点并选择“安装缺少的 npm 包”   。

## <a name="explore-the-ide"></a>探索 IDE

1. 查看右窗格中的“解决方案资源管理器”  。

     ![Vue.js 解决方案](../javascript/media/vuejs-solution.png)

   - 粗体突出显示的是项目，其名称是在“新建项目”  对话框中指定的名称。 在磁盘上，此项目由项目文件夹中的 .njsproj 文件表示  。

   - 顶层是一个解决方案，它与项目默认同名。 解决方案（在磁盘上由 .sln 文件表示）是一个或多个相关项目的容器  。

   - npm 节点显示任何已安装的 npm 包  。 可以右键单击 npm 节点搜索 npm 包，并使用对话框安装 npm 包。

2. 如果想要从命令提示符安装 npm 包或运行 Node.js 命令，请右键单击项目节点，然后选择“在此处打开命令提示符”  。

## <a name="add-a-vue-file-to-the-project"></a>向项目添加一个 .vue 文件

1. 在“解决方案资源管理器”中，右键单击任意文件夹（如 src/components 文件夹），然后选择“添加” > “新项”    。

1. 选择“JavaScript 单个文件组件”或“TypeScript Vue 单个文件组件”，然后单击“添加”    。

    Visual Studio 将向项目添加新文件。

## <a name="build-the-project"></a>生成项目

1. （仅限 TypeScript 项目）在 Visual Studio 中，选择“生成” > “清洁解决方案”   。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 随附的 TypeScript 模板中，跳过此步骤。
    ::: moniker-end

1. 接下来，选择“生成” > “生成解决方案”以生成项目   。 检查“输出”窗口以查看生成结果，并从“显示输出来源”列表中选择“生成”    。

    JavaScript Vue.js 项目模板（以及旧版本的 TypeScript 模板）通过配置后期生成事件使用 `build` npm 脚本。 如果要修改此设置，在“Windows 资源管理器”中打开项目文件 (\<projectname\>.njsproj) 并找到下面的代码行  ：

    ```xml
    <PostBuildEvent>npm run build</PostBuildEvent>
    ```

## <a name="run-the-application"></a>运行此应用程序

1. 按 Ctrl+F5（或“调试”>“开始执行(不调试)”）运行应用程序    。

   在控制台中，你将看到消息“正在启动开发服务器”  。

   应用将在浏览器中打开。
   
   如果看不到正在运行的应用，请刷新页面。

   ![在浏览器中运行的 Vue.js 应用](../javascript/media/vuejs-running-app.png)

1. 关闭 Web 浏览器。

祝贺你完成此快速入门！ 希望你已对 Visual Studio IDE 和 Vue.js 有了一定了解。 若要深入了解其功能，请继续阅读目录中“教程”部分的教程  。

## <a name="next-steps"></a>后续步骤

- 浏览 [Node.js 和 Express 教程](tutorial-nodejs.md)
- 浏览 [Node.js 和 React 教程](tutorial-nodejs-with-react-and-jsx.md)
- [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)