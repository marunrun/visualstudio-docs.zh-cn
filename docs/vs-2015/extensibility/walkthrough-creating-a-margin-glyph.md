---
title: 演练：创建边缘字形 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa18b900ca44fbb52c646bfdf021beed6e77f504
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148847"
---
# <a name="walkthrough-creating-a-margin-glyph"></a>演练：创建边缘字形
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用自定义编辑器扩展自定义编辑器边距的外观。 本演练中放入自定义标志符号指示器边距时代码注释中显示单词"todo"。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `TodoGlyphTest`。  
  
2. 添加编辑器分类器项目项。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="defining-the-glyph"></a>定义标志符号  
 通过实现定义标志符号<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>接口。  
  
#### <a name="to-define-the-glyph"></a>若要定义标志符号  
  
1. 添加一个类文件并将其命名为 `TodoGlyphFactory`。  
  
2. 添加以下 using 声明。  
  
     [!code-csharp[VSSDKTodoGlyphTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#1)]
     [!code-vb[VSSDKTodoGlyphTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#1)]  
  
3. 添加名为的类`TodoGlyphFactory`实现<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>。  
  
     [!code-csharp[VSSDKTodoGlyphTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#2)]
     [!code-vb[VSSDKTodoGlyphTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#2)]  
  
4. 添加定义标志符号尺寸的私有字段。  
  
     [!code-csharp[VSSDKTodoGlyphTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#3)]
     [!code-vb[VSSDKTodoGlyphTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#3)]  
  
5. 实现`GenerateGlyph`通过定义标志符号的用户界面 (UI) 元素。 `TodoTag` 稍后在本演练中定义。  
  
     [!code-csharp[VSSDKTodoGlyphTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#4)]
     [!code-vb[VSSDKTodoGlyphTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#4)]  
  
6. 添加名为的类`TodoGlyphFactoryProvider`实现<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider>。 导出使用此类<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"TodoGlyph"<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>的后 VsTextMarker<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"代码"和一个<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>TodoTag。  
  
     [!code-csharp[VSSDKTodoGlyphTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#5)]
     [!code-vb[VSSDKTodoGlyphTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#5)]  
  
7. 实现<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>方法通过实例化`TodoGlyphFactory`。  
  
     [!code-csharp[VSSDKTodoGlyphTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#6)]
     [!code-vb[VSSDKTodoGlyphTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#6)]  
  
## <a name="defining-a-todo-tag-and-tagger"></a>定义 Todo 标记和标记器  
 通过创建标记类型和标记器，并将其导出使用标记器提供程序定义的上一步骤中定义的用户界面元素和指示器边距之间的关系。  
  
#### <a name="to-define-a-todo-tag-and-tagger"></a>若要定义 todo 标记和标记器  
  
1. 向项目添加一个新类文件并将其命名`TodoTagger`。  
  
2. 添加以下导入。  
  
     [!code-csharp[VSSDKTodoGlyphTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#7)]
     [!code-vb[VSSDKTodoGlyphTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#7)]  
  
3. 添加一个名为类`TodoTag`。  
  
     [!code-csharp[VSSDKTodoGlyphTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#8)]
     [!code-vb[VSSDKTodoGlyphTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#8)]  
  
4. 修改名为的类`TodoTagger`，它实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>类型的`TodoTag`。  
  
     [!code-csharp[VSSDKTodoGlyphTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#9)]
     [!code-vb[VSSDKTodoGlyphTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#9)]  
  
5. 向`TodoTagger`类中，添加私有字段<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>和要查找的分类中的文本的跨度。  
  
     [!code-csharp[VSSDKTodoGlyphTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#10)]
     [!code-vb[VSSDKTodoGlyphTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#10)]  
  
6. 添加设置的分类器的构造函数。  
  
     [!code-csharp[VSSDKTodoGlyphTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#11)]
     [!code-vb[VSSDKTodoGlyphTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#11)]  
  
7. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>通过查找所有分类的方法跨其名称中包含单词"注释"，以及其中的文本包括搜索文本。 只要找到搜索文本，重新生成一个新<xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601>类型的`TodoTag`。  
  
     [!code-csharp[VSSDKTodoGlyphTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#12)]
     [!code-vb[VSSDKTodoGlyphTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#12)]  
  
8. 声明`TagsChanged`事件。  
  
     [!code-csharp[VSSDKTodoGlyphTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#13)]
     [!code-vb[VSSDKTodoGlyphTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#13)]  
  
9. 添加名为的类`TodoTaggerProvider`，它实现<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>，并将其与导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"代码"和一个<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>TodoTag。  
  
     [!code-csharp[VSSDKTodoGlyphTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#14)]
     [!code-vb[VSSDKTodoGlyphTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#14)]  
  
10. 导入<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>。  
  
     [!code-csharp[VSSDKTodoGlyphTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#15)]
     [!code-vb[VSSDKTodoGlyphTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#15)]  
  
11. 实现<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>方法通过实例化`TodoTagger`。  
  
     [!code-csharp[VSSDKTodoGlyphTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#16)]
     [!code-vb[VSSDKTodoGlyphTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#16)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 TodoGlyphTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-todoglyphtest-solution"></a>若要生成和测试 TodoGlyphTest 解决方案  
  
1. 生成解决方案。  
  
2. 通过按 F5 运行项目。 Visual Studio 的第二个实例进行实例化。  
  
3. 请确保显示指示器边距。 (在**工具**菜单上，单击**选项**。 在**文本编辑器**页上，请确保**指示器边距**处于选中状态。)  
  
4. 打开具有注释的代码文件。 将单词"todo"添加到注释部分之一。  
  
5. 将具有深蓝色的轮廓的浅蓝色圆形应出现在代码窗口左侧的指示器边距。
