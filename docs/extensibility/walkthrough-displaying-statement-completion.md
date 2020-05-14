---
title: 演练：显示语句完成 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: acangialosi
ms.author: anthc
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 1d2f5499511c9dc0bbb6711d0da630315384f8e7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697411"
---
# <a name="walkthrough-display-statement-completion"></a>演练：显示语句完成
可以通过定义要为其提供完成的标识符，然后触发完成会话来实现基于语言的语句完成。 您可以在语言服务的上下文中定义语句完成，定义自己的文件名扩展名和内容类型，然后仅显示该类型的完成情况。 或者，您可以触发现有内容类型的完成，例如"纯文本"。 本演练演示如何为"纯文本"内容类型（即文本文件的内容类型）触发语句完成。 "文本"内容类型是所有其他内容类型（包括代码和 XML 文件）的祖先。

 语句完成通常是通过键入某些字符触发的，例如，通过键入标识符的开头（如"使用"）。 它通常通过按**空格键**、**选项卡**或**Enter**键来提交选择来消除。 通过使用击键（<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口）的命令处理程序和实现接口的处理程序提供程序，可以实现在键入字符时触发的<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>IntelliSense 功能。 要创建完成源（即参与完成的标识符列表），请实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>接口和完成源提供程序（<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>接口）。 提供程序是托管扩展框架 （MEF） 组件部件。 他们负责导出源类和控制器类以及导入服务和代理（例如，<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>启用文本缓冲区中的导航的 和 触发完成会话的 。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>

 本演练演示如何实现硬编码标识符集的语句完成。 在完全实现中，语言服务和语言文档负责提供该内容。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`CompletionTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 添加对项目的以下引用，并确保**CopyLocal**设置为`false`：

     微软.VisualStudio.编辑器

     Microsoft.VisualStudio.Language.Intellisense

     微软.VisualStudio.OLE.Interop

     微软.VisualStudio.shell.15.0

     微软.VisualStudio.shell.不可改变.10.0

     微软.VisualStudio.文本管理器.互通

## <a name="implement-the-completion-source"></a>实现完成源
 当用户键入完成触发器（如标识符的第一个字母）时，完成源负责收集标识符集并将内容添加到完成窗口。 在此示例中，标识符及其描述在<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>方法中硬编码。 在大多数实际使用中，您将使用语言的解析器来获取令牌来填充完成列表。

### <a name="to-implement-the-completion-source"></a>实现完成源

1. 添加一个类文件并将其命名为 `TestCompletionSource`。

2. 添加以下导入：

     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]

3. 修改类声明，`TestCompletionSource`以便实现<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>：

     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]

4. 为源提供程序、文本缓冲区和<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>对象列表添加私有字段（对应于将参与完成会话的标识符）：

     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]

5. 添加设置源提供程序和缓冲区的构造函数。 类`TestCompletionSourceProvider`在后续步骤中定义：

     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]

6. 通过添加<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>包含要在上下文中提供的完成完成的完成集来实现该方法。 每个完成集包含一组<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>完成，并对应于完成窗口的选项卡。 （在可视化基本项目中，完成窗口选项卡名为 **"通用****"和"全部**"。"该方法`FindTokenSpanAtPosition`在下一步中定义。

     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]

7. 以下方法用于从光标的位置查找当前单词：

     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]

8. 实现方法`Dispose()`：

     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]

## <a name="implement-the-completion-source-provider"></a>实现完成源提供程序
 完成源提供程序是实例化完成源的 MEF 组件部分。

### <a name="to-implement-the-completion-source-provider"></a>实现完成源提供程序

1. 添加名为`TestCompletionSourceProvider`的类<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>，实现 。 使用<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"纯文本"和"测试完成"导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>此类。

     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]

2. 导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，在完成源中查找当前单词。

     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]

3. 实现实例<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A>化完成源的方法。

     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]

## <a name="implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序
 完成命令处理程序提供程序派生自 ，<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>它侦听文本视图创建事件，并将视图从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>- 启用将命令添加到 Visual Studio shell 的命令链 —<xref:Microsoft.VisualStudio.Text.Editor.ITextView>到 。 由于此类是 MEF 导出，因此还可以使用它导入命令处理程序本身所需的服务。

#### <a name="to-implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序

1. 添加名为 的文件`TestCompletionCommandHandler`。

2. 使用指令添加这些指令：

     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]

3. 添加名为`TestCompletionHandlerProvider`的类<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>，实现 。 使用<xref:Microsoft.VisualStudio.Utilities.NameAttribute>"令牌完成处理程序"、"<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>纯文本"和 a<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>导出此类。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>

     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]

4. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>， 启用从 转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>到<xref:Microsoft.VisualStudio.Text.Editor.ITextView>，<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>和<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>， 允许访问标准 Visual Studio 服务。

     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]

5. 实现该方法<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>以实例化命令处理程序。

     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]

## <a name="implement-the-completion-command-handler"></a>实现完成命令处理程序
 由于语句完成是由击键触发的，因此必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口来接收和处理触发、提交和关闭完成会话的击键。

#### <a name="to-implement-the-completion-command-handler"></a>实现完成命令处理程序

1. 添加名为的`TestCompletionCommandHandler`类，该<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>类实现 ：

    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]

2. 为下一个命令处理程序（将命令传递给该命令）、文本视图、命令处理程序提供程序（允许访问各种服务）和完成会话添加私有字段：

    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]

3. 添加一个构造函数，用于设置文本视图和提供程序字段，并将命令添加到命令链：

    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]

4. 通过传递<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>命令来实现方法：

    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 当此方法收到击键时，它必须执行以下操作之一：

   - 允许将字符写入缓冲区，然后触发或筛选完成。 （打印字符执行此操作。

   - 提交完成，但不允许将字符写入缓冲区。 （显示完成会话时，将执行此操作，为"空格 **"、"选项卡**"和"**输入**"。

   - 允许将命令传递给下一个处理程序。 （所有其他命令。

     由于此方法可能会显示 UI，因此<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A>调用以确保在自动化上下文中不调用它：

     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]

6. 此代码是触发完成会话的私有方法：

    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]

7. 下一个示例是取消订阅事件的<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed>私有方法：

    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请生成完成测试解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-completiontest-solution"></a>构建和测试完成测试解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件并键入一些包含"添加"字的文本。

4. 当您先键入"a"，然后键入"d"时，应显示包含"添加"和"适应"的列表。 请注意，已选择添加。 当您键入另一个"d"时，列表应仅包含"添加"，现在已选中。 您可以通过按**空格键**、**选项卡**或**Enter**键提交"添加"，或者通过键入 Esc 或任何其他键来关闭列表。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
