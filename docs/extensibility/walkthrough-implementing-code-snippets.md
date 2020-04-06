---
title: 演练：实现代码段 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: acangialosi
ms.author: anthc
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: ba1b6e0852c1ec1b306938b791eed78e79d211ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697103"
---
# <a name="walkthrough-implement-code-snippets"></a>演练：实现代码段
您可以创建代码段并将其包含在编辑器扩展中，以便扩展的用户可以将它们添加到自己的代码中。

 代码段是可以合并到文件中的代码或其他文本片段。 要查看已注册为特定编程语言的所有代码段，请在 **"工具"** 菜单上单击**代码段管理器**。 若要在文件中插入代码段，请右键单击所需的代码段，单击"插入代码段"或"**环绕"，** 找到所需的代码段，然后双击该代码段。 按 **"选项卡**"或 **"移位**+**"选项卡**可修改代码段的相关部分，然后按**Enter**或**Esc**将其接受。 有关详细信息，请参阅[代码代码段](../ide/code-snippets.md)。

 代码段包含在具有 .snippet® 文件名扩展名的 XML 文件中。 代码段可以包含插入代码段后突出显示的字段，以便用户可以查找和更改这些字段。 代码段文件还为**代码代码段管理器**提供信息，以便它可以在正确的类别中显示代码段名称。 有关代码段架构的信息，请参阅[代码代码段架构引用](../ide/code-snippets-schema-reference.md)。

 本演练将介绍如何完成这些任务：

1. 为特定语言创建和注册代码段。

2. 将 **"插入代码段"** 命令添加到快捷菜单。

3. 实现代码段扩展。

   本演练基于[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-and-register-code-snippets"></a>创建和注册代码段
 通常，代码段与注册的语言服务相关联。 但是，您不必实现<xref:Microsoft.VisualStudio.Package.LanguageService>注册代码段。 相反，只需在代码段索引文件中指定 GUID，然后在添加到项目中的 GUID<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>中使用相同的 GUID。

 以下步骤演示如何创建代码段并将其与特定的 GUID 相关联。

1. 创建以下目录结构：

    **%安装 Dir%\测试片段\片段\1033\\**

    *其中 %InstallDir%* 是可视化工作室安装文件夹。 （尽管此路径通常用于安装代码段，但您可以指定任何路径。

2. 在 {1033} 文件夹中，创建一个 *.xml*文件并将其命名为**TestSnippets.xml**。 （尽管此名称通常用于代码段索引文件，但只要具有 *.xml*文件名扩展名，就可以指定任何名称。添加以下文本，然后删除占位符 GUID 并添加您自己的文本。

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

3. 在代码段文件夹中创建文件，命名它**测试**`.snippet`，然后添加以下文本：

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

   以下步骤演示如何注册代码段。

### <a name="to-register-code-snippets-for-a-specific-guid"></a>注册特定 GUID 的代码段

1. 打开**完成测试**项目。 有关如何创建此项目的信息，请参阅[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

2. 在项目中，添加对以下程序集的引用：

    - 微软.VisualStudio.文本管理器.互通

    - 微软.VisualStudio.文本管理器.Interop.8.0

    - 微软.msxml

3. 在项目中，打开**源.扩展.vsixmanifest**文件。

4. 确保 **"资产"** 选项卡包含**VsPackage**内容类型，并且**项目**已设置为项目的名称。

5. 选择"完成测试"项目，并在"属性"窗口集中**将 Pkgdef 文件生成****为 true**。 保存项目。

6. 向项目添加`SnippetUtilities`静态类。

     [!code-csharp[VSSDKCompletionTest#22](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_1.cs)]
     [!code-vb[VSSDKCompletionTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_1.vb)]

7. 在代码段实用程序类中，定义 GUID 并赋予它在*代码段索引.xml*文件中使用的值。

     [!code-csharp[VSSDKCompletionTest#23](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_2.cs)]
     [!code-vb[VSSDKCompletionTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_2.vb)]

8. 将<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>添加到`TestCompletionHandler`类。 此属性可以添加到项目中的任何公共或内部（非静态）类。 （您可能需要为 Microsoft 添加`using`指令。VisualStudio.Shell 命名空间。

     [!code-csharp[VSSDKCompletionTest#24](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_3.cs)]
     [!code-vb[VSSDKCompletionTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_3.vb)]

9. 生成并运行该项目。 在运行项目时开始的 Visual Studio 实验实例中，您刚刚注册的代码段应以**TestSnippets**语言显示在**代码片段管理器**中。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>将"插入代码段"命令添加到快捷菜单
 文本文件的快捷菜单中不包括"**插入代码段"** 命令。 因此，必须启用 该命令。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>将"插入代码段"命令添加到快捷菜单

1. 打开类`TestCompletionCommandHandler`文件。

     由于此类实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，因此可以在<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法中激活**插入代码段**命令。 在启用该命令之前，请检查在自动化函数中未调用此方法，因为单击 **"插入代码段"** 命令时，将显示代码段选取器用户界面 （UI）。

     [!code-csharp[VSSDKCompletionTest#25](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_4.cs)]
     [!code-vb[VSSDKCompletionTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_4.vb)]

2. 生成并运行该项目。 在实验实例中，打开具有 *.zzz*文件名扩展名的文件，然后右键单击其中的任意位置。 **"插入代码段"** 命令应出现在快捷菜单上。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>在代码段选取器 UI 中实现代码段扩展
 本节演示如何实现代码段扩展，以便在单击快捷菜单上单击**插入代码段**时显示代码段选取器 UI。 当用户键入代码段快捷方式然后按**Tab**时，代码段也会展开。

 要显示代码段选取器 UI 并启用导航和插入后代码段接受，<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>请使用 方法。 插入本身由 方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>处理。

 代码段扩展的实现使用旧接口<xref:Microsoft.VisualStudio.TextManager.Interop>。 从当前编辑器类转换为旧代码时，请记住，旧接口使用行号和列号的组合来指定文本缓冲区中的位置，但当前类使用一个索引。 因此，如果缓冲区有三行，每行有 10 个字符（加上一个换行符，这表示为一个字符），则第三行的第四个字符在当前实现中位于位置 27，但它位于旧实现中的行 2 位置 3。

#### <a name="to-implement-snippet-expansion"></a>实现代码段扩展

1. 到包含类`TestCompletionCommandHandler`的文件，添加以下`using`指令。

     [!code-csharp[VSSDKCompletionTest#26](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_5.cs)]
     [!code-vb[VSSDKCompletionTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_5.vb)]

2. 使`TestCompletionCommandHandler`类实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>接口。

     [!code-csharp[VSSDKCompletionTest#27](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_6.cs)]
     [!code-vb[VSSDKCompletionTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_6.vb)]

3. 在`TestCompletionCommandHandlerProvider`类中，导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>。

     [!code-csharp[VSSDKCompletionTest#28](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_7.cs)]
     [!code-vb[VSSDKCompletionTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_7.vb)]

4. 为代码扩展接口和 添加一些私有字段<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。

     [!code-csharp[VSSDKCompletionTest#29](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_8.cs)]
     [!code-vb[VSSDKCompletionTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_8.vb)]

5. 在类的构造函数中`TestCompletionCommandHandler`，设置以下字段。

     [!code-csharp[VSSDKCompletionTest#30](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_9.cs)]
     [!code-vb[VSSDKCompletionTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_9.vb)]

6. 若要在用户单击 **"插入代码段"** 命令时显示代码段选取器，请将以下代码添加到<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法。 （为了使此解释更具可读性，不`Exec()`显示用于语句完成的代码;相反，代码块将添加到现有方法中。在检查字符的代码之后添加以下代码块。

     [!code-csharp[VSSDKCompletionTest#31](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_10.cs)]
     [!code-vb[VSSDKCompletionTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_10.vb)]

7. 如果代码段具有可导航的字段，则扩展会话将保持打开状态，直到显式接受扩展;如果代码段没有字段，则会话将关闭，`null`并由<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A>方法返回。 在方法<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>中，在上一步中添加的代码段选取器 UI 代码后，添加以下代码来处理代码段导航（当用户在代码段插入后按**Tab**或**Shift**+**选项卡**）。

     [!code-csharp[VSSDKCompletionTest#32](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_11.cs)]
     [!code-vb[VSSDKCompletionTest#32](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_11.vb)]

8. 若要在用户键入相应的快捷方式然后按**Tab**时插入代码段，<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>请向 方法添加代码。 插入代码段的私有方法将在后面的步骤中显示。 在上一步骤中添加的导航代码后添加以下代码。

     [!code-csharp[VSSDKCompletionTest#33](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_12.cs)]
     [!code-vb[VSSDKCompletionTest#33](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_12.vb)]

9. 实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>接口的方法。 在此实现中，唯一感兴趣的方法是<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>。 其他方法应该返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>。

     [!code-csharp[VSSDKCompletionTest#34](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_13.cs)]
     [!code-vb[VSSDKCompletionTest#34](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_13.vb)]

10. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 方法。 后续步骤将介绍实际插入扩展的帮助器方法。 提供<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>行和列信息，可以从 获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。

     [!code-csharp[VSSDKCompletionTest#35](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_14.cs)]
     [!code-vb[VSSDKCompletionTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_14.vb)]

11. 以下私有方法基于快捷方式或标题和路径插入代码段。 然后，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A>它使用代码段调用方法。

     [!code-csharp[VSSDKCompletionTest#36](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_15.cs)]
     [!code-vb[VSSDKCompletionTest#36](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_15.vb)]

## <a name="build-and-test-code-snippet-expansion"></a>生成和测试代码段扩展
 您可以测试代码段扩展是否在项目中有效。

1. 生成解决方案。 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

2. 打开文本文件并键入一些文本。

3. 右键单击文本中的某处，然后单击"**插入代码段**"。

4. 代码段选取器 UI 应带有一个弹出窗口，其中显示 **"测试替换字段**"。 双击弹出窗口。

     应插入以下代码段。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     不要按**Enter**或**Esc**。

5. 按 **"选项卡****"和"移位**+**"选项卡**在"第一"和"第二"之间切换。

6. 通过按**Enter**或**Esc**接受插入。

7. 在文本的不同部分，键入"测试"，然后按**Tab**。由于"测试"是代码段快捷方式，因此应再次插入代码段。

## <a name="next-steps"></a>后续步骤
