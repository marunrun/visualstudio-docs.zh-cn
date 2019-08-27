---
title: 演练：显示匹配的括号 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caaafd0143d3b09a51518ee5f54a02b06dbf10aa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68165777"
---
# <a name="walkthrough-displaying-matching-braces"></a>演练：显示匹配的括号
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以实现基于语言的功能，如大括号匹配通过定义您希望匹配，大的括号和并将文本标记标记添加到匹配大括号，当脱字号上一个大括号。 可以在上下文中的一种语言，定义大括号，或者可以定义自己的文件名称扩展和内容类型并将标记应用于只是该类型，或将标记应用到现有内容类型 （例如"text")。 下面的演练演示如何将应用标记为"text"内容类型匹配的大括号。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="implementing-a-brace-matching-tagger"></a>实现的大括号匹配标记器  
 若要获取大括号突出显示与 Visual Studio 中使用的一个示例类似的效果，可以实现的类型的标记器<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。 下面的代码演示如何定义的任何层级的嵌套的大括号对标记器。 在此示例中，大括号对 []。 []，和{}在标记器构造函数中，而相关的大括号对语言规范中定义的完整语言实现定义。  
  
#### <a name="to-implement-a-brace-matching-tagger"></a>若要实现的大括号匹配标记器  
  
1. 添加一个类文件并将其命名括号匹配。  
  
2. 导入以下命名空间。  
  
     [!code-csharp[VSSDKBraceMatchingTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#1)]
     [!code-vb[VSSDKBraceMatchingTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#1)]  
  
3. 定义一个类`BraceMatchingTagger`，它继承自<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>类型的<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。  
  
     [!code-csharp[VSSDKBraceMatchingTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#2)]
     [!code-vb[VSSDKBraceMatchingTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#2)]  
  
4. 为文本视图中，源缓冲区和当前快照点，以及一组大括号对添加属性。  
  
     [!code-csharp[VSSDKBraceMatchingTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#3)]
     [!code-vb[VSSDKBraceMatchingTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#3)]  
  
5. 标记器构造函数中，在设置属性和订阅以查看更改的事件<xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>和<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>。 在此示例中，用于说明目的，匹配对还定义构造函数中。  
  
     [!code-csharp[VSSDKBraceMatchingTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#4)]
     [!code-vb[VSSDKBraceMatchingTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#4)]  
  
6. 作为的一部分<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>实现中，声明 TagsChanged 事件。  
  
     [!code-csharp[VSSDKBraceMatchingTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#5)]
     [!code-vb[VSSDKBraceMatchingTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#5)]  
  
7. 事件处理程序更新的当前插入符号位置`CurrentChar`属性和引发 TagsChanged 事件。  
  
     [!code-csharp[VSSDKBraceMatchingTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#6)]
     [!code-vb[VSSDKBraceMatchingTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#6)]  
  
8. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>方法来匹配大括号内的任何一个时的当前字符是左大括号或前一个字符时关闭的大括号，如 Visual Studio 中所示。 当找到匹配项时，此方法实例化两个标记、 左大括号和右大括号。  
  
     [!code-csharp[VSSDKBraceMatchingTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#7)]
     [!code-vb[VSSDKBraceMatchingTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#7)]  
  
9. 下面的私有方法查找任何层级的嵌套的匹配大括号。 第一种方法查找匹配的打开的字符的关闭字符：  
  
     [!code-csharp[VSSDKBraceMatchingTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#8)]
     [!code-vb[VSSDKBraceMatchingTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#8)]  
  
10. 以下帮助器方法查找打开与关闭字符匹配的字符：  
  
     [!code-csharp[VSSDKBraceMatchingTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#9)]
     [!code-vb[VSSDKBraceMatchingTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#9)]  
  
## <a name="implementing-a-brace-matching-tagger-provider"></a>实现的大括号匹配标记器提供程序  
 除了实现标记器，还必须实现并导出标记器提供程序。 在这种情况下，提供程序的内容类型是"text"。 这意味着，大括号匹配会显示在所有类型的文本文件，但更完整的实现将应用仅与特定的内容类型相匹配的大括号。  
  
#### <a name="to-implement-a-brace-matching-tagger-provider"></a>若要实现的大括号匹配标记器提供程序  
  
1. 声明的标记器提供程序继承自<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>，其命名为 BraceMatchingTaggerProvider，并将其与导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"和一个<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>的<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。  
  
     [!code-csharp[VSSDKBraceMatchingTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#10)]
     [!code-vb[VSSDKBraceMatchingTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#10)]  
  
2. 实现<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>方法可实例化 BraceMatchingTagger。  
  
     [!code-csharp[VSSDKBraceMatchingTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#11)]
     [!code-vb[VSSDKBraceMatchingTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#11)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 BraceMatchingTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-bracematchingtest-solution"></a>若要生成和测试 BraceMatchingTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本，其中包括匹配大括号。  
  
    ```  
    hello {  
    goodbye}  
  
    {}  
  
    {hello}  
    ```  
  
4. 当将左大括号之前插入符号时，该大括号和关闭的匹配大括号应突出显示。 时恰好在关闭的大括号后放置光标，该大括号和匹配的左大括号应突出显示。  
  
## <a name="see-also"></a>请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
