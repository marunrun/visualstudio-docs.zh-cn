---
title: 演练：显示签名帮助 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b88c8555904bb31c2804579459ad3096d640b0c2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904819"
---
# <a name="walkthrough-display-signature-help"></a>演练：显示签名帮助
签名帮助（也称为*参数信息*）在用户键入参数列表开始字符（通常是左括号）时，在工具提示中显示方法的签名。 如果键入了参数和参数分隔符（通常为逗号），则工具提示将更新为以粗体显示下一个参数。 可以通过以下方式定义签名帮助：在语言服务的上下文中，定义自己的文件扩展名和内容类型，并为该类型仅显示签名帮助，或显示现有内容类型（例如，"文本"）的签名帮助。 本演练演示如何为 "文本" 内容类型显示签名帮助。

 签名帮助通常通过键入特定字符来触发，例如 "（" （左括号），并通过键入另一个字符（例如 "）" （右括号）来消除。 通过使用键击（ <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口）和实现接口的处理程序提供程序的命令处理程序，可以实现通过键入字符触发的 IntelliSense 功能 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 。 若要创建签名帮助源（参与签名帮助的签名列表），请实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 接口和运行接口的源提供程序 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 。 提供程序是 Managed Extensibility Framework （MEF）组件部件，负责导出源和控制器类，以及导入服务和代理，例如，可 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 让你在文本缓冲区中导航和 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> ，这会触发签名帮助会话。

 本演练演示如何为硬编码的标识符集设置签名帮助。 在完整实现中，语言负责提供该内容。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="creating-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。）命名解决方案 `SignatureHelpTest` 。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，并确保**CopyLocal**设置为 `false` ：

     VisualStudio

     Microsoft.VisualStudio.Language.Intellisense

     VisualStudio。

     VisualStudio。14。0

     VisualStudio. TextManager

## <a name="implement-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数
 签名帮助源基于实现的签名 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> ，其中每个都包含实现的参数 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。 在完整的实现中，将从语言文档中获取此信息，但在此示例中，签名是硬编码的。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>实现签名帮助签名和参数

1. 添加一个类文件并将其命名为 `SignatureHelpSource`。

2. 添加以下 import 语句。

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. 添加一个名为 `TestParameter` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. 添加设置所有属性的构造函数。

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. 添加的属性 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> 。

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. 添加一个名为 `TestSignature` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> 。

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. 添加一些私有字段。

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. 添加一个构造函数，该构造函数设置字段并订阅 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> 事件。

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. 声明 `CurrentParameterChanged` 事件。 当用户填写签名中的一个参数时，将引发此事件。

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 属性，以便 `CurrentParameterChanged` 在属性值更改时引发事件。

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. 添加引发事件的方法 `CurrentParameterChanged` 。

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. 添加一个方法，该方法通过将中的逗号数 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 与签名中的逗号数进行比较来计算当前参数。

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. 为调用方法的事件添加事件处理程序 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` 。

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> 属性。 此属性包含与 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 签名应用到的缓冲区中的文本范围相对应的。

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. 实现其他参数。

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>实现签名帮助源
 签名帮助源是您提供信息的一组签名。

#### <a name="to-implement-the-signature-help-source"></a>实现签名帮助源

1. 添加一个名为 `TestSignatureHelpSource` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> 。

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. 添加对文本缓冲区的引用。

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. 添加一个构造函数，用于设置文本缓冲区和签名帮助源提供程序。

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> 方法。 在此示例中，签名是硬编码的，但在完整实现中，你将从语言文档中获取此信息。

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. `CreateSignature()`仅为说明提供帮助器方法。

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> 方法。 在此示例中，只有两个签名，其中每个都有两个参数。 因此，此方法不是必需的。 在更完整的实现中，有多个签名帮助源可用时，此方法用于确定最高优先级的签名帮助源是否可提供匹配的签名。 如果无法实现，该方法将返回 null，并要求下一个最高优先级的源提供匹配项。

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. 实现 `Dispose()` 方法：

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序
 签名帮助源提供程序负责导出 Managed Extensibility Framework （MEF）组件部分和实例化签名帮助源。

#### <a name="to-implement-the-signature-help-source-provider"></a>实现签名帮助源提供程序

1. 添加一个名为的名为的类， `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> 并将其导出为 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、一个为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text"，并将指定为 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default"。

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>通过实例化实现 `TestSignatureHelpSource` 。

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>实现命令处理程序
 签名帮助通常由左括号 "（" 字符和右括号 "）" 字符来触发。 你可以通过运行来处理这些击键 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，使其在收到一个带有已知方法名称的左括号字符时触发签名帮助会话，并在收到右括号字符时关闭会话。

#### <a name="to-implement-the-command-handler"></a>实现命令处理程序

1. 添加一个名为 `TestSignatureHelpCommand` 的类，该类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. 为适配器添加私有字段 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> （这使你可以将命令处理程序添加到命令处理程序链中）、文本视图、签名帮助代理和会话、以及 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> 下一步 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. 添加构造函数以初始化这些字段并将命令筛选器添加到命令筛选器链。

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>当命令筛选器接收到一个已知方法名称后面的左括号 "（" 字符后，若要在会话仍处于活动状态时在收到右括号 "）" 字符时消除会话，请实现方法以触发签名帮助会话。 在每种情况下，都将转发该命令。

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法，以便始终转发命令。

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序
 可以通过实现来提供签名帮助命令 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ，以便在创建文本视图时实例化命令处理程序。

### <a name="to-implement-the-signature-help-command-provider"></a>实现签名帮助命令提供程序

1. 添加一个名为 `TestSignatureHelpController` 的类，该类实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 并将其与 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、和一起导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 。

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. 导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> （可在给定对象的情况下获取） <xref:Microsoft.VisualStudio.Text.Editor.ITextView> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 、 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> （用于查找当前单词）和 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> （用于触发签名帮助会话）。

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>通过实例化实现方法 `TestSignatureCommandHandler` 。

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 SignatureHelpTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>生成和测试 SignatureHelpTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包含单词 "add" 加上一个左括号。

4. 键入左括号后，应该会看到工具提示，其中显示了该方法的两个签名的列表 `add()` 。

## <a name="see-also"></a>另请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
