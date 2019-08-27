---
title: 演练：显示智能标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - smart tags
ms.assetid: 10bb4f69-b259-41f0-b91a-69b04385d9a5
caps.latest.revision: 31
manager: jillfra
ms.openlocfilehash: 116f76324a2150413c0ae6d08bc99e114efcc50e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436515"
---
# <a name="walkthrough-displaying-smarttags"></a>演练：显示智能标记
为支持灯泡已弃用智能标记。 请参阅[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)。  
  
 智能标记是文本上的标记，展开即可显示一组操作。 例如，在 Visual Basic 或 Visual C# 项目中，重命名变量名称等标识符时，单词下方将出现一条红线。 将指针移到下划线上时，指针旁将出现一个按钮。 如果单击该按钮，则会显示建议的操作，例如“将 IsRead 重命名为 IsReady” 。 如果单击该操作，则项目中对 **IsRead** 的所有引用均将重命名为 **IsReady**。  
  
 虽然智能标记是编辑器中 IntelliSense 实现的一部分，但是你可以通过子类化 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag>，然后实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 接口和 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> 接口来实现智能标记。  
  
> [!NOTE]
> 可以采用类似的方式实现其他类型的标记。  
  
 下面的演练演示如何创建一个智能标记，将显示在当前单词上并且具有两个建议的操作：**将转换为大写**并**转换为小写**。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
#### <a name="to-create-a-mef-project"></a>创建 MEF 项目  
  
1. 创建编辑器分类器项目。 将解决方案命名为 `SmartTagTest`。  
  
2. 在 VSIX 清单编辑器中打开 source.extension.vsixmanifest 文件。  
  
3. 确保“资产”  部分包含 `Microsoft.VisualStudio.MefComponent` 类型，“源”  设置为 `A project in current solution`，并且“项目”  设置为 SmartTagTest.dll。  
  
4. 保存并关闭 source.extension.vsixmanifest。  
  
5. 将以下引用添加到项目，并将“CopyLocal”  设置为 `false`：  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
6. 删除现有的类文件。  
  
## <a name="implementing-a-tagger-for-smart-tags"></a>实现智能标记的标记器  
  
#### <a name="to-implement-a-tagger-for-smart-tags"></a>实现智能标记的标记器  
  
1. 添加一个类文件并将其命名为 `TestSmartTag`。  
  
2. 添加以下导入内容：  
  
     [!code-csharp[VSSDKSmartTagTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#1)]
     [!code-vb[VSSDKSmartTagTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#1)]  
  
3. 添加一个从 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag> 继承的名为 `TestSmartTag` 的类。  
  
     [!code-csharp[VSSDKSmartTagTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#2)]
     [!code-vb[VSSDKSmartTagTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#2)]  
  
4. 为此类添加一个使用 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType> 的 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType> 调用基构造函数的构造函数，这将导致单词的第一个字符下方出现一条蓝线。 （如果使用 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType>，则单词的最后一个字符下方将出现一条红线。）  
  
     [!code-csharp[VSSDKSmartTagTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#3)]
     [!code-vb[VSSDKSmartTagTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#3)]  
  
5. 添加一个从 `TestSmartTag` 类型的 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 继承的名为 `TestSmartTagger` 的类，并实现 <xref:System.IDisposable>。  
  
     [!code-csharp[VSSDKSmartTagTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#4)]
     [!code-vb[VSSDKSmartTagTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#4)]  
  
6. 将以下私有字段添加到标记器类。  
  
     [!code-csharp[VSSDKSmartTagTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#5)]
     [!code-vb[VSSDKSmartTagTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#5)]  
  
7. 添加一个设置私有字段并订阅 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 事件的构造函数。  
  
     [!code-csharp[VSSDKSmartTagTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#6)]
     [!code-vb[VSSDKSmartTagTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#6)]  
  
8. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>，以便为当前的单词创建标记。 （此方法还会调用私有方法 `GetSmartTagActions` ，此方法将在后面介绍。）  
  
     [!code-csharp[VSSDKSmartTagTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#7)]
     [!code-vb[VSSDKSmartTagTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#7)]  
  
9. 添加 `GetSmartTagActions` 方法以设置智能标记操作。 这些操作将在后续步骤中自行实现。  
  
     [!code-csharp[VSSDKSmartTagTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#8)]
     [!code-vb[VSSDKSmartTagTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#8)]  
  
10. 声明 `SmartTagsChanged` 事件。  
  
     [!code-csharp[VSSDKSmartTagTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#9)]
     [!code-vb[VSSDKSmartTagTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#9)]  
  
11. 实现 `OnLayoutChanged` 事件处理程序以引发 `TagsChanged` 事件，这将调用 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>。  
  
     [!code-csharp[VSSDKSmartTagTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#10)]
     [!code-vb[VSSDKSmartTagTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#10)]  
  
12. 实现 <xref:System.IDisposable.Dispose%2A> 方法，以便取消订阅 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 事件。  
  
     [!code-csharp[VSSDKSmartTagTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#11)]
     [!code-vb[VSSDKSmartTagTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#11)]  
  
## <a name="implementing-the-smart-tag-tagger-provider"></a>实现智能标记标记器提供程序  
  
#### <a name="to-implement-the-smart-tag-tagger-provider"></a>实现智能标记标记器提供程序  
  
1. 添加一个从 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> 继承的名为 `TestSmartTagTaggerProvider` 的类。 导出为以下形式：具有“text”的 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>、Before="default" 的 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> 以及 <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag> 的 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>。  
  
     [!code-csharp[VSSDKSmartTagTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#12)]
     [!code-vb[VSSDKSmartTagTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#12)]  
  
2. 将 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 作为属性导入。  
  
     [!code-csharp[VSSDKSmartTagTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#13)]
     [!code-vb[VSSDKSmartTagTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#13)]  
  
3. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> 方法。  
  
     [!code-csharp[VSSDKSmartTagTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#14)]
     [!code-vb[VSSDKSmartTagTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#14)]  
  
## <a name="implementing-smart-tag-actions"></a>实现智能标记操作  
  
#### <a name="to-implement-smart-tag-actions"></a>实现智能标记操作  
  
1. 创建两个类，第一个名为 `UpperCaseSmartTagAction` ，第二个名为 `LowerCaseSmartTagAction`。 两个类都实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagAction>。  
  
    [!code-csharp[VSSDKSmartTagTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#15)]
    [!code-vb[VSSDKSmartTagTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#15)]  
  
    [!code-csharp[VSSDKSmartTagTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#16)]
    [!code-vb[VSSDKSmartTagTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#16)]  
  
   这两个类相似，只不过其中一个调用 <xref:System.String.ToUpper%2A>，另一个调用 <xref:System.String.ToLower%2A>。 以下步骤仅说明大写操作类，但你必须实现这两个类。 将实现大写操作的步骤用作实现小写操作的模式。  
  
2. 声明一组私有字段。  
  
    [!code-csharp[VSSDKSmartTagTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#17)]
    [!code-vb[VSSDKSmartTagTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#17)]  
  
3. 添加设置该字段的构造函数。  
  
    [!code-csharp[VSSDKSmartTagTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#18)]
    [!code-vb[VSSDKSmartTagTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#18)]  
  
4. 如下所示实现属性。  
  
    [!code-csharp[VSSDKSmartTagTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#19)]
    [!code-vb[VSSDKSmartTagTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#19)]  
  
5. 通过将范围中的文本替换为其大写形式来实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagAction.Invoke%2A> 方法。  
  
    [!code-csharp[VSSDKSmartTagTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#20)]
    [!code-vb[VSSDKSmartTagTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#20)]  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 要测试此代码，请生成 SmartTagTest 解决方案并在实验实例中运行它。  
  
#### <a name="to-build-and-test-the-smarttagtest-solution"></a>生成和测试 SmartTagTest 解决方案  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本。  
  
     文本第一个单词的首字母下应显示一条蓝线。  
  
4. 将指针移到蓝线上。  
  
     指针旁将出现一个按钮。  
  
5. 当单击按钮时，应显示两个建议的操作：**将转换为大写**并**转换为小写**。 如果单击第一个操作，则当前单词中的所有文本都将转换为大写。 如果单击第二个操作，则所有文本都将转换为小写。  
  
## <a name="see-also"></a>请参阅  
 [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)