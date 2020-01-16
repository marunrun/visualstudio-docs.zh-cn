---
title: 使用 TypeScript 创建 ASP.NET Core 应用
description: 在本教程中，使用 ASP.NET Core 和 TypeScript 创建应用
ms.date: 01/03/2020
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 40011b035afdf4a04eb760d13c001e39d9c578c4
ms.sourcegitcommit: 91a054beb6b3a16ed5140f9f829239ec31bbbec8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2020
ms.locfileid: "75810578"
---
# <a name="tutorial-create-an-aspnet-core-app-with-typescript-in-visual-studio"></a>教程：在 Visual Studio 中使用 TypeScript 创建 ASP.NET Core 应用

在本 Visual Studio 开发 ASP.NET Core 和 TypeScript 教程中，你将创建一个简单的 Web 应用程序，添加一些 TypeScript 代码，然后运行应用。 

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

在本教程中，你将了解：
> [!div class="checklist"]
> * 创建 ASP.NET Core 项目
> * 添加用于 TypeScript 支持的 NuGet 包
> * 添加一些 TypeScript 代码
> * 运行应用

## <a name="prerequisites"></a>先决条件

* 必须安装 Visual Studio 且具有 ASP.NET Web 开发工作负载。

    ::: moniker range=">=vs-2019"
    如果尚未安装 Visual Studio 2019，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio 2017，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改”   。

## <a name="create-a-new-aspnet-core-mvc-project"></a>创建新的 ASP.NET Core MVC 项目

Visual Studio 管理项目中的单个应用程序的文件  。 该项目包括源代码、资源和配置文件。

在本教程中，将从一个包含 ASP.NET Core MVC 应用代码的简单项目开始。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q  以打开搜索框，键入“ASP.NET”  ，然后选择“ASP.NET Core Web 应用程序 - C#”  。 在出现的对话框中，选择“创建”  。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左侧窗格中，展开“Visual C#”，然后选择“.NET Core”    。 在中间窗格中，选择“ASP.NET Core Web 应用程序 - C#”  ，然后选择“确定”  。
    ::: moniker-end
    如果未显示“ASP.NET Core Web 应用程序”  项目模板，必须添加“ASP.NET 和 Web 开发”  工作负载。 有关详细说明，请参阅[先决条件](#prerequisites)。

1. 选择“创建”  之后，在对话框中选择“Web 应用程序(模型-视图-控制器)”  ，然后选择“创建”  。

   ![选择 MVC 模板](../javascript/media/aspnet-core-ts-mvc-template.png)

    Visual Studio 创建新的解决方案并在右窗格中打开项目。

## <a name="add-some-code"></a>添加一些代码

1. 在解决方案资源管理器中（右侧窗格）。 右键单击项目节点，然后选择“管理 NuGet 包”  。 在“浏览”  选项卡中，搜索“Microsoft.TypeScript.MSBuild”  ，然后单击右侧的“安装”  来安装包。

   ![添加 NuGet 包](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio 会将 NuGet 包添加到解决方案资源管理器中的“依赖项”  节点下。

   > [!NOTE]
   > 本教程需要 NuGet 包。 或者，在你自己的应用中，你可能想要使用 [TypeScript npm 包](https://www.npmjs.com/package/typescript)。

1. 在解决方案资源管理器中，右键单击项目节点，然后选择“添加”>“新文件夹”  。 为新文件夹使用名称“scripts”  。

1. 右键单击“scripts”  文件夹，然后选择“添加”>“新项”  。 选择“TypeScript JSON 配置文件”  ，然后单击“添加”  。

   Visual Studio 将 tsconfig.json  文件添加到“scripts”  文件夹中。 可以使用此文件为 TypeScript 编译器[配置选项](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

1. 打开 tsconfig.json  ，将默认代码替换为以下代码：

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "../wwwroot/js"
     },
     "exclude": [
       "node_modules",
       "wwwroot"
     ]
   }
   ```

   “outDir”  选项指定 TypeScript 编译器转译的计划 JavaScript 文件的输出文件夹。

   此配置提供了使用 TypeScript 的基本简介。 在其他情况下，例如，在使用 [gulp 或 webpack](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) 时，你可能需要为转译的 JavaScript 文件提供不同的中间位置，而不是 ../wwwroot/js  ，具体取决于你的工具和配置首选项。

1. 右键单击“scripts”  文件夹，然后选择“添加”>“新项”  。 选择“TypeScript 文件”  ，键入文件名“app.config”  ，然后单击“添加”  。

   Visual Studio 将 app.config  添加到“scripts”  文件夹。

1. 打开 app.config  并添加以下 TypeScript 代码。

    ```ts
    function TSButton() {
       let name: string = "Fred";
       document.getElementById("ts-example").innerHTML = greeter(user);
    }

    class Student {
       fullName: string;
       constructor(public firstName: string, public middleInitial: string, public lastName: string) {
           this.fullName = firstName + " " + middleInitial + " " + lastName;
       }
    }

    interface Person {
       firstName: string;
       lastName: string;
    }

    function greeter(person: Person) {
       return "Hello, " + person.firstName + " " + person.lastName;
    }

    let user = new Student("Fred", "M.", "Smith");
    ```

    Visual Studio 为 TypeScript 代码提供 IntelliSense 支持。

    若要对此进行测试，请从 `greeter` 函数中删除 `.lastName`，然后重新键入“.”，将看到 IntelliSense。

    ![查看 IntelliSense](../javascript/media/aspnet-core-ts-intellisense.png)

    选择 `lastName`，将最后一个名称添加回代码。

1. 打开“Views / Home”  文件夹，然后打开 index.html  。

1. 在文件末尾添加以下 HTML 代码。

    ```html
    <div id="ts-example">
        <br />
        <button type="button" class="btn btn-primary btn-md" onclick="TSButton()">
            Click Me
        </button>
    </div>
    ```

1. 打开“Views / Shared”  文件夹，然后打开 _Layout.cshtml  。

1. 在调用 `@RenderSection("Scripts", required: false)` 前添加以下脚本引用：

    ```js
    <script src="~/js/app.js"></script>
    ````

## <a name="build-the-application"></a>生成应用程序

1. 选择“生成”>“生成解决方案”  。

   尽管应用程序会在运行时自动生成，但我们想要查看在生成过程中发生的一些事情。

1. 打开“wwwroot / js”  文件夹，并找到两个新文件：app.js  和源映射文件 app.js.map  。 这些文件由 TypeScript 编译器生成。

   调试需要源映射文件。

## <a name="run-the-application"></a>运行此应用程序

1. 按 F5  （“调试”   > “启动调试”  ）来运行该应用程序。

    应用将在浏览器中打开。

    在浏览器窗口中，会看到“欢迎”  标题和“单击我”  按钮。

    ![含 TypeScript 的 ASP.NET Core](../javascript/media/aspnet-core-ts-running-app.png)

1. 单击该按钮可显示在 TypeScript 文件中指定的消息。

## <a name="debug-the-application"></a>调试应用程序

1. 通过在代码编辑器中单击左侧空白，在 `app.ts` 的 `greeter` 函数中设置断点。

    ![设置断点](../javascript/media/aspnet-core-ts-set-breakpoint.png)

1. 按 **F5** 运行该应用程序。

   你可能需要响应消息来启用脚本调试。

   应用程序在断点处暂停。 现在，可以检查变量并使用调试器功能。

## <a name="next-steps"></a>后续步骤

你可能想要了解有关将 TypeScript 与 ASP.NET Core 结合使用的更多详细信息。

> [!div class="nextstepaction"]
> [ASP.NET Core 和 TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)
