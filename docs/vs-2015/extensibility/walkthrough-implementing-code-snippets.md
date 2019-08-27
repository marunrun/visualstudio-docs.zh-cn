---
title: 演练：实现代码片段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb720589bc9bc31b7cf2a04b05559cb9c9d46961
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201984"
---
# <a name="walkthrough-implementing-code-snippets"></a>演练：实现代码片段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以创建的代码段，并将其包含在编辑器扩展，以便扩展的用户可以将它们添加到其自己的代码。  
  
 代码片段是一段代码或其他可合并的文件中的文本。 若要查看已为特定编程语言中注册的所有代码段**工具**菜单上，单击**代码片段管理器**。 若要插入代码段在文件中，右键单击要代码片段中，单击**插入代码段**或**Surround With**、 找到所需的代码段，然后双击它。 按 TAB 或 SHIFT + TAB 修改代码段的相关部分，然后按 ENTER 或 esc 键来接受它。 有关详细信息，请参阅[代码片段](../ide/code-snippets.md)。  
  
 代码段包含在具有.snippet 文件扩展名的 XML 文件中。 代码片段可以包含插入代码段，以便用户可以查找和更改它们之后会突出显示的字段。 代码片段文件还提供了有关的信息**代码片段管理器**，以便它可以正确类别中显示代码段名称。 有关代码段架构信息，请参阅[代码片段架构参考](../ide/code-snippets-schema-reference.md)。  
  
 本演练介绍了如何完成这些任务：  
  
1. 创建并注册为特定语言的代码段。  
  
2. 添加**插入代码段**向快捷菜单命令。  
  
3. 实现展开代码片段。  
  
   此演练基于[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。  
  
## <a name="prerequisites"></a>先决条件  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-and-registering-code-snippets"></a>创建和注册的代码片段  
 通常情况下，代码片段是与已注册的语言服务相关联。 但是，不需要实现<xref:Microsoft.VisualStudio.Package.LanguageService>注册代码段。 相反，只需在代码片段索引文件中指定一个 GUID，然后使用中的相同 GUID<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>添加到你的项目。  
  
 以下步骤演示如何创建代码段并将其关联与特定的 GUID。  
  
1. 创建以下目录结构：  
  
    **%InstallDir%\TestSnippets\Snippets\1033\\**  
  
    其中 *%installdir%* 是 Visual Studio 安装文件夹。 （尽管此路径通常用来安装代码片段，你可以指定任何路径）。  
  
2. \1033\ 文件夹中创建的.xml 文件并将其命名**TestSnippets.xml**。 （尽管此名称通常用于代码片段索引文件，您可以指定任何名称，只要它具有文件扩展名为.xml。）添加以下文本，然后删除占位符 GUID 并添加您自己。  
  
   ```xml  
   <?xml version="1.0" encoding="utf-8" ?>  
   <SnippetCollection>  
       <Language Lang="TestSnippets" Guid="{00000000-0000-0000-0000-000000000000}">  
           <SnippetDir>  
               <OnOff>On</OnOff>  
               <Installed>true</Installed>  
               <Locale>1033</Locale>  
               <DirPath>%InstallRoot%\TestSnippets\Snippets\%LCID%\</DirPath>  
               <LocalizedName>Snippets</LocalizedName>  
           </SnippetDir>  
       </Language>  
   </SnippetCollection>  
   ```  
  
3. 在代码片段文件夹中创建一个文件，将其命名**测试**`.snippet`，然后添加以下文本：  
  
   ```xml  
   <?xml version="1.0" encoding="utf-8" ?>  
   <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
       <CodeSnippet Format="1.0.0">  
           <Header>  
               <Title>Test replacement fields</Title>  
               <Shortcut>test</Shortcut>  
               <Description>Code snippet for testing replacement fields</Description>  
               <Author>MSIT</Author>  
               <SnippetTypes>  
                   <SnippetType>Expansion</SnippetType>  
               </SnippetTypes>  
           </Header>  
           <Snippet>  
               <Declarations>  
                   <Literal>  
                     <ID>param1</ID>  
                       <ToolTip>First field</ToolTip>  
                       <Default>first</Default>  
                   </Literal>  
                   <Literal>  
                       <ID>param2</ID>  
                       <ToolTip>Second field</ToolTip>  
                       <Default>second</Default>  
                   </Literal>  
               </Declarations>  
               <References>  
                  <Reference>  
                      <Assembly>System.Windows.Forms.dll</Assembly>  
                  </Reference>  
               </References>  
               <Code Language="TestSnippets">  
                   <![CDATA[MessageBox.Show("$param1$");  
        MessageBox.Show("$param2$");]]>  
               </Code>    
           </Snippet>  
       </CodeSnippet>  
   </CodeSnippets>  
   ```  
  
   以下步骤说明如何注册的代码段。  
  
#### <a name="to-register-code-snippets-for-a-specific-guid"></a>若要为特定 GUID 注册代码片段  
  
1. 打开**CompletionTest**项目。 有关如何创建此项目的信息，请参阅[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。  
  
2. 在项目中，添加对以下程序集的引用：  
  
    - Microsoft.VisualStudio.TextManager.Interop  
  
    - Microsoft.VisualStudio.TextManager.Interop.8.0  
  
    - microsoft.msxml  
  
3. 在项目中，打开 source.extension.vsixmanifest 文件中。  
  
4. 请确保**资产**选项卡包含**VsPackage**内容类型，且**项目**设置为项目的名称。  
  
5. 选择 CompletionTest 项目，然后在属性窗口中设置**生成 Pkgdef 文件**到**true**。 保存项目。  
  
6. 添加静态`SnippetUtilities`到项目的类。  
  
     [!code-csharp[VSSDKCompletionTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#22)]
     [!code-vb[VSSDKCompletionTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#22)]  
  
7. 在 SnippetUtilities 类中，定义一个 GUID，并为其提供 SnippetsIndex.xml 文件中使用的值。  
  
     [!code-csharp[VSSDKCompletionTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#23)]
     [!code-vb[VSSDKCompletionTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#23)]  
  
8. 添加<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>到`TestCompletionHandler`类。 此属性可以添加到项目中的任何公共或内部 （非静态） 类。 (您可能必须添加`using`Microsoft.VisualStudio.Shell 命名空间的语句。)  
  
     [!code-csharp[VSSDKCompletionTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#24)]
     [!code-vb[VSSDKCompletionTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#24)]  
  
9. 生成并运行该项目。 在运行项目时启动的 Visual Studio 的实验实例中，只需注册的代码片段应显示在**代码片段管理器**下**TestSnippets**语言。  
  
## <a name="adding-the-insert-snippet-command-to-the-shortcut-menu"></a>将插入代码片段命令添加到快捷菜单  
 **插入代码段**命令不会包含文本文件的快捷菜单。 因此，必须启用该命令。  
  
#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>若要添加到快捷菜单插入代码段命令  
  
1. 打开`TestCompletionCommandHandler`类文件。  
  
     因为此类实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，则可以激活**插入代码片段**命令，在<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法。 启用该命令之前，请检查，因为自动化函数内部不调用此方法时**插入代码段**单击命令时，它将显示代码片段选取器用户界面 (UI)。  
  
     [!code-csharp[VSSDKCompletionTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#25)]
     [!code-vb[VSSDKCompletionTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#25)]  
  
2. 生成并运行该项目。 在实验实例中，打开具有.zzz 文件扩展名的文件，并右键单击任意位置它。 **插入代码段**命令应显示的快捷菜单上。  
  
## <a name="implementing-snippet-expansion-in-the-snippet-picker-ui"></a>在代码片段选取器 UI 中实现展开代码片段  
 本部分演示如何实现代码片段扩展以使代码片段选取器 UI 时显示**插入代码段**快捷菜单上单击。 当用户键入的代码片段快捷方式并按下 TAB 组合键时，也会扩展代码片段。  
  
 若要显示的代码片段选取器 UI 并启用导航并接受后插入代码片段，请使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法。 插入操作本身由<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>方法。  
  
 代码片段扩展的实现使用旧版<xref:Microsoft.VisualStudio.TextManager.Interop>接口。 转换时从当前的编辑器类到旧代码，请记住，旧式界面使用行号和列号的组合可以在文本缓冲区中，指定位置，但当前类使用一个索引。 因此，如果缓冲区具有每个都有 10 个字符的三行 （加上一个换行符，计为 1 个字符），在第三行的第四个字符位于位置 27 在当前实现中，但它是第 2 行，则位置 3 旧实现中。  
  
#### <a name="to-implement-snippet-expansion"></a>若要实现展开代码片段  
  
1. 对包含文件`TestCompletionCommandHandler`类中，添加以下`using`语句。  
  
     [!code-csharp[VSSDKCompletionTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#26)]
     [!code-vb[VSSDKCompletionTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#26)]  
  
2. 请`TestCompletionCommandHandler`类实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>接口。  
  
     [!code-csharp[VSSDKCompletionTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#27)]
     [!code-vb[VSSDKCompletionTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#27)]  
  
3. 在中`TestCompletionCommandHandlerProvider`类中，导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>。  
  
     [!code-csharp[VSSDKCompletionTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#28)]
     [!code-vb[VSSDKCompletionTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#28)]  
  
4. 添加一些代码扩展接口的私有字段和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。  
  
     [!code-csharp[VSSDKCompletionTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#29)]
     [!code-vb[VSSDKCompletionTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#29)]  
  
5. 构造函数中`TestCompletionCommandHandler`类中，设置以下字段。  
  
     [!code-csharp[VSSDKCompletionTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#30)]
     [!code-vb[VSSDKCompletionTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#30)]  
  
6. 若要显示的代码片段选取器，当用户单击**插入代码段**命令，将以下代码添加到<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法。 （若要使这种解释更具可读性，exec （） 用于语句完成不显示代码; 相反，将代码块添加到现有的方法。）检查字符的代码后面添加以下代码块。  
  
     [!code-csharp[VSSDKCompletionTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#31)]
     [!code-vb[VSSDKCompletionTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#31)]  
  
7. 如果代码片段具有可导航的字段，扩展会话保持打开状态直到显式接受扩展;如果代码片段不具有任何字段，该会话已关闭，并且返回作为`null`通过<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A>方法。 在<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法，代码片段选取器在上一步骤中，添加的 UI 代码之后添加以下代码以处理段导航 （当用户在插入代码段后按 TAB 或 SHIFT + TAB）。  
  
     [!code-csharp[VSSDKCompletionTest#32](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#32)]
     [!code-vb[VSSDKCompletionTest#32](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#32)]  
  
8. 若要插入代码片段，当用户键入相应的快捷方式并按下 TAB 组合键时，将代码添加到<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法。 私有方法，它将插入代码段将在稍后的步骤中所示。 在上一步中添加的导航代码后面添加以下代码。  
  
     [!code-csharp[VSSDKCompletionTest#33](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#33)]
     [!code-vb[VSSDKCompletionTest#33](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#33)]  
  
9. 实现方法的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>接口。 在此实现中，所需的唯一方法是<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>。 其他方法应只返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>。  
  
     [!code-csharp[VSSDKCompletionTest#34](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#34)]
     [!code-vb[VSSDKCompletionTest#34](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#34)]  
  
10. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 方法。 将在后面的步骤介绍实际插入扩展的帮助器方法。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>提供了行和列信息，你可以从获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。  
  
     [!code-csharp[VSSDKCompletionTest#35](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#35)]
     [!code-vb[VSSDKCompletionTest#35](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#35)]  
  
11. 以下专用方法，将插入代码段中，基于该快捷方式或根据标题和路径。 然后，它调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A>方法与该代码段。  
  
     [!code-csharp[VSSDKCompletionTest#36](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#36)]
     [!code-vb[VSSDKCompletionTest#36](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#36)]  
  
## <a name="building-and-testing-code-snippet-expansion"></a>生成和测试代码片段扩展  
 您可以测试是否在项目中的展开代码片段可以正常工作。  
  
1. 生成解决方案。 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
2. 打开一个文本文件并键入一些文本。  
  
3. 右键单击文本中的某个位置，然后依次**插入代码段**。  
  
4. 片段选取器中的 UI 应显示使用弹出窗口，指出**测试替换字段**。 双击弹出窗口中。  
  
     应插入以下代码片段。  
  
    ```  
    MessageBox.Show("first");  
    MessageBox.Show("second");  
    ```  
  
     不要按 ENTER 或 esc 键。  
  
5. 按 TAB 键和 SHIFT + TAB 切换"first"和"第二个"之间。  
  
6. 按 ENTER 或 esc 键以接受插入。  
  
7. 在文本的不同部分中，键入"test"，然后按选项卡。 由于"test"的代码片段快捷方式，应再次插入代码段。  
  
## <a name="next-steps"></a>后续步骤
