---
title: 演练：实现代码段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: madskristensen
ms.author: madsk
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 84674a12165a3c5cd47c9004274669d377d330c5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72632511"
---
# <a name="walkthrough-implement-code-snippets"></a>演练：实现代码片段
你可以创建代码片段并将它们包含在编辑器扩展中，以便扩展的用户可以将其添加到自己的代码中。

 代码段是可以在文件中合并的代码片段或其他文本。 若要查看已注册特定编程语言的所有代码段，请在 "**工具**" 菜单上单击 "**代码片段管理器**"。 若要在文件中插入代码片段，请右键单击要在其中放置代码片段的位置，单击 "插入代码片段" 或 "**外侧**代码"，找到所需的代码段，然后双击它。 按**tab**或**Shift** + "**选项卡**以修改代码段的相关部分，然后按**enter**或**Esc**来接受它。 有关详细信息，请参阅[代码片段](../ide/code-snippets.md)。

 代码片段包含在具有代码片段 * 文件扩展名的 XML 文件中。 代码段可以包含在插入代码段之后突出显示的字段，以便用户可以查找并更改它们。 代码片段文件还为**代码片段管理器**提供信息，以便它可以在正确的类别中显示代码片段名称。 有关代码片段架构的信息，请参阅[代码片段架构参考](../ide/code-snippets-schema-reference.md)。

 本演练介绍了如何完成以下任务：

1. 创建并注册特定语言的代码段。

2. 将 "**插入代码段**" 命令添加到快捷菜单。

3. 实现代码段扩展。

   本演练基于[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

## <a name="prerequisites"></a>Prerequisites
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-and-register-code-snippets"></a>创建和注册代码段
 通常，代码片段与注册的语言服务相关联。 但是，您不必实现 <xref:Microsoft.VisualStudio.Package.LanguageService> 来注册代码段。 相反，只需在代码段索引文件中指定一个 GUID，然后在添加到项目的 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> 中使用同一 GUID 即可。

 以下步骤演示如何创建代码段并将其与特定 GUID 相关联。

1. 创建以下目录结构：

    **%InstallDir%\TestSnippets\Snippets\1033 \\**

    其中 *% InstallDir%* 是 Visual Studio 安装文件夹。 （虽然此路径通常用于安装代码段，但你可以指定任何路径。）

2. 在 \ 1033 \ 文件夹中，创建一个 *.xml*文件并将其命名为**TestSnippets**。 （虽然此名称通常用于代码段索引文件，但你可以指定任何名称，只要它具有 *.xml*文件扩展名。）添加以下文本，然后删除占位符 GUID 并添加自己的 GUID。

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

3. 在 "代码段" 文件夹中创建一个文件，将其命名为**test** `.snippet`，然后添加以下文本：

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

1. 打开**CompletionTest**项目。 有关如何创建此项目的信息，请参阅[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)。

2. 在项目中，添加对以下程序集的引用：

    - VisualStudio. TextManager

    - VisualStudio. TextManager. 8。0

    - microsoft msxml

3. 在项目中，打开**source.extension.vsixmanifest**文件。

4. 请确保 "**资产**" 选项卡包含**VsPackage**内容类型，并且该**项目**已设置为项目的名称。

5. 选择 CompletionTest 项目，并在 "将 **.Pkgdef 文件生成**到属性窗口" 设置为**true**。 保存项目。

6. 将静态 `SnippetUtilities` 类添加到项目。

     [!code-csharp[VSSDKCompletionTest#22](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_1.cs)]
     [!code-vb[VSSDKCompletionTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_1.vb)]

7. 在 SnippetUtilities 类中，定义一个 GUID，并为其指定在*SnippetsIndex*文件中使用的值。

     [!code-csharp[VSSDKCompletionTest#23](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_2.cs)]
     [!code-vb[VSSDKCompletionTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_2.vb)]

8. 将 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> 添加到 `TestCompletionHandler` 类。 此属性可添加到项目中的任何公共或内部（非静态）类中。 （可能需要为 VisualStudio 命名空间添加一个 `using` 指令。）

     [!code-csharp[VSSDKCompletionTest#24](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_3.cs)]
     [!code-vb[VSSDKCompletionTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_3.vb)]

9. 生成并运行该项目。 在运行项目时启动的 Visual Studio 的实验实例中，你刚注册的代码段应在**TestSnippets**语言下显示在**代码段管理器**中。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>将 "插入代码段" 命令添加到快捷菜单
 "**插入代码段**" 命令不包含在文本文件的快捷菜单中。 因此，您必须启用命令。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>将 "插入代码段" 命令添加到快捷菜单

1. 打开 `TestCompletionCommandHandler` 类文件。

     由于此类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，因此你可以在 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法中激活 "**插入代码段**" 命令。 启用该命令之前，请检查未在自动化函数内调用此方法，因为在单击 "**插入代码段**" 命令时，它将显示代码段选取器用户界面（UI）。

     [!code-csharp[VSSDKCompletionTest#25](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_4.cs)]
     [!code-vb[VSSDKCompletionTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_4.vb)]

2. 生成并运行该项目。 在实验实例中，打开文件扩展名为*zzz*的文件，然后右键单击其中的任意位置。 "**插入代码段**" 命令应出现在快捷菜单上。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>在代码段选取器 UI 中实现代码段扩展
 本部分演示如何实现代码片段扩展，以便在快捷菜单上单击**插入代码段**时显示代码段选取器 UI。 用户键入代码段快捷方式，然后按**Tab 键**时，还会展开代码片段。

 若要显示代码段选取器 UI 并启用导航和插入后代码段接受，请使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 插入本身由 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 方法处理。

 代码片段扩展的实现使用旧 <xref:Microsoft.VisualStudio.TextManager.Interop> 接口。 当您从当前编辑器类转换为旧代码时，请记住，旧接口使用行号和列号的组合在文本缓冲区中指定位置，但当前类使用一个索引。 因此，如果缓冲区包含三行，其中每个行都有10个字符（加上一个字符作为一个字符的行），则第三行中的第四个字符在当前实现中的位置27，但在旧实现中的位置为第2个。

#### <a name="to-implement-snippet-expansion"></a>实现代码段扩展

1. 对于包含 `TestCompletionCommandHandler` 类的文件，请添加以下 `using` 指令。

     [!code-csharp[VSSDKCompletionTest#26](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_5.cs)]
     [!code-vb[VSSDKCompletionTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_5.vb)]

2. 使 `TestCompletionCommandHandler` 类实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> 接口。

     [!code-csharp[VSSDKCompletionTest#27](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_6.cs)]
     [!code-vb[VSSDKCompletionTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_6.vb)]

3. 在 `TestCompletionCommandHandlerProvider` 类中，导入 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>。

     [!code-csharp[VSSDKCompletionTest#28](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_7.cs)]
     [!code-vb[VSSDKCompletionTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_7.vb)]

4. 为代码扩展接口和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 添加一些私有字段。

     [!code-csharp[VSSDKCompletionTest#29](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_8.cs)]
     [!code-vb[VSSDKCompletionTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_8.vb)]

5. 在 `TestCompletionCommandHandler` 类的构造函数中，设置以下字段。

     [!code-csharp[VSSDKCompletionTest#30](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_9.cs)]
     [!code-vb[VSSDKCompletionTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_9.vb)]

6. 若要在用户单击 "**插入代码段**" 命令时显示代码段选取器，请将以下代码添加到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 （若要使此说明可读性更高，则不会显示用于语句完成的 `Exec()`code，而是将代码块添加到现有方法中。）在用于检查字符的代码后添加以下代码块。

     [!code-csharp[VSSDKCompletionTest#31](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_10.cs)]
     [!code-vb[VSSDKCompletionTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_10.vb)]

7. 如果代码段包含可导航的字段，扩展会话将一直保持打开状态，直到显式接受扩展;如果代码段没有字段，则会话将关闭并以 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> 方法 `null` 的方式返回。 在 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法中，在您在上一步中添加的代码段选取器 UI 代码之后，添加以下代码以处理代码段导航（当用户在代码段插入后按**tab**或**Shift** +**tab** ）。

     [!code-csharp[VSSDKCompletionTest#32](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_11.cs)]
     [!code-vb[VSSDKCompletionTest#32](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_11.vb)]

8. 若要在用户键入相应的快捷方式时插入代码段，然后按**Tab**，请将代码添加到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 稍后的步骤会显示插入代码段的私有方法。 将以下代码添加到在上一步中添加的导航代码之后。

     [!code-csharp[VSSDKCompletionTest#33](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_12.cs)]
     [!code-vb[VSSDKCompletionTest#33](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_12.vb)]

9. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> 接口的方法。 在此实现中，只 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 相关方法。 其他方法应该只返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。

     [!code-csharp[VSSDKCompletionTest#34](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_13.cs)]
     [!code-vb[VSSDKCompletionTest#34](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_13.vb)]

10. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 方法。 稍后的步骤介绍了实际插入扩展的帮助器方法。 @No__t_0 提供了行和列信息，你可以从 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 中获取这些信息。

     [!code-csharp[VSSDKCompletionTest#35](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_14.cs)]
     [!code-vb[VSSDKCompletionTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_14.vb)]

11. 以下私有方法基于快捷方式或标题和路径插入代码片段。 然后，它通过代码段调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> 方法。

     [!code-csharp[VSSDKCompletionTest#36](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_15.cs)]
     [!code-vb[VSSDKCompletionTest#36](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_15.vb)]

## <a name="build-and-test-code-snippet-expansion"></a>生成和测试代码片段扩展
 可以测试项目中的代码片段扩展是否正常工作。

1. 生成解决方案。 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

2. 打开一个文本文件并键入一些文本。

3. 右键单击文本中的某个位置，然后单击 "**插入代码片段**"。

4. 代码段选取器 UI 应显示一个弹出窗口，其中显示了 "**测试替换字段**"。 双击弹出窗口。

     应插入以下代码段。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     不要按**enter**或**Esc 键**。

5. 按**tab**并按下**Shift** + "**选项卡**，在" first "和" second "之间切换。

6. 按**enter**或**Esc**接受插入。

7. 在文本的其他部分中，键入 "test"，然后按**tab**。由于 "test" 是代码段快捷方式，因此应再次插入代码段。

## <a name="next-steps"></a>后续步骤
