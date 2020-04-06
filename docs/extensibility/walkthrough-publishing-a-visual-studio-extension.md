---
title: 演练：发布视觉工作室扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a34260124baedeba297dbd64e8a2c1856b55ec5a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697144"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>演练：发布可视化工作室扩展

本演练将介绍如何将可视化工作室扩展发布到可视化工作室市场。 将扩展添加到应用商店时，开发人员可以使用**扩展和更新**来浏览新的和更新的扩展。

## <a name="prerequisites"></a>先决条件

 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-visual-studio-extension"></a>创建可视化工作室扩展

本文使用默认的 VSPackage 扩展，但这些步骤对于每种扩展都有效。

1. 在 C#`TestPublish`中创建具有菜单命令的 VSPackage。 有关详细信息，请参阅[创建您的第一个扩展：你好世界](../extensibility/extensibility-hello-world.md)。

## <a name="package-your-extension"></a>打包扩展

1. 使用有关产品名称、作者和版本的正确信息更新扩展 *.vsix 清单*。

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 在**释放**模式下生成扩展。 现在，您的扩展在 \bin_释放文件夹中打包为 VSIX。

3. 您可以双击 VSIX 以验证安装。

## <a name="test-the-extension"></a>测试扩展

 在分发扩展之前，请生成并对其进行测试，以确保它在 Visual Studio 的实验实例中正确安装。

1. 在可视化工作室中，开始调试以打开 Visual Studio 的实验实例。

2. 在实验实例中，转到 **"工具"** 菜单，然后单击 **"扩展和更新**"。 测试发布扩展应显示在中心窗格中并启用。

3. 在 **"工具"** 菜单上，请确保看到测试命令。

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>将扩展发布到可视化工作室市场

1. 请确保您已构建扩展的发布版本，并且该版本是最新的。

2. 在 Web 浏览器中，打开[可视化工作室应用商店](https://marketplace.visualstudio.com/vs)网站。

3. 在右上角，单击"**登录**"。

4. 使用您的 Microsoft 帐户登录。 如果您没有 Microsoft 帐户，此时可以创建一个帐户。

5. 单击 **"发布扩展**"。  此选项将引导您访问所有扩展的管理页面。 如果您没有发布者帐户，系统将提示您此时创建一个。

   ![上传到市场](media/upload-to-marketplace.png)

6. 选择要用于上载扩展的发布者。 您可以通过单击左侧列出的发布者名称来更改发布者。 单击 **"新建扩展"** 并选择**视觉工作室**。

7. 在**1：上传扩展名**，你可以选择上传一个VSIX文件直接到可视化工作室市场或只是添加一个链接到自己的网站。 在此示例中，将上载扩展 *，TestPublish.vsix。* 拖放扩展名或使用**单击**链接浏览文件。 在项目的 [bin_释放文件夹中找到您的扩展名。  单击“继续”****。

8. 在**2：提供扩展详细信息**时，某些字段从*源*自动填充。 在下面查找有关每个内容的更多详细信息：

    * **内部名称**用于扩展的详细信息页的 URL。 例如，在发布者名称"myname"下发布扩展并将内部名称指定为"我的扩展"会导致扩展的详细信息页中的 URL"市场.visualstudio\.com/item？itemName_myname.my 扩展"。

    * **显示**扩展名。 此名称是从*source.扩展.vsixmanifest*文件自动填充的。

    * 要上载的扩展**的版本号。** 此版本是从*源.扩展.vsixmanifest*文件自动填充的。

    * **VSIX ID**是 Visual Studio 用于扩展的唯一标识符。 如果要自动更新扩展，则需要此标识符。 此标识符是从*source.扩展.vsixmanifest*文件自动填充的。

    * 用于扩展的**徽标**。 此徽标从*source.扩展.vsixmanifest*文件（如果提供）自动填充。

    * **扩展功能的简短描述**。 此说明是从*source.扩展.vsixmanifest*文件自动填充的。

    * **概述**是包含屏幕截图和有关扩展功能的详细信息的好地方。

    * **支持的可视化工作室版本**允许您选择扩展将处理的 Visual Studio 版本。 您的扩展仅安装到这些版本。

    * *支持的视觉工作室版本允许您选择哪些版本的视觉工作室，您的扩展将工作。 您的扩展仅安装到这些版本。

    * “类型”****。 最常见的扩展类型是**工具**。

    * **类别**. 最多取三个最适合您的扩展。

    * **标签**是帮助用户找到扩展名的关键字。 标记可帮助提高应用商店中扩展的搜索相关性。

    * **定价类别**是您的扩展成本。

    * **源代码存储库**允许您与社区共享指向源代码的链接。

    * **允许 Q&A 进行扩展**，用户可以在扩展条目页面上留下问题。

9. 单击"**保存&上载**。 此选项将带您返回发布者管理页面。 您的扩展尚未发布。 要发布扩展，请右键单击扩展并选择"**公开**"。 您可以通过选择 **"查看扩展**"来查看扩展在应用商店中的外观。 有关购置编号，请单击 **"报表**"。 要更改扩展名，请单击"**编辑**"。

   ![扩展条目菜单](media/extension-entry-menu.png)

10. 单击 **"公开"** 后，您的扩展现在公开。 在可视化工作室市场搜索您的扩展。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>添加其他用户来管理您的发布者帐户

应用商店支持授予其他用户访问和管理发布者帐户的权限。

1. 导航到要向其添加其他用户的发布者帐户。

2. 选择 **"成员"** 并单击"**添加**"。

   ![添加其他用户](media/add-users.png)

3. 然后，您可以在 **"选择角色**"下指定要添加的用户的电子邮件地址并授予正确的访问级别。  可从以下选项中选择：

   * **创建者**：用户可以发布扩展，但不能查看或管理其他用户发布的扩展。

   * **读取器**：用户可以查看扩展，但不能发布或管理扩展。

   * **参与者**：用户可以发布和管理扩展，但不能编辑发布者设置或管理访问权限。

   * **所有者**：用户可以发布和管理扩展、编辑发布者设置和管理访问权限。

## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从可视化工作室市场安装扩展

现在，扩展已发布，请将其安装在 Visual Studio 中并在那里进行测试。

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新**"。

2. 单击 **"联机"，** 然后搜索**测试发布**。

3. 单击“下载”  。 然后计划安装扩展。

4. 要完成安装，关闭可视化工作室的所有实例。

## <a name="remove-the-extension"></a>删除扩展

可以从可视化工作室应用商店和计算机中删除扩展。

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>从可视化工作室市场中删除扩展

1. 打开[可视化工作室市场](https://marketplace.visualstudio.com/vs)网站。

2. 在右上角，单击 **"发布**扩展"。 选择用于发布**TestPublish**的发布者。 将显示**测试发布**的列表。

3. 右键单击扩展条目，然后单击 **"删除**"。 系统将要求您确认是否要删除扩展。 单击“确定”。

### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展名

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新**"。

2. 选择 **"测试发布"，** 然后单击"**卸载**"。 然后，将扩展计划卸载。

3. 要完成卸载，关闭可视化工作室的所有实例。
