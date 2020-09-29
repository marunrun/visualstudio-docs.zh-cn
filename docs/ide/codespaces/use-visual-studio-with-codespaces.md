---
title: 将 Visual Studio 用于 codespace（预览）
description: 了解有关将 Visual Studio IDE 用于 GitHub Codespaces 以进行 Windows 开发的信息。
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: c3a2e14236c2d24bc9650fab81150cc295826844
ms.sourcegitcommit: 09d1f5cef5360cdc1cdfd4b22a1a426b38079618
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "91006249"
---
# <a name="how-to-use-visual-studio-with-a-codespace-preview"></a>如何将 Visual Studio 用于 codespace（预览）

Visual Studio 对在 GitHub Codespaces 中进行开发提供了强大的支持。 可以创建并连接到 codespace，使用 Visual Studio 的全部功能在远程托管环境中处理项目。 即使你的源代码和工具位于 codespace 中，而编译和调试是在云中进行的，你的开发体验也会如在本地操作一样，快速且顺畅。 可在 Visual Studio 2019 Preview 中使用 codespace （[注册有限的 public beta 版本](https://github.com/features/codespaces/signup-vs)）。

> [!NOTE]
> 本文专门介绍如何使用 Visual Studio 连接到 GitHub Codespaces。 可以在 [Visual Studio Code](https://docs.github.com/github/developing-online-with-codespaces/connecting-to-your-codespace-from-visual-studio-code) 或 [GitHub](https://docs.github.com/github/developing-online-with-codespaces/developing-in-a-codespace) 文档中了解如何使用其他客户端连接到 codespace。

> [!NOTE]
> 如果尚未安装 [Visual Studio 2019 Preview](https://aka.ms/vspreview)，可以从 [visualstudio.microsoft.com](https://aka.ms/vspreview) 下载。

## <a name="enable-connect-to-github-codespaces"></a>启用“连接到 GitHub Codespaces”

Visual Studio 2019 Preview 默认不启用“连接到 GitHub Codespaces”，因此首先需要启用“预览功能”选项。

1. 在 Visual Studio 2019 Preview 中，使用“工具” > “选项”菜单项，以打开“选项”对话框 。

2. 在“环境”下，选择“预览功能”并查看“连接到 GitHub Codespaces”预览功能  。

   ![选中“连接到 GitHub Codespaces”预览功能](media/connect-to-github-codespaces-preview-feature.png)

3. 需要重启 Visual Studio 才能使用该功能。

## <a name="create-a-codespace"></a>创建 codespace

如果还没有 codespace，则可以从 Visual Studio 创建一个。

1. 启动 Visual Studio 时，“启动”窗口的“开始使用”下将显示“连接到 codespace”按钮。

   ![显示“连接到 codespace”的 Visual Studio“启动”窗口](media/visual-studio-start-window.png)

2. 选择“连接到 codespace”，系统将提示你登录 GitHub。 如果还没有 GitHub 帐户，还可以创建一个。

   ![Visual Studio 中“登录 GitHub”](media/visual-studio-sign-in-to-github.png)

   选择“登录 GitHub”后，请按照在线 GitHub 登录工作流进行操作。

3. 如果从未创建过 codespace，系统将提示你创建一个。

   在“Codespace 详细信息”下，需要提供“存储库 URL”。 创建 codespace 时，GitHub Codespaces 会将指定的存储库克隆到 codespace 中。

   还可以通过下拉菜单修改“实例类型”和“在超时之后挂起” 。 设置 codespace 详细信息后，选择“创建并连接”按钮。

   ![Visual Studio codespace 详细信息](media/visual-studio-codespace-details.png)

   Codespace 准备就绪后，GitHub Codespaces 将开始准备 codespace 并打开 Visual Studio。

   Codespace 名称将显示在菜单栏的远程指示器中。

   ![Visual Studio 已连接到 eShopOnWeb 存储库 codespace](media/visual-studio-eshoponweb-codespace.png)

4. 开始使用 Visual Studio，就像在本地使用一样。 要尝试的操作：

   * 浏览源代码。
   * 选择一个解决方案文件，然后生成该解决方案 (Ctrl+Shift+B)。
   * 在源文件中设置断点，然后按 F5 在调试器中启动该应用程序。
   * 进行更改，并将其提交到存储库。   

> [!NOTE]
> 目前，不能通过 GitHub [Codespaces 门户](https://github.com/codespaces)为 Visual Studio 创建 GitHub Codespaces。 只能使用 Visual Studio 创建。

## <a name="connect-to-a-codespace"></a>连接到 codespace

创建 codespace 后，可以直接从 Visual Studio 中打开 codespace。

1. 启动 Visual Studio 时，“启动”窗口的“开始使用”下将显示“连接到 codespace”按钮。

   ![显示“连接到 codespace”的 Visual Studio“启动”窗口](media/visual-studio-start-window.png)

   如果已在 Visual Studio 中，则可以使用“文件” > ”连接到 codespace”菜单项 。

   ![Visual Studio 的“文件”>“连接到 codespace”菜单项](media/visual-studio-file-connect-to-codespace.png)

2. 选择“连接到 codespace”。 如果尚未登录，系统会提示你登录到 GitHub。

3. 然后，你将在右侧面板中看到所有 GitHub codespace 及其详细信息。

   ![显示可用 GitHub codespace 和详细信息的 Visual Studio](media/visual-studio-connect-codespace.png)

   克隆了 Azure DevOps 存储库的任何 codespace 仅在 Visual Studio 中可见，而在 GitHub Codespaces 页面中不可见。

4. 选择一个 codespace，然后选择“连接”按钮。 如果该 codespace 已暂停，则将重启，且 Visual Studio 将打开与该 codespace 的连接。

   Codespace 名称将显示在菜单栏的远程指示器中。

   ![Visual Studio 已连接到 eShopOnWeb 存储库 codespace](media/visual-studio-eshoponweb-codespace.png)

5. 开始使用 Visual Studio，就像在本地使用一样。 要尝试的操作：

   * 浏览源代码。
   * 选择一个解决方案文件，然后生成该解决方案 (Ctrl+Shift+B)。
   * 在源文件中设置断点，然后按 F5 在调试器中启动该应用程序。
   * 进行更改，并将其提交到存储库。

<!-- TBD ## Suspend a codespace -->

<!-- TBD ## Disconnect from a codespace -->

## <a name="see-also"></a>另请参阅

* [什么是 GitHub Codespaces？](codespaces-overview.md)
* [如何自定义 codespace](customize-codespaces.md)
* [受支持的 Visual Studio 功能](supported-features-codespaces.md)
