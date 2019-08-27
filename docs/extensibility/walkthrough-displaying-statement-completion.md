---
title: 演练：显示语句完成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f117209c8e1d57c64ab53df608fe55ae27f0cff0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312406"
---
# <a name="walkthrough-display-statement-completion"></a>演练：显示语句完成
可以通过定义您想要提供完成的标识符，然后触发完成会话实现的基于语言的语句结束。 可以在语言服务的上下文中定义的语句结束、 定义您自己的文件扩展名和内容类型，然后显示完成只是该类型。 或者，可以触发的现有内容类型完成 — 例如，"纯文本"。 本演练演示如何触发"纯文本"内容类型，这是文本文件的内容类型的语句完成。 "Text"内容类型是所有其他内容类型，包括代码和 XML 文件的上级。

 通过键入某些字符通常触发语句完成 — 例如，通过键入如"使用"标识符的开头。 它通常通过按来取消**空格键**，**选项卡**，或**Enter**键以提交所选内容。 您可以实现通过击键命令处理程序中键入字符时触发的 IntelliSense 功能 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口) 和实现的处理程序提供程序<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>接口。 若要创建完成源时，这是参与完成的标识符的列表，实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>接口和完成源提供程序 (<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>接口)。 提供商将 Managed Extensibility Framework (MEF) 组件部分。 它们是负责导出的源和控制器类和导入服务和代理 — 例如， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，这样文本缓冲区中的导航和<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>，随即将会触发完成会话。

 本演练演示如何实现硬编码的一组标识符的语句完成。 在完全实现中，语言服务和语言文档是负责提供该内容。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，不要从下载中心安装 Visual Studio SDK。 它包含作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

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

## <a name="implement-the-completion-source"></a>实现完成源
 完成源是负责收集组标识符，并将内容添加到完成窗口中，当用户键入完成触发器，例如标识符的第一个字母。 在此示例中，标识符和及其说明是硬编码在<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>方法。 在大多数实际使用时，将使用你的语言分析器以获取令牌，填充的完成列表。

### <a name="to-implement-the-completion-source"></a>若要实现完成源

1. 添加一个类文件并将其命名为 `TestCompletionSource`。

2. 添加这些导入：

     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]

3. 修改的类声明`TestCompletionSource`，以便实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>:

     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]

4. 添加私有字段的源提供程序、 文本缓冲区和一系列<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>对象 （分别对应于将参与完成会话的标识符）：

     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]

5. 添加设置的源提供程序和缓冲区的构造函数。 `TestCompletionSourceProvider`在后续步骤中定义类：

     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]

6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>想要提供的上下文中通过添加包含完成一完成组的方法。 每个完成项集合包含一组<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>完成，并对应于完成窗口的选项卡。 (在 Visual Basic 项目中，完成窗口选项卡名为**常见**并**所有**。)下一步中将定义 `FindTokenSpanAtPosition` 方法。

     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]

7. 使用以下方法查找当前单词从光标的位置：

     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]

8. 实现`Dispose()`方法：

     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]

## <a name="implement-the-completion-source-provider"></a>实现完成源提供程序
 完成源提供程序是实例化完成源的 MEF 组件部分。

### <a name="to-implement-the-completion-source-provider"></a>若要实现完成源提供程序

1. 添加名为的类`TestCompletionSourceProvider`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>。 导出使用此类<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"纯文本"和一个<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"测试完成"。

     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]

2. 导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，这在完成源中查找当前的单词。

     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]

3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A>方法实例化完成源。

     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]

## <a name="implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序
 完成命令处理程序提供程序派生自<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>，它侦听文本视图创建事件并将从该视图转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>— 这样添加到 Visual Studio shell 的命令链命令 —到<xref:Microsoft.VisualStudio.Text.Editor.ITextView>. 由于此类是 MEF 导出，也可以使用导入所需的命令处理程序本身的服务

#### <a name="to-implement-the-completion-command-handler-provider"></a>若要实现完成命令处理程序提供程序

1. 添加名为的文件`TestCompletionCommandHandler`。

2. 添加以下 using 语句：

     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]

3. 添加名为的类`TestCompletionHandlerProvider`实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>。 导出使用此类<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"标记完成处理程序"<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"纯文本"和一个<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>的<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>。

     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]

4. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>，这样从转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>到<xref:Microsoft.VisualStudio.Text.Editor.ITextView>即<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>，和一个<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>，可以访问标准 Visual Studio 服务。

     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]

5. 实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>方法可实例化的命令处理程序。

     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]

## <a name="implement-the-completion-command-handler"></a>实现完成命令处理程序
 由于通过击键触发语句完成时，您必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口来接收和处理的键击触发、 提交和关闭完成会话。

#### <a name="to-implement-the-completion-command-handler"></a>若要实现完成命令处理程序

1. 添加名为的类`TestCompletionCommandHandler`实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:

    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]

2. 添加私有字段 （向其传递该命令） 的下一个命令处理程序、 文本视图、 命令处理程序提供程序，（这样就能够对各种服务的访问），并完成会话：

    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]

3. 添加设置文本视图和提供程序字段中，并将命令添加到命令链的构造函数：

    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]

4. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法并传递该命令传递给：

    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 当此方法将接收击键时，它必须执行这些操作之一：

   - 允许的字符写入到缓冲区，并触发或筛选完成。 （打印字符执行此操作。）

   - 提交完成，但不是允许写入到缓冲区的字符。 (空格、**选项卡**，并**Enter**显示完成会话时执行此操作。)

   - 允许要传递到下一个处理程序的命令。 （所有其他命令。）

     由于此方法可能会显示 UI，请调用<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A>以确保它不调用自动化上下文中：

     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]

6. 此代码是触发完成会话的私有方法：

    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]

7. 下一个示例是一个专用方法，从取消订阅<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed>事件：

    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，生成 CompletionTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-completiontest-solution"></a>若要生成和测试 CompletionTest 解决方案

1. 生成解决方案。

2. 当在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包括单词"添加"。

4. 当您第一次键入"a"，然后"d"时，应显示一个列表，其中包含"加法"和"改写"。 请注意，选择添加。 当你键入另一个"d"时，列表应包含仅"加法"，现在处于选中状态。 您可以通过按提交"加法"**空格键**，**选项卡**，或**Enter**键，或通过键入 Esc 或按任意键关闭该列表。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到的文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)