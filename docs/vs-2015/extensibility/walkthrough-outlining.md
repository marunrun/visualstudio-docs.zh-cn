---
title: 演练：大纲显示 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7c1dd3d28b9978b52c95b5ff905d57720ed10f5d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201960"
---
# <a name="walkthrough-outlining"></a>演练：大纲显示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以实现基于语言的功能，例如通过定义类型的文本区域，你想要展开或折叠大纲显示。 可以在语言服务的上下文中定义区域，或者可以定义自己的文件名称扩展和内容类型并将区域定义应用于只为该类型，或可以将区域定义应用于现有内容类型 （例如"text")。 本演练演示如何定义和显示大纲区域。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建一个 VSIX 项目。 将解决方案命名为 `OutlineRegionTest`。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="implementing-an-outlining-tagger"></a>实现大纲显示标记器  
 大纲区域被标记为的类型的标记 (<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>)。 此标记提供了标准大纲显示行为。 可以展开或折叠大纲方式显示的区域。 空心的区域将被标记为正号，如果它处于折叠状态或负号由它将展开，并展开的区域一条竖直线方式来划分。  
  
 以下步骤演示如何定义创建大纲区域的所有地区的由分隔的标记器"["和"]"。  
  
#### <a name="to-implement-an-outlining-tagger"></a>若要实现大纲显示标记器  
  
1. 添加一个类文件并将其命名为 `OutliningTagger`。  
  
2. 导入以下命名空间。  
  
     [!code-csharp[VSSDKOutlineRegionTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#1)]
     [!code-vb[VSSDKOutlineRegionTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#1)]  
  
3. 创建一个名为类`OutliningTagger`，并让其实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>:  
  
     [!code-csharp[VSSDKOutlineRegionTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#2)]
     [!code-vb[VSSDKOutlineRegionTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#2)]  
  
4. 添加一些字段来跟踪文本缓冲区和快照和累积应标记为大纲显示区域的行集。 此代码包括区域表示对象 （若要在以后定义） 的大纲显示区域的列表。  
  
     [!code-csharp[VSSDKOutlineRegionTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#3)]
     [!code-vb[VSSDKOutlineRegionTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#3)]  
  
5. 添加字段，初始化一个标记器构造函数分析缓冲区，并添加到事件处理程序<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>事件。  
  
     [!code-csharp[VSSDKOutlineRegionTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#4)]
     [!code-vb[VSSDKOutlineRegionTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#4)]  
  
6. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>方法，它会实例化标记跨越。 此示例假定在 span<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>中传递给该方法是连续的尽管这可能不始终是这种情况。 此方法为每个大纲区域实例化新的标记跨度。  
  
     [!code-csharp[VSSDKOutlineRegionTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#5)]
     [!code-vb[VSSDKOutlineRegionTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#5)]  
  
7. 声明`TagsChanged`事件处理程序。  
  
     [!code-csharp[VSSDKOutlineRegionTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#6)]
     [!code-vb[VSSDKOutlineRegionTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#6)]  
  
8. 添加`BufferChanged`事件处理程序来响应<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>通过分析的文本缓冲区的事件。  
  
     [!code-csharp[VSSDKOutlineRegionTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#7)]
     [!code-vb[VSSDKOutlineRegionTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#7)]  
  
9. 添加一个方法，用以分析缓冲区。 此处提供的示例是仅用于说明目的。 以同步方式将缓冲区分析为嵌套大纲区域。  
  
     [!code-csharp[VSSDKOutlineRegionTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#8)]
     [!code-vb[VSSDKOutlineRegionTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#8)]  
  
10. 以下帮助器方法获取一个整数，表示级别的大纲显示，以便 1 是最左边的大括号对。  
  
     [!code-csharp[VSSDKOutlineRegionTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#9)]
     [!code-vb[VSSDKOutlineRegionTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#9)]  
  
11. 以下帮助器方法转换 SnapshotSpan （稍后在本主题中定义） 的区域。  
  
     [!code-csharp[VSSDKOutlineRegionTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#10)]
     [!code-vb[VSSDKOutlineRegionTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#10)]  
  
12. 下面的代码是仅用于说明目的。 它定义包含的行号和偏移量开始的大纲区域，以及对父区域 （如果有） 的引用的 PartialRegion 类。 这使分析器来设置嵌套大纲区域。 派生的区域类包含对大纲区域末尾的行号的引用。  
  
     [!code-csharp[VSSDKOutlineRegionTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#11)]
     [!code-vb[VSSDKOutlineRegionTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#11)]  
  
## <a name="implementing-a-tagger-provider"></a>实现标记器提供程序  
 必须在标记器的导出标记器提供程序。 标记器提供程序创建`OutliningTagger`的"text"内容类型或其他返回缓冲区`OutliningTagger`如果缓冲区已经包含一个。  
  
#### <a name="to-implement-a-tagger-provider"></a>若要实现一个标记器提供程序  
  
1. 创建一个名为类`OutliningTaggerProvider`实现<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>，并将其导出具有 ContentType 和 TagType 属性。  
  
     [!code-csharp[VSSDKOutlineRegionTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#12)]
     [!code-vb[VSSDKOutlineRegionTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#12)]  
  
2. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>方法通过添加`OutliningTagger`到缓冲区的属性。  
  
     [!code-csharp[VSSDKOutlineRegionTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#13)]
     [!code-vb[VSSDKOutlineRegionTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#13)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 OutlineRegionTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-outlineregiontest-solution"></a>若要生成和测试 OutlineRegionTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建文本文件。 键入一些文本，其中包括左大括号和右大括号。  
  
    ```  
    [  
       Hello  
    ]  
    ```  
  
4. 应包含这两个大括号的大纲区域。 您应可以通过单击左侧的左大括号负号，若要折叠大纲区域。 当区域处于折叠状态，省略号 （...） 应显示在折叠的区域和一个弹出窗口，其中包含文本的左侧**将鼠标悬停在文本**应显示的省略号上移动指针时。  
  
## <a name="see-also"></a>请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
