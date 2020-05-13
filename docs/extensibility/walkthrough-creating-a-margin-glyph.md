---
title: 演练：创建边距字形 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9588b150dd795fc2bc5e6c55d8f6e2359f609939
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697692"
---
# <a name="walkthrough-create-a-margin-glyph"></a>演练：创建边距字形
您可以使用自定义编辑器扩展自定义编辑器边距的外观。 本演练在代码注释中出现单词"待做"时，在指标边距上放置自定义字形。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`TodoGlyphTest`。

2. 添加编辑器分类器项目项。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-the-glyph"></a>定义字形
 通过运行<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>接口定义字形。

### <a name="to-define-the-glyph"></a>定义字形

1. 添加一个类文件并将其命名为 `TodoGlyphFactory`。

2. 使用声明添加以下代码。

     [!code-csharp[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_1.cs)]
     [!code-vb[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_1.vb)]

3. 添加名为`TodoGlyphFactory`的类<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>，实现 。

     [!code-csharp[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_2.cs)]
     [!code-vb[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_2.vb)]

4. 添加定义字形尺寸的私有字段。

     [!code-csharp[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_3.cs)]
     [!code-vb[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_3.vb)]

5. 通过`GenerateGlyph`定义字形用户界面 （UI） 元素来实现。 `TodoTag`在本演练的后面部分定义。

     [!code-csharp[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_4.cs)]
     [!code-vb[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_4.vb)]

6. 添加名为`TodoGlyphFactoryProvider`的类<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider>，实现 。 导出此类<xref:Microsoft.VisualStudio.Utilities.NameAttribute>与"TodoGlyph"，一<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>个后VsTextMarker，一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"代码"，和TodoTag。 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>

     [!code-csharp[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_5.cs)]
     [!code-vb[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_5.vb)]

7. 通过实例<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>化 实现`TodoGlyphFactory`方法。

     [!code-csharp[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_6.cs)]
     [!code-vb[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_6.vb)]

## <a name="define-a-todo-tag-and-tagger"></a>定义 Todo 标记和标记器
 定义在前面的步骤中定义的 UI 元素与指标边距之间的关系。 创建标记类型并标记，并使用标记提供程序导出标记。

### <a name="to-define-a-todo-tag-and-tagger"></a>定义 todo 标记和标记器

1. 向项目添加新类文件并将其命名为`TodoTagger`。

2. 添加以下 import 语句。

     [!code-csharp[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_7.cs)]
     [!code-vb[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_7.vb)]

3. 添加名为的 `TodoTag` 的类。

     [!code-csharp[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_8.cs)]
     [!code-vb[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_8.vb)]

4. 修改名为`TodoTagger`的类，<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>该实现`TodoTag`者的类型 。

     [!code-csharp[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_9.cs)]
     [!code-vb[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_9.vb)]

5. 到`TodoTagger`类中，为 和<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>添加私有字段，供在分类范围内查找的文本。

     [!code-csharp[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_10.cs)]
     [!code-vb[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_10.vb)]

6. 添加设置分类器的构造函数。

     [!code-csharp[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_11.cs)]
     [!code-vb[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_11.vb)]

7. 通过查找<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>名称包括单词"注释"且其文本包含搜索文本的所有分类范围来实现该方法。 每当找到搜索文本时，都会返回新的<xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601>类型`TodoTag`。

     [!code-csharp[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_12.cs)]
     [!code-vb[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_12.vb)]

8. 声明事件`TagsChanged`。

     [!code-csharp[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_13.cs)]
     [!code-vb[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_13.vb)]

9. 添加名为 的`TodoTaggerProvider`类，<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>实现 ，然后导出它<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>与 "代码"和<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>TodoTag。

     [!code-csharp[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_14.cs)]
     [!code-vb[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_14.vb)]

10. 导入<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>。

     [!code-csharp[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_15.cs)]
     [!code-vb[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_15.vb)]

11. 通过实例<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>化 实现`TodoTagger`方法。

     [!code-csharp[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_16.cs)]
     [!code-vb[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_16.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请构建 TodoGlyphTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>构建和测试 TodoGlyphTest 解决方案

1. 生成解决方案。

2. 按**F5**运行项目。 视觉工作室的第二个实例开始。

3. 确保显示指标边距。 （在 **"工具"** 菜单上，单击 **"选项**"。 在 **"文本编辑器"** 页上，请确保选择了**指标边距**。

4. 打开具有注释的代码文件。 将单词"todo"添加到其中一个注释部分。

5. 代码窗口左侧的指标边距中将显示一个深蓝色圆，带有深蓝色轮廓。
