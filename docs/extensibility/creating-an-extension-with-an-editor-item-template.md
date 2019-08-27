---
title: 使用编辑器项模板创建扩展 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0bef42c67f34b8a24ac26a7765fecddc104ae74a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351004"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>使用编辑器项模板创建扩展
可以使用 Visual Studio SDK 创建基本编辑器扩展，添加到编辑器分类器、 在修饰和边距中包含的项模板。 编辑器项模板是适用于 Visual C# 或 Visual Basic VSIX 项目。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-classifier-extension"></a>创建分类器扩展
 编辑器分类器项目模板创建一个相应的文本进行着色的编辑器分类器 (在这种情况下，所有内容) 文本的任何文件。

1. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic** ，然后单击**扩展性**。 在中**模板**窗格中，选择**VSIX 项目**。 在“名称”  框中键入 `TestClassifier`。 单击 **“确定”** 。

2. 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 转到 Visual C#**扩展性**节点，然后选择**编辑器分类器**。 保留默认的文件名称 (*EditorClassifier1.cs*)。

3. 有四个代码文件，按如下所示：

    - *EditorClassifier1.cs*包含`EditorClassifier1`类。

    - *EditorClassifier1ClassificationDefinition.cs*包含`EditorClassifier1ClassificationDefinition`类。

    - *EditorClassifier1Format.cs*包含`EditorClassifier1Format`类。

    - *EditorClassifier1Provider.cs*包含`EditorClassifier1Provider`类。

4. 生成项目并启动调试。 将显示 Visual Studio 的实验实例。

     如果您打开一个文本文件，紫色背景中带下划线的文本。

## <a name="create-a-text-relative-adornment-extension"></a>创建一个相对于文本的修饰扩展
 编辑器文本修饰模板创建修饰的文本字符的所有实例相对于文本的修饰 a 使用一个具有红色边框和背景为蓝色的框。 它是相对于文本的因为框始终覆盖的 a 字符，即使它们已移动或重新格式化。

1. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic** ，然后单击**扩展性**。 在中**模板**窗格中，选择**VSIX 项目**。 在“名称”  框中键入 `TestAdornment`。 单击 **“确定”** 。

2. 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 转到 Visual C#**扩展性**节点，然后选择**编辑器文本修饰**。 保留默认的文件名称 (*TextAdornment1.cs/vb*)。

3. 有两个代码文件，按如下所示：

    - *TextAdornment1.cs*包含`TextAdornment1`类。

    - *TextAdornment1TextViewCreationListener.cs*包含`TextAdornment1TextViewCreationListener`类。

4. 生成项目并启动调试。 将显示在实验实例。 如果您打开一个文本文件，以蓝色背景的红色概述了在文本中的所有 a 字符。

## <a name="create-a-viewport-relative-adornment-extension"></a>创建一个相对于视区的修饰扩展
 编辑器视区修饰模板会创建将添加一个具有视区的右上角，以红色的紫色框相对于视区的修饰。

> [!NOTE]
> **视区**是当前显示的文本视图的区域。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>若要使用的编辑器视区修饰模板创建的视区修饰扩展

1. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic** ，然后单击**扩展性**。 在中**模板**窗格中，选择**VSIX 项目**。 在“名称”  框中键入 `ViewportAdornment`。 单击 **“确定”** 。

2. 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 转到 Visual C#**扩展性**节点，然后选择**编辑器视区修饰**。 保留默认的文件名称 (*ViewportAdornment1.cs/vb*)。

3. 有两个代码文件，按如下所示：

    - *ViewportAdornment1.cs*包含`ViewportAdornment1`类。

    - *ViewportAdornment1TextViewCreationListener.cs*包含`ViewportAdornment1TextViewCreationListener`类

4. 生成项目并启动调试。 将显示在实验实例。 如果创建新的文本文件，都有一个红色的框的紫色框显示在视区的右上角。

## <a name="create-a-margin-extension"></a>创建边距扩展
 该编辑器边距模板将创建与单词一起显示的绿色边距 **Hello world ！* 水平滚动条下方。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>若要使用的编辑器边距模板创建边距扩展

1. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic** ，然后单击**扩展性**。 在中**模板**窗格中，选择**VSIX 项目**。 在“名称”  框中键入 `MarginExtension`。 单击 **“确定”** 。

2. 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 转到 Visual C#**扩展性**节点，然后选择**编辑器边距**。 保留默认的文件名称 (EditorMargin1.cs/vb)。

3. 有两个代码文件，按如下所示：

    - *EditorMargin1.cs*包含`EditorMargin1`类。

    - *EditorMargin1Factory.cs*包含`EditorMargin1Factory`类。

4. 生成此项目并启动调试。 将显示在实验实例。 如果您打开一个文本文件，将词的绿色边距**Hello EditorMargin1**显示水平滚动条下方。

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
