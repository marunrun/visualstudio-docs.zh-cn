---
title: 发布扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5238274d66296a21e15b47d1a090ab01c1a1299d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201966"
---
# <a name="walkthrough-publishing-a-visual-studio-extension"></a>演练：发布 Visual Studio 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**说明**：Visual Studio 库即将被 Visual Studio Marketplace。 请参阅本主题的详细信息的最新版本。

此演练演示如何将 Visual Studio 扩展发布到 Visual Studio 库。 当您向库中添加你的扩展时，开发人员可以使用**扩展和更新**从中浏览新建和更新的扩展。

## <a name="prerequisites"></a>系统必备
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="create-a-visual-studio-extension"></a>创建 Visual Studio 扩展
 在这种情况下，我们将使用默认 VSPackage 扩展，但相同的步骤适用于在每个类型的扩展。

1. 在名为 C# 中创建 VSPackage`TestPublishing`具有菜单命令。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="test-the-extension"></a>测试此扩展
 分发扩展之前，生成和测试，以确保 Visual Studio 的实验实例中正确安装。

1. 在 Visual Studio 中，开始调试。 若要打开的 Visual Studio 实验实例。

2. 在实验实例中，转到**工具**菜单，然后单击**扩展管理器**。 TestPublishing 扩展应显示在中心窗格中，启用。

3. 上**工具**菜单中，请确保您看到测试命令。

## <a name="publish-the-extension-to-the-visual-studio-gallery"></a>将扩展发布到 Visual Studio 库
 现在你可以将扩展发布到 Visual Studio 库。

1. 请确保你已经构建了您的扩展插件的版本并且保持最新状态。

2. 在 web 浏览器中，打开[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站。

3. 在右上角中，单击**登录 IN**。

4. 使用您的 Microsoft 帐户登录。 如果还没有 Microsoft 帐户，你可以在这里创建一个。

5. 单击“上载”  。

6. 在**步骤 1:扩展类型**，选择**工具**，然后单击**下一步**。

7. 在**步骤 2:上传**，可以选择直接向 Visual Studio 库上传或只是将链接添加到你自己的网站。 在这种情况下选择**我想要上传我的工具**。 **选择您的控件**框会显示。 单击**浏览**，然后在项目的 \bin\Release 文件夹中选择 TestPublish.vsix。 单击 **“下一步”** 。

8. 在**步骤 3:基本信息**，将显示 source.extension.vsixmanifest 文件中的字段。 选择相应**类别**并添加**标记**以帮助用户找到您的扩展插件。 您可能想要添加更多详细摘要和描述 （说明必须至少 280 个字符）。 将保留**扩展类型**作为**Microsoft 扩展**并**成本类别**作为**试用版**。

9. 阅读在页面底部的发布内容协议并检查**我同意**。

10. 单击**创建发布内容**。 这将显示您的扩展插件会在 Visual Studio 库，与页面尚未发布一条消息的页。

11. 单击“发布”  。

12. 你的扩展在 Visual Studio 库中搜索。 应显示为 TestPublish 扩展插件的列表。

## <a name="install-the-extension-from-the-visual-studio-gallery"></a>从 Visual Studio 库安装扩展
 现在，发布扩展时，在 Visual Studio 中安装它，然后对其进行测试。

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

2. 单击**Online** TestPublish 然后搜索。 应显示为 TestPublish 扩展插件的列表。

3. 单击 **“下载”** 。 下载该扩展后，单击“安装”  。

4. 若要完成安装，重新启动 Visual Studio。

## <a name="removing-the-extension"></a>删除扩展
 从 Visual Studio 库和您的计算机，可以删除该扩展。

#### <a name="to-remove-the-extension-from-the-visual-studio-gallery"></a>若要从 Visual Studio 库中删除扩展

1. 打开[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站。

2. 在右上角中，单击**我 Extenions**。 显示 TestPublish 的列表。

3. 单击“删除”  。

#### <a name="to-remove-the-extension-from-your-computer"></a>若要从您的计算机中删除扩展

1. 在 Visual Studio 的“工具”  菜单中，单击“扩展管理器”  。

2. 选择 TestPublish，然后单击**卸载**。

3. 若要完成卸载，重新启动 Visual Studio。
