---
title: 使用扩展包项目模板创建扩展包 |微软文档
ms.date: 07/27/2018
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: acangialosi
ms.author: anthc
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: fa1c141e18a3870eaad4b155d816e30ee207f45d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697749"
---
# <a name="walkthrough-create-an-extension-pack"></a>演练：创建扩展包

扩展包是一组可以一起安装的扩展。 扩展包使您能够轻松地与其他用户共享您最喜爱的扩展，或针对特定方案将一组扩展捆绑在一起。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，Visual Studio SDK 将作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

扩展包功能可从视觉工作室 15.8 预览 2 开始。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>使用扩展包项目模板创建扩展

扩展包项目模板创建一个扩展包，其中包含一组可以一起安装的扩展。

1. 在 **"新项目"** 对话框中，搜索"vsix"并选择**VSIX 项目**。 对于**项目名称**，键入"测试扩展包"。 选择“创建”  。

2. 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 转到可视化 C#**扩展性**节点并选择**扩展包**。 保留默认文件名 （ExtensionPack1.cs）。

3. 扩展包1.vsext文件被添加，其中包含以下代码

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

4. 要包含在扩展包中的扩展的 vsixid 可以在[可视化工作室应用商店](https://marketplace.visualstudio.com/)中找到。 查找要包含的扩展名，然后单击 **"复制 ID**"。 您可以在上述文件中更新现有**vsixId，** 或向列表中添加另一个扩展名。

    ![从应用商店复制 VsixId](media/vsixid-marketplace.png)

5. 生成项目并将扩展上载到应用商店。 请参阅[发布可视化工作室扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

> [!NOTE]
> 扩展包只能安装[在可视化工作室市场](https://marketplace.visualstudio.com/)或[专用库](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)上可用的扩展。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>从可视化工作室市场安装扩展包

现在，扩展已发布，请将其安装在 Visual Studio 中并在那里进行测试。

::: moniker range="vs-2017"

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新**"。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在可视化工作室中，在 **"扩展"** 菜单上，单击 **"托管扩展**"。

::: moniker-end

2. 单击 **"联机"，** 然后搜索"测试扩展包"。

3. 单击“下载”  。 然后，将安排扩展包中包含的扩展及其扩展列表进行安装。

4. 下面是 **"管理扩展"** 对话框的示例扩展包下载视图。 如果只想在扩展包中安装某些包含的扩展，则可以修改 **"计划安装"** 中的扩展列表。

    ![从应用商店下载扩展包](media/vside-extensionpack.png)

5. 要完成安装，关闭可视化工作室的所有实例。

## <a name="remove-the-extension"></a>删除扩展

要从计算机中删除扩展名，请：

::: moniker range="vs-2017"

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新**"。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在可视化工作室中，在 **"扩展"** 菜单上，单击 **"托管扩展**"。

::: moniker-end

2. 选择**测试扩展包**，然后单击 **"卸载**"。 然后，扩展包中包含的扩展及其扩展列表将安排卸载。

3. 要完成卸载，关闭可视化工作室的所有实例。
