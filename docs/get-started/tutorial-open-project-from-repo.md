---
title: 教程：打开存储库中的项目
description: 了解如何使用 Visual Studio 打开 Git 或 Azure DevOps 存储库中的项目。
ms.custom: get-started
ms.date: 03/30/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 3af54d663cee1ad2b2dd4e8241678b88c635d376
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180439"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>教程：打开存储库中的项目

在本教程中，你将使用 Visual Studio 首次连接到存储库，然后打开其中的一个项目。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="open-a-project-from-a-github-repo"></a>打开 GitHub 存储库中的项目

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏上，选择“文件”>“打开”>“在源代码管理中打开”    。

   随即打开“团队资源管理器 - 连接”  窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口](./media/open-proj-repo-team-explorer.png)

1. 在“本地 Git 存储库”  部分中，选择“克隆”  。

    ![从“本地 Git 存储库”部分中选择“克隆”](./media/open-proj-repo-local-git-repo-clone.png)

1. 在“输入要克隆的 Git 存储库的 URL”框中，键入或粘贴存储库的 URL，然后按 Enter  。 （可能会收到登录到 GitHub 的提示；如果是这样，请按照提示操作。）

   Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。  选择“解决方案和文件夹”  。

   ![从解决方案资源管理器中选择“解决方案和文件夹”](./media/open-proj-repo-github-solutions-folders.png)

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![选择想要从“解决方案资源管理器”下拉列表中打开的解决方案](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

### <a name="review-your-work"></a>检查工作

查看以下动画以检查你在上一节中完成的工作。

   ![使用 Visual Studio 的 GitHub 存储库中打开项目的动画](./media/open-project-from-github.gif)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

1. 在“开始”窗口上，选择“克隆或签出代码”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 输入或键入存储库位置，然后选择“克隆”  。

   ![查看“克隆或签出代码”窗口](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Visual Studio 从存储库打开项目。

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![选择想要从“解决方案资源管理器”下拉列表中打开的解决方案](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

## <a name="open-a-project-from-an-azure-devops-repo"></a>打开 Azure DevOps 存储库中的项目

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏上，选择“文件”>“打开”>“在源代码管理中打开”    。

   随即打开“团队资源管理器 - 连接”  窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口](./media/open-proj-repo-team-explorer.png)

1. 可通过两种方式连接到 Azure DevOps 存储库：

      - 在“托管服务提供程序”  部分中，选择“连接...”  。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“托管服务提供程序”部分](./media/open-proj-repo-azure-devops.png)

      - 在“管理连接”  下拉列表中，选择“连接到项目...”  。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“管理连接”部分](./media/open-proj-repo-azuredevops-manage-connections.png)

1. 在“连接到项目”  对话框中，选择要连接的存储库，然后选择“克隆”  。

      ![从 Visual Studio 生成的“连接到项目”对话框](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

1. Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。  选择“解决方案和文件夹”  。

      ![Visual Studio 中团队资源管理器中的“解决方案和文件夹”通知](./media/open-proj-repo-solutions-folders.png)

   “解决方案和文件夹”弹出菜单中会显示一个解决方案文件（具体是 .sln 文件）。 选择它后，Visual Studio 将打开你的解决方案。

   如果存储库中没有解决方案文件，弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

1. 在“开始”窗口上，选择“克隆或签出代码”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps”   。

   ![查看“克隆或签出代码”窗口](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   如果看到登录窗口，请登录帐户。

1. 在“连接到项目”  对话框中，选择要连接的存储库，然后选择“克隆”  。

      ![从 Visual Studio 生成的“连接到项目”对话框](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

   克隆完成后，Visual Studio 会打开“团队资源管理器”并显示通知  。

     ![克隆完成后 Visual Studio 中的“团队资源管理器”窗口](./media/vs-2019/clone-complete-azure-devops.png)

1. 若要查看文件夹和文件，请选择“显示文件夹视图”链接  。

     ![克隆完成后 Visual Studio 中“团队资源管理器”窗口的“解决方案”部分](./media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio 随即打开“解决方案资源管理器”  。

1. 选择“解决方案和文件夹”链接，搜索要打开的解决方案文件（具体而言，.sln 文件）  。

      ![Visual Studio 中团队资源管理器中的“解决方案和文件夹”通知](./media/open-proj-repo-solutions-folders.png)

   如果存储库中没有解决方案文件，则会显示消息“找不到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

## <a name="next-steps"></a>后续步骤

如果你已准备好使用 Visual Studio 进行编码，请深入了解以下特定于语言的任何教程：

- [Visual Studio 教程 | C#  ](./csharp/index.yml)
- [Visual Studio 教程 | Visual Basic  ](./visual-basic/index.yml)
- [Visual Studio 教程 | C++  ](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio 教程 | Python  ](/visualstudio/python/)
- [Visual Studio 教程 | JavaScript、TypeScript 和 Node.js    ](/visualstudio/javascript/)

## <a name="see-also"></a>请参阅

- [Azure DevOps Services：Azure Repos 和 Visual Studio 入门](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn：Azure DevOps 入门](/learn/modules/get-started-with-devops/)