---
title: 演练：创建边距标志符号 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b94ab61f56d74537758c189adc9c104516f67f92
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905044"
---
# <a name="walkthrough-create-a-margin-glyph"></a>演练：创建边距标志符号
您可以使用自定义编辑器扩展自定义编辑器边距的外观。 此演练在代码注释中出现 "todo" 一词时，将自定义标志符号放置在指示器边距上。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。）命名解决方案 `TodoGlyphTest` 。

2. 添加编辑器分类器项目项。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-the-glyph"></a>定义标志符号
 通过运行接口定义标志符号 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> 。

### <a name="to-define-the-glyph"></a>定义标志符号

1. 添加一个类文件并将其命名为 `TodoGlyphFactory`。

2. 使用声明添加以下代码。

     [!code-csharp[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_1.cs)]
     [!code-vb[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_1.vb)]

3. 添加一个名为 `TodoGlyphFactory` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> 。

     [!code-csharp[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_2.cs)]
     [!code-vb[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_2.vb)]

4. 添加定义标志符号尺寸的私有字段。

     [!code-csharp[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_3.cs)]
     [!code-vb[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_3.vb)]

5. `GenerateGlyph`通过定义标志符号用户界面（UI）元素实现。 `TodoTag`在本演练的后面部分定义。

     [!code-csharp[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_4.cs)]
     [!code-vb[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_4.vb)]

6. 添加一个名为 `TodoGlyphFactoryProvider` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> 。 使用 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "TodoGlyph"、" <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> VsTextMarker"、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "code" 和 "TodoTag" 的 "导出此类 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> 。

     [!code-csharp[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_5.cs)]
     [!code-vb[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_5.vb)]

7. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>通过实例化实现方法 `TodoGlyphFactory` 。

     [!code-csharp[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_6.cs)]
     [!code-vb[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_6.vb)]

## <a name="define-a-todo-tag-and-tagger"></a>定义 Todo 标记和标记
 定义您在前面的步骤中定义的 UI 元素与指示器边距之间的关系。 创建标记类型，并使用标记器提供程序来将其导出。

### <a name="to-define-a-todo-tag-and-tagger"></a>定义 todo 标记和标记

1. 向项目中添加一个新的类文件并将其命名为 `TodoTagger` 。

2. 添加以下 import 语句。

     [!code-csharp[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_7.cs)]
     [!code-vb[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_7.vb)]

3. 添加名为的 `TodoTag` 的类。

     [!code-csharp[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_8.cs)]
     [!code-vb[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_8.vb)]

4. 修改名为 `TodoTagger` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 类型 `TodoTag` 。

     [!code-csharp[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_9.cs)]
     [!code-vb[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_9.vb)]

5. `TodoTagger`对于类，为 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> 要在分类范围中查找的文本添加和的私有字段。

     [!code-csharp[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_10.cs)]
     [!code-vb[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_10.vb)]

6. 添加设置分类器的构造函数。

     [!code-csharp[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_11.cs)]
     [!code-vb[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_11.vb)]

7. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>通过查找名称中包含 "comment" 一词并且文本包含搜索文本的所有分类范围来实现方法。 每当找到搜索文本时，将生成类型为的新 <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> `TodoTag` 。

     [!code-csharp[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_12.cs)]
     [!code-vb[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_12.vb)]

8. 声明 `TagsChanged` 事件。

     [!code-csharp[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_13.cs)]
     [!code-vb[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_13.vb)]

9. 添加一个名为的类，该类 `TodoTaggerProvider` 实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> ，并将其导出为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Code" 和 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> TodoTag 的。

     [!code-csharp[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_14.cs)]
     [!code-vb[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_14.vb)]

10. 导入 <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> 。

     [!code-csharp[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_15.cs)]
     [!code-vb[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_15.vb)]

11. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>通过实例化实现方法 `TodoTagger` 。

     [!code-csharp[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_16.cs)]
     [!code-vb[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_16.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 TodoGlyphTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>生成和测试 TodoGlyphTest 解决方案

1. 生成解决方案。

2. 按**F5**运行项目。 将启动 Visual Studio 的第二个实例。

3. 确保显示指示器边距。 （单击 "**工具**" 菜单上的 "**选项**"。 在 "**文本编辑器**" 页上，确保已选择 "**指示器边距**"。

4. 打开包含注释的代码文件。 将 "todo" 一词添加到注释部分。

5. "代码" 窗口左侧的指示器边距中会显示浅蓝色的浅蓝色圆圈。
