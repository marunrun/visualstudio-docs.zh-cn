---
title: 演练：显示匹配的大括号 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165777"
---
# <a name="walkthrough-displaying-matching-braces"></a>演练：显示匹配括号
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以通过定义要匹配的大括号来实现基于语言的功能（如大括号匹配），然后在插入符号位于其中一个大括号中时向匹配大括号添加文本标记标记。 你可以在语言上下文中定义大括号，或者可以定义自己的文件扩展名和内容类型，并将标记应用到该类型，也可以将标记应用于现有内容类型 (如 "text" ) 。 下面的演练演示如何将大括号匹配标记应用于 "text" 内容类型。  
  
## <a name="prerequisites"></a>必备条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="implementing-a-brace-matching-tagger"></a>实现括号匹配标记  
 若要获取类似于在 Visual Studio 中使用的大括号突出显示效果，可以实现类型的标记 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。 下面的代码演示如何在任何嵌套级别为大括号对定义标记。 在此示例中，大括号对 []。 [] 和 {} 是在标记构造函数中定义的，但在完整语言实现中，将在语言规范中定义相关的大括号对。  
  
#### <a name="to-implement-a-brace-matching-tagger"></a>实现括号匹配标记  
  
1. 添加一个类文件并将其命名为 BraceMatching。  
  
2. 导入以下命名空间。  
  
     [!code-csharp[VSSDKBraceMatchingTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#1)]
     [!code-vb[VSSDKBraceMatchingTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#1)]  
  
3. 定义 `BraceMatchingTagger` 从类型继承的类 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。  
  
     [!code-csharp[VSSDKBraceMatchingTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#2)]
     [!code-vb[VSSDKBraceMatchingTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#2)]  
  
4. 添加文本视图的属性、源缓冲区和当前快照点，还添加一组大括号对。  
  
     [!code-csharp[VSSDKBraceMatchingTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#3)]
     [!code-vb[VSSDKBraceMatchingTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#3)]  
  
5. 在标记构造函数中，设置属性并订阅视图更改事件 <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> 和 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 。 在此示例中，出于演示目的，也在构造函数中定义了匹配对。  
  
     [!code-csharp[VSSDKBraceMatchingTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#4)]
     [!code-vb[VSSDKBraceMatchingTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#4)]  
  
6. 作为实现的一部分 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> ，请声明一个 TagsChanged 事件。  
  
     [!code-csharp[VSSDKBraceMatchingTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#5)]
     [!code-vb[VSSDKBraceMatchingTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#5)]  
  
7. 事件处理程序更新属性的当前脱字号位置 `CurrentChar` ，并引发 TagsChanged 事件。  
  
     [!code-csharp[VSSDKBraceMatchingTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#6)]
     [!code-vb[VSSDKBraceMatchingTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#6)]  
  
8. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>当当前字符为左大括号时，或在上一个字符为右大括号（如 Visual Studio 中）时，实现方法来匹配大括号。 当找到匹配项时，此方法将实例化两个标记，一个用于左大括号，另一个用于右大括号。  
  
     [!code-csharp[VSSDKBraceMatchingTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#7)]
     [!code-vb[VSSDKBraceMatchingTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#7)]  
  
9. 以下私有方法查找任何嵌套级别的匹配大括号。 第一种方法查找匹配左字符的接近字符：  
  
     [!code-csharp[VSSDKBraceMatchingTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#8)]
     [!code-vb[VSSDKBraceMatchingTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#8)]  
  
10. 以下 helper 方法查找与 close 字符匹配的开放字符：  
  
     [!code-csharp[VSSDKBraceMatchingTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#9)]
     [!code-vb[VSSDKBraceMatchingTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#9)]  
  
## <a name="implementing-a-brace-matching-tagger-provider"></a>实现与标记提供程序匹配的大括号  
 除了实现标记外，还必须实现和导出标记提供程序。 在这种情况下，提供程序的内容类型为 "text"。 这意味着，大括号匹配将显示在所有类型的文本文件中，但更完整的实现会将大括号匹配仅应用于特定内容类型。  
  
#### <a name="to-implement-a-brace-matching-tagger-provider"></a>实现与标记提供程序匹配的大括号  
  
1. 声明从继承的标记提供程序 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> ，将其命名为 BraceMatchingTaggerProvider，然后将其导出为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" 和 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> 的 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。  
  
     [!code-csharp[VSSDKBraceMatchingTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#10)]
     [!code-vb[VSSDKBraceMatchingTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#10)]  
  
2. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> 方法以实例化 BraceMatchingTagger。  
  
     [!code-csharp[VSSDKBraceMatchingTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#11)]
     [!code-vb[VSSDKBraceMatchingTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#11)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，请生成 BraceMatchingTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-bracematchingtest-solution"></a>生成和测试 BraceMatchingTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本，其中包含匹配的大括号。  
  
    ```  
    hello {  
    goodbye}  
  
    {}  
  
    {hello}  
    ```  
  
4. 将插入符号放置在左大括号前时，应突出显示这两个大括号和匹配的右大括号。 将光标置于右大括号之后时，应突出显示这两个大括号和匹配的左大括号。  
  
## <a name="see-also"></a>另请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
