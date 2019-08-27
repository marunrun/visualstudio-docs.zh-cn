---
title: 演练：显示签名帮助 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 280b5b517089ad9e5b38cb00dc9b14c68253d1e6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202050"
---
# <a name="walkthrough-displaying-signature-help"></a>演练：显示签名帮助
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

签名帮助 (也称为*的参数信息*) 工具提示中显示的一种方法的签名，当用户键入的参数列表开始字符 （通常是一个左括号）。 参数和参数分隔符 （通常为逗号） 类型化，工具提示会更新以显示下一个参数以粗体显示。 可以在语言服务的上下文中定义签名帮助或可以定义自己的文件名称扩展和内容类型并显示签名帮助只是该类型或可以为现有的内容类型 (例如，"text") 显示签名帮助。 本演练演示如何显示为"text"内容类型的签名帮助。  
  
 签名帮助通常会触发通过键入特定字符，例如，"("（左括号），并通过键入另一个字符，例如，已解除")"（右括号）。 可以通过击键命令处理程序实现触发键入字符的 IntelliSense 功能 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口) 和实现的处理程序提供程序<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>接口。 若要创建的签名帮助源，这是参与签名帮助中的签名的列表，实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>接口和实现的源提供程序<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>接口。 提供程序是 Managed Extensibility Framework (MEF) 组件部分，并负责导出的源和控制器类和导入服务和代理，例如， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，这样，在文本缓冲区中导航和<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>，随即将会触发签名帮助会话。  
  
 本演练演示如何实现的硬编码的一组标识符的签名帮助。 在完全实现中，语言是负责提供该内容。  
  
## <a name="prerequisites"></a>先决条件  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
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
  
## <a name="implementing-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数  
 签名帮助源取决于实现的签名<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>，其中每个包含用于实现的参数<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。 在完整的实现中，将从语言文档，获取此信息，但在此示例中，签名是硬编码。  
  
#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>若要实现的签名帮助签名和参数  
  
1. 添加一个类文件并将其命名为 `SignatureHelpSource`。  
  
2. 添加以下导入。  
  
     [!code-csharp[VSSDKSignatureHelpTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#1)]
     [!code-vb[VSSDKSignatureHelpTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#1)]  
  
3. 添加名为的类`TestParameter`实现<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#2)]
     [!code-vb[VSSDKSignatureHelpTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#2)]  
  
4. 添加设置的所有属性的构造函数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#3)]
     [!code-vb[VSSDKSignatureHelpTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#3)]  
  
5. 添加的属性<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#4)]
     [!code-vb[VSSDKSignatureHelpTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#4)]  
  
6. 添加名为的类`TestSignature`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#5)]
     [!code-vb[VSSDKSignatureHelpTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#5)]  
  
7. 添加一些私有字段。  
  
     [!code-csharp[VSSDKSignatureHelpTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#6)]
     [!code-vb[VSSDKSignatureHelpTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#6)]  
  
8. 添加一个构造函数设置的字段并订阅<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#7)]
     [!code-vb[VSSDKSignatureHelpTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#7)]  
  
9. 声明`CurrentParameterChanged`事件。 在签名中的参数之一的用户填写时，引发此事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#8)]
     [!code-vb[VSSDKSignatureHelpTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#8)]  
  
10. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A>属性，以便它引发`CurrentParameterChanged`事件的属性值更改时。  
  
     [!code-csharp[VSSDKSignatureHelpTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#9)]
     [!code-vb[VSSDKSignatureHelpTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#9)]  
  
11. 添加一个方法来引发`CurrentParameterChanged`事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#10)]
     [!code-vb[VSSDKSignatureHelpTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#10)]  
  
12. 添加一个方法来计算当前参数，方法是比较中的逗号数量<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>到签名中的逗号数量。  
  
     [!code-csharp[VSSDKSignatureHelpTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#11)]
     [!code-vb[VSSDKSignatureHelpTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#11)]  
  
13. 添加事件处理程序<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>调用的事件`ComputeCurrentParameter()`方法。  
  
     [!code-csharp[VSSDKSignatureHelpTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#12)]
     [!code-vb[VSSDKSignatureHelpTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#12)]  
  
14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含<xref:Microsoft.VisualStudio.Text.ITrackingSpan>，它对应于签名应用到的缓冲区中的文本范围。  
  
     [!code-csharp[VSSDKSignatureHelpTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#13)]
     [!code-vb[VSSDKSignatureHelpTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#13)]  
  
15. 实现其他参数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#14)]
     [!code-vb[VSSDKSignatureHelpTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#14)]  
  
## <a name="implementing-the-signature-help-source"></a>实现签名帮助源  
 签名帮助源是的签名为其提供信息集。  
  
#### <a name="to-implement-the-signature-help-source"></a>若要实现的签名帮助源  
  
1. 添加名为的类`TestSignatureHelpSource`实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#15)]
     [!code-vb[VSSDKSignatureHelpTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#15)]  
  
2. 添加到文本缓冲区的引用。  
  
     [!code-csharp[VSSDKSignatureHelpTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#16)]
     [!code-vb[VSSDKSignatureHelpTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#16)]  
  
3. 添加设置的文本缓冲区和签名帮助源提供程序的构造函数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#17)]
     [!code-vb[VSSDKSignatureHelpTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#17)]  
  
4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码，但在完整的实现将从语言文档获取此信息。  
  
     [!code-csharp[VSSDKSignatureHelpTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#18)]
     [!code-vb[VSSDKSignatureHelpTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#18)]  
  
5. 帮助器方法`CreateSignature()`仅供演示。  
  
     [!code-csharp[VSSDKSignatureHelpTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#19)]
     [!code-vb[VSSDKSignatureHelpTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#19)]  
  
6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，有两个签名，其中每个具有两个参数。 因此，此方法不是必需的。 在更完整的实现中，在其中多个签名帮助源不可用，此方法用于决定的优先级最高的签名帮助源是否可以提供匹配的签名。 如果不能该方法返回 null 并下一步最高优先级源要求提供一个匹配项。  
  
     [!code-csharp[VSSDKSignatureHelpTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#20)]
     [!code-vb[VSSDKSignatureHelpTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#20)]  
  
7. 实现 dispose （） 方法：  
  
     [!code-csharp[VSSDKSignatureHelpTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#21)]
     [!code-vb[VSSDKSignatureHelpTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#21)]  
  
## <a name="implementing-the-signature-help-source-provider"></a>实现的签名帮助源提供程序  
 签名帮助源提供程序负责将导出的 Managed Extensibility Framework (MEF) 组件部分并实例化的签名帮助源。  
  
#### <a name="to-implement-the-signature-help-source-provider"></a>若要实现的签名帮助源提供程序  
  
1. 添加名为的类`TestSignatureHelpSourceProvider`，它实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>，并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>、 一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"和一个<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>的 Before ="default"。  
  
     [!code-csharp[VSSDKSignatureHelpTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#22)]
     [!code-vb[VSSDKSignatureHelpTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#22)]  
  
2. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>通过实例化`TestSignatureHelpSource`。  
  
     [!code-csharp[VSSDKSignatureHelpTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#23)]
     [!code-vb[VSSDKSignatureHelpTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#23)]  
  
## <a name="implementing-the-command-handler"></a>实现命令处理程序  
 签名帮助通常由触发 (字符和通过已消除) 字符。 可以通过实现来处理这些击键<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，以便它将触发当它收到的签名帮助的会话 (字符前面有一个已知的方法名称，并将关闭时，它接收到的会话) 字符。  
  
#### <a name="to-implement-the-command-handler"></a>若要实现的命令处理程序  
  
1. 添加名为的类`TestSignatureHelpCommand`实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#24)]
     [!code-vb[VSSDKSignatureHelpTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#24)]  
  
2. 添加私有字段<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>适配器 （这可以让你将命令处理程序添加到链的命令处理程序），文本视图、 签名帮助代理和会话中， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>，以及接下来的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#25)]
     [!code-vb[VSSDKSignatureHelpTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#25)]  
  
3. 添加构造函数来初始化这些字段并将命令筛选器添加到命令链筛选器。  
  
     [!code-csharp[VSSDKSignatureHelpTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#26)]
     [!code-vb[VSSDKSignatureHelpTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#26)]  
  
4. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法可用于触发命令筛选器时收到的签名帮助的会话 (字符后之一已知的方法名称，并关闭时，它接收到的会话) 字符在会话处于仍处于活动状态时。 在所有情况下，该命令将转发。  
  
     [!code-csharp[VSSDKSignatureHelpTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#27)]
     [!code-vb[VSSDKSignatureHelpTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#27)]  
  
5. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法，以便它始终会转发该命令。  
  
     [!code-csharp[VSSDKSignatureHelpTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#28)]
     [!code-vb[VSSDKSignatureHelpTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#28)]  
  
## <a name="implementing-the-signature-help-command-provider"></a>实现签名帮助命令提供程序  
 通过实现可以提供签名帮助命令<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>若要创建文本视图时实例化的命令处理程序。  
  
#### <a name="to-implement-the-signature-help-command-provider"></a>若要实现的签名帮助命令提供程序  
  
1. 添加名为的类`TestSignatureHelpController`，它实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>， <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>，和<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>。  
  
     [!code-csharp[VSSDKSignatureHelpTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#29)]
     [!code-vb[VSSDKSignatureHelpTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#29)]  
  
2. 导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>(用于获取<xref:Microsoft.VisualStudio.Text.Editor.ITextView>给定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象)，则<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>（用于查找在当前单词），和<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>（用于触发签名帮助会话）。  
  
     [!code-csharp[VSSDKSignatureHelpTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#30)]
     [!code-vb[VSSDKSignatureHelpTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#30)]  
  
3. 实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>方法通过实例化`TestSignatureCommandHandler`。  
  
     [!code-csharp[VSSDKSignatureHelpTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#31)]
     [!code-vb[VSSDKSignatureHelpTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#31)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 SignatureHelpTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>若要生成和测试 SignatureHelpTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件和一些文本，其中包括单词"添加"的类型以及一个左括号。  
  
4. 键入左括号之后，将看到显示一系列的两个签名的工具提示`add()`方法。  
  
## <a name="see-also"></a>请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
