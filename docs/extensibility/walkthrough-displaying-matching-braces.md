---
title: 演练：显示匹配的大括号 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 107610733ab9b5c8085b3f987fa999250b453d63
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697454"
---
# <a name="walkthrough-display-matching-braces"></a>演练：显示匹配的大括号
实现基于语言的功能，例如，通过定义要匹配的大括号来匹配大括号，并在 caret 位于其中一个大括号上时向匹配大括号添加文本标记标记。 您可以在语言上下文中定义大括号，定义自己的文件名扩展名和内容类型，并将标记仅应用于该类型，或将标记应用于现有内容类型（如"文本"）。 以下演练演示如何将大括号匹配标记应用于"文本"内容类型。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建托管扩展框架 （MEF） 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-a-brace-matching-tagger"></a>实现大括号匹配标记器
 要获得类似于 Visual Studio 中使用的大括号突出显示效果，可以实现类型<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>标记。 以下代码演示如何在任何嵌套级别为大括号对定义标记。 在此示例中，*的大括号对在{}标记器构造函数中定义，但在完整语言实现中，将在语言规范中定义相关的大括号对。

### <a name="to-implement-a-brace-matching-tagger"></a>实现大括号匹配标记器

1. 添加类文件并将其命名为 Brace 匹配。

2. 导入以下命名空间。

     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]

3. 定义从`BraceMatchingTagger`<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>类型<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>继承的类。

     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]

4. 添加文本视图、源缓冲区、当前快照点以及一组大括号对的属性。

     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]

5. 在标记器构造函数中，设置属性并订阅视图更改事件<xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>和<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>。 在此示例中，为了便于说明，匹配对也在构造函数中定义。

     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]

6. 作为实现的一<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>部分，声明 Tag 已更改事件。

     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]

7. 事件处理程序更新`CurrentChar`属性的当前位置并引发 Tag 已更改事件。

     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]

8. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>方法以匹配大括号，当当前字符是开放大括号或当前一个字符是紧密大括号时，如 Visual Studio 中那样。 找到匹配项时，此方法会实例化两个标记，一个用于开放大括号，一个用于紧密大括号。

     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]

9. 以下私有方法在任何嵌套级别查找匹配的大括号。 第一种方法查找与打开字符匹配的紧密字符：

     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]

10. 以下帮助程序方法查找与近字符匹配的开放字符：

     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]

## <a name="implement-a-brace-matching-tagger-provider"></a>实现大括号匹配标记提供程序
 除了实现标记器外，还必须实现并导出标记提供程序。 在这种情况下，提供程序的内容类型是"文本"。 因此，大括号匹配将显示在所有类型的文本文件中，但更全面的实现仅将大括号匹配应用于特定内容类型。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>实现大括号匹配标记提供程序

1. 声明从<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>继承的标记提供程序 ，将其命名为 Brace匹配 Tagger 提供程序，然后将其导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>为"文本"和<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute><xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。

     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]

2. 实现实例<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>化支架匹配标记的方法。

     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请构建 Brace匹配测试解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>构建和测试大括号匹配测试解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件并键入一些包含匹配大括号的文本。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 将 care 放置在打开的大括号之前时，应突出显示该大括号和匹配的紧密大括号。 当您在关闭大括号之后定位光标时，应突出显示该大括号和匹配的打开大括号。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
