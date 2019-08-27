---
title: 发布到网站
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae1d142058b2f655bb55e5140a6ad6ac5f119742
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263503"
---
# <a name="publish-a-web-app-to-a-web-site-using-visual-studio"></a>使用 Visual Studio 将 Web 应用发布到网站

可以使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到网站。 对于 Node.js，支持这些步骤但用户界面不同。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> 如果需要将 Windows 桌面应用程序发布到网络文件共享，请参阅[使用 ClickOnce 部署桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)（C# 或 Visual Basic）。 对于 C++/CLR，请参阅[使用 ClickOnce 部署本机应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)，或者对于 C/C++，请参阅[使用安装项目部署本机应用](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)。

## <a name="publish-to-a-web-site"></a>发布到网站

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择“发布”")

1. 如果先前配置了任何发布配置文件，则“发布”窗格会显示。 选择“新建配置文件”。

1. 在“选取发布目标”对话框中，选择 IIS、FTP 等。

    ![选择 IIS、FTP 等](../deployment/media/quickstart-publish-iis-ftp.png "Choose IIS, FTP, etc.")

1. 选择“发布”。 该配置文件的“发布设置”对话框随即打开。

    ![选择文件夹](../deployment/media/quickstart-publish-settings-web.png "Choose Folder")

1. 在“发布方法”字段中，选择如“Web 部署”或“FTP”等方法。 接下来所看到的设置对应发布方法。 Web 部署简化了将 Web 应用程序和网站部署到 IIS 服务器的过程，并且必须作为应用程序安装在服务器上。 使用 [Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)进行安装。

1. 为发布方法配置所需设置，并选择“验证连接”。 如果服务器或目标可用且设置正确，则会显示一条指示已验证连接的消息，并且已准备好发布。

    ![验证连接](../deployment/media/quickstart-publish-web-deploy.png "Validate your connection")

1. 选择“设置”以配置其他部署设置（如是部署“调试”配置还是“发布”配置），然后选择“保存”。 如果进行远程调试，则需要调试配置。

1. 若要发布，请选择“发布”。 “输出”窗口显示部署进度和结果。

## <a name="next-steps"></a>后续步骤

在本快速入门中，学习了如何使用 Visual Studio 创建发布配置文件。 此外可以通过导入发布设置来配置发布配置文件。

> [!div class="nextstepaction"]
> [导入发布设置并部署到 IIS](tutorial-import-publish-settings-iis.md)
