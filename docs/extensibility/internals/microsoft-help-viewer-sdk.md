---
title: Microsoft 帮助查看器 SDK |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a3e7cc2064e1ce74e2256d2246e46d2960c1cacc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349299"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft Help Viewer SDK

本文包含 Visual Studio 帮助查看器集成商的以下任务：

- 正在创建主题 （F1 支持）

- 创建帮助查看器内容品牌包

- 部署一组文章

- 添加到 Visual Studio shell （集成或独立） 的帮助

- 其他资源

## <a name="create-a-topic-f1-support"></a>创建主题 （F1 支持）

本部分概述的组件提供的主题，主题要求、 如何创建使用其呈现结果的主题 （包括 F1 支持要求） 和最后，示例主题的简短说明。

**帮助查看器主题概述**

呈现的调用时主题，帮助查看器获取标记时的安装或上一次更新，以及主题 XHTML，主题与相关联的包元素，并结合了两个导致呈现的内容视图 (品牌数据 +主题数据）。  品牌包中包含徽标、 对内容的行为和品牌文本 （版权，等） 的支持。  请"创建品牌包"参阅下面有关品牌包元素的详细信息。  事件没有任何与主题相关联的品牌包，则帮助查看器将使用位于帮助查看器应用程序根目录 (Branding_en US.mshc) 中的回退品牌包。

**帮助查看器主题要求**

若要在帮助查看器中正确呈现，原始的主题内容必须是 W3C 基本 1.1 XHTML。

主题通常包含两个部分：

- 元数据 （请参阅内容元数据引用）： 有关主题，例如，主题的唯一 ID，主题 TOC ID 的关键字值的数据的父节点 ID，等等。

- 正文内容： 符合 W3C 基本 1.1 XHTML，其中包括支持内容行为 （可折叠区域、 代码段等。完整列表如下所示）。

Visual Studio 品牌包支持的控件：

- 链接

- CodeSnippet

- CollapsibleArea

- 继承的成员

- LanguageSpecificText

受支持的语言字符串 （不区分大小写）：

- javascript

- c# 或 c#

- cplusplus 或 visual c + + 或 c + +

- jscript

- visual basic 或 vb

- f #、 fsharp 或 fs

- 其他-一个字符串，表示语言名称

**创建一个帮助查看器的主题**

创建名为 ContosoTopic4.htm，新的 XHTML 文档并包括 title 标记 （下面）。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

接下来，添加数据如何定义主题的方式显示 （自身或不带有品牌信息），若要引用本主题的 F1，此主题在目录中，其 ID （对于通过其他主题的链接引用） 中存在的位置，等等。请参阅"内容元数据"下表中支持的元数据的完整列表。

- 在这种情况下，我们将使用我们自己的品牌包，Visual Studio 帮助查看器品牌包的一个变体。

- 添加 F1 元名称和值 ("Microsoft.Help.F1"内容 ="ContosoTopic4")，将匹配 IDE 属性包中提供的 F1 值。 （请参阅 F1 支持部分，了解详细信息。）这是与 F1 匹配的值从 IDE 以在 IDE 中选择 f1 键时显示此主题中的调用。

- 添加主题 id。 这是其他主题用于链接到本主题的字符串。 它是本主题的帮助查看器 ID。

- 目录中，将添加本主题的父节点，以定义此主题 TOC 节点出现的位置。

- 目录中，将添加本主题的节点顺序。 当父节点具有`n`编号的子节点按子节点的顺序定义本主题的位置。 例如，本主题是多 4 个 4 子主题。

元数据示例部分：

```html
<html>
<head>
<title>Contoso Topic 4</title>

<meta name="SelfBranded" content="false" />
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />

</head>

<body>

</body>
</html>
```

**主题正文**

（不包括页眉和页脚） 主题的正文将包含页的链接、 注意部分、 可折叠区域、 代码段中和特定于语言的文本的一部分。  请参阅品牌部分以了解有关这些方面提供主题的信息。

1. 添加主题标题标记：  `<div class="title">Contoso Topic 4</div>`

2. 添加注释部分： `<div class="alert"> add your table tag and text </div>`

3. 添加的可折叠区域：  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. 添加代码片段：  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. 添加代码特定于语言的文本：`<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` 请注意，`devLangnu=`允许您输入其他语言。 例如，`devLangnu="Fortran"`显示 Fortran 时代码片段 DisplayLanguage = Fortran

6. 添加页链接： `<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注意： 对于不受支持新"显示语言"(示例中， F#，Cobol、 Fortran) 中的代码段的代码着色将单色。

**示例帮助查看器主题**该代码演示如何定义元数据、 代码段、 可折叠区域中和特定于语言的文本。

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
<head>
<title>Contoso Topic 4</title>

    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />
<meta name="SelfBranded" content="false" />
</head>

<body>
<div class="title">Contoso Topic 4</div>

  <div id="header">
<table id="bottomTable" cellpadding="0" cellspacing="0"  width="100%">
        <tr id="headerTableRow2"><td align="left">
            <span id="nsrTitle">Contoso Topic 1</span>
          </td>
<td align="right">
</td></tr>
<tr id="headerTableRow1"><td align="left">
            <span id="runningHeaderText">Contoso Widgets & Sprockets</span>
          </td></tr>
      </table>
</div>

<h2>Table of Contents</h2>

<ul class="toc">
<li class="tocline1"><a href="#introduction" target="_self">1.0 Introduction</a></li>
<li class="tocline1"><a href="#seealso" target="_self">See Also</a></li>
</ul>

<div class="topic">

<div id="mainSection">
<div id="mainBody">

<a name="introduction"></a>
<h2>1.0 Introduction</h2>
<p>[This documentation is for sample purposes only.]</p>

<p>Contoso Topic 1 contains examples of:
<ul>
<li>Collapsible Area</li>
<li>Bookmark ("See also")</li>
<li>Code Snippets from Branding Package</li>
</ul>
 </p>
<div class="alert"><table><tr><th>
<strong>Note </strong></th></tr>
<tr><td>
<p>This is an example of a <span class="label">Note </span>section.
Call out important items for your reader in this <span class="label">Note </span>box.
</p></td></tr>
</table>
</div>
</div>

<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading">

            <a id="sectionToggle0"><!----></a>

<div>
Example of Collapsible Area
<br/>
Lorem ipsum dolor sit amet...
</div>
</CollapsibleArea>

<div id="snippetGroup" >
<CodeSnippet EnableCopyCode="true" Language="VisualBasic" ContainsMarkup="false" DisplayLanguage="Visual Basic" >
Private Sub ToolStripRenderer1_RenderGrip(sender as Object, e as ToolStripGripRenderEventArgs) _ Handles ToolStripRenderer1.RenderGrip
Dim messageBoxVB as New System.Text.StringBuilder()
    messageBoxVB.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds)
    messageBoxVB.AppendLine()
 ...
    MessageBox.Show(messageBoxVB.ToString(),"RenderGrip Event")
End Sub
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" >
private void ToolStripRenderer1_RenderGrip(Object sender, ToolStripGripRenderEventArgs e)
{
System.Text.StringBuilder messageBoxCS = new System.Text.StringBuilder();
messageBoxCS.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds );
messageBoxCS.AppendLine();
...
MessageBox.Show(messageBoxCS.ToString(), "RenderGrip Event" );
}
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="fsharp" ContainsMarkup="false" DisplayLanguage="F#" >
some F# code
</CodeSnippet>
</div>

<h4 class="subHeading">Example of code specific text</h4>Language = <LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />

<a name="seealso"></a>
<h1 class="heading">See Also</h1>

    <div id="seeAlsoSection" class="section">
    <div class="seeAlsoStyle">
        <a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>
```

**F1 支持**

在 Visual Studio 中，选择 F1 生成在 IDE 中光标的位置提供的值，并填充"属性包"使用提供的值 （基于光标所在的位置。 当光标位于功能 x 时，功能 x 是活动/的焦点，并填充值的属性包。  选择 F1 时填充的属性包和 Visual Studio F1 代码看起来是否有客户默认帮助源本地或联机 （online 是默认值），然后创建根据设置的用户的相应字符串 （online 是默认值） 的命令行程序执行（请参阅帮助管理员指南以便了解 exe 启动参数） 的本地帮助查看器 + 如果本地帮助是默认值或包含在参数列表中的关键字的 MSDN URL 属性包中的关键字的参数。

如果为 F1 返回三个字符串，引用要为多值字符串，第一个词，查找为执行一次点击，并且如果找到，我们已完成;否则，将移动到下一个字符串。  顺序很重要。 表示法的多值关键字应该是最长到最短的字符串的字符串。  若要验证这一点在多值的关键字的情况下，查看将包含所选的关键字的联机 F1 URL 字符串。

在 Visual Studio 2012 中，我们有意之间所做更强的除联机还是脱机，因此，如果用户的设置为联机，然后我们只需 F1 请求直接传递到我们的联机查询服务 MSDN，而无需通过帮助库代理路由我们将在 Visual Studio 2010 中。 我们然后依赖于状态的"安装的供应商内容 = true"以确定是否要执行该上下文中的其他内容。 如果为 true，我们则执行此解析和路由的逻辑，具体取决于你想要为客户支持。 如果为 false，然后我们只需转到 MSDN。 如果用户的设置为 Local，则所有调用都转到本地帮助引擎。

F1 流关系图：

![F1 流](../../extensibility/internals/media/f1flow.png "F1flow")

如果帮助查看器的默认帮助内容源设置为联机状态 （启动浏览器中）：

- Visual Studio 合作伙伴 (VSP) 功能发出到 F1 属性包 （属性包 prefix.keyword 和注册表中找到前缀为 online URL） 的值：F1 VSP URL + 参数向浏览器发送。

- Visual Studio 功能 （语言编辑器，Visual Studio 特定菜单项，等等。）：F1 将 Visual Studio URL 发送到浏览器。

如果帮助查看器的默认帮助内容源设置为本地帮助 （启动帮助查看器中）：

- VSP 功能关键字 F1 属性包和本地存储区索引之间的匹配位置 (即，属性包 prefix.keyword = 本地存储索引中找到的值):F1 呈现帮助查看器中的主题。

- Visual Studio 功能 （VSP 重写从 Visual Studio 功能发出的属性包的任何选项）：F1 呈现帮助查看器中的 Visual Studio 主题。

设置以下注册表值可让 F1 回退供应商的帮助内容。 F1 回退意味着帮助查看器设置为查找 F1 帮助内容的联机，供应商内容本地安装到用户的硬盘。 即使默认设置是联机帮助的帮助查看器应查看本地帮助内容。

1. 设置**VendorContent**帮助 2.3 注册表项下的值：

   - 对于 32 位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent"= dword: 00000001

   - 对于 64 位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent"= dword: 00000001

2. 注册帮助 2.3 注册表项下的合作伙伴命名空间：

   - 对于 32 位操作系统：

      HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner<em>\\<namespace\></em>

      "位置"="脱机"

   - 对于 64 位操作系统：

      HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner<em>\\<namespace\></em>

      "位置"="脱机"

**分析的基础本机 Namespace**

若要启用分析的基础本机命名空间，请在注册表中添加一个新的 dword 值的名称：BaseNativeNamespaces 并将其值设置为 1 （在下他们想要支持的目录键）。  例如，如果你想要使用 Visual Studio 目录，无法将密钥添加到路径：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

当遇到标头/方法的格式中的 F1 关键字时，/ 字符将分析，从而导致以下构造：

- 标头： 将可用于在注册表中注册的命名空间

- 方法： 这将成为获取传递的关键字。

例如，给定一个名为 CustomLibrary 的自定义库和一个名为 MyTestMethod，当请求传入 F1 将被格式化为方法`CustomLibrary/MyTestMethod`。

用户可以注册 CustomLibrary 为命名空间位于合作伙伴的配置单元，并提供他们所需的任何位置密钥并且传递给查询的关键字将 MyTestMethod。

**启用调试工具在 IDE 中的帮助**

添加以下注册表项和值：

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic Help**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Dynamic Help**

::: moniker-end

值：零售数据中显示调试输出：是

在 IDE 中下的帮助菜单项，选择**调试帮助上下文**。

**内容元数据**

下表中出现的括号之间的任何字符串是一个占位符，必须替换为已识别的值。 例如，在\<元 name="Microsoft.Help.Locale"内容 ="[语言代码]"/ >，"[语言代码]"必须替换为一个值，例如"en-我们"。

| 属性 （HTML 表示形式） | 描述 |
| - | - |
| \< meta name="Microsoft.Help.Locale" content="[language-code]" /> | 设置本主题中的区域设置。 如果在主题中使用此标记，则它必须使用只需一次并且必须插入以上任何其他 Microsoft 帮助标记该域。 如果未使用此标记，通过使用断字符与该键关联的产品区域设置中，如果指定它，则为索引的主题的正文文本否则为 en-我们使用断字符。 ISOC RFC 4646 符合此标记。 若要确保 Microsoft 帮助正确工作，而不是常规的语言属性使用此属性。 |
| \< meta name="Microsoft.Help.TopicLocale" content="[language-code]" /> | 设置本主题中的区域设置时也可使用其他区域设置。 如果在主题中使用此标记，则必须使用它只需一次。 该目录包含多个语言的内容时，请使用此标记。 在目录中的多个主题可以有相同的 ID，但每次必须指定唯一 TopicLocale。 指定匹配的区域设置 TopicLocale 的主题是目录的目录中显示的主题。 但是，在搜索结果中显示的主题的所有语言版本。 |
| \< 标题 > [Title] \< /t > | 指定此主题的标题。 此标记是必需的并且必须使用在主题中的只是一次。 如果该主题的正文不包含标题\<d i v > 部分中，此标题将显示在主题以及目录中。 |
| \< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/> | 指定在帮助查看器的索引窗格中显示的链接的文本。 单击该链接时，将显示主题。 你可以指定多个索引关键字主题，或如果不希望出现在索引中本主题的链接，则可以忽略此标记。 从早期版本的帮助"K"关键字可以转换为此属性。 |
| \< meta name="Microsoft.Help.Id" content="[TopicID]"/> | 设置本主题的标识符。 此标记是必需的并且必须使用在主题中的只是一次。 ID 必须是唯一的目录中的主题，具有相同的区域设置。 在另一个主题中，可以创建此主题的链接，通过使用此 id。 |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/> | 指定此主题的 F1 关键字。 你可以指定多个主题的 F1 关键字，或如果不希望应用程序用户按 F1 时要显示本主题，则可以忽略此标记。 通常情况下，只需一个 F1 关键字指定主题。 从早期版本的帮助的"F"关键字可以转换为此属性。 |
| \< meta name="Description" content="[topic description]" /> | 提供了此主题中的内容的简短摘要。 如果在主题中使用此标记，则必须使用它只需一次。 此属性可直接通过查询库中;它不存储在索引文件。 |
| meta name="Microsoft.Help.TocParent" content="[parent_Id]"/> | 指定目录中的本主题的父主题。 此标记是必需的并且必须使用在主题中的只是一次。 值是父级的 Microsoft.Help.Id。 本主题可以只是一个表中的内容的位置。 "-1"被视为目录根的主题 ID。 在[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]，该网页是帮助查看器主页。 这是我们明确将 TocParent = 1 添加到一些主题，以确保，它们显示在顶部级别相同的原因。 帮助查看器主页上是系统页面并因此不可替换。 如果 VSP 尝试添加 id 为-1 页，它可能会添加到内容集，但帮助查看器将始终使用系统页的帮助查看器主页 |
| \< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/> | 指定的目录中本主题的显示位置相对于其对等主题。 此标记是必需的并且必须使用在主题中的只是一次。 值是一个整数。 指定的值较小的整数的主题的主题，它指定更高价值整数上方会出现。 |
| \< meta name="Microsoft.Help.Product" content="[product code]"/> | 指定本主题介绍该产品。 如果在主题中使用此标记，则必须使用它只需一次。 此外可以作为参数传递给帮助索引器提供此信息。 |
| \< 元 name="Microsoft.Help.ProductVersion"内容 ="[版本号]"/ > | 指定本主题介绍该产品的版本。 如果在主题中使用此标记，则必须使用它只需一次。 此外可以作为参数传递给帮助索引器提供此信息。 |
| \< meta name="Microsoft.Help.Category" content="[string]"/> | 按产品用于标识子节的内容。 可以标识多个小节的一个主题，或如果不希望标识任何子节的链接，则可以忽略此标记。 此标记用于目标 Os 和 TargetFrameworkMoniker 存储属性，当一个主题转换从早期版本的帮助。 内容的格式为 AttributeName:AttributeValue。 |
| \< 元 name="Microsoft.Help.TopicVersion 内容 ="[主题版本编号]"/ > | 在目录中存在多个版本时，请指定此版本的主题。 Microsoft.Help.Id 不保证是唯一的因为多个版本的主题的目录中存在，例如，目录中包含的主题针对.NET Framework 3.5 和主题，针对.NET Framework 4 和都具有相同的 Micro 时此标记时需要软。Help.Id。 |
| \< 元名称 ="SelfBranded"content ="[TRUE 或 FALSE]"/ > | 指定本主题使用 Help Library 管理器启动品牌包或特定于主题的品牌包。 此标记必须为 TRUE 或 FALSE。 如果其值为 TRUE，则关联的主题的品牌包重写 Help Library 管理器启动，以便运行安装程序，即使它不同于其他内容的呈现呈现主题时设置的品牌包。 如果为 FALSE，基于 Help Library 管理器启动时设置的品牌包呈现当前主题。 默认情况下，Help Library 管理器假定自品牌，除非 SelfBranded 变量声明为 TRUE; 否则为 false因此，不需要声明\<元名称 ="SelfBranded"content ="FALSE"/ >。 |

## <a name="create-a-branding-package"></a>创建品牌包

Visual Studio 版本包含许多不同 Visual Studio 产品，包括 Visual Studio 合作伙伴： 独立和集成的 shell。  每个这些产品需要某种程度的基于主题的帮助内容的品牌支持，唯一的产品。  例如，Visual Studio 主题需要具有一致的品牌的演示内容，而 SQL Studio，包装 ISO Shell，则需要其自己唯一的帮助内容的标记每个主题。  集成的 Shell 合作伙伴可以其维护其自己的主题品牌时是在父 Visual Studio 产品的帮助内容的帮助主题。

安装品牌包包含帮助查看器的产品。  用于 Visual Studio 产品：

- 回退的品牌包 (Branding_\<区域设置 > 能使用.mshc) 安装帮助查看器 2.3 应用根目录中 (示例：C:\Program 文件 (x86) \Microsoft Help Viewer\v2.3) 的帮助查看器语言包。  这用于未安装任一产品品牌包的情况下 （已安装任何内容），或者其中已安装的品牌包已损坏。  使用应用程序根回退品牌包时，会忽略 （徽标和反馈） 的 Visual Studio 元素。

- Visual Studio 内容安装时从内容包服务，品牌包也会安装 （适用于第一个时间内容安装方案）。  如果没有对品牌包的更新，更新安装的下一次的内容更新或其他包安装操作发生时。

Microsoft 帮助查看器支持基于主题的元数据的主题的品牌。

- 其中主题元数据定义自助品牌 = true，呈现主题原样，不执行任何操作 （至于品牌）。

- 其中主题元数据定义自助品牌 = false，使用与 TopicVendor 元数据值关联的品牌包。

- 其中主题元数据定义 name="Microsoft.Help.TopicVendor"内容 =\<中供应商 MSHA 品牌包名称 >，使用中的内容值定义的品牌包。

- Visual Studio 目录中没有的品牌包的优先级应用程序。  应用第一个 Visual Studio 默认品牌，，然后，如果主题元数据中定义和支持 （如安装 msha 中定义） 相关联的品牌包，供应商定义的品牌应用作为替代。

标记元素通常分为三个主要类别：

- （示例包括反馈链接、 条件免责声明文本、 徽标） 的标头元素

- 内容行为 （示例包括展开/折叠控件文本元素和代码片段元素）

- 页脚元素 （例如版权）

考虑，因为经过品牌打造的元素包括的项 （此规范中详细说明）：

- 目录/产品徽标 （例如，Visual Studio）

- 反馈链接和电子邮件元素

- 免责声明文本

- 版权文本

在 Visual Studio 帮助查看器品牌包的支持文件包括：

- 图形 （徽标、 图标等）

- Branding.js-脚本文件支持内容的行为

- Branding.xml-一致地使用在目录内容的字符串。  注意： 对于 branding.xml，在 Visual Studio 本地化文本元素包含 _locID ="\<唯一值 >"

- Branding.css-样式定义的演示文稿一致性

- Printing.css-一致打印的演示文稿的样式定义

如上文所述，品牌包相关联的主题：

- 当 SelfBranded = false 定义的元数据中的主题继承品牌包的目录

- 时，或者当 SelfBranded = false 和那里唯一的品牌包在 MSHA 和定义可用时安装内容

用于实现自定义品牌包的 Vsp (VSP 内容，SelfBranded = True)，继续执行的一种方法是启动与回退品牌包 （安装与帮助查看器），并将更改为相应的文件的名称。  Branding_\<区域设置 > 能使用.mshc 文件是更改为能使用.mshc 文件扩展名的 zip 文件，因此只需将扩展名从能使用.mshc 更改为.zip 并提取内容。  请参阅下面有关品牌包元素并根据需要修改 （例如，更改到 VSP 徽标和对 Branding.xml 文件中的徽标的引用的徽标、 Branding.xml 更新每个 VSP 详细信息，等等）。

完成所有修改后，创建包含所需的标记元素的 zip 文件并将扩展名更改为能使用.mshc。

若要将自定义品牌包相关联，创建 MSHA，其中包含对品牌的 mshc 文件和内容 mshc （包含主题） 的引用。  请参阅下面有关如何创建基本 MSHA"MSHA"。

Branding.xml 文件包含用于本主题包含时一致地呈现在主题中的特定项的元素的列表\<元 name="Microsoft.Help.SelfBranded"内容 ="false"/ >。  下面列出了 Visual Studio 系列 Branding.xml 文件中的元素。  此列表用于根据需求的 ISO Shell 采用者，它们在其中修改这些元素 （例如徽标、 反馈和版权） 以满足自己的产品署名的模板使用。

注意： 标记"{n}"所示的变量具有代码依赖项-删除或更改这些值将导致错误和可能是应用程序崩溃。 在 Visual Studio 品牌包中包含本地化标识符 (示例 _locID="codesnippet.n")。

**Branding.xml**

| | |
| - | - |
| 功能： | **CollapsibleArea** |
| 使用: | 展开折叠内容控件文本 |
| **元素** | **值** |
| ExpandText | Expand |
| CollapseText | 折叠 |
| 功能： | **CodeSnippet** |
| 使用: | 代码片段控件文本。  注意:具有"非中断性"空间的代码段内容将更改为空间。 |
| **元素** | **值** |
| CopyToClipboard | 复制到剪贴板 |
| ViewColorizedText | 查看着色文本 |
| CombinedVBTabDisplayLanguage | Visual Basic （示例） |
| VBDeclaration | 声明 |
| VBUsage | 用法 |
| 功能： | **反馈、 页脚和徽标** |
| 使用: | 提供客户提供有关当前通过电子邮件主题的反馈的反馈控件。  版权文本内容。  徽标定义。 |
| **元素** | **值 （这些字符串可修改以满足内容采用者需要。）** |
| 版权所有 | © 2013 Microsoft Corporation. 保留所有权利。 |
| SendFeedback | \<a ="{0}" {1}> 发送反馈 \< /a > 有关此主题的 Microsoft。 |
| FeedbackLink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| 功能： | **免责声明** |
| 使用: | 一组计算机的特定于用例的免责声明翻译内容。 |
| **元素** | **值** |
| MT_Editable | 此文章由机器翻译。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| MT_NonEditable | 此文章由机器翻译。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| MT_QualityEditable | 此文章由人工翻译。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| MT_QualityNonEditable | 此文章由人工翻译。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| MT_BetaContents | 此文章由机器翻译，用于预发行版本。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| MT_BetaRecycledContents | 此文章由人工翻译的预发行版本。 如果您有 Internet 连接，选择"联机查看本主题"在同一时间在原始英文内容的可编辑模式下查看此页。 |
| 功能： | **LinkTable** |
| 使用: | 支持联机主题链接 |
| **元素** | **值** |
| LinkTableTitle | 链接表 |
| TopicEnuLinkText | 查看的英文版 \< /a > 可在您的计算机找到本主题。 |
| TopicOnlineLinkText | 查看本主题\<href ="{0}" {1}> 联机 \< /a > |
| OnlineText | Online |
| 功能： | **视频的音频控件** |
| 使用: | 显示元素和视频内容的文本 |
| **元素** | **值** |
| MultiMediaNotSupported | Internet Explorer 9 或更高版本必须安装以支持{0}内容。 |
| VideoText | 显示视频 |
| AudioText | 流式处理音频 |
| OnlineVideoLinkText | \<p > 若要查看与本主题相关的视频，请单击{0} \<href ="{1}">{2}此处\</a >。\</ p > |
| OnlineAudioLinkText | \<p > 若要收听与本主题相关的音频，请单击{0} \<href ="{1}">{2}此处\</a >。\</ p > |
| 功能： | **未安装的内容控件** |
| 使用: | 用于 contentnotinstalled.htm 呈现文本元素 （字符串） |
| **元素** | **值** |
| ContentNotInstalledTitle | 您的计算机上不找到任何内容。 |
| ContentNotInstalledDownloadContentText | \<p > 将内容下载到您的计算机\<href ="{0}" {1}> 单击管理选项卡\</a >。\</ p > |
| ContentNotInstalledText | \<p > 您的计算机上安装任何内容。 请参阅您的管理员以本地帮助内容安装。 \< /p > |
| 功能： | **主题找不到控件** |
| 使用: | 用于 topicnotfound.htm 呈现文本元素 （字符串） |
| **元素** | **值** |
| TopicNotFoundTitle | 您的计算机上找不到请求的主题。 |
| TopicNotFoundViewOnlineText | \<p > 您的计算机上找不到您请求的主题，但你可以\<href ="{0}" {1}> 联机查看主题\</a >。\</ p > |
| TopicNotFoundDownloadContentText | \<p > 请参阅有关类似主题的链接的导航窗格或\<href ="{0}" {1}> 单击管理选项卡\</a > 将内容下载到您的计算机。\</ p > |
| TopicNotFoundText | \<p > 您的计算机上找不到您请求的主题。 \< /p > |
| 功能： | **主题已损坏的控件** |
| 使用: | 用于 topiccorrupted.htm 呈现文本元素 （字符串） |
| **元素** | **值** |
| TopicCorruptedTitle | 无法显示请求的主题。 |
| TopicCorruptedViewOnlineText | \<p > 帮助查看器无法显示请求的主题。 可能有该主题的内容或基础系统依赖项中的错误。 \< /p > |
| 功能： | **主页上的控件** |
| 使用: | 支持帮助查看器的顶级节点内容的显示文本。 |
| **元素** | **值** |
| HomePageTitle | 帮助查看器主页 |
| HomePageIntroduction | \<p > 欢迎使用 Microsoft Help Viewer，为每个用户使用 Microsoft 工具、 产品、 技术和服务的信息的重要途径。 帮助查看器使您可以访问的操作方法和参考信息、 示例代码、 技术文章和的详细信息。 若要查找所需浏览内容目录的内容，请使用全文搜索，或通过内容使用关键字索引导航。 \< /p > |
| HomePageContentInstallText | \<p >\<b / > 使用\<href ="{0}" {1}> 管理内容\</a > 选项卡可执行以下操作：\<u l >\<l i > 将内容添加到您的计算机。\</ l i >\<l i > 检查本地内容的更新。\</ l i >\<l i > 从计算机中删除内容。\</ l i >\</u l > \< /p > |
| HomePageInstalledBooks | 已安装的书籍 |
| HomePageNoBooksInstalled | 您的计算机上不找到任何内容。 |
| HomePageHelpSettings | 帮助内容设置 |
| HomePageHelpSettingsText | \<p > 您的当前设置是本地帮助。 帮助查看器显示已安装在计算机的内容。\<b / > 若要更改您的源的帮助内容，在 Visual Studio 菜单栏上，选择\<s p a n style ="{0}"> 帮助，请设置帮助首选项\</s p a n >。\<b / > \< /p > |
| MegaByte | MB |

**branding.js**

Branding.js 文件包含由 Visual Studio 帮助查看器标记元素的 JavaScript。  下面是标记元素和支持的 JavaScript 函数的列表。  在此文件的顶部的"可本地化的字符串"部分中定义要本地化为此文件的所有字符串。  已为 branding.js 文件中的本地化字符串创建 ICL 文件。

||||
|-|-|-|
|**品牌功能**|**JavaScript 函数**|**说明**|
|Var...||定义变量|
|获取用户代码语言|setUserPreferenceLang|将索引映射到代码语言的 #|
|设置和获取 cookie 值|getCookie setCookie||
|继承的成员|changeMembersLabel|展开/折叠继承的成员|
|When SelfBranded=False|onLoad|读取查询字符串来检查其是否打印请求。  设置所有 codesnippets 将重点放在用户的首选选项卡。如果是打印请求，然后设置 isPrinterFriendly 为 true。 检查高对比度模式。|
|代码片段|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||ChangeTab||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|CollapsibleArea|addToCollapsibleControlSet|写入到列表中的所有可折叠控件对象。|
||CA_Click|基于状态的可折叠区域时，将定义的图像和文本呈现|
|对徽标的对比度支持|isBlackBackground()|调用以确定背景为黑色。  准确时，才在高对比度模式下。|
||isHighContrast()|使用彩色的跨度检测高对比度模式|
||onHighContrast(black)|检测到高对比度时调用|
|LST 功能|||
||addToLanSpecTextIdSet(id)||
||updateLST(currentLang)||
||getDevLangFromCodeSnippet(lang)||
|多媒体功能|标题 （开始，结束时，文本样式）||
||findAllMediaControls(normalizedId)||
||getActivePlayer(normalizedId)||
||captionsOnOff(id)||
||toSeconds(t)||
||getAllComments(node)||
||styleRectify(styleName, styleValue)||
||showCC(id)||
||subtitle(id)||

**HTM 文件**

品牌包中包含一组用于进行通信密钥信息的帮助内容的用户，例如主页，其中包含一节介绍了安装哪些内容集和页面时主题不能告诉用户支持方案的 HTM 文件本地组主题中找到。 按产品，可以修改这些 HTM 文件。  ISO Shell 供应商就能够获取默认品牌程序包并将更改的行为和这些页面的内容为套件需求。  这些文件是指其相应的品牌程序包以便从 branding.xml 文件中获取相应的内容的品牌标记。

||||
|-|-|-|
|**文件**|**使用**|**显示内容源**|
|homepage.htm|这是当前安装的内容，并相应向有关其内容的用户提供的任何其他消息将显示一个页面。  此文件具有其他的元数据属性"Microsoft.Help.Id"内容 ="-1"将此顶部本地内容目录的内容。||
||<META_HOME_PAGE_TITLE_ADD />|Branding.xml、 标记\<HomePageTitle >|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD />|Branding.xml、 标记\<HomePageIntroduction >|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD />|Branding.xml、 标记\<HomePageContentInstallText >|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD />|标题部分 Branding.xml 标记\<HomePageInstalledBooks >，从应用程序中，生成的数据\<HomePageNoBooksInstalled > 时则会安装没有书籍。|
||<HOME_PAGE_SETTINGS_SECTION_ADD />|标题部分 Branding.xml 标记\<HomePageHelpSettings >，部分文本\<HomePageHelpSettingsText >。|
|topiccorrupted.htm|当一个主题存在于本地集中，但由于某种原因不能显示 （已损坏的内容）。||
||<META_TOPIC_CORRUPTED_TITLE_ADD />|Branding.xml、 标记\<TopicCorruptedTitle >|
||<TOPIC_CORRUPTED_SECTION_ADD />|Branding.xml、 标记\<TopicCorruptedViewOnlineText >|
|topicnotfound.htm|当一个主题中未找到本地内容设置，也不提供联机||
||<META_TOPIC_NOT_FOUND_TITLE_ADD />|Branding.xml、 标记\<TopicNotFoundTitle >|
||<META_TOPIC_NOT_FOUND_ID_ADD />|Branding.xml, tag \<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD />|Branding.xml、 标记\<TopicNotFoundText >|
|contentnotinstalled.htm|当已安装了该产品没有本地内容。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD />|Branding.xml、 标记\<ContentNotInstalledTitle >|
||<META_CONTENT_NOT_INSTALLED_ID_ADD />|Branding.xml、 标记\<ContentNotInstalledDownloadContentText >|
||<CONTENT_NOT_INSTALLED_SECTION_ADD />|Branding.xml、 标记\<ContentNotInstalledText >|

**CSS 文件**

Visual Studio 帮助查看器品牌包包含两个 css 文件，以支持一致 Visual Studio 帮助内容的呈现：

- Branding.css-包含用于呈现 where css 元素 SelfBranded = false

- Printer.css-包含用于呈现 where css 元素 SelfBranded = false

Branding.css 文件包括 Visual Studio 主题的演示文稿的定义 (需要注意的是，branding.css 包含在 Branding_\<区域设置 > 从包服务能使用.mshc 可能会更改)。

**图形文件**

Visual Studio 内容显示 Visual Studio 徽标，以及其他图形。  Visual Studio 帮助查看器品牌包中的图形文件的完整列表如下所示。

||||
|-|-|-|
|**文件**|**使用**|**示例**|
|clear.gif|用于呈现可折叠区域||
|footer_slice.gif|页脚演示文稿||
|info_icon.gif|显示信息时使用|免责声明|
|online_icon.gif|此图标是为与联机链接相关联||
|tabLeftBD.gif|用于呈现代码片段容器||
|tabRightBD.gif|用于呈现代码片段容器||
|vs_logo_bk.gif|用于正常对比度徽标引用在 Branding.xml 标记中定义\<LogoFileName >。  对于 Visual Studio 产品徽标名称是 vs_logo_bk.gif。||
|vs_logo_wh.gif|用于正常高徽标引用在 Branding.xml 标记中定义\<LogoFileNameHC >。  对于 Visual Studio 产品徽标名称是 vs_logo_wh.gif。||
|ccOff.png|隐藏式字幕图||
|ccOn.png|隐藏式字幕图||
|ImageSprite.png|用于呈现可折叠区域|展开或折叠图|

## <a name="deploy-a-set-of-topics"></a>部署一的组主题

这是用于创建帮助查看器内容部署集 MSHA 文件和 cab 数或 MSHCs 包含主题的集合组成的简单和快速教程。 MSHA 是描述一组的 cab 文件的 XML 文件或 MSHC 文件。 帮助查看器可以读取 MSHA 获取一系列内容 (。CAB 或。MSHC 文件） 可用于本地安装。

这是仅用于帮助查看器 MSHA 描述非常基本的 XML 架构的入门读物。  没有此简要概述和示例 HelpContentSetup.msha 下面的示例实现。

此入门，出于 MSHA 的名称是文件的的 HelpContentSetup.msha （的名称可以是文件的任何内容，其扩展名。MSHA)。 HelpContentSetup.msha （下面的示例） 应包含 MSHCs 可用的 cab 文件的列表。  文件类型必须为 （不支持 MSHA 和 CAB 文件类型的组合） MSHA 中保持一致。 对于每个 CAB 或 MSHC，应该有\<d i v class ="软件包">...\</div > （请参阅下面的示例）。

注意： 在实现下面的示例，我们已提供很多品牌包。 这是必须包含，以便获取所需的 Visual Studio 内容呈现元素和内容行为。

示例 HelpContentSetup.msha 文件：(替换为"内容设置名称 1"和"内容集 name 2" 等文件名称。)

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>.
```

1. 创建本地文件夹，类似于"C:\SampleContent"

2. 对于此示例中，我们将使用 MSHC 文件以包含主题。  MSHC 是 zip 文件扩展名从.zip 到更改。MSHC。

3. 创建为文本文件的 HelpContentSetup.msha 如下 （记事本用于创建该文件） 并将其保存到上面记下文件夹 （请参阅步骤 1）。

类"品牌"存在且是唯一的。 品牌 mshc 包含在此入门中，以便安装的内容将具有品牌打造，并且 MSHCs 中包含的内容行为将品牌包中包含的相应的支持元素。 如果没有，系统会为不属于翻录 （安装） 的支持项内容时，将导致错误。

若要获取 Visual Studio 品牌包，将在 C:\Program Files (x86) \Microsoft Help Viewer\v2.3\ Branding_en US.mshc 文件复制到您的工作文件夹中。

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>
<div class="package">
<span class="packageType">branding</span>
<span class="name">Branding_en-US</span>
<span class="deployed">True</span>
<a class="current-link" href="Branding_en-US.mshc">Branding_en-US.mshc</a>
</div>
</div>
</body>
</html>
```

**摘要**

使用和扩展的上述步骤将启用 Vsp 来为 Visual Studio 帮助查看器中部署其内容集。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>将帮助添加到 Visual Studio Shell （集成和独立）

**介绍**

本演练演示如何将帮助内容合并到 Visual Studio Shell 应用程序，然后将其部署。

**要求**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [Visual Studio 2013 独立 Shell Redist](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**概述**

[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Shell 是版本的[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]IDE 可基于应用程序。 此类应用程序包含与你创建的扩展独立 Shell。 使用独立 Shell 项目模板，其中包含在[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]SDK 来构建的扩展。

创建基于独立 Shell 的应用程序和其帮助的基本步骤：

1. 获取[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]ISO Shell 可再发行组件 （Microsoft 下载中心）。

2. 在 Visual Studio 中，创建基于独立 Shell，例如帮助扩展，稍后在本演练中描述的 Contoso 帮助扩展。

3. 包装扩展和 ISO Shell 可再发行组件到部署 MSI （应用程序安装程序）。 本演练不包括安装步骤。

创建 Visual Studio 内容存储区。 对于集成外壳方案中，更改 Visual Studio12 为产品目录名称，如下所示：

- 创建文件夹 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15。

- 创建一个名为 CatalogType.xml 文件并将其添加到的文件夹。 该文件应包含以下代码行：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

在注册表中定义的内容存储。 有关集成 Shell 中，将更改 VisualStudio15 产品目录名称：

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   键:LocationPath 字符串值：C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   键:CatalogName 字符串值：[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档

**创建项目**

若要创建的独立 Shell 扩展：

1. 在 Visual Studio 中下,**文件**，选择**新项目**下**其他项目类型**选择**扩展性**，然后选择**Visual Studio 独立 Shell**。 将项目命名`ContosoHelpShell`) 创建基于 Visual Studio 独立 Shell 模板可扩展性项目。

2. 在解决方案资源管理器，在 ContosoHelpShellUI 项目中，在资源文件文件夹中，打开 ApplicationCommands.vsct。 请确保此行已被注释掉 （搜索"No_Help"）： `<!-- <define name="No_HelpMenuCommands"/> -->`

3. 选择 F5 键来编译和运行**调试**。 在隔离的 Shell IDE 的实验实例中，选择**帮助**菜单。 请确保**查看帮助**，**添加和删除帮助内容**，并**设置帮助首选项**命令将出现。

4. 在解决方案资源管理器，在 ContosHelpShell 项目中，在命令行程序自定义文件夹中，打开 ContosoHelpShell.pkgdef。 若要定义 Contoso 帮助目录，请添加以下行：

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. 在解决方案资源管理器，在 ContosHelpShell 项目中，在命令行程序自定义文件夹中，打开 ContosoHelpShell.Application.pkgdef。 若要启用 F1 帮助，请添加以下行：

    ```
    // F1 Help Provider

    [$RootKey$\HelpProviders\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="13407"
    "Package"="{DA9FB551-C724-11d0-AE1F-00A0C90FFFC3}"
    @="Help3 Provider"
    [$RootKey$\HelpProviders]
    @="{C99BDC23-FF29-46bf-9658-ADD634CCAED8}"
    [$RootKey$\Services\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="Help3 Provider"
    @="{4A791146-19E4-11D3-B86B-00C04F79F802}"
    ```

6. 在解决方案资源管理器，在 ContosoHelpShell 解决方案的上下文菜单上选择**属性**菜单项。 下**配置属性**，选择**Configuration Manager**。 在中**配置**列中，将每个"Debug"的值更改为"发布"。

7. 生成解决方案。 这将创建一组文件在发布文件夹中，将在下一节中使用。

若要测试这像部署：

1. 在计算机上部署 Contoso，安装下载的 ISO 命令行程序 （通过）。

2. 创建一个文件夹中的\\\Program Files (x86)\\，并将其命名`Contoso`。

3. 将内容复制到 ContosoHelpShell release 文件夹从\\\Program Files (x86) \Contoso\ 文件夹。

4. 通过选择启动注册表编辑器**运行**中**启动**菜单，然后输入`Regedit`。 在注册表编辑器中，选择**文件**，然后**导入**。 浏览到 ContosoHelpShell 项目文件夹。 在 ContosoHelpShell 子文件夹中，选择 ContosoHelpShell.reg。

5. 创建内容存储区：

    对于 ISO Shell-创建 Contoso 内容存储 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12

    有关[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]集成 Shell 中，创建文件夹 C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15

6. 创建 CatalogType.xml 并添加到包含的内容存储区 （上一步）：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 添加以下注册表项：

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key:LocationPath 字符串值：

    ISO shell:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 集成的 Shell:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-US

    键:CatalogName 字符串值：[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 文档。 对于 ISO Shell 中，这是你目录的名称。

8. 将你的内容 （cab 或 MSHC 和 MSHA） 复制到本地文件夹。

9. 用于测试的内容存储的示例集成 Shell 命令行。 ISO Shell 中，将更改相应以匹配该产品的目录和 launchingApp 值。

     "C:\Program Files (x86)\Microsoft Help Viewer\v2.3\HlpViewer.exe" /catalogName VisualStudio15 /helpQuery method="page&id=ContosoTopic0" /launchingApp Microsoft,VisualStudio,12.0

10. 启动 Contoso 应用程序 （从 Contoso 应用根目录开始）。 在 ISO Shell 中，选择**帮助**菜单项，并更改**设置帮助首选项**到**使用本地帮助**。

11. 在外壳中，选择**帮助**菜单项，然后**查看帮助**。 本地帮助查看器应会启动。 选择“管理内容”  选项卡。下**安装源**，选择**磁盘**选项按钮。 选择 **...** 按钮，并浏览到包含 Contoso 内容 （复制到上述步骤中的本地文件夹） 的本地文件夹。 选择 HelpContentSetup.msha。 Contoso 现在应显示为一本书中的通讯簿选择。 选择**外**，然后选择**更新**按钮 （底部右下角）。

12. Contoso IDE 中，选择 F1 键来测试 F1 功能。

## <a name="additional-resources"></a>其他资源

运行时 API，请参阅[Windows 帮助 API](/previous-versions/windows/desktop/helpapi/helpapi-portal)。

有关如何利用帮助 API 的详细信息，请参阅[帮助查看器的代码示例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)。

可以提交功能建议[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)。
