---
title: 针对 Visual Studio 的 R 工具常见问题解答
description: 有关 Visual Studio 中的 R 的常见问题。
ms.date: 12/04/2017
ms.topic: reference
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 4eef8e79023bdd3bde03fec33c16a1c8f6d90446
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "72306262"
---
# <a name="frequently-asked-questions"></a>常见问题

## <a name="visual-studio-support"></a>Visual Studio 支持

**问：能否在 OS X 或 Linux 上使用 RTVS？**

答： RTVS 当前是在 Visual Studio 的基础之上生成的，这是仅限 Windows 的实现。 Microsoft 正在调查 Visual Studio Code 和 Visual Studio for Mac 上的支持。 请参阅 [RTVS 问题 #1295](https://github.com/Microsoft/RTVS/issues/1295)。

**问：RTVS 能否用于 Visual Studio Express 版本？**

答： 不是。

**问：我能否将 Visual Studio 插件与 RTVS 结合使用？**

答： 当然可以。 实际上，用户常常将下面的一些插件与 R 结合使用。

- [适用于 vim 键绑定的 VsVim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)
- [GitHub](https://marketplace.visualstudio.com/items?itemName=GitHub.GitHubExtensionforVisualStudio)
- [提供实时预览的 Markdown Editor](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.MarkdownEditor)

请访问 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)，了解详细信息。

**问：由于 RTVS 包含在 Visual Studio 中，这是否意味着可以将 R 轻松用于 C#、C++ 和其他 Microsoft 语言？**

答： 不是。 RTVS 是使用标准本机 R 解释器的 R 代码开发工具。 当前不支持 R 和其他语言之间的互操作。

**问：RTVS 能否使用非英语区域设置？**

答： RTVS 1.0 版仅可使用英语。 1\.1 版将本地化成 Visual Studio 本身使用的一组相同语言。 在此期间，使用[适用于 Visual Studio 2015 的英语语言包](https://www.microsoft.com/download/details.aspx?id=48157)；或在 Visual Studio 2017 中，运行安装程序，并选择“语言包”  选项卡中的“英语”。

![Visual Studio 2017 的“区域设置”](media/FAQ-international-settings.png)

**问：虽然我确实很喜欢当前的 Visual Studio 设置，但我想要尝试新的数据科学设置。我该怎么办？**

答： 请通过“工具” > “导入和导出设置”保存当前的 Visual Studio 设置，然后切换到数据科学设置   。 要还原已保存的设置，请再次使用“导入和导出设置”命令  。

**问：我能否在网络共享上存储我的 Visual Studio 项目？**

答： 否，Visual Studio 不支持从网络共享中加载项目。

## <a name="r-interpretersintegration"></a>R 解释器/集成

**问：哪些 R 解释器可用于 RTVS？**

答： [CRAN R](https://cran.r-project.org/)、[Microsoft R Client 和 Microsoft Machine Learning Server](/machine-learning-server/)

**问：从哪里可以下载这些解释器？**

答： 请参阅[安装](installing-r-tools-for-visual-studio.md)。

问：**Microsoft R Server 是什么？**

答： R Server 是 [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) 的曾用名。

**问：RTVS 能否用于 32 位版本的 R？**

答： 不能，RTVS 仅支持在 64 位版本的 Windows 上运行 64 位版本的 R。

**问：RTVS 能否用于我的源代码管理系统？**

答： 能，可以使用 Visual Studio 中集成的任何源代码管理系统。

**问：建议对 RTVS 项目采用哪种 .gitignore 设置**  ？

答： Github 继续使用所推荐 .gitignore 文件的主存储库  。 请访问：[R .gitignore](https://github.com/github/gitignore/blob/master/R.gitignore)

## <a name="remote-services"></a>远程服务

问： **Visual Studio 中的数据服务是什么？**

答： Visual Studio 的远程 R 服务使你可以设置 Windows 或 Linux 计算机，然后从 RTVS 连接到它。 请参阅[设置远程工作区](setting-up-remote-r-workspaces.md)。

问： **RTVS 能否连接 Microsoft Machine Learning Server？**

答： 否，因为 Microsoft ML Server 是一种不同的技术，其提供的连接机制与 RTVS 要求的不同。

问： **RTVS 是否可以连接到在 Azure 上使用数据科学 VM 映像创建的 VM？**

答： 可以；[数据科学 VM - Windows 2016](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)映像随 Visual Studio 的远程 R 服务进行预安装。

问：**RTVS 是否可以连接到安装了 R 的远程计算机？**

若要在远程计算机上执行 R 代码，必须存在某种侦听请求、接收代码并将结果发送回客户端计算机的服务。 这是 Visual Studio 的远程 R 服务所执行的操作。 请参阅[设置远程工作区](setting-up-remote-r-workspaces.md)。

问： **远程会话是什么？**

答： 请参阅 Machine Learning Server 文档中的文章[在远程服务器上执行](/machine-learning-server/r/how-to-execute-code-remotely)。

## <a name="rtvs-development-and-features"></a>RTVS 开发和功能

**问：虽然缺少功能 X，但 RStudio 有！**

答： 经过多年开发，RStudio 已成为适用于 R 的成熟优质 IDE。 RTVS 旨在囊括你取得成功所需的全部关键功能。 通过在 [GitHub](https://github.com/Microsoft/RTVS/issues/) 上提交问题来帮助确定未来工作的优先级。

**问：我能否参与 RTVS 发布？**

答： 当然可以！ 源代码位于 [Github](https://github.com/microsoft/RTVS) 上。 请使用问题跟踪程序来提交 bug，并对已发布的文件发表评论。

也欢迎你参与此文档的编写 &mdash; 只需选择任意页面右上角的“编辑”  命令。 同样欢迎在任意页面的底部对文档发表评论。
