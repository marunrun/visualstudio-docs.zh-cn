---
title: 使用扩展包项目模板创建的扩展包 |Microsoft Docs
ms.date: 07/27/2018
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: madskristensen
ms.author: madsk
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: 66a1c42340a88f0756d4fcc1f323433ab2640127
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322797"
---
# <a name="walkthrough-create-an-extension-pack"></a>演练：创建扩展包

扩展包是一套可以一起安装的扩展插件。 扩展包，可以轻松地与其他用户共享你喜欢的扩展或捆绑包的一组一起使用以获得特定方案的扩展。

## <a name="prerequisites"></a>系统必备

从 Visual Studio 2015 开始，Visual Studio SDK 附带了作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

可从 Visual Studio 15.8 预览版 2 开始的扩展包功能。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>使用的扩展包，项模板创建扩展

扩展包，项模板创建具有可以一起安装的扩展插件的设置的扩展包。

1. 在中**新的项目**对话框中，搜索"vsix"，然后选择**VSIX 项目**。 有关**项目名称**，键入"测试扩展包"。 选择“创建”  。

2. 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 转到 Visual C#**扩展性**节点，然后选择**扩展包**。 保留默认的文件名称 (ExtensionPack1.cs)。

3. 其中包含以下代码添加 ExtensionPack1.vsext 文件

   ```json
   {
    "id": "ExtensionPack1",
    "name": "ExtensionPack1",
    "description": "Read about creating extension packs at https://aka.ms/vsextpack",
    "version": "1.0.0.0",
    "extensions": [  // List of extensions that are included in the Extension Pack.
      {
        "vsixId": "41858b2d-ff0b-4a43-80b0-f1b2d6084935", // The vsix id of the extension you want to   include.
        "name": "AlignAssignments"
      },
      {
          "vsixId": "42374550-426a-400e-96f9-237682e8dea6",
        "name": "CopyAsHtml"
      }
    ]
   }
   ```

4. 在找不到要包含在扩展包中的扩展 vsixid [Visual Studio Marketplace](https://marketplace.visualstudio.com/)。 找到你想要包括，然后单击的扩展**复制 ID**。 您可以更新现有**vsixId** ，以上文件，或者将另一个扩展添加到列表。

    ![从 Marketplace 复制 VsixId](media/vsixid-marketplace.png)

5. 生成项目，并将你的扩展上传到 Marketplace。 请参阅[发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

> [!NOTE]
> 扩展包只能安装可用的扩展[Visual Studio Marketplace](https://marketplace.visualstudio.com/)或[专用库](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展包

现在，发布扩展时，在 Visual Studio 中安装它，然后对其进行测试。

::: moniker range="vs-2017"

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中，在**扩展**菜单上，单击**托管扩展**。

::: moniker-end

2. 单击**Online** ，然后搜索"测试扩展包"。

3. 单击 **“下载”** 。 然后将安装计划扩展和扩展包中包括的扩展其列表。

4. 下面是示例的扩展包，下载视图**管理扩展**对话框。 如果想要安装扩展包中只有某些包含扩展插件，则可以修改的扩展列表中**计划安装**。

    ![从 Marketplace 下载扩展包](media/vside-extensionpack.png)

5. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

若要从计算机中删除该扩展：

::: moniker range="vs-2017"

1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中，在**扩展**菜单上，单击**托管扩展**。

::: moniker-end

2. 选择**测试扩展包**，然后单击**卸载**。 然后将卸载计划扩展和扩展包中包括的扩展其列表。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
