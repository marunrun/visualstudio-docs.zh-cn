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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202050"
---
# <a name="walkthrough-displaying-signature-help"></a>演练：显示签名帮助
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

签名帮助 (也称为 *参数信息*) 当用户键入参数列表开始字符时，将在工具提示中显示方法的签名， (通常为左括号) 。 作为参数和参数分隔符 (通常会键入逗号) ，工具提示将更新以以粗体显示下一个参数。 你可以在语言服务的上下文中定义签名帮助，也可以定义自己的文件扩展名和内容类型，并为该类型仅显示签名帮助，或者可以为现有内容类型显示签名帮助 (例如，"text" ) 。 本演练演示如何为 "文本" 内容类型显示签名帮助。  
  
 签名帮助通常是通过键入特定字符来触发的，例如 " (" (左括号) ，并通过键入另一个字符来消除，如 ") " (右括号) 。 通过使用命令处理程序 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口) 和实现接口的处理程序提供程序，可以实现通过键入字符触发的 IntelliSense 功能 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 。 若要创建签名帮助源（参与签名帮助的签名列表），请实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 接口和实现接口的源提供程序 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 。 提供程序 Managed Extensibility Framework (MEF) 组件部件，并负责导出源和控制器类，以及导入服务和代理，例如，可 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 让你在文本缓冲区中导航，并将 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 触发签名帮助会话。  
  
 本演练演示如何实现硬编码的标识符集的签名帮助。 在完整实现中，语言负责提供该内容。  
  
## <a name="prerequisites"></a>必备条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建 c # VSIX 项目。  (在 " **新建项目** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。 ) 将解决方案命名为 `SignatureHelpTest` 。  
  
2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
4. 将以下引用添加到项目，并确保 **CopyLocal** 设置为 `false` ：  
  
     VisualStudio  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     VisualStudio。  
  
     VisualStudio。14。0  
  
     VisualStudio. TextManager  
  
## <a name="implementing-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数  
 签名帮助源基于实现的签名 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> ，其中每个都包含实现的参数 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。 在完整的实现中，将从语言文档中获取此信息，但在此示例中，签名是硬编码的。  
  
#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数  
  
1. 添加一个类文件并将其命名为 `SignatureHelpSource`。  
  
2. 添加以下 import 语句。  
  
     [!code-csharp[VSSDKSignatureHelpTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#1)]
     [!code-vb[VSSDKSignatureHelpTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#1)]  
  
3. 添加一个名为 `TestParameter` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#2)]
     [!code-vb[VSSDKSignatureHelpTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#2)]  
  
4. 添加设置所有属性的构造函数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#3)]
     [!code-vb[VSSDKSignatureHelpTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#3)]  
  
5. 添加的属性 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#4)]
     [!code-vb[VSSDKSignatureHelpTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#4)]  
  
6. 添加一个名为 `TestSignature` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#5)]
     [!code-vb[VSSDKSignatureHelpTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#5)]  
  
7. 添加一些私有字段。  
  
     [!code-csharp[VSSDKSignatureHelpTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#6)]
     [!code-vb[VSSDKSignatureHelpTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#6)]  
  
8. 添加一个构造函数，该构造函数设置字段并订阅 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#7)]
     [!code-vb[VSSDKSignatureHelpTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#7)]  
  
9. 声明 `CurrentParameterChanged` 事件。 当用户填写签名中的一个参数时，将引发此事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#8)]
     [!code-vb[VSSDKSignatureHelpTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#8)]  
  
10. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 属性，以便 `CurrentParameterChanged` 在属性值更改时引发事件。  
  
     [!code-csharp[VSSDKSignatureHelpTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#9)]
     [!code-vb[VSSDKSignatureHelpTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#9)]  
  
11. 添加引发事件的方法 `CurrentParameterChanged` 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#10)]
     [!code-vb[VSSDKSignatureHelpTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#10)]  
  
12. 添加一个方法，该方法通过将中的逗号数 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 与签名中的逗号数进行比较来计算当前参数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#11)]
     [!code-vb[VSSDKSignatureHelpTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#11)]  
  
13. 为调用方法的事件添加事件处理程序 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#12)]
     [!code-vb[VSSDKSignatureHelpTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#12)]  
  
14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含与 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 签名应用到的缓冲区中的文本范围相对应的。  
  
     [!code-csharp[VSSDKSignatureHelpTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#13)]
     [!code-vb[VSSDKSignatureHelpTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#13)]  
  
15. 实现其他参数。  
  
     [!code-csharp[VSSDKSignatureHelpTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#14)]
     [!code-vb[VSSDKSignatureHelpTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#14)]  
  
## <a name="implementing-the-signature-help-source"></a>实现签名帮助源  
 签名帮助源是您提供信息的一组签名。  
  
#### <a name="to-implement-the-signature-help-source"></a>实现签名帮助源  
  
1. 添加一个名为 `TestSignatureHelpSource` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#15)]
     [!code-vb[VSSDKSignatureHelpTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#15)]  
  
2. 添加对文本缓冲区的引用。  
  
     [!code-csharp[VSSDKSignatureHelpTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#16)]
     [!code-vb[VSSDKSignatureHelpTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#16)]  
  
3. 添加一个构造函数，用于设置文本缓冲区和签名帮助源提供程序。  
  
     [!code-csharp[VSSDKSignatureHelpTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#17)]
     [!code-vb[VSSDKSignatureHelpTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#17)]  
  
4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码的，但在完整实现中，你将从语言文档中获取此信息。  
  
     [!code-csharp[VSSDKSignatureHelpTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#18)]
     [!code-vb[VSSDKSignatureHelpTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#18)]  
  
5. `CreateSignature()`仅为说明提供帮助器方法。  
  
     [!code-csharp[VSSDKSignatureHelpTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#19)]
     [!code-vb[VSSDKSignatureHelpTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#19)]  
  
6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，只有两个签名，其中每个都有两个参数。 因此，此方法不是必需的。 在更完整的实现中，有多个签名帮助源可用时，此方法用于确定最高优先级的签名帮助源是否可提供匹配的签名。 如果无法实现，该方法将返回 null，并要求下一个最高优先级的源提供匹配项。  
  
     [!code-csharp[VSSDKSignatureHelpTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#20)]
     [!code-vb[VSSDKSignatureHelpTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#20)]  
  
7. 实现 Dispose ( # A1 方法：  
  
     [!code-csharp[VSSDKSignatureHelpTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#21)]
     [!code-vb[VSSDKSignatureHelpTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#21)]  
  
## <a name="implementing-the-signature-help-source-provider"></a>实现签名帮助源提供程序  
 签名帮助源提供程序负责导出 Managed Extensibility Framework (MEF) 组件部件和实例化签名帮助源。  
  
#### <a name="to-implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序  
  
1. 添加一个名为的名为的类， `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 并将其导出为 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、一个为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text"，并将指定为 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default"。  
  
     [!code-csharp[VSSDKSignatureHelpTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#22)]
     [!code-vb[VSSDKSignatureHelpTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#22)]  
  
2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>通过实例化实现 `TestSignatureHelpSource` 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#23)]
     [!code-vb[VSSDKSignatureHelpTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#23)]  
  
## <a name="implementing-the-command-handler"></a>实现命令处理程序  
 签名帮助通常由 ( 字符触发，并由 ) 字符消除。 您可以通过实现来处理这些击键 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，使其在收到名为已知方法名称的 ( 字符时触发签名帮助会话，并在收到 ) 字符时关闭会话。  
  
#### <a name="to-implement-the-command-handler"></a>实现命令处理程序  
  
1. 添加一个名为 `TestSignatureHelpCommand` 的类，该类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#24)]
     [!code-vb[VSSDKSignatureHelpTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#24)]  
  
2. 为适配器 (添加私有字段 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ，该字段允许你将命令处理程序添加到命令处理程序链，) ，文本视图，签名帮助代理和会话， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> ，以及下一步 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#25)]
     [!code-vb[VSSDKSignatureHelpTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#25)]  
  
3. 添加构造函数以初始化这些字段并将命令筛选器添加到命令筛选器链。  
  
     [!code-csharp[VSSDKSignatureHelpTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#26)]
     [!code-vb[VSSDKSignatureHelpTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#26)]  
  
4. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法，以便在命令筛选器接收到一个已知方法名称后面的 ( 字符时触发签名帮助会话，并在会话仍处于活动状态时，在收到 ) 字符时消除会话。 在每种情况下，都将转发该命令。  
  
     [!code-csharp[VSSDKSignatureHelpTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#27)]
     [!code-vb[VSSDKSignatureHelpTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#27)]  
  
5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法，以便始终转发命令。  
  
     [!code-csharp[VSSDKSignatureHelpTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#28)]
     [!code-vb[VSSDKSignatureHelpTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#28)]  
  
## <a name="implementing-the-signature-help-command-provider"></a>实现签名帮助命令提供程序  
 可以通过实现来提供签名帮助命令 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ，以便在创建文本视图时实例化命令处理程序。  
  
#### <a name="to-implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序  
  
1. 添加一个名为 `TestSignatureHelpController` 的类，该类实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 并将其与 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、和一起导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#29)]
     [!code-vb[VSSDKSignatureHelpTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#29)]  
  
2. 导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 用于获取的 (<xref:Microsoft.VisualStudio.Text.Editor.ITextView> ，给定 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象) 、 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 用于查找当前单词) 的 (和用于 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 触发签名帮助会话 (的) 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#30)]
     [!code-vb[VSSDKSignatureHelpTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#30)]  
  
3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>通过实例化实现方法 `TestSignatureCommandHandler` 。  
  
     [!code-csharp[VSSDKSignatureHelpTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#31)]
     [!code-vb[VSSDKSignatureHelpTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#31)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，请生成 SignatureHelpTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>生成和测试 SignatureHelpTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本，其中包含单词 "add" 加上一个左括号。  
  
4. 键入左括号后，应该会看到工具提示，其中显示了该方法的两个签名的列表 `add()` 。  
  
## <a name="see-also"></a>另请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
