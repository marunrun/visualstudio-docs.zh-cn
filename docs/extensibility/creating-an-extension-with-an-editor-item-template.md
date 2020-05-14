---
title: 使用编辑器项目模板创建扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7ac19d99bf75c79ad011bfd0d5a56ecf3880b100
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739508"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>使用编辑器项模板创建扩展
您可以使用 Visual Studio SDK 中包含的项目模板创建基本编辑器扩展，向编辑器添加分类器、修饰和边距。 编辑器项模板可用于可视化 C# 或可视化基本 VSIX 项目。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-classifier-extension"></a>创建分类器扩展
 编辑器分类器项模板创建一个编辑器分类器，用于在任何文本文件中为适当的文本（本例中为所有内容）提供颜色。

1. 在 **"新项目**"对话框中，展开**可视化 C#** 或**可视化基本，** 然后单击"**可扩展性**"。 在 **"模板"** 窗格中，选择**VSIX 项目**。 在“名称”框中键入 `TestClassifier`。**** 单击“确定”。

2. 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 转到可视化 C#**扩展性**节点并选择**编辑器分类器**。 保留默认文件名 *（EditorClassifier1.cs*）。

3. 有四个代码文件，如下所示：

    - *EditorClassifier1.cs*包含类`EditorClassifier1`。

    - *EditorClassifier1ClassificationDefinition.cs*包含类`EditorClassifier1ClassificationDefinition`。

    - *EditorClassifier1Format.cs*包含该`EditorClassifier1Format`类。

    - *EditorClassifier1Provider.cs*包含该`EditorClassifier1Provider`类。

4. 生成项目并启动调试。 视觉工作室的实验实例出现。

     如果打开文本文件，则所有文本都以紫色背景下划线。

## <a name="create-a-text-relative-adornment-extension"></a>创建文本相关修饰扩展
 编辑器文本修饰模板创建一个文本相关修饰，通过使用具有红色轮廓和蓝色背景的框来修饰文本字符"a"的所有实例。 它是与文本相关的，因为框始终覆盖"a"字符，即使它们被移动或重新格式化也是如此。

1. 在 **"新项目**"对话框中，展开**可视化 C#** 或**可视化基本，** 然后单击"**可扩展性**"。 在 **"模板"** 窗格中，选择**VSIX 项目**。 在“名称”框中键入 `TestAdornment`。**** 单击“确定”。

2. 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 转到可视化 C#**扩展性**节点并选择**编辑器文本修饰**。 保留默认文件名 *（TextAdornment1.cs/vb*）。

3. 有两个代码文件，如下所示：

    - *TextAdornment1.cs*包含该`TextAdornment1`类。

    - *TextAdornment1TextViewCreationListener.cs*包含该`TextAdornment1TextViewCreationListener`类。

4. 生成项目并启动调试。 出现实验实例。 如果打开文本文件，文本中的所有"a"字符在蓝色背景中以红色表示。

## <a name="create-a-viewport-relative-adornment-extension"></a>创建视口相对修饰扩展
 编辑器视口装饰模板创建一个视口相对修饰，该装饰在视口右上角添加了一个带有红色轮廓的紫色框。

> [!NOTE]
> **视口**是当前显示的文本视图的区域。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>使用编辑器视口装饰模板创建视口修饰扩展

1. 在 **"新项目**"对话框中，展开**可视化 C#** 或**可视化基本，** 然后单击"**可扩展性**"。 在 **"模板"** 窗格中，选择**VSIX 项目**。 在“名称”框中键入 `ViewportAdornment`。**** 单击“确定”。

2. 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 转到可视化 C#**扩展性**节点并选择**编辑器视口修饰**。 保留默认文件名 *（ViewportAdornment1.cs/vb*）。

3. 有两个代码文件，如下所示：

    - *ViewportAdornment1.cs*包含该`ViewportAdornment1`类。

    - *ViewportAdornment1TextViewCreationListener.cs*包含类`ViewportAdornment1TextViewCreationListener`

4. 生成项目并启动调试。 出现实验实例。 如果创建新的文本文件，则视口右上角将显示一个带有红色轮廓的紫色框。

## <a name="create-a-margin-extension"></a>创建边距扩展
 编辑器边距模板创建一个绿色边距，与单词 "*你好世界！* 在水平滚动条下方。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>使用编辑器边距模板创建保证金扩展

1. 在 **"新项目**"对话框中，展开**可视化 C#** 或**可视化基本，** 然后单击"**可扩展性**"。 在 **"模板"** 窗格中，选择**VSIX 项目**。 在“名称”框中键入 `MarginExtension`。**** 单击“确定”。

2. 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 转到可视化 C#**扩展性**节点并选择**编辑器边距**。 保留默认文件名 （EditorMargin1.cs/vb）。

3. 有两个代码文件，如下所示：

    - *EditorMargin1.cs*包含该`EditorMargin1`类。

    - *EditorMargin1Factory.cs*包含该`EditorMargin1Factory`类。

4. 生成此项目并开始调试。 出现实验实例。 如果打开文本文件，水平滚动栏下方将显示一个绿色边距，该边距的单词 **"Hello EditorMargin1"。"表示**"

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
