---
title: 演练：大纲显示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb338803d50b2ecc9af8c8db6a6b6dc2f3631161
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906175"
---
# <a name="walkthrough-outlining"></a>演练：大纲显示
通过定义要展开或折叠的文本区域的类型，设置基于语言的功能，如大纲显示。 可在语言服务的上下文中定义区域，或定义自己的文件扩展名和内容类型，并将区域定义仅应用于该类型，或者将区域定义应用于现有内容类型（如 "text"）。 此演练演示如何定义和显示大纲显示区域。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework （MEF）项目

### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 VSIX 项目。 将解决方案命名为 `OutlineRegionTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-an-outlining-tagger"></a>实现大纲显示标记
 大纲显示区域由一类标记（）标记 <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> 。 此标记提供标准大纲显示行为。 可展开或折叠分级显示的区域。 如果轮廓区域是折叠的，则通过加号（）对其进行标记 **+** ，如果展开，则使用减号（）对其进行标记 **-** ，并且展开的区域将 demarcated 竖线。

 以下步骤演示如何定义一个标记，该标记可为用方括号（**[**，**]**）分隔的所有区域创建大纲区域。

### <a name="to-implement-an-outlining-tagger"></a>实现大纲显示标记

1. 添加一个类文件并将其命名为 `OutliningTagger`。

2. 导入以下命名空间。

     [!code-csharp[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/CSharp/walkthrough-outlining_1.cs)]
     [!code-vb[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_1.vb)]

3. 创建一个名为的类 `OutliningTagger` ，并让它实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> ：

     [!code-csharp[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/CSharp/walkthrough-outlining_2.cs)]
     [!code-vb[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_2.vb)]

4. 添加一些字段以跟踪文本缓冲区和快照，并累积应该标记为大纲显示区域的行集。 此代码包括表示大纲区域的区域对象（稍后要定义）的列表。

     [!code-csharp[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/CSharp/walkthrough-outlining_3.cs)]
     [!code-vb[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_3.vb)]

5. 添加一个用于初始化字段的标记构造函数，分析缓冲区，并向事件添加事件处理程序 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 。

     [!code-csharp[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/CSharp/walkthrough-outlining_4.cs)]
     [!code-vb[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_4.vb)]

6. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> 方法，此方法实例化标记范围。 此示例假设传入到方法的中的范围 <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 是连续的，尽管可能并非总是如此。 此方法实例化每个大纲显示区域的新标记范围。

     [!code-csharp[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/CSharp/walkthrough-outlining_5.cs)]
     [!code-vb[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_5.vb)]

7. 声明 `TagsChanged` 事件处理程序。

     [!code-csharp[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/CSharp/walkthrough-outlining_6.cs)]
     [!code-vb[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_6.vb)]

8. 添加一个 `BufferChanged` 事件处理程序，它 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 通过分析文本缓冲区来响应事件。

     [!code-csharp[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/CSharp/walkthrough-outlining_7.cs)]
     [!code-vb[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_7.vb)]

9. 添加用于分析缓冲区的方法。 此处提供的示例仅用于说明。 它将缓冲区同步分析为嵌套的大纲区域。

     [!code-csharp[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/CSharp/walkthrough-outlining_8.cs)]
     [!code-vb[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_8.vb)]

10. 下面的 helper 方法获取一个整数，该整数表示大纲显示级别，这表示1是最左侧的大括号对。

     [!code-csharp[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/CSharp/walkthrough-outlining_9.cs)]
     [!code-vb[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_9.vb)]

11. 以下 helper 方法将区域（在本文后面部分定义）转换为 SnapshotSpan。

     [!code-csharp[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/CSharp/walkthrough-outlining_10.cs)]
     [!code-vb[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_10.vb)]

12. 下面的代码仅用于说明。 它定义了一个 PartialRegion 类，该类包含大纲区域开头的行号和偏移量以及对父区域（如果有）的引用。 此代码使分析器可以设置嵌套的大纲区域。 派生区域类包含对大纲区域末尾行号的引用。

     [!code-csharp[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/CSharp/walkthrough-outlining_11.cs)]
     [!code-vb[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_11.vb)]

## <a name="implement-a-tagger-provider"></a>实现标记提供程序
 导出用于标记的标记器提供程序。 标记器提供程序 `OutliningTagger` 为 "text" 内容类型的缓冲区创建一个， `OutliningTagger` 如果缓冲区已经有一个，则返回。

### <a name="to-implement-a-tagger-provider"></a>实现标记器提供程序

1. 创建一个名为的类，该类 `OutliningTaggerProvider` 实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> ，并使用 ContentType 和 TagType 属性将其导出。

     [!code-csharp[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/CSharp/walkthrough-outlining_12.cs)]
     [!code-vb[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_12.vb)]

2. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>通过将添加 `OutliningTagger` 到缓冲区的属性来实现方法。

     [!code-csharp[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/CSharp/walkthrough-outlining_13.cs)]
     [!code-vb[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_13.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 OutlineRegionTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>生成和测试 OutlineRegionTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件。 键入一些文本，其中包括左大括号和右括号。

    ```
    [
       Hello
    ]
    ```

4. 应有一个包含两个方括号的大纲区域。 您应该能够单击左方括号左侧的减号来折叠大纲显示区域。 当区域处于折叠状态时，省略号符号（*...*）应出现在折叠区域的左侧，而当您将指针移到省略号上时，将显示包含文本**悬停文本**的弹出窗口。

## <a name="see-also"></a>另请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
