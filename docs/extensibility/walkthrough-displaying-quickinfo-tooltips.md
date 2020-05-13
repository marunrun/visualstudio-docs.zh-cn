---
title: 演练：显示快速信息工具提示 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: 47a14ca0692ad0338b56fd1d372307fb0e2ccc4c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697435"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>演练：显示快速信息工具提示
QuickInfo 是一个 IntelliSense 功能，当用户在方法名称上移动指针时，显示方法签名和说明。 您可以通过定义要为其提供 QuickInfo 说明的标识符，然后创建用于显示内容的工具提示来实现基于语言的功能，例如 QuickInfo。 您可以在语言服务的上下文中定义 QuickInfo，也可以定义自己的文件名扩展名和内容类型，并仅显示该类型的 QuickInfo，也可以显示现有内容类型的 QuickInfo（如"文本"）。 本演练演示如何显示"文本"内容类型的 QuickInfo。

 本演练中的 QuickInfo 示例显示当用户将指针移到方法名称上时的工具提示。 此设计要求您实现以下四个接口：

- 源接口

- 源提供程序接口

- 控制器接口

- 控制器提供程序接口

  源和控制器提供程序是托管扩展框架 （MEF） 组件，负责导出源和控制器类以及导入服务和代理，如 创建工具提示文本缓冲区的 和<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService><xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>触发 QuickInfo 会话的 。

  在此示例中，QuickInfo 源使用方法名称和说明的硬编码列表，但在完全实现中，语言服务和语言文档负责提供该内容。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您无需从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`QuickInfoTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-the-quickinfo-source"></a>实现快速信息源
 QuickInfo 源负责收集标识符集及其说明，并在遇到其中一个标识符时将内容添加到工具提示文本缓冲区。 在此示例中，标识符及其描述只是添加到源构造函数中。

#### <a name="to-implement-the-quickinfo-source"></a>实现快速信息源

1. 添加一个类文件并将其命名为 `TestQuickInfoSource`。

2. 添加对*微软的引用.VisualStudio.语言.IntelliSense*。

3. 添加以下 import 语句。

     [!code-vb[VSSDKQuickInfoTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_1.vb)]
     [!code-csharp[VSSDKQuickInfoTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_1.cs)]

4. 声明实现<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>的类并命名它`TestQuickInfoSource`。

     [!code-vb[VSSDKQuickInfoTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_2.vb)]
     [!code-csharp[VSSDKQuickInfoTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_2.cs)]

5. 为 QuickInfo 源提供程序、文本缓冲区以及一组方法名称和方法签名添加字段。 在此示例中，方法名称和签名在构造函数中`TestQuickInfoSource`初始化。

     [!code-vb[VSSDKQuickInfoTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_3.vb)]
     [!code-csharp[VSSDKQuickInfoTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_3.cs)]

6. 添加一个构造函数，用于设置 QuickInfo 源提供程序和文本缓冲区，并填充方法名称集以及方法签名和说明。

     [!code-vb[VSSDKQuickInfoTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_4.vb)]
     [!code-csharp[VSSDKQuickInfoTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_4.cs)]

7. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> 方法。 在此示例中，如果光标位于行或文本缓冲区的末尾，则该方法查找当前单词或上一个单词。 如果单词是方法名称之一，则该方法名称的说明将添加到 QuickInfo 内容中。

     [!code-vb[VSSDKQuickInfoTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_5.vb)]
     [!code-csharp[VSSDKQuickInfoTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_5.cs)]

8. 您还必须实现 Dispose（） 方法，因为<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>实现<xref:System.IDisposable>：

     [!code-vb[VSSDKQuickInfoTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_6.vb)]
     [!code-csharp[VSSDKQuickInfoTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_6.cs)]

## <a name="implement-a-quickinfo-source-provider"></a>实施 QuickInfo 源提供商
 QuickInfo 源的提供程序主要用于导出自身作为 MEF 组件部分并实例化 QuickInfo 源。 因为它是 MEF 组件部件，因此可以导入其他 MEF 组件部件。

#### <a name="to-implement-a-quickinfo-source-provider"></a>实现 QuickInfo 源提供程序

1. 声明名为 的名为 的`TestQuickInfoSourceProvider`QuickInfo<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>源提供程序，并<xref:Microsoft.VisualStudio.Utilities.NameAttribute>导出它与"ToolTip QuickInfo<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>源"，一个前="默认<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"和一个"文本"。

     [!code-vb[VSSDKQuickInfoTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_7.vb)]
     [!code-csharp[VSSDKQuickInfoTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_7.cs)]

2. 导入两个编辑器服务<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>并将 作为`TestQuickInfoSourceProvider`的属性。

     [!code-vb[VSSDKQuickInfoTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_8.vb)]
     [!code-csharp[VSSDKQuickInfoTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_8.cs)]

3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A>以返回新的`TestQuickInfoSource`。

     [!code-vb[VSSDKQuickInfoTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_9.vb)]
     [!code-csharp[VSSDKQuickInfoTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_9.cs)]

## <a name="implement-a-quickinfo-controller"></a>实现快速信息控制器
 QuickInfo 控制器确定何时显示 QuickInfo。 在此示例中，当指针位于对应于其中一个方法名称的单词上时，将显示 QuickInfo。 QuickInfo 控制器实现一个鼠标悬停事件处理程序，该处理程序触发 QuickInfo 会话。

### <a name="to-implement-a-quickinfo-controller"></a>实现快速信息控制器

1. 声明实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>的类并命名它`TestQuickInfoController`。

     [!code-vb[VSSDKQuickInfoTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_10.vb)]
     [!code-csharp[VSSDKQuickInfoTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_10.cs)]

2. 为文本视图、文本视图中表示的文本缓冲区、QuickInfo 会话和 QuickInfo 控制器提供程序添加私有字段。

     [!code-vb[VSSDKQuickInfoTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_11.vb)]
     [!code-csharp[VSSDKQuickInfoTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_11.cs)]

3. 添加一个构造函数，用于设置字段并添加鼠标悬停事件处理程序。

     [!code-vb[VSSDKQuickInfoTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_12.vb)]
     [!code-csharp[VSSDKQuickInfoTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_12.cs)]

4. 添加触发 QuickInfo 会话的鼠标悬停事件处理程序。

     [!code-vb[VSSDKQuickInfoTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_13.vb)]
     [!code-csharp[VSSDKQuickInfoTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_13.cs)]

5. 实现该方法<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A>，以便在控制器从文本视图分离时删除鼠标悬停事件处理程序。

     [!code-vb[VSSDKQuickInfoTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_14.vb)]
     [!code-csharp[VSSDKQuickInfoTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_14.cs)]

6. 将<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A>该方法和<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A>该方法作为此示例的空方法实现。

     [!code-vb[VSSDKQuickInfoTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_15.vb)]
     [!code-csharp[VSSDKQuickInfoTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_15.cs)]

## <a name="implementing-the-quickinfo-controller-provider"></a>实现 QuickInfo 控制器提供程序
 QuickInfo 控制器的提供程序主要用于导出自身作为 MEF 组件部分并实例化 QuickInfo 控制器。 因为它是 MEF 组件部件，因此可以导入其他 MEF 组件部件。

### <a name="to-implement-the-quickinfo-controller-provider"></a>实现 QuickInfo 控制器提供程序

1. 声明名为 的`TestQuickInfoControllerProvider`类，<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider>实现 ，并导出它与<xref:Microsoft.VisualStudio.Utilities.NameAttribute>"ToolTip QuickInfo 控制器"和<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"文本"：

     [!code-vb[VSSDKQuickInfoTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_16.vb)]
     [!code-csharp[VSSDKQuickInfoTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_16.cs)]

2. 将 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> 作为属性导入。

     [!code-vb[VSSDKQuickInfoTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_17.vb)]
     [!code-csharp[VSSDKQuickInfoTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_17.cs)]

3. 通过实例<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A>化 QuickInfo 控制器来实现该方法。

     [!code-vb[VSSDKQuickInfoTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_18.vb)]
     [!code-csharp[VSSDKQuickInfoTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_18.cs)]

## <a name="build-and-test-the-code"></a>构建和测试代码
 要测试此代码，请构建 QuickInfoTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-quickinfotest-solution"></a>构建和测试 QuickInfoTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件并键入一些包含"添加"和"减法"字样的文本。

4. 将指针移到"添加"的一个匹配项上。 应显示`add`方法的签名和说明。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
