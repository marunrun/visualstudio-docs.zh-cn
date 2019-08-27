---
title: 通过使用连接服务添加移动服务
description: 使用 Visual Studio 将添加连接服务对话框中添加移动服务
documentationcenter: na
author: ghogen
manager: jillfra
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.topic: conceptual
ms.workload: azure-vs
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: 4bfda342952820b4472a1f826273a7b9075faa9a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963952"
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>通过使用 Visual Studio 连接服务添加移动服务
使用 Visual Studio 2015，您可以使用连接到 Azure 移动服务**添加连接的服务**对话框。 你可以从任何连接C#客户端应用程序、 任何 JavaScript 应用程序或跨平台 Cordova 应用。 连接后，可以创建和访问数据、 创建自定义 Api 和计划的作业，或添加对推送通知的支持。  连接的服务操作将添加所有适当的引用和连接代码。 您还可以充分利用对各种常用身份标识方案，例如 Azure AD 的身份验证的内置支持 Facebook、 Twitter 和 Microsoft 帐户。

## <a name="supported-project-types"></a>支持的项目类型
> [!NOTE]
> 在 Visual Studio 2015 中，使用添加连接服务对话框中将 Azure 移动服务添加到通用 Windows (Windows 10) 的项目不支持。 可以通过安装相应的程序包，为你的项目中使用 NuGet 包管理器来添加 Azure 移动服务。
>
>

连接服务对话框可用于以下项目类型中连接到 Azure 移动服务。

* .NET Windows 8.1 应用商店、 手机和通用应用项目
* JavaScript Windows 8.1 应用商店、 手机和通用应用项目
* 使用 Visual Studio Tools for Apache Cordova 创建的项目

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a>连接到 Azure 移动服务使用添加连接服务对话框
1. 请确保你有 Azure 帐户。 如果还没有 Azure 帐户，你可以注册[免费试用版](http://go.microsoft.com/fwlink/?LinkId=518146)。
2. 打开**添加连接服务**对话框。

   * 对于.NET 应用程序，Visual Studio 中打开你的项目中，打开的上下文菜单**引用**在解决方案资源管理器中的节点，然后选择**添加连接的服务**

        ![连接到 Azure 移动服务](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * 对于 Apache Cordova 应用项目，Visual Studio 中打开你的项目，在解决方案资源管理器中打开项目节点的上下文菜单，然后选择**添加连接的服务**。
3. 在中**添加连接的服务**对话框框中，选择**Azure 移动服务**，然后选择**配置**按钮。 您可能会提示登录到 Azure，如果尚未这样做。

    ![添加 Azure 移动服务](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. 在中**Azure 移动服务**对话框框中，如果有，请选择现有的移动服务。 如果需要创建新的 Azure 移动服务，请按照下面要执行此操作的过程。 否则，请跳到下一步。

    若要创建新的移动服务帐户：

   1. 选择**创建服务**对话框底部的链接。
       ![添加新的移动连接的服务](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. 上**创建移动服务**对话框中，可以选择 JavaScript 后端移动服务或从.NET 后端移动服务**运行时**下拉列表。

       ![创建移动服务](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)

       JavaScript 后端服务是简单而强大。 如果创建 JavaScript 后端移动服务，服务器端 JavaScript 代码存储在云中，但可以通过使用服务器资源管理器或在 Azure 管理门户编辑服务器脚本。

       .NET 后端移动服务提供的全部功能和灵活性的 Web API 和实体框架。 如果创建.NET 后端移动服务，是为您创建并添加到解决方案中的项目。
   3. 选择**区域**其中需要移动服务，然后输入服务器的用户名和密码。
   4. 输入所需的所有信息后，选择**创建**按钮创建移动服务。
   5. 在新移动服务上应出现在服务列表**Azure 移动服务**对话框。 在列表中选择新的移动服务，然后选择**添加**按钮以将服务添加到你的项目。
5. 查看显示入门页，了解项目的修改。 只要您将添加一个连接的服务，则将显示一个入门页面在浏览器中。 您可以查看建议的后续步骤和代码示例，或切换到发生了什么情况页以查看哪些引用已添加到你的项目，以及如何修改你的代码和配置文件了。
6. 使用代码示例作为指南，开始编写代码来访问你的移动服务 ！

## <a name="how-your-project-is-modified"></a>项目的修改情况
Visual Studio 如何修改你的项目取决于项目类型。 有关C#客户端应用，请参阅[发生了什么 –C#项目](http://go.microsoft.com/fwlink/p/?LinkId=513119)。 JavaScript 客户端应用程序，请参阅[完成的操作 – JavaScript 项目](http://go.microsoft.com/fwlink/p/?LinkId=513120)。 对于 Cordova 应用，请参阅[完成的操作 – Cordova 项目](http://go.microsoft.com/fwlink/p/?LinkId=513116)。

## <a name="next-steps"></a>后续步骤
提出问题并获得帮助：

* [MSDN 论坛：Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Microsoft Azure 团队博客上的 azure 移动服务](https://azure.microsoft.com/blog/topics/mobile/)
* [在 azure.microsoft.com 上的 azure 移动服务](https://azure.microsoft.com/services/mobile-services/)
* [在 azure.microsoft.com 上的 azure 移动服务文档](https://azure.microsoft.com/documentation/services/mobile-services/)
