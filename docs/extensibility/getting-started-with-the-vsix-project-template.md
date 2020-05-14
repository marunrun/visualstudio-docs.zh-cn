---
title: 开始使用 VSIX 项目模板 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 773e9e6891599cd9672888d0521e94891e0d9f41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711246"
---
# <a name="get-started-with-the-vsix-project-template"></a>开始使用 VSIX 项目模板

您可以使用 VSIX 项目模板创建扩展或打包现有扩展进行部署。 VSIX 项目模板同时具有可视化基本版和可视化 C++ 版本，并作为可视化工作室 SDK 的一部分安装。

 VSIX 项目模板仅包含一个*source.扩展.vsix清单*文件，该文件包含有关扩展及其提供的资产的信息。

 要查找 VSIX 项目模板，必须安装可视化工作室 SDK。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="deploy-a-custom-project-template-using-the-vsix-project-template"></a>使用 VSIX 项目模板部署自定义项目模板

 以下步骤演示如何使用 VSIX 项目打包项目模板，以便与其他开发人员共享或上载到可视化工作室库。

1. 创建项目模板。

    1. 打开从中创建模板的项目。 此项目可以是任何项目类型。

    2. 在“项目”菜单上，单击“导出模板”********。 完成向导的步骤。

         *.zip*文件以 *%USERPROFILE%%\我的文档\可视化工作室[版本]创建[我的导出模板\\*] 。

2. 创建空 VSIX 项目。

     选择 **"文件** > **新项目** > **"。** 在搜索框中，键入"vsix"并选择**VSIX 项目的** **C#** 或**可视基本**版本。

3. 将 *.zip*文件添加到项目中。 将其 **"复制到输出目录"** 属性设置为`Copy Always`。

4. 在**解决方案资源管理器**中，双击*source.扩展.vsixmanifest*文件以在**VSIX 清单设计器**中打开该文件，然后进行以下更改：

    - 将**产品名称**字段设置为 **"我的项目模板**"。

    - 将**产品 ID**字段设置为 **"我的项目模板 - 1"。**

    - 将 **"作者"** 字段设置为**法布里卡姆**。

    - 将 **"描述"** 字段设置为 **"我的项目模板**"。

    - 在 **"资产"** 部分中，添加**Microsoft.VisualStudio.ProjectTemplate**类型，并将其路径设置为 *.zip*文件的名称。

5. 保存并关闭*源.扩展.vsixmanifest*文件。

6. 生成项目。

7. 在输出目录中，双击 *.vsix*文件。

8. 将显示**一个 VSIX 安装程序**消息框。 按照说明安装扩展。

9. 关闭 Visual Studio，然后重新打开它。

::: moniker range="vs-2017"

10. 选择**扩展和更新**（在 **"工具"** 菜单上），然后选择 **"模板"** 类别。 可用扩展之一应该是 **"我的项目模板**"。

::: moniker-end

::: moniker range=">=vs-2019"

10. 选择 **"管理扩展**"（在 **"扩展"** 菜单上），然后选择 **"模板"** 类别。 可用扩展之一应该是 **"我的项目模板**"。

::: moniker-end

11. 新项目模板显示在与原始项目模板相同的"**新项目"** 对话框中。 例如，如果从可视化基本控制台应用程序创建了名为**VB 控制台**的模板，则**VB 控制台**将显示在与可视化基本**控制台应用程序**模板相同的窗格中。

### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>在"新项目"对话框中指定模板的位置

1. 模板文件夹位于 *[视觉工作室安装路径][通用 7_IDE_项目模板*和 *[视觉工作室安装路径]_Common7_IDE_ItemTemplates*目录中。 **"新项目"** 对话框中顶级部分的名称与模板文件夹的名称不完全匹配。 如果它们不同，请使用模板文件夹的名称。

    将 *.vsix*文件扩展名更改为 *.zip，* 然后打开该文件。

2. 创建与模板应出现在的 **"新项目"** 对话框中具有相同名称的新文件夹。

3. 如果模板要出现在子节中，请创建同名子文件夹。

4. 将模板 *.zip*文件移动到新文件夹中。

5. 将 *.zip*扩展更改为 *.vsix*。

6. 打开 VSIX 清单。

7. 在 VSIX 清单中，更新模板**的资产**路径，以便它指向包含模板文件的目录树的根目录。 例如，如果模板位于 *[CSharp]Windows*中，则引用应指向 *_CSharp*。
