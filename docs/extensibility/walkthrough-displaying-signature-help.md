---
title: 演练：显示签名帮助 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 403009367f6cdf8a9fd1ebb750ee9bb020690685
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312417"
---
# <a name="walkthrough-display-signature-help"></a>演练：显示签名帮助
签名帮助 (也称为*的参数信息*) 工具提示中显示的一种方法的签名，当用户键入的参数列表开始字符 （通常是一个左括号）。 参数和参数分隔符 （通常为逗号） 类型化，工具提示会更新以显示下一个参数以粗体显示。 可以按以下方式定义签名帮助： 在语言服务的上下文中，定义自己的文件扩展名和内容类型和显示签名帮助只是该类型，或为现有内容类型 (例如，"text") 显示签名帮助。 本演练演示如何显示为"text"内容类型的签名帮助。

 签名帮助通常会触发通过键入特定字符，例如，"("（左括号），并通过键入另一个字符，例如，已解除")"（右括号）。 可以通过击键命令处理程序实现触发键入字符的 IntelliSense 功能 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口) 和实现的处理程序提供程序<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>接口。 若要创建的签名帮助源，这是参与签名帮助中的签名的列表，实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>接口和源代码提供程序运行<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>接口。 提供程序是 Managed Extensibility Framework (MEF) 组件部分，并负责导出的源和控制器类和导入服务和代理，例如， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，这样，在文本缓冲区中导航和<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>，随即将会触发签名帮助会话。

 本演练演示如何为硬编码的一组标识符设置签名帮助。 在完全实现中，语言是负责提供该内容。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，不要从下载中心安装 Visual Studio SDK。 它包含作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="creating-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `SignatureHelpTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 添加以下引用到项目中，并确保**CopyLocal**设置为`false`:

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     Microsoft.VisualStudio.Shell.14.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数
 签名帮助源取决于实现的签名<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>，其中每个包含用于实现的参数<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。 在完整的实现中，将从语言文档，获取此信息，但在此示例中，签名是硬编码。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>若要实现的签名帮助签名和参数

1. 添加一个类文件并将其命名为 `SignatureHelpSource`。

2. 添加以下导入。

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. 添加名为的类`TestParameter`实现<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. 添加设置的所有属性的构造函数。

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. 添加的属性<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. 添加名为的类`TestSignature`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>。

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. 添加一些私有字段。

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. 添加一个构造函数设置的字段并订阅<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>事件。

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. 声明`CurrentParameterChanged`事件。 在签名中的参数之一的用户填写时，引发此事件。

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A>属性，以便它引发`CurrentParameterChanged`事件的属性值更改时。

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. 添加一个方法来引发`CurrentParameterChanged`事件。

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. 添加一个方法来计算当前参数，方法是比较中的逗号数量<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>到签名中的逗号数量。

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. 添加事件处理程序<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>调用的事件`ComputeCurrentParameter()`方法。

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含<xref:Microsoft.VisualStudio.Text.ITrackingSpan>，它对应于签名应用到的缓冲区中的文本范围。

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. 实现其他参数。

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>实现的签名帮助源
 签名帮助源是的签名为其提供信息集。

#### <a name="to-implement-the-signature-help-source"></a>若要实现的签名帮助源

1. 添加名为的类`TestSignatureHelpSource`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>。

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. 添加到文本缓冲区的引用。

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. 添加设置的文本缓冲区和签名帮助源提供程序的构造函数。

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码，但在完整的实现将从语言文档获取此信息。

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. 帮助器方法`CreateSignature()`仅供演示。

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，有两个签名，其中每个具有两个参数。 因此，此方法不是必需的。 在更完整的实现中，在其中多个签名帮助源不可用，此方法用于决定的优先级最高的签名帮助源是否可以提供匹配的签名。 如果不能该方法返回 null 并下一步最高优先级源要求提供一个匹配项。

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. 实现`Dispose()`方法：

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>实现的签名帮助源提供程序
 签名帮助源提供程序负责将导出的 Managed Extensibility Framework (MEF) 组件部分并实例化的签名帮助源。

#### <a name="to-implement-the-signature-help-source-provider"></a>若要实现的签名帮助源提供程序

1. 添加名为的类`TestSignatureHelpSourceProvider`，它实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>，并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>、 一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"和一个<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>的 Before ="default"。

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>通过实例化`TestSignatureHelpSource`。

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>实现命令处理程序
 签名帮助通常会触发紧跟左括号"（"字符和右括号的已消除"）"字符。 可以通过运行处理这些击键<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，以便它将触发时收到一个打开的签名帮助的会话括号字符前面有一个已知的方法名称，并将关闭的会话时收到一个结束括号字符。

#### <a name="to-implement-the-command-handler"></a>若要实现的命令处理程序

1. 添加名为的类`TestSignatureHelpCommand`实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. 添加私有字段<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>适配器 （这可以让你将命令处理程序添加到链的命令处理程序），文本视图、 签名帮助代理和会话中， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>，以及接下来的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. 添加构造函数来初始化这些字段并将命令筛选器添加到命令链筛选器。

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法可用于触发签名帮助的会话命令筛选器时收到一个左括号"（"字符后之一已知的方法名称，并关闭的会话时收到一个右括号"）"字符虽然会话仍处于活动状态。 在所有情况下，该命令将转发。

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法，以便它始终会转发该命令。

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>实现的签名帮助命令提供程序
 通过实现可以提供签名帮助命令<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>若要创建文本视图时实例化的命令处理程序。

### <a name="to-implement-the-signature-help-command-provider"></a>若要实现的签名帮助命令提供程序

1. 添加名为的类`TestSignatureHelpController`，它实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>， <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>，和<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>。

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>(用于获取<xref:Microsoft.VisualStudio.Text.Editor.ITextView>给定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象)，则<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>（用于查找在当前单词），和<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>（用于触发签名帮助会话）。

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. 实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>方法通过实例化`TestSignatureCommandHandler`。

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，生成 SignatureHelpTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>若要生成和测试 SignatureHelpTest 解决方案

1. 生成解决方案。

2. 当在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件和一些文本，其中包括单词"添加"的类型以及一个左括号。

4. 键入左括号之后，将看到显示一系列的两个签名的工具提示`add()`方法。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到的文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)