---
title: 演练：显示语句完成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
caps.latest.revision: 37
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: db4e63beb1e3d4ff53e547492ae9eae7ee8001e8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202014"
---
# <a name="walkthrough-displaying-statement-completion"></a>演练：显示语句完成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过定义您想要提供完成的标识符，然后触发完成会话实现的基于语言的语句结束。 可以定义的语言服务上下文中的语句完成、 定义您自己的文件扩展名和内容类型，然后显示完成只是该类型，或者可以触发的现有内容类型完成 — 例如，"纯文本"。 本演练演示如何触发"纯文本"内容类型，这是文本文件的内容类型的语句完成。 "Text"内容类型是所有其他内容类型，包括代码和 XML 文件的上级。  
  
 通过键入某些字符通常触发语句完成 — 例如，通过键入如"使用"标识符的开头。 它通常被按下空格键、 Tab 或 Enter 键以提交所选内容。 您可以实现由键入字符的击键使用命令处理程序触发的 IntelliSense 功能 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口) 和实现的处理程序提供程序<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>接口。 若要创建完成源时，这是参与完成的标识符的列表，实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>接口和完成源提供程序 (<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>接口)。 提供商将 Managed Extensibility Framework (MEF) 组件部分。 他们负责导出的源和控制器类和导入服务和代理 — 例如， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，这样文本缓冲区中的导航和<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>，随即将会触发完成会话。  
  
 本演练演示如何实现硬编码的一组标识符的语句完成。 在完全实现中，语言服务和语言文档是负责提供该内容。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `CompletionTest`。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
4. 添加对项目的以下引用并确保选中**CopyLocal**设置为`false`:  
  
     Microsoft.VisualStudio.Editor  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     Microsoft.VisualStudio.Shell.14.0  
  
     Microsoft.VisualStudio.Shell.Immutable.10.0  
  
     Microsoft.VisualStudio.TextManager.Interop  
  
## <a name="implementing-the-completion-source"></a>实现完成源  
 完成源是负责收集组标识符，并将内容添加到完成窗口中，当用户键入完成触发器，例如标识符的第一个字母。 在此示例中，标识符和及其说明是硬编码在<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>方法。 在大多数实际使用时，将使用你的语言分析器以获取令牌，填充的完成列表。  
  
#### <a name="to-implement-the-completion-source"></a>若要实现完成源  
  
1. 添加一个类文件并将其命名为 `TestCompletionSource`。  
  
2. 添加这些导入：  
  
     [!code-csharp[VSSDKCompletionTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#1)]
     [!code-vb[VSSDKCompletionTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#1)]  
  
3. 修改的类声明`TestCompletionSource`，以便实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>:  
  
     [!code-csharp[VSSDKCompletionTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#2)]
     [!code-vb[VSSDKCompletionTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#2)]  
  
4. 添加私有字段的源提供程序、 文本缓冲区和一系列<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>对象 （分别对应于将参与完成会话的标识符）：  
  
     [!code-csharp[VSSDKCompletionTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#3)]
     [!code-vb[VSSDKCompletionTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#3)]  
  
5. 添加设置的源提供程序和缓冲区的构造函数。 `TestCompletionSourceProvider`在后续步骤中定义类：  
  
     [!code-csharp[VSSDKCompletionTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#4)]
     [!code-vb[VSSDKCompletionTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#4)]  
  
6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>想要提供的上下文中通过添加包含完成一完成组的方法。 每个完成项集合包含一组<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>完成，并对应于完成窗口的选项卡。 (在 Visual Basic 项目中，完成窗口选项卡名为**常见**并**所有**。)FindTokenSpanAtPosition 方法是在下一步中定义的。  
  
     [!code-csharp[VSSDKCompletionTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#5)]
     [!code-vb[VSSDKCompletionTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#5)]  
  
7. 使用以下方法查找当前单词从光标的位置：  
  
     [!code-csharp[VSSDKCompletionTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#6)]
     [!code-vb[VSSDKCompletionTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#6)]  
  
8. 实现`Dispose()`方法：  
  
     [!code-csharp[VSSDKCompletionTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#7)]
     [!code-vb[VSSDKCompletionTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#7)]  
  
## <a name="implementing-the-completion-source-provider"></a>实现完成源提供程序  
 完成源提供程序是实例化完成源的 MEF 组件部分。  
  
#### <a name="to-implement-the-completion-source-provider"></a>若要实现完成源提供程序  
  
1. 添加名为的类`TestCompletionSourceProvider`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>。 导出使用此类<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"纯文本"和一个<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"测试完成"。  
  
     [!code-csharp[VSSDKCompletionTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#8)]
     [!code-vb[VSSDKCompletionTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#8)]  
  
2. 导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，用于完成源中查找当前的单词。  
  
     [!code-csharp[VSSDKCompletionTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#9)]
     [!code-vb[VSSDKCompletionTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#9)]  
  
3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A>方法实例化完成源。  
  
     [!code-csharp[VSSDKCompletionTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#10)]
     [!code-vb[VSSDKCompletionTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#10)]  
  
## <a name="implementing-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序  
 完成命令处理程序提供程序派生自<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>，它侦听文本视图创建事件并将从该视图转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>— 这样添加到 Visual Studio shell 的命令链命令 —到<xref:Microsoft.VisualStudio.Text.Editor.ITextView>. 由于此类是 MEF 导出，也可以使用导入所需的命令处理程序本身的服务  
  
#### <a name="to-implement-the-completion-command-handler-provider"></a>若要实现完成命令处理程序提供程序  
  
1. 添加名为的文件`TestCompletionCommandHandler`。  
  
2. 添加以下 using 语句：  
  
     [!code-csharp[VSSDKCompletionTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#11)]
     [!code-vb[VSSDKCompletionTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#11)]  
  
3. 添加名为的类`TestCompletionHandlerProvider`实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>。 导出使用此类<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"标记完成处理程序"<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"纯文本"和一个<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>的<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>。  
  
     [!code-csharp[VSSDKCompletionTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#12)]
     [!code-vb[VSSDKCompletionTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#12)]  
  
4. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>，这样从转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>到<xref:Microsoft.VisualStudio.Text.Editor.ITextView>即<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>，和一个<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>，可以访问标准 Visual Studio 服务。  
  
     [!code-csharp[VSSDKCompletionTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#13)]
     [!code-vb[VSSDKCompletionTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#13)]  
  
5. 实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>方法可实例化的命令处理程序。  
  
     [!code-csharp[VSSDKCompletionTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#14)]
     [!code-vb[VSSDKCompletionTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#14)]  
  
## <a name="implementing-the-completion-command-handler"></a>实现完成命令处理程序  
 由于通过击键触发语句完成时，您必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口来接收和处理的键击触发、 提交和关闭完成会话。  
  
#### <a name="to-implement-the-completion-command-handler"></a>若要实现完成命令处理程序  
  
1. 添加名为的类`TestCompletionCommandHandler`实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:  
  
    [!code-csharp[VSSDKCompletionTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#15)]
    [!code-vb[VSSDKCompletionTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#15)]  
  
2. 添加私有字段 （向其传递该命令） 的下一个命令处理程序、 文本视图、 命令处理程序提供程序，（这样就能够对各种服务的访问），并完成会话：  
  
    [!code-csharp[VSSDKCompletionTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#16)]
    [!code-vb[VSSDKCompletionTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#16)]  
  
3. 添加设置文本视图和提供程序字段中，并将命令添加到命令链的构造函数：  
  
    [!code-csharp[VSSDKCompletionTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#17)]
    [!code-vb[VSSDKCompletionTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#17)]  
  
4. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法并传递该命令传递给：  
  
    [!code-csharp[VSSDKCompletionTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#18)]
    [!code-vb[VSSDKCompletionTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#18)]  
  
5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 当此方法将接收击键时，它必须执行这些操作之一：  
  
   - 允许的字符写入到缓冲区，并触发或筛选完成。 （打印字符执行此操作。）  
  
   - 提交完成，但不是允许写入到缓冲区的字符。 （空格、 制表符和 Enter 执行此操作显示完成会话时。）  
  
   - 允许要传递到下一个处理程序的命令。 （所有其他命令。）  
  
     由于此方法可能会显示 UI，请调用<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A>以确保它不调用自动化上下文中：  
  
     [!code-csharp[VSSDKCompletionTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#19)]
     [!code-vb[VSSDKCompletionTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#19)]  
  
6. 此代码是触发完成会话的私有方法：  
  
    [!code-csharp[VSSDKCompletionTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#20)]
    [!code-vb[VSSDKCompletionTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#20)]  
  
7. 下一个示例是一个专用方法，从取消订阅<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed>事件：  
  
    [!code-csharp[VSSDKCompletionTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#21)]
    [!code-vb[VSSDKCompletionTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#21)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 CompletionTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-completiontest-solution"></a>若要生成和测试 CompletionTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本，其中包括单词"添加"。  
  
4. 当您第一次键入"a"，然后"d"时，应显示一个列表，其中包含"加法"和"改写"。 请注意，选择添加。 当你键入另一个"d"时，列表应包含仅"加法"，现在处于选中状态。 可以通过按空格键、 Tab 或 Enter 键，提交"添加"，也可以通过键入 Esc 或按任意键关闭该列表。  
  
## <a name="see-also"></a>请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
