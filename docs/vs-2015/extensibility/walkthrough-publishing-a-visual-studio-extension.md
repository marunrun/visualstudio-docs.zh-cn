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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201966"
---
# <a name="walkthrough-publishing-a-visual-studio-extension"></a>演练：发布 Visual Studio 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**注意**： Visual Studio 库将被 Visual Studio Marketplace 替换。 有关详细信息，请参阅本主题的最新版本。

本演练演示如何将 Visual Studio 扩展发布到 Visual Studio 库。 将扩展添加到库时，开发人员可以使用 **扩展和更新** 在其中浏览新的和已更新的扩展。

## <a name="prerequisites"></a>必备条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="create-a-visual-studio-extension"></a>创建 Visual Studio 扩展
 在这种情况下，我们将使用默认的 VSPackage 扩展，但相同的步骤对每种类型的扩展都有效。

1. 在名为的 c # 中创建一个 `TestPublishing` 具有菜单命令的 VSPackage。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="test-the-extension"></a>测试扩展
 在分发扩展之前，对其进行生成和测试，以确保它已正确安装在 Visual Studio 的实验实例中。

1. 在 Visual Studio 中，启动调试。 打开 Visual Studio 的实验实例。

2. 在实验实例中，请单击 " **工具** " 菜单，然后单击 " **扩展管理器**"。 TestPublishing 扩展应显示在中心窗格中并启用。

3. 在 " **工具** " 菜单上，确保看到 "测试" 命令。

## <a name="publish-the-extension-to-the-visual-studio-gallery"></a>将扩展发布到 Visual Studio 库
 现在，可以将扩展发布到 Visual Studio 库。

1. 请确保已生成扩展的发行版，并且该版本是最新版本。

2. 在 web 浏览器中，打开 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站。

3. 在右上角，单击 " **登录**"。

4. 使用您的 Microsoft 帐户登录。 如果没有 Microsoft 帐户，此时可以创建一个。

5. 单击“上载” 。

6. 在 " **步骤1：扩展类型**" 中选择 " **工具** "，然后单击 " **下一步**"。

7. 在 " **步骤2：上载**" 中，你可以选择直接上传到 Visual Studio 库，或者只是将链接添加到你自己的网站。 在这种情况下，请选择 **"我想上传工具"**。 此时将显示 " **选择控件** " 框。 单击 " **浏览** "，然后在项目的 "\bin\Release" 文件夹中选择 "TestPublish"。 单击“配置目录分区”  。

8. 在 " **步骤3：基本信息**" 中，将显示 source.extension.vsixmanifest 文件中的字段。 选择适当的 **类别** ，并添加 **标记** 以帮助用户找到你的扩展。 你可能想要添加更详细的摘要和描述 (说明的长度必须至少为280个字符) 。 将 **扩展类型** 保留为 " **不是 Microsoft 扩展** "，将 " **成本类别** " 保留为 **试用版**。

9. 阅读页面底部的 "贡献协议"，并选中 " **我同意**"。

10. 单击 " **创建贡献**"。 这会显示你的扩展将在 Visual Studio 库中具有的页面，并显示一条消息，指出该页尚未发布。

11. 单击“发布” 。

12. 在 Visual Studio 库中搜索扩展。 应显示 TestPublish 扩展的列表。

## <a name="install-the-extension-from-the-visual-studio-gallery"></a>从 Visual Studio 库安装扩展
 扩展已发布后，请在 Visual Studio 中进行安装，并在其中进行测试。

1. 在 Visual Studio 的 " **工具** " 菜单上，单击 " **扩展和更新**"。

2. 单击 " **联机** "，然后搜索 "TestPublish"。 应显示 TestPublish 扩展的列表。

3. 单击“下载”  。 下载该扩展后，单击“安装” ****。

4. 若要完成安装，请重新启动 Visual Studio。

## <a name="removing-the-extension"></a>删除扩展
 你可以从 Visual Studio 库和计算机中删除该扩展。

#### <a name="to-remove-the-extension-from-the-visual-studio-gallery"></a>从 Visual Studio 库中删除扩展

1. 打开 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站。

2. 在右上角，单击 **"我的 Extenions**"。 将显示 TestPublish 的列表。

3. 单击 **“删除”** 。

#### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展

1. 在 Visual Studio 的“工具” **** 菜单中，单击“扩展管理器” ****。

2. 选择 "TestPublish"，然后单击 " **卸载**"。

3. 若要完成卸载，请重启 Visual Studio。
