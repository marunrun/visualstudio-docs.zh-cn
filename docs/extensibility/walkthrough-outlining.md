---
title: 演练：大纲 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 97b9dcbb2a24f1a3ed336a4a6bb7de4a15e907b4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697216"
---
# <a name="walkthrough-outlining"></a>演练：大纲显示
设置基于语言的功能，例如通过定义要展开或折叠的文本区域类型来大纲排列。 您可以在语言服务上下文中定义区域，或者定义自己的文件名扩展名和内容类型，并将区域定义仅应用于该类型，或者将区域定义应用于现有内容类型（如"文本"）。 本演练演示如何定义和显示大纲区域。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建托管扩展框架 （MEF） 项目

### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 VSIX 项目。 将解决方案命名为 `OutlineRegionTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-an-outlining-tagger"></a>实现大纲标记器
 大纲区域用一种标记 （ ）<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>标记。 此标记提供标准大纲行为。 可以展开或折叠概述的区域。 如果已折叠，则轮廓区域**+**（）或"减号"（）（）（）**-** 表示，并且扩展区域由垂直线划定。

 以下步骤演示如何定义标记器，该标记器为由括号 **（*****）** 分隔的所有区域创建大纲区域。

### <a name="to-implement-an-outlining-tagger"></a>实现大纲标记

1. 添加一个类文件并将其命名为 `OutliningTagger`。

2. 导入以下命名空间。

     [!code-csharp[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/CSharp/walkthrough-outlining_1.cs)]
     [!code-vb[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_1.vb)]

3. 创建名为 的`OutliningTagger`类，并让它实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>：

     [!code-csharp[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/CSharp/walkthrough-outlining_2.cs)]
     [!code-vb[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_2.vb)]

4. 添加一些字段以跟踪文本缓冲区和快照，并累积应标记为大纲区域的行集。 此代码包括表示大纲区域的区域对象列表（稍后定义）。

     [!code-csharp[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/CSharp/walkthrough-outlining_3.cs)]
     [!code-vb[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_3.vb)]

5. 添加标记器构造函数，该构造函数将初始化字段、分析缓冲区并将事件处理程序添加到<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>事件。

     [!code-csharp[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/CSharp/walkthrough-outlining_4.cs)]
     [!code-vb[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_4.vb)]

6. 实现该方法<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>，该方法实例化标记范围。 此示例假定<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>传入到方法的跨度是连续的，尽管可能并不总是这样。 此方法实例化每个大纲区域的新标记范围。

     [!code-csharp[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/CSharp/walkthrough-outlining_5.cs)]
     [!code-vb[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_5.vb)]

7. 声明事件`TagsChanged`处理程序。

     [!code-csharp[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/CSharp/walkthrough-outlining_6.cs)]
     [!code-vb[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_6.vb)]

8. 通过分析`BufferChanged`文本缓冲区添加响应<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>事件的事件处理程序。

     [!code-csharp[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/CSharp/walkthrough-outlining_7.cs)]
     [!code-vb[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_7.vb)]

9. 添加分析缓冲区的方法。 此处给出的示例仅用于说明。 它将缓冲区同步解析为嵌套大纲区域。

     [!code-csharp[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/CSharp/walkthrough-outlining_8.cs)]
     [!code-vb[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_8.vb)]

10. 以下帮助器方法获取表示大纲级别的整数，以便 1 是最左侧的大括号对。

     [!code-csharp[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/CSharp/walkthrough-outlining_9.cs)]
     [!code-vb[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_9.vb)]

11. 以下帮助器方法将区域（本文后面定义）转换为快照范围。

     [!code-csharp[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/CSharp/walkthrough-outlining_10.cs)]
     [!code-vb[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_10.vb)]

12. 以下代码仅用于说明。 它定义一个部分区域类，其中包含大纲区域开头的行号和偏移量，以及对父区域（如果有）的引用。 此代码使解析器能够设置嵌套的大纲区域。 派生的"区域"类包含对大纲区域末尾的行号的引用。

     [!code-csharp[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/CSharp/walkthrough-outlining_11.cs)]
     [!code-vb[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_11.vb)]

## <a name="implement-a-tagger-provider"></a>实现标记提供程序
 导出标记器的标记提供程序。 标记提供程序为"文本"`OutliningTagger`内容类型的缓冲区创建 一个缓冲区，或者如果缓冲区已有缓冲区，`OutliningTagger`则返回 。

### <a name="to-implement-a-tagger-provider"></a>实现标记提供程序

1. 创建一个名为`OutliningTaggerProvider`的<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>类，实现 ，并导出它与 ContentType 和 TagType 属性。

     [!code-csharp[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/CSharp/walkthrough-outlining_12.cs)]
     [!code-vb[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_12.vb)]

2. 通过将<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>a`OutliningTagger`添加到缓冲区的属性来实现该方法。

     [!code-csharp[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/CSharp/walkthrough-outlining_13.cs)]
     [!code-vb[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_13.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请生成大纲区域测试解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>构建和测试大纲区域测试解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件。 键入一些包含左括号和右括号的文本。

    ```
    [
       Hello
    ]
    ```

4. 应该有一个包含两个括号的大纲区域。 您应该能够单击开放括号左侧的减号以折叠大纲区域。 当区域折叠时，椭圆符号 （*...）* 应出现在折叠区域的左侧，并且当您将指针移到椭圆上时，应会出现包含文本**悬停文本**的弹出窗口。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
