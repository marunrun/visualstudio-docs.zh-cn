---
title: 部署到本地文件夹
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bcf17504f5ae057e68544d26e071bb74cc7b83bf
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263526"
---
# <a name="deploy-an-app-to-a-local-folder-using-visual-studio"></a>使用 Visual Studio 将应用部署到本地文件夹

可以使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到本地文件夹。 对于 Node.js，支持这些步骤但用户界面不同。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> 如果需要将 Windows 桌面应用程序发布到本地文件夹，请参阅[使用 ClickOnce 部署桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)（C# 或 Visual Basic）。 对于 C++/CLR，请参阅[使用 ClickOnce 部署本机应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)，或者对于 C/C++，请参阅[使用安装项目部署本机应用](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)。

## <a name="deploy-to-a-local-folder"></a>部署到本地文件夹

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择“发布”")

1. 如果先前配置了任何发布配置文件，则“发布”窗格会显示。 选择“新建配置文件”。

1. 在“选取发布目标”对话框中，选择“文件夹”。

    ![选择本地文件夹作为发布目标](../deployment/media/quickstart-publish-folder.png "选择文件夹")

1. 输入路径，或选择“浏览”以指定本地文件夹。

1. 选择“发布”。 Visual Studio 将生成项目并将其发布到指定文件夹。 项目属性“发布”窗格出现，显示配置文件摘要。

    ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-folder-summary.png)

1. 若要配置部署设置，请选择配置文件摘要中的“配置”并选择“设置”选项卡。

    ![配置文件设置](../deployment/media/quickstart-profile-settings.png "配置文件设置")

1. 配置选项（如是部署“调试”配置还是“发布”配置），然后选择“保存”。

1. 若要重新发布，请选择“发布”。

可按照任何喜欢的方式部署已发布的文件。 例如，可以使用简单的复制命令将其打包为 .zip 文件，或者使用选择的任何安装包进行部署。

## <a name="next-steps"></a>后续步骤

- [使用发布工具部署 .NET Core 应用程序](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [为 Microsoft Store 打包桌面应用（桌面桥）](/windows/uwp/porting/desktop-to-uwp-packaging-dot-net?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- (.NET) [部署 .NET Framework 和应用程序](/dotnet/framework/deployment/)
