---
title: 演练：发布 Visual Studio 扩展 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 86ed2455b19a3f7e56c92a37a9402b7d65bf70a3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337928"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>演练：发布 Visual Studio 扩展

本演练演示如何将 Visual Studio 扩展发布到 Visual Studio Marketplace。 当你的扩展添加到 Marketplace 后时，开发人员可以使用**扩展和更新**浏览到新的和更新扩展。

## <a name="prerequisites"></a>系统必备

 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-visual-studio-extension"></a>创建 Visual Studio 扩展

本文使用默认 VSPackage 扩展，但对扩展的每一种有效执行的步骤。

1. 在名为 C# 中创建 VSPackage`TestPublish`具有菜单命令。 有关详细信息，请参阅[创建第一个扩展：Hello World](../extensibility/extensibility-hello-world.md)。

## <a name="package-your-extension"></a>打包你的扩展

1. 更新扩展 *.vsixmanifest*有关产品名称、 作者和版本的正确信息。

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 构建您的扩展插件**版本**模式。 现在你的扩展打包为 VSIX \bin\Release 文件夹中。

3. 你可以双击 VSIX 验证安装成功。

## <a name="test-the-extension"></a>测试此扩展

 分发扩展之前，生成和测试，以确保 Visual Studio 的实验实例中正确安装。

1. 在 Visual Studio 中，开始调试以打开 Visual Studio 的实验实例。

2. 在实验实例中，转到**工具**菜单，然后单击**扩展和更新**。 TestPublish 扩展应显示在中心窗格中，启用。

3. 上**工具**菜单中，请确保您看到测试命令。

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>将扩展发布到 Visual Studio Marketplace

1. 请确保你已经构建了您的扩展插件的版本并且保持最新状态。

2. 在 web 浏览器中，打开[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)网站。

3. 在右上角中，单击**登录**。

4. 使用您的 Microsoft 帐户登录。 如果还没有 Microsoft 帐户，你可以在这里创建一个。

5. 单击**发布的扩展**。  此选项可导航到你的所有扩展的管理页。 如果你没有发布者帐户，系统会提示创建一个在这一次。

   ![将上传到 Marketplace](media/upload-to-marketplace.png)

6. 选择你想要用于上传你的扩展发布的服务器。 可以通过单击左侧列出的发布服务器名称更改发布服务器。 单击**新的扩展插件**，然后选择**Visual Studio**。

7. 在**1:上传扩展**，您可以选择将 VSIX 文件上传到 Visual Studio Marketplace 直接或只是将链接添加到你自己的网站。 在此示例中，该扩展*TestPublish.vsix*上传。 拖放在扩展或使用**单击**链接以浏览方式查找文件。 在项目的 \bin\Release 文件夹中查找您的扩展插件。  单击 **“继续”** 。

8. 在**2:提供扩展详细信息**，某些字段会自动填充从*source.extension.vsixmanifest*文件从您的扩展插件。 查找有关每个以下的更多详细信息：

    * **内部名称**扩展的详细信息页的 URL 中使用。 例如，发布在发布服务器名称"myname"扩展和指定的内部名称为"my 扩展"结果中的 URL"marketplace.visualstudio\.com/items?itemName=myname.myextension"扩展的详细信息页。

    * **显示名称**您的扩展。 此名称是从自动填充*source.extension.vsixmanifest*文件。

    * **版本**数要上传的扩展。 此版本已从自动填充*source.extension.vsixmanifest*文件。

    * **VSIX ID**是 Visual Studio 将使用为扩展插件的唯一标识符。 如果你想要让您自动更新的扩展，则需要使用此标识符。 此标识符是从自动填充*source.extension.vsixmanifest*文件。

    * **徽标**用于你的扩展。 此徽标是从自动填充*source.extension.vsixmanifest*文件提供。

    * **简短说明**的扩展功能的。 此说明是从自动填充*source.extension.vsixmanifest*文件。

    * **概述**是包括屏幕截图和有关您的扩展插件的作用的详细的信息的好时机。

    * **支持的 Visual Studio 版本**允许您选择的 Visual Studio 版本中将处理您的扩展插件。 您的扩展插件仅安装到这些版本。

    * * * 支持 Visual Studio 版本，可以选择您的扩展插件将适用于 Visual Studio 的版本。 您的扩展插件仅安装到这些版本。

    * **类型**。 最常见的扩展类型是**工具**。

    * **类别**。 选择最多三个是最佳适合您的扩展插件的。

    * **标记**是关键字，可帮助用户找到您的扩展插件。 标记可帮助提高你的扩展在 Marketplace 中搜索相关性。

    * **定价类别**是您的扩展插件的成本。

    * **源代码存储库**使您可以与社区分享你的源代码的链接。

    * **您的扩展允许问答**允许用户在你扩展条目页面留下的问题。

9. 单击**保存并上传**。 此选项操作，将返回到发布服务器管理页。 您的扩展插件尚未发布。 若要发布扩展，右键单击扩展，然后选择**设为公开**。 您可以查看您的扩展插件的外观像在 Marketplace 上通过选择**查看扩展**。 获取数字，请单击**报表**。 若要更改您的扩展插件，请单击**编辑**。

   ![扩展项菜单](media/extension-entry-menu.png)

10. 单击后**设为公开**，您的扩展现在是公共的。 你的扩展在 Visual Studio Marketplace 中搜索。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>添加其他用户管理发布者帐户

Marketplace 支持授予其他用户权限来访问和管理发布者帐户。

1. 导航到想要添加到其他用户的发布者帐户。

2. 选择**成员**，然后单击**添加**。

   ![添加其他用户](media/add-users.png)

3. 然后可以指定你想要添加并授予适当的下的访问级别的用户的电子邮件地址**选择一个角色**。  可从以下选项中进行选择：

   * **创建者**:用户可以发布扩展，但不能查看或管理其他用户发布的扩展。

   * **读取器**:用户可以查看扩展，但不能发布或管理扩展。

   * **参与者**:用户可以发布和管理扩展，但不能编辑发布服务器设置或管理访问权限。

   * **所有者**:用户可以发布和管理扩展，编辑发布服务器设置和管理访问权限。

## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展

现在，发布扩展时，在 Visual Studio 中安装它，然后对其进行测试。

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

2. 单击**联机**，然后搜索**TestPublish**。

3. 单击 **“下载”** 。 然后计划安装的扩展。

4. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

从 Visual Studio Marketplace 和您的计算机，可以删除该扩展。

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>若要从 Visual Studio Marketplace 中删除扩展

1. 打开[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)网站。

2. 在右上角中，单击**发布**扩展。 选择发布服务器，用来发布**TestPublish**。 列表**TestPublish**出现。

3. 右键单击扩展条目，然后单击**删除**。 需要确认你想要删除该扩展。 单击 **“确定”** 。

### <a name="to-remove-the-extension-from-your-computer"></a>若要从您的计算机中删除扩展

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

2. 选择**TestPublish** ，然后单击**卸载**。 卸载然后计划扩展。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
