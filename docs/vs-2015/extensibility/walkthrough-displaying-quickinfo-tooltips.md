---
title: 演练：显示 QuickInfo 工具提示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3b349f0293071dfa30677b7558ca93985d16d55e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840579"
---
# <a name="walkthrough-displaying-quickinfo-tooltips"></a>演练：显示 QuickInfo 工具提示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

QuickInfo 是一项 IntelliSense 功能，当用户将指针移到方法名称上时，它将显示方法签名和说明。 可以通过定义要为其提供 QuickInfo 说明的标识符，然后创建用于显示内容的工具提示，来实现基于语言的功能（如 QuickInfo）。 你可以在语言服务的上下文中定义 QuickInfo，或者可以定义自己的文件扩展名和内容类型，并只为该类型显示 QuickInfo，也可以为现有内容类型 (如 "text" ) 显示 QuickInfo。 本演练演示如何为 "文本" 内容类型显示 QuickInfo。  
  
 本演练中的 QuickInfo 示例将在用户将指针移到方法名称上时显示工具提示。 此设计要求实现以下四个接口：  
  
- 源接口  
  
- 源提供程序接口  
  
- 控制器接口  
  
- 控制器提供程序接口  
  
  源和控制器提供程序 Managed Extensibility Framework (MEF) 组件部件，并负责导出源和控制器类，以及导入服务和代理（例如 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> ），后者将创建工具提示文本缓冲区和，这会 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> 触发 QuickInfo 会话。  
  
  在此示例中，QuickInfo 源使用方法名称和说明的硬编码列表，但在完整实现中，语言服务和语言文档负责提供该内容。  
  
## <a name="prerequisites"></a>先决条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建 c # VSIX 项目。  (在 " **新建项目** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。 ) 将解决方案命名为 `QuickInfoTest` 。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
## <a name="implementing-the-quickinfo-source"></a>实现 QuickInfo 源  
 QuickInfo 源负责收集标识符集及其说明，并在遇到某个标识符时将内容添加到工具提示文本缓冲区。 在此示例中，标识符和它们的说明只添加在源构造函数中。  
  
#### <a name="to-implement-the-quickinfo-source"></a>实现 QuickInfo 源  
  
1. 添加一个类文件并将其命名为 `TestQuickInfoSource`。  
  
2. 添加对 VisualStudio 的引用。  
  
3. 添加以下 import 语句。  
  
     [!code-csharp[VSSDKQuickInfoTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#1)]
     [!code-vb[VSSDKQuickInfoTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#1)]  
  
4. 声明一个实现的类 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> ，并将其命名为 `TestQuickInfoSource` 。  
  
     [!code-csharp[VSSDKQuickInfoTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#2)]
     [!code-vb[VSSDKQuickInfoTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#2)]  
  
5. 为 QuickInfo 源提供程序、文本缓冲区和一组方法名称和方法签名添加字段。 在此示例中，方法名称和签名在构造函数中进行初始化 `TestQuickInfoSource` 。  
  
     [!code-csharp[VSSDKQuickInfoTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#3)]
     [!code-vb[VSSDKQuickInfoTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#3)]  
  
6. 添加一个构造函数，用于设置 QuickInfo 源提供程序和文本缓冲区，并填充方法名称的集合以及方法签名和说明。  
  
     [!code-csharp[VSSDKQuickInfoTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#4)]
     [!code-vb[VSSDKQuickInfoTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#4)]  
  
7. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> 方法。 在此示例中，方法查找当前单词，如果光标位于行尾或文本缓冲区，则查找上一个单词。 如果该单词为方法名称之一，则该方法名称的说明将添加到 QuickInfo 内容。  
  
     [!code-csharp[VSSDKQuickInfoTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#5)]
     [!code-vb[VSSDKQuickInfoTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#5)]  
  
8. 还必须实现 Dispose ( # A1 方法，因为它 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> 实现 <xref:System.IDisposable> ：  
  
     [!code-csharp[VSSDKQuickInfoTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#6)]
     [!code-vb[VSSDKQuickInfoTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#6)]  
  
## <a name="implementing-a-quickinfo-source-provider"></a>实现 QuickInfo 源提供程序  
 QuickInfo 源的提供程序主要用于将自身导出为 MEF 组件部件并实例化 QuickInfo 源。 由于它是一个 MEF 组件部件，因此它可以导入其他 MEF 组件部件。  
  
#### <a name="to-implement-a-quickinfo-source-provider"></a>实现 QuickInfo 源提供程序  
  
1. 声明一个名为的 QuickInfo 源提供程序， `TestQuickInfoSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider> 并将其导出为 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip QuickInfo Source"、 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default" 和 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" 的。  
  
     [!code-csharp[VSSDKQuickInfoTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#7)]
     [!code-vb[VSSDKQuickInfoTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#7)]  
  
2. 导入两个编辑器服务 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 和 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> ，作为的属性 `TestQuickInfoSourceProvider` 。  
  
     [!code-csharp[VSSDKQuickInfoTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#8)]
     [!code-vb[VSSDKQuickInfoTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#8)]  
  
3. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> 以返回一个新的 `TestQuickInfoSource` 。  
  
     [!code-csharp[VSSDKQuickInfoTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#9)]
     [!code-vb[VSSDKQuickInfoTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#9)]  
  
## <a name="implementing-a-quickinfo-controller"></a>实现 QuickInfo 控制器  
 QuickInfo 控制器确定何时应显示 QuickInfo。 在此示例中，当指针位于与方法名称之一相对应的单词上时，将显示 QuickInfo。 QuickInfo 控制器实现了一个触发 QuickInfo 会话的鼠标悬停事件处理程序。  
  
#### <a name="to-implement-a-quickinfo-controller"></a>实现 QuickInfo 控制器  
  
1. 声明一个实现的类 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> ，并将其命名为 `TestQuickInfoController` 。  
  
     [!code-csharp[VSSDKQuickInfoTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#10)]
     [!code-vb[VSSDKQuickInfoTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#10)]  
  
2. 为文本视图、在文本视图中表示的文本缓冲区、QuickInfo 会话和 QuickInfo 控制器提供程序添加私有字段。  
  
     [!code-csharp[VSSDKQuickInfoTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#11)]
     [!code-vb[VSSDKQuickInfoTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#11)]  
  
3. 添加一个构造函数，该构造函数设置字段并添加鼠标悬停事件处理程序。  
  
     [!code-csharp[VSSDKQuickInfoTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#12)]
     [!code-vb[VSSDKQuickInfoTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#12)]  
  
4. 添加触发 QuickInfo 会话的鼠标悬停事件处理程序。  
  
     [!code-csharp[VSSDKQuickInfoTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#13)]
     [!code-vb[VSSDKQuickInfoTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#13)]  
  
5. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A> 方法，以便在从文本视图分离控制器时删除鼠标悬停事件处理程序。  
  
     [!code-csharp[VSSDKQuickInfoTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#14)]
     [!code-vb[VSSDKQuickInfoTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#14)]  
  
6. 在 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A> 此示例中，将方法和 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> 方法实现为空方法。  
  
     [!code-csharp[VSSDKQuickInfoTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#15)]
     [!code-vb[VSSDKQuickInfoTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#15)]  
  
## <a name="implementing-the-quickinfo-controller-provider"></a>实现 QuickInfo 控制器提供程序  
 QuickInfo 控制器的提供程序主要用于将自身导出为 MEF 组件部件并实例化 QuickInfo 控制器。 由于它是一个 MEF 组件部件，因此它可以导入其他 MEF 组件部件。  
  
#### <a name="to-implement-the-quickinfo-controller-provider"></a>实现 QuickInfo 控制器提供程序  
  
1. 声明一个名为的类，该类 `TestQuickInfoControllerProvider` 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider> ，并使用 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip QuickInfo 控制器" 和 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" 的进行导出：  
  
     [!code-csharp[VSSDKQuickInfoTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#16)]
     [!code-vb[VSSDKQuickInfoTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#16)]  
  
2. 将 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> 作为属性导入。  
  
     [!code-csharp[VSSDKQuickInfoTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#17)]
     [!code-vb[VSSDKQuickInfoTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#17)]  
  
3. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A>通过实例化 QuickInfo 控制器来实现方法。  
  
     [!code-csharp[VSSDKQuickInfoTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#18)]
     [!code-vb[VSSDKQuickInfoTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#18)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，请生成 QuickInfoTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-quickinfotest-solution"></a>生成和测试 QuickInfoTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本，其中包含 "add" 和 "减法" 字样。  
  
4. 将指针移到 "添加" 的一个匹配项上方。 应显示该方法的签名和说明 `add` 。  
  
## <a name="see-also"></a>另请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
