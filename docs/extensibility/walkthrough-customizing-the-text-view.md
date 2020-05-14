---
title: 演练：自定义文本视图 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d99f9201761bbe079c34ccf61339158863509dd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697457"
---
# <a name="walkthrough-customize-the-text-view"></a>演练：自定义文本视图
您可以通过修改其编辑器格式映射中的以下任一属性来自定义文本视图：

- 指示器边距

- 插入卡托

- 覆盖 care

- 所选文本

- 非活动所选文本（即失去焦点的选定文本）

- 可见空白

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`ViewPropertyTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-the-content-type"></a>定义内容类型

1. 添加一个类文件并将其命名为 `ViewPropertyModifier`。

2. 然后，添加以下 `using` 指令：

    [!code-csharp[VSSDKViewPropertyTest#1](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_1.cs)]
    [!code-vb[VSSDKViewPropertyTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_1.vb)]

3. 声明从 继承`TestViewCreationListener`的<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>名为 的类。 使用以下属性导出此类：

   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>指定此侦听器应用的内容类型。

   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>指定此侦听器的角色。

     [!code-csharp[VSSDKViewPropertyTest#2](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_2.cs)]
     [!code-vb[VSSDKViewPropertyTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_2.vb)]

4. 在此类中，导入<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>。

    [!code-csharp[VSSDKViewPropertyTest#3](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_3.cs)]
    [!code-vb[VSSDKViewPropertyTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_3.vb)]

## <a name="change-the-view-properties"></a>更改视图属性

1. 设置 方法<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>，以便在打开视图时更改视图属性。 要进行更改，首先查找<xref:System.Windows.ResourceDictionary>与要查找的视图的方面对应的。 然后，更改资源字典中的相应属性并设置属性。 在设置属性之前调用<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A><xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A>方法，然后在设置属性<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A>之后对 方法进行批处理调用。

     [!code-csharp[VSSDKViewPropertyTest#4](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_4.cs)]
     [!code-vb[VSSDKViewPropertyTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_4.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码

1. 生成解决方案。

     在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

2. 创建一个文本文件并键入一些文本。

    - 插入护记应该是洋红色，覆盖的护处理应该是绿松石。

    - 指标边距（文本视图左侧）应为浅绿色。

3. 选择键入的文本。 所选文本的颜色应为浅粉红色。

4. 选择文本时，单击文本窗口外部的任意位置。 所选文本的颜色应为深粉色。

5. 打开可见的空白。 （在 **"编辑"** 菜单上，指向 **"高级"，** 然后单击"**查看空白**"。 在文本中键入某些选项卡。 应显示表示选项卡的红色箭头。

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
