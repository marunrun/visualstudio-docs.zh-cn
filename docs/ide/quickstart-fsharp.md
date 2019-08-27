---
title: 快速入门：在 F# 中创建 ASP.NET Core Web 服务
description: 了解如何在 Visual Studio 中使用 F# 逐步创建 ASP.NET Core Web 服务。
ms.date: 08/24/2018
ms.topic: quickstart
author: cartermp
ms.author: phcart
manager: andrehal
dev_langs:
- FSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: c24803f3817aa8461f9445e390fe44853d2d27c5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953310"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-service-in-f"></a>快速入门：使用 Visual Studio 在 F\# 中创建首个 ASP.NET Core Web 服务

在这个 5-10 分钟的有关 Visual Studio 中 F# 的介绍中，将创建一个 F# ASP.NET Core Web 应用程序。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建一个 ASP.NET Core Web API 项目。 即使尚未添加任何内容，项目类型随附的模板文件里也包含一个功能性 Web 服务！

::: moniker range="vs-2017"

1. 打开 Visual Studio。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”。

3. 在“新建项目”对话框的左窗格中，展开“Visual F#”，然后选择“Web”。 在中间窗格中，选择“ASP.NET Core Web 应用程序”，然后选择“确定”。

     如果没有看到“.NET Core”项目模板类别，请选择左侧窗格中的“打开 Visual Studio 安装程序”链接。 Visual Studio 安装程序启动。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改”。

     ![VS 安装程序的 ASP.NET 工作负载](../ide/media/quickstart-aspnet-workload.png)

4. 在“新建 ASP.NET Core Web 应用程序”对话框中，从顶部下拉菜单选择“ASP.NET Core 2.1”。 （如果没有在列表中看到“ASP.NET Core 2.1”，请通过“下载”链接进行安装，该链接显示在对话框顶部附近的黄色栏中。）选择 **“确定”**。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。

2. 在“开始”窗口上，选择“创建新项目”。

3. 在“创建新项目”页上，将“f # web”键入搜索框，然后选择“ASP.NET Core Web 应用程序”项目模板。 选择“下一步”。

4. 在“配置新项目”页上，输入名称，然后选择“创建”。

5. 在“新建 ASP.NET Core Web 应用程序”页上，从顶部下拉菜单选择“ASP.NET Core 2.1”，然后选择“创建”。

::: moniker-end

## <a name="explore-the-ide"></a>探索 IDE

1. 在“解决方案资源管理器”工具栏中，展开“控制器”文件夹，然后选择“ValuesController.fs”，在编辑器中将其打开。

   ![解决方案资源管理器，其 F# Web API 项目中的控制器文件夹呈展开状态](../ide/media/hello-world-fs-sln-explorer.png)

2. 接下来，将 `Get()` 成员修改为以下内容：

   ```fsharp
   [<HttpGet>]
   member this.Get() =
       let values = [|"Hello"; "World"; "First F#/ASP.NET Core web API!"|]
       ActionResult<string[]>(values)
   ```

此代码非常简单。 将 F# 数组值绑定到 `values` 名称，然后作为 `ActionResult` 传递给 ASP.NET Core MVC 框架。 ASP.NET Core 会完成其余部分。

在编辑器中是这样的：

![已修改的 Get 成员](../ide/media/hello-world-fs-get-member.png)

## <a name="run-the-application"></a>运行此应用程序

1. 按 Ctrl+F5 运行此应用程序，并在 Web 浏览器中打开它。

2. 页面会转到 `/api/values` 路由，如果没有，请在浏览器中输入 `https://localhost:44396/api/values`。

Web 浏览器现在将显示与之前键入的内容匹配的 JSON。

## <a name="next-steps"></a>后续步骤

祝贺你完成此快速入门！ 希望你已对 F#、ASP.NET Core 和 Visual Studio IDE 有了一定了解。 若要查看公共服务器上运行的应用，请选择下面的按钮。

> [!div class="nextstepaction"]
> [将应用部署到 Azure 应用服务](../deployment/quickstart-deploy-to-azure.md)

若要了解有关 F# 的详细信息，请查看 [F# 指南](/dotnet/fsharp/index)。