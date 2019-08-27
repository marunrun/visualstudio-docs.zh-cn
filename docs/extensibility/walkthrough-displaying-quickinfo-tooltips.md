---
title: 演练：显示快速信息工具提示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b7cb51edb41109d9664e5aeda0a5393d2cd34f38
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312437"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>演练：显示快速信息工具提示
快速信息 IntelliSense 功能，用于显示方法签名，说明当用户将指针移到方法名称。 您可以通过定义的标识符来提供快速信息的说明，并创建要在其中显示内容的工具提示实现基于语言的功能，例如快速信息。 可以在语言服务的上下文中定义 QuickInfo 或可以定义自己的文件名称扩展和内容类型并显示快速信息只是该类型或可以为现有内容类型 （例如"text") 显示快速信息。 本演练演示如何显示快速信息的"text"内容类型。

 当用户将指针移到方法名称，在本演练中的快速信息示例将显示工具提示。 此设计要求您实现这些四个接口：

- 源接口

- 源提供程序接口

- 控制器接口

- 控制器提供程序接口

  源和控制器提供程序是 Managed Extensibility Framework (MEF) 组件部分，并负责将导出的源和控制器类和导入服务，并如中转站<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>，这将创建的工具提示文本缓冲区，和<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>，随即将会触发 QuickInfo 会话。

  在此示例中，快速信息源，使用硬编码列表方法名称和说明，但在完整的实现，该语言服务和语言文档是负责提供该内容。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，不需要从下载中心安装 Visual Studio SDK。 它包含作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `QuickInfoTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-the-quickinfo-source"></a>实现快速信息源
 快速信息源是负责收集组的标识符和及其说明，并将内容添加到工具提示文本缓冲区时遇到的一个标识符。 在此示例中，标识符和及其说明源构造函数中只需添加。

#### <a name="to-implement-the-quickinfo-source"></a>若要实现的快速信息源

1. 添加一个类文件并将其命名为 `TestQuickInfoSource`。

2. 添加对的引用*Microsoft.VisualStudio.Language.IntelliSense*。

3. 添加以下导入。

     [!code-vb[VSSDKQuickInfoTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_1.vb)]
     [!code-csharp[VSSDKQuickInfoTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_1.cs)]

4. 声明的类，实现<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>，并将其命名`TestQuickInfoSource`。

     [!code-vb[VSSDKQuickInfoTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_2.vb)]
     [!code-csharp[VSSDKQuickInfoTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_2.cs)]

5. 快速信息源提供程序、 文本缓冲区和一组方法名称和方法签名添加字段。 在此示例中，方法名称和签名初始化中`TestQuickInfoSource`构造函数。

     [!code-vb[VSSDKQuickInfoTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_3.vb)]
     [!code-csharp[VSSDKQuickInfoTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_3.cs)]

6. 添加一个构造函数设置的快速信息源提供程序和文本缓冲区，并填充一组的方法名称和方法签名和说明。

     [!code-vb[VSSDKQuickInfoTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_4.vb)]
     [!code-csharp[VSSDKQuickInfoTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_4.cs)]

7. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> 方法。 在此示例中，该方法查找当前的单词或上一个词如果游标在行或文本缓冲区的末尾处。 如果单词为其中一个方法名称，该方法名称的描述被添加到快速信息内容。

     [!code-vb[VSSDKQuickInfoTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_5.vb)]
     [!code-csharp[VSSDKQuickInfoTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_5.cs)]

8. 此外必须实现的 dispose （） 方法，因为<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>实现<xref:System.IDisposable>:

     [!code-vb[VSSDKQuickInfoTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_6.vb)]
     [!code-csharp[VSSDKQuickInfoTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_6.cs)]

## <a name="implement-a-quickinfo-source-provider"></a>实现快速信息源提供程序
 快速信息源的提供者提供主要是为了导出本身为 MEF 组件部分实例化的快速信息源。 因为它是 MEF 组件部分，它可以导入其他 MEF 组件部分。

#### <a name="to-implement-a-quickinfo-source-provider"></a>若要实现的快速信息源提供程序

1. 声明为的快速信息源提供程序`TestQuickInfoSourceProvider`，它实现<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>，并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"工具提示 QuickInfo 源"<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>的 Before ="default"，和一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"。

     [!code-vb[VSSDKQuickInfoTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_7.vb)]
     [!code-csharp[VSSDKQuickInfoTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_7.cs)]

2. 导入两个编辑器服务，<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>并<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>，为属性的`TestQuickInfoSourceProvider`。

     [!code-vb[VSSDKQuickInfoTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_8.vb)]
     [!code-csharp[VSSDKQuickInfoTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_8.cs)]

3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A>返回一个新`TestQuickInfoSource`。

     [!code-vb[VSSDKQuickInfoTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_9.vb)]
     [!code-csharp[VSSDKQuickInfoTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_9.cs)]

## <a name="implement-a-quickinfo-controller"></a>实现快速信息控制器
 QuickInfo 控制器确定何时显示快速信息。 在此示例中，鼠标指针位于与方法名称之一相对应的单词时，将显示快速信息。 QuickInfo 控制器实现的鼠标悬停事件处理程序触发 QuickInfo 会话。

### <a name="to-implement-a-quickinfo-controller"></a>若要实现 QuickInfo 控制器

1. 声明的类，实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>，并将其命名`TestQuickInfoController`。

     [!code-vb[VSSDKQuickInfoTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_10.vb)]
     [!code-csharp[VSSDKQuickInfoTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_10.cs)]

2. 添加私有字段文本视图中，在文本视图、 快速信息会话和快速信息 controller 提供程序中表示的文本缓冲区。

     [!code-vb[VSSDKQuickInfoTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_11.vb)]
     [!code-csharp[VSSDKQuickInfoTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_11.cs)]

3. 添加设置字段并将鼠标悬停事件处理程序的构造函数。

     [!code-vb[VSSDKQuickInfoTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_12.vb)]
     [!code-csharp[VSSDKQuickInfoTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_12.cs)]

4. 添加的鼠标悬停事件处理程序触发 QuickInfo 会话。

     [!code-vb[VSSDKQuickInfoTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_13.vb)]
     [!code-csharp[VSSDKQuickInfoTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_13.cs)]

5. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A>方法，以便它时从文本视图分离控制器中移除的鼠标悬停事件处理程序。

     [!code-vb[VSSDKQuickInfoTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_14.vb)]
     [!code-csharp[VSSDKQuickInfoTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_14.cs)]

6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A>方法和<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A>为此示例中的空方法的方法。

     [!code-vb[VSSDKQuickInfoTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_15.vb)]
     [!code-csharp[VSSDKQuickInfoTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_15.cs)]

## <a name="implementing-the-quickinfo-controller-provider"></a>实现快速信息控制器提供程序
 QuickInfo 控制器的提供者提供主要是为了导出本身为 MEF 组件部分实例化 QuickInfo 控制器。 因为它是 MEF 组件部分，它可以导入其他 MEF 组件部分。

### <a name="to-implement-the-quickinfo-controller-provider"></a>若要实现 QuickInfo 控制器提供程序

1. 声明一个名为的类`TestQuickInfoControllerProvider`，它实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider>，并将其与导出<xref:Microsoft.VisualStudio.Utilities.NameAttribute>的"工具提示 QuickInfo Controller"和一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text":

     [!code-vb[VSSDKQuickInfoTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_16.vb)]
     [!code-csharp[VSSDKQuickInfoTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_16.cs)]

2. 将 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> 作为属性导入。

     [!code-vb[VSSDKQuickInfoTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_17.vb)]
     [!code-csharp[VSSDKQuickInfoTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_17.cs)]

3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A>通过实例化的快速信息控制器方法。

     [!code-vb[VSSDKQuickInfoTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_18.vb)]
     [!code-csharp[VSSDKQuickInfoTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_18.cs)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，生成 QuickInfoTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-quickinfotest-solution"></a>若要生成和测试 QuickInfoTest 解决方案

1. 生成解决方案。

2. 当在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包括单词"添加"和"减去"。

4. 将指针移动一个出现的"添加"。 签名和说明`add`应显示方法。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到的文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)