---
title: 创建扩展包
description: 了解如何使用扩展包项目模板创建扩展包
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: c959660b920abc18be70b228fa6b40de1ab585f8
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037655"
---
# <a name="walkthrough-create-an-extension-pack"></a>演练：创建扩展包

扩展包是一组可以一起安装的扩展。 扩展包使你能够轻松地与其他用户共享你喜爱的扩展，或者将一组扩展捆绑在一起以用于特定方案。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，Visual Studio SDK 作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

从 Visual Studio 15.8 Preview 2 开始提供扩展包功能。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>使用扩展包项目模板创建扩展

"扩展包项目" 模板创建一个扩展包，其中包含一组可一起安装的扩展。

1. 在 " **新建项目** " 对话框中，搜索 "vsix" 并选择 " **vsix 项目**"。 对于 " **项目名称**"，键入 "Test Extension Pack"。 选择“创建” 。

2. 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 中转到 "Visual c # **扩展性** " 节点，并选择 " **扩展包**"。 保留默认文件名 (ExtensionPack1.cs) "。

3. 添加了 ExtensionPack1 vsext 文件，其中包含以下代码

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

4. 可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)中找到扩展包中要包含的扩展的 vsixid。 找到要包含的扩展，并单击 " **复制 ID**"。 您可以更新上述文件中的现有 **vsixId** ，或者向列表中添加另一个扩展。

    ![从 Marketplace 复制 VsixId](media/vsixid-marketplace.png)

5. 生成项目，并将扩展上传到 Marketplace。 请参阅 [发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

> [!NOTE]
> 扩展包只能安装 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 或 [专用库](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)中可用的扩展。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>从 Visual Studio Marketplace 安装扩展包

扩展已发布后，请在 Visual Studio 中进行安装，并在其中进行测试。

::: moniker range="vs-2017"

1. 在 Visual Studio 的 " **工具** " 菜单上，单击 " **扩展和更新**"。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中的 " **扩展** " 菜单上，单击 " **托管扩展**"。

::: moniker-end

2. 单击 " **联机** "，然后搜索 "测试扩展包"。

3. 单击“下载”。 然后，将为安装计划扩展插件及其扩展列表。

4. 下面是 " **管理扩展** " 对话框的扩展包下载视图示例。 如果你希望仅安装扩展包中包含的某些扩展，则可以在 " **计划安装**" 中修改扩展列表。

    ![从 Marketplace 下载扩展包](media/vside-extensionpack.png)

5. 若要完成安装，请关闭 Visual Studio 的所有实例。

## <a name="remove-the-extension"></a>删除扩展

若要从计算机中删除该扩展，请执行以下操作：

::: moniker range="vs-2017"

1. 在 Visual Studio 的 " **工具** " 菜单上，单击 " **扩展和更新**"。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中的 " **扩展** " 菜单上，单击 " **托管扩展**"。

::: moniker-end

2. 选择 " **测试扩展包** "，然后单击 " **卸载**"。 然后，将对扩展插件及其扩展列表中包含的扩展列表进行卸载计划。

3. 若要完成卸载，请关闭 Visual Studio 的所有实例。
