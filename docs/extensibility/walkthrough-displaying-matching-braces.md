---
title: 演练：显示匹配的括号 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8bbea179eb2140706ee868a8a48215e7f490f57d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312524"
---
# <a name="walkthrough-display-matching-braces"></a>演练：显示匹配大括号
实现基于语言的功能，例如，大括号匹配通过定义您希望匹配，括在括号的内，并将文本标记标记添加到匹配大括号，当脱字号上一个大括号。 可以定义一种语言的上下文中的大括号、 定义您自己的文件扩展名和内容类型和应用标签来只是该类型或将标记应用到现有内容类型 （例如"text")。 下面的演练演示如何将应用标记为"text"内容类型匹配的大括号。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，不要从下载中心安装 Visual Studio SDK。 它包含作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-a-brace-matching-tagger"></a>实现的大括号匹配标记器
 若要获取大括号突出显示与 Visual Studio 中使用的一个示例类似的效果，可以实现的类型的标记器<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。 下面的代码演示如何定义的任何层级的嵌套的大括号对标记器。 在此示例中，[] 的大括号对和{}中标记器构造函数中，但在完整的语言实现，对语言规范中定义的相关大括号中定义。

### <a name="to-implement-a-brace-matching-tagger"></a>若要实现的大括号匹配标记器

1. 添加一个类文件并将其命名括号匹配。

2. 导入以下命名空间。

     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]

3. 定义一个类`BraceMatchingTagger`，它继承自<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>类型的<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。

     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]

4. 添加文本视图、 源缓冲区、 当前快照点，以及一组大括号对的属性。

     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]

5. 标记器构造函数中，在设置属性和订阅以查看更改的事件<xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>和<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>。 在此示例中，用于说明目的，匹配对还定义构造函数中。

     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]

6. 作为的一部分<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>实现中，声明 TagsChanged 事件。

     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]

7. 事件处理程序更新的当前插入符号位置`CurrentChar`属性和引发 TagsChanged 事件。

     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]

8. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>方法来匹配大括号内的任何一个时的当前字符是左大括号或前一个字符时关闭的大括号，如 Visual Studio 中所示。 当找到匹配项时，此方法实例化两个标记、 左大括号和右大括号。

     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]

9. 下面的私有方法查找任何层级的嵌套的匹配大括号。 第一种方法查找匹配的打开的字符的关闭字符：

     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]

10. 以下帮助器方法查找打开与关闭字符匹配的字符：

     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]

## <a name="implement-a-brace-matching-tagger-provider"></a>实现的大括号匹配标记器提供程序
 除了实现标记器，还必须实现并导出标记器提供程序。 在这种情况下，提供程序的内容类型是"text"。 因此，大括号匹配会显示在所有类型的文本文件，但更完整实现应用仅与特定的内容类型相匹配的大括号。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>若要实现的大括号匹配标记器提供程序

1. 声明的标记器提供程序继承自<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>，其命名为 BraceMatchingTaggerProvider，并将其与导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"和一个<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>的<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。

     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]

2. 实现<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>方法可实例化 BraceMatchingTagger。

     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，生成 BraceMatchingTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>若要生成和测试 BraceMatchingTest 解决方案

1. 生成解决方案。

2. 当在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包括匹配大括号。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 当将左大括号之前插入符号时，该大括号和关闭的匹配大括号应突出显示。 时恰好在关闭的大括号后放置光标，该大括号和匹配的左大括号应突出显示。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到的文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)