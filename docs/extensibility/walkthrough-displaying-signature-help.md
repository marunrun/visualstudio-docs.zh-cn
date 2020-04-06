---
title: 演练：显示签名帮助 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f85d7eb3959064468e7583ec0c8a927f3e139daf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697420"
---
# <a name="walkthrough-display-signature-help"></a>演练：显示签名帮助
当用户键入参数列表开始字符（通常是打开括号）时，签名帮助（也称为*参数信息*）在工具提示中显示方法的签名。 当键入参数和参数分隔符（通常是逗号）时，工具提示将更新以粗体显示下一个参数。 您可以通过以下方式定义签名帮助：在语言服务的上下文中，定义您自己的文件名扩展名和内容类型，并仅显示该类型的签名帮助，或显示现有内容类型的签名帮助（例如，"文本"）。 本演练演示如何显示"文本"内容类型的签名帮助。

 签名帮助通常通过键入特定字符（例如"（"（"（打开括号））触发，并通过键入另一个字符（例如"）"（关闭括号）来消除。 通过键入字符触发的 IntelliSense 功能可以通过使用击键（<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口）的命令处理程序和实现接口的<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>处理程序提供程序实现。 要创建签名帮助源（即参与签名帮助的签名列表），请实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>接口和运行该接口的<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>源提供程序。 提供程序是托管扩展框架 （MEF） 组件，负责导出源和控制器类以及导入服务和代理，例如，允许您在文本缓冲区中导航的 和<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>触发签名帮助会话的 。 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>

 本演练演示如何为硬编码的标识符集设置签名帮助。 在完全实现中，语言负责提供该内容。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="creating-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`SignatureHelpTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 添加对项目的以下引用，并确保**CopyLocal**设置为`false`：

     微软.VisualStudio.编辑器

     Microsoft.VisualStudio.Language.Intellisense

     微软.VisualStudio.OLE.Interop

     微软.VisualStudio.shell.14.0

     微软.VisualStudio.文本管理器.互通

## <a name="implement-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数
 签名帮助源基于实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>的签名，每个签名都包含实现<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>的参数。 在完全实现中，此信息将从语言文档获得，但在此示例中，签名是硬编码的。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数

1. 添加一个类文件并将其命名为 `SignatureHelpSource`。

2. 添加以下 import 语句。

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. 添加名为`TestParameter`的类<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>，实现 。

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. 添加设置所有属性的构造函数。

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. 添加 的属性<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. 添加名为`TestSignature`的类<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>，实现 。

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. 添加一些私有字段。

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. 添加一个构造函数，用于设置字段并订阅事件<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>。

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. 声明事件`CurrentParameterChanged`。 当用户填写签名中的一个参数时，将引发此事件。

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. 实现该<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A>属性，以便在更改属性值`CurrentParameterChanged`时引发事件。

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. 添加引发`CurrentParameterChanged`事件的方法。

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. 添加一个计算当前参数的方法，方法是将 中的逗号<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>数与签名中的逗号数进行比较。

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. 为调用<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>`ComputeCurrentParameter()`该方法的事件添加事件处理程序。

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性保存与签名<xref:Microsoft.VisualStudio.Text.ITrackingSpan>应用的缓冲区中的文本范围对应的 。

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. 实现其他参数。

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>实现签名帮助源
 签名帮助源是您为其提供信息的签名集。

#### <a name="to-implement-the-signature-help-source"></a>实现签名帮助源

1. 添加名为`TestSignatureHelpSource`的类<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>，实现 。

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. 添加对文本缓冲区的引用。

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. 添加设置文本缓冲区和签名帮助源提供程序的构造函数。

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码的，但在完全实现中，您将从语言文档中获取此信息。

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. 帮助器方法`CreateSignature()`仅供说明。

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，只有两个签名，每个签名都有两个参数。 因此，此方法不是必需的。 在具有多个签名帮助源的更完整实现中，此方法用于决定优先级最高的签名帮助源是否可以提供匹配的签名。 如果不能，该方法将返回 null，并且要求下一个优先级最高的源提供匹配项。

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. 实现方法`Dispose()`：

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序
 签名帮助源提供程序负责导出托管扩展框架 （MEF） 组件部分并实例化签名帮助源。

#### <a name="to-implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序

1. 添加名为 的`TestSignatureHelpSourceProvider`类，<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>实现 ，并导出它<xref:Microsoft.VisualStudio.Utilities.NameAttribute>与<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的 "文本"和<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>前 = "默认值"。

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. 通过<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>实例化 实现`TestSignatureHelpSource`。

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>实现命令处理程序
 签名帮助通常由开放括号"（"字符）触发，并通过关闭括号"）"字符关闭。 可以通过运行 来处理<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>这些击键，以便在它收到打开的括号字符之前具有已知方法名称时触发签名帮助会话，并在会话收到关闭的括号字符时将其关闭。

#### <a name="to-implement-the-command-handler"></a>实现命令处理程序

1. 添加名为`TestSignatureHelpCommand`的类<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，实现 。

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. 为<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>适配器添加私有字段（允许您将命令处理程序添加到命令处理程序链）、文本视图、签名帮助代理和会话、和<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>下一个<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. 添加构造函数来初始化这些字段，并将命令筛选器添加到命令筛选器链中。

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法在命令筛选器收到一个已知方法名称后的开放括号"（"）字符时触发签名帮助会话;并在会话仍然处于活动状态时收到关闭括号"）字符时关闭会话"。 在每种情况下，命令都会被转发。

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. 实现该方法<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>，以便它始终转发命令。

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序
 可以通过在创建文本视图时实现实例化命令<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>处理程序来提供签名帮助命令。

### <a name="to-implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序

1. 添加名为 的`TestSignatureHelpController`类，<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>该类实现并导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>它<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>与<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>。

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>（<xref:Microsoft.VisualStudio.Text.Editor.ITextView>用于获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>给定对象）、（<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>用于查找当前单词）和<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>（用于触发签名帮助会话）。

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. 通过实例<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>化 实现`TestSignatureCommandHandler`方法。

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请构建签名帮助测试解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>构建和测试签名帮助测试解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件并键入一些包含单词"add"加上开口括号的文本。

4. 键入打开括号后，应看到一个工具提示，显示`add()`该方法的两个签名的列表。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
