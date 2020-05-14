---
title: 微软帮助查看器 SDK |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 721623edabcaf3b395a143dd193cae3fd71d93d6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707155"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft Help Viewer SDK

本文包含可视化工作室帮助查看器集成商的以下任务：

- 创建主题（F1 支持）

- 创建帮助查看器内容品牌包

- 部署一组文章

- 向可视化工作室外壳添加帮助（集成或隔离）

- 其他资源

## <a name="create-a-topic-f1-support"></a>创建主题（F1 支持）

本节概述了呈现的主题的组件、主题要求、有关如何创建主题的简短说明（包括 F1 支持要求），最后提供了一个示例主题及其呈现的结果。

**帮助查看器主题概述**

当调用主题进行呈现时，帮助查看器获取在安装或上次更新时与主题关联的品牌包元素以及主题 XHTML，并将两者合并以产生呈现的内容视图（品牌数据 + 主题数据）。  品牌包包含徽标、对内容行为的支持以及品牌文本（版权等）。  有关品牌包元素的详细信息，请参阅下面的"创建品牌包"。  如果没有与主题关联的品牌包，帮助查看器将使用位于帮助查看器应用程序根（Branding_en-US.mshc）中的回退品牌包。

**帮助查看者主题要求**

要在帮助查看器中正确呈现，原始主题内容必须是 W3C 基本 1.1 XHTML。

主题通常包含两个部分：

- 元数据（请参阅内容元数据参考）：有关主题的数据，例如主题唯一 ID、关键字值、主题 TOC ID、父节点 ID 等。

- 正文内容：符合 W3C 基本 1.1 XHTML，其中包括支持的内容行为（可折叠区域、代码段等）。完整列表如下所示）。

支持可视化工作室品牌包的控件：

- 链接

- 代码段

- 可折叠区域

- 继承成员

- 语言特异性文本

支持的语言字符串（不区分大小写）：

- javascript

- csharp 或 c#

- 加号或视觉+或 c#

- jscript

- 视觉基础或 vb

- f# 或 fsharp 或 fs

- 其他 - 表示语言名称的字符串

**创建帮助查看器主题**

创建新的 XHTML 文档名为 ContosoTopic4.htm，并包括标题标记（如下所示）。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

接下来，添加数据以定义如何呈现主题（是否自品牌）、如何为 F1 引用此主题、该主题存在于 TOC 中、其 ID（供其他主题链接引用）等。有关支持的元数据的完整列表，请参阅下面的"内容元数据"表。

- 在这种情况下，我们将使用我们自己的品牌包，可视化工作室帮助查看器品牌包的变体。

- 添加与 IDE 属性袋中提供的 F1 值匹配的 F1 元名称和值（"Microsoft.Help.F1"内容="ContosoTopic4"）。 （有关详细信息，请参阅 F1 支持部分。这是从 IDE 中与 F1 调用匹配的值，用于在 IDE 中选择 F1 时显示此主题。

- 添加主题 ID。 这是其他主题用于链接到本主题的字符串。 它是本主题的帮助查看器 ID。

- 对于 TOC，添加本主题的父节点以定义本主题 TOC 节点的显示位置。

- 对于 TOC，添加本主题的节点顺序。 当父节点具有`n`子节点数时，请按子节点的顺序定义本主题的位置。 例如，本主题是 4 个子主题中的数字 4。

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

主题的正文（不包括标题和页脚）将包含页面链接、注释部分、可折叠区域、代码段和特定于语言的文本部分。  有关所介绍主题的这些领域的信息，请参阅品牌部分。

1. 添加主题标题标记：`<div class="title">Contoso Topic 4</div>`

2. 添加注释部分：`<div class="alert"> add your table tag and text </div>`

3. 添加可折叠区域：`<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. 添加代码段：`<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. 添加特定于代码语言的文本：`<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />`允许您输入其他`devLangnu=`语言的注释。 例如，`devLangnu="Fortran"`在代码段显示语言 + Fortran 时显示 Fortran

6. 添加页面链接：`<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注意：对于不支持的新"显示语言"（例如，F#、Cobol、Fortran），代码段中的代码着色将是单色的。

**帮助查看器主题示例**该代码说明了如何定义元数据、代码段、可折叠区域和特定于语言的文本。

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

在 Visual Studio 中，选择 F1 会生成从游标放置在 IDE 中提供的值，并填充带有提供值的"属性包"（基于光标位置）。 当光标超过特征 x 时，要素 x 处于活动状态/聚焦，并且用值填充属性包。  选择 F1 时，将填充属性包，Visual Studio F1 代码查看客户默认帮助源是本地还是联机（联机是默认值），然后根据用户设置（联机是默认值） 创建相应的字符串 - shell 执行（请参阅帮助管理员指南，了解 exe 启动参数），以及属性袋中的本地帮助查看器 + 关键字（如果本地帮助是默认值）的参数或参数列表中包含关键字的 MSDN URL。

如果为 F1 返回三个字符串（称为多值字符串），则采用第一个术语，查找命中，如果找到，我们就完成;如果没有，则移动到下一个字符串。  订单很重要。 多值关键字的表示应为最长字符串到最短字符串。  要验证多值关键字的情况，请查看联机 F1 URL 字符串，该字符串将包括所选关键字。

在 Visual Studio 2012 中，我们有意在联机和脱机之间进行更强烈的划分，因此，如果用户的设置是联机的，则只需将 F1 请求直接传递到 MSDN 上的联机查询服务，而不是通过 Visual Studio 2010 中的帮助库代理路由。 然后，我们依靠"已安装的供应商内容 = true"的状态来确定是否在这种情况下执行不同操作。 如果为 true，则根据您希望支持您的客户的内容执行此分析和路由逻辑。 如果为 false，则只需转到 MSDN。 如果用户的设置是本地，则所有呼叫都转到本地帮助引擎。

F1 流程图：

![F1 流](../../extensibility/internals/media/f1flow.png "F1流")

当帮助查看器默认帮助内容源设置为联机时（在浏览器中启动）：

- Visual Studio 合作伙伴 （VSP） 功能向 F1 属性包（属性包前缀.关键字和注册表中前缀的在线 URL）发出值：F1 向浏览器发送 VSP URL+ 参数。

- 可视化工作室功能（语言编辑器、可视化工作室特定菜单项等）：F1 向浏览器发送视觉工作室 URL。

当帮助查看器默认帮助内容源设置为本地帮助时（在帮助查看器中启动）：

- VSP 具有 F1 属性包和本地存储索引（即属性包前缀.关键字 = 本地存储索引中找到的值）之间的关键字匹配功能：F1 呈现帮助查看器中的主题。

- 可视化工作室功能（VSP 没有选项可以覆盖从 Visual Studio 功能发出的属性包）：F1 在帮助查看器中呈现视觉工作室主题。

设置以下注册表值，以便为供应商帮助内容启用 F1 回退。 F1 回退意味着帮助查看器设置为联机查找 F1 帮助内容，并且供应商内容在本地安装到用户的硬盘驱动器上。 帮助查看器应查看内容的本地帮助，即使默认设置用于联机帮助。

1. 在帮助 2.3 注册表键下设置**供应商内容**值：

   - 对于 32 位操作系统：

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "供应商内容"=dword：0000001

   - 对于 64 位操作系统：

        HKEY_LOCAL_MACHINE_SOFTWARE_Wow6432Node_微软\帮助\v2.3_目录_VisualStudio15

        "供应商内容"=dword：0000001

2. 在帮助 2.3 注册表项下注册合作伙伴命名空间：

   - 对于 32 位操作系统：

      HKEY_LOCAL_MACHINE_SOFTWARE_微软\帮助\v2.3_合作伙伴<em>\\<命名空间\></em>

      "位置"="脱机"

   - 对于 64 位操作系统：

      HKEY_LOCAL_MACHINE_软件_哇6432Node_微软\帮助\v2.3_合作伙伴<em>\\<命名空间\></em>

      "位置"="脱机"

**基本本机命名空间解析**

要打开基本本机命名空间解析，在注册表中添加一个新的 DWORD 名称：BaseNativeNamespace 并将其值设置为 1（在他们想要支持的目录键下）。  例如，如果要使用 Visual Studio 目录，则可以将密钥添加到路径：

HKEY_LOCAL_MACHINE_SOFTWARE_Wow6432Node_微软\帮助\v2.3_目录_VisualStudio15

当遇到格式为"HEADER/METHOD"的 F1 关键字时，将解析"/"字符，从而生成以下构造：

- 标题：是可用于在注册表中注册的命名空间

- 方法：这将成为传递的关键字。

例如，给定一个名为自定义库的自定义库和一个称为 MyTestMethod 的方法，当 F1 请求进来时，它将`CustomLibrary/MyTestMethod`格式化为 。

然后，用户可以将自定义库注册为合作伙伴配置单元下的命名空间，并提供所需的任何位置键，传递给查询的关键字将是 MyTestMethod。

**在 IDE 中启用帮助调试工具**

添加以下注册表项和值：

::: moniker range="vs-2017"

**HKEY_CURRENT_USER_软件\微软_VisualStudio_15.0\动态帮助**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER_软件\微软_VisualStudio_16.0\动态帮助**

::: moniker-end

值：在零售数据中显示调试输出：是

在 IDE 中，在"帮助"菜单项下，选择 **"调试帮助上下文**"。

**内容元数据**

在下表中，括号之间出现的任何字符串都是必须替换为已识别值的占位符。 例如，在元\<名中="Microsoft.Help.Locale"内容="[语言代码]"/>，"语言代码"必须替换为"en-us"等值。

| 属性（HTML 表示） | 描述 |
| - | - |
| \<元名称="Microsoft.Help.Locale"内容="[语言代码]"/> | 设置此主题的区域设置。 如果此标记在主题中使用，则必须只使用一次，并且必须插入任何其他 Microsoft 帮助标记上方。 如果未使用此标记，则通过使用与产品区域设置关联的断字器（如果指定）对主题的正文文本进行索引;否则，使用 en-us 断字符。 此标记符合 ISOC RFC 4646。 为确保 Microsoft 帮助正常工作，请使用此属性而不是常规语言属性。 |
| \<元名称="微软.帮助.主题本地"内容="[语言代码]"/> | 在也使用其他区域设置时，为本主题设置区域设置。 如果此标记在主题中使用，则只能使用一次。 当目录包含多种语言的内容时，使用此标记。 目录中的多个主题可以具有相同的 ID，但每个主题必须指定唯一的主题区域设置。 指定与目录区域设置匹配的 TopicLocale 的主题是显示在目录中的主题。 但是，主题的所有语言版本都显示在搜索结果中。 |
| \<标题>[标题]\</标题> | 指定本主题的标题。 此标记是必需的，并且必须在主题中只使用一次。 如果主题的正文不包含标题\<div> 部分，则此标题将显示在主题和目录中。 |
| \<元名称="微软.帮助.关键字"内容"[关键字短语]"/> | 指定在帮助查看器的索引窗格中显示的链接的文本。 单击链接时，将显示主题。 您可以为主题指定多个索引关键字，或者如果不希望指向此主题的链接显示在索引中，则可以省略此标记。 早期版本的"帮助"关键字可以转换为此属性。 |
| \<元名="微软.帮助.Id"内容"[主题ID]"/> | 设置本主题的标识符。 此标记是必需的，并且必须在主题中只使用一次。 ID 必须在目录中具有相同区域设置的主题中唯一。 在另一个主题中，您可以使用此 ID 创建指向此主题的链接。 |
| \<元名称="微软.帮助.F1"内容="[系统.Windows.控制.原始.I回收项目容器生成器]"/> | 指定此主题的 F1 关键字。 您可以为主题指定多个 F1 关键字，或者如果不希望在应用程序用户按 F1 时显示此主题，则可以省略此标记。 通常，只为主题指定一个 F1 关键字。 早期版本的"帮助"关键字可以转换为此属性。 |
| \<元名称="描述"内容="[主题描述]"/> | 提供本主题中内容的简短摘要。 如果此标记在主题中使用，则只能使用一次。 查询库直接访问此属性;它不存储在索引文件中。 |
| 元名="微软.帮助.Tocparent"内容"[parent_Id]"/> | 在内容表中指定此主题的父主题。 此标记是必需的，并且必须在主题中只使用一次。 该值是父值的Microsoft.Help.Id。 主题在目录中只能有一个位置。 "-1"被视为目录根的主题 ID。 在[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]中，该页是帮助查看器主页。 这也是我们专门将 TocParent_-1 添加到某些主题以确保它们显示在顶层的原因。 帮助查看器主页是系统页面，因此不可替换。 如果 VSP 尝试添加 ID 为 -1 的页面，它可能会添加到内容集中，但帮助查看器将始终使用系统页面 - 帮助查看者主页 |
| \<元名称="微软.帮助.Tocorder"内容="[正整数]"/> | 指定此主题相对于其对等主题在目录中显示的位置。 此标记是必需的，并且必须在主题中只使用一次。 该值是一个整数。 指定较低值整数的主题显示在指定较高值整数的主题的上方。 |
| \<元名称="微软.帮助.产品"内容="[产品代码]"/> | 指定本主题介绍的产品。 如果此标记在主题中使用，则只能使用一次。 此信息也可以作为传递给帮助索引器的参数提供。 |
| \<元名称="微软.帮助.ProductVersion"内容="[版本号]"/> | 指定本主题介绍的产品版本。 如果此标记在主题中使用，则只能使用一次。 此信息也可以作为传递给帮助索引器的参数提供。 |
| \<元名称="微软.帮助.类别"内容="[字符串]"/> | 产品用于标识内容的子部分。 您可以为主题标识多个子节，或者如果不希望链接标识任何子节，则可以省略此标记。 此标记用于存储从早期版本的帮助转换主题时，用于存储 TargetOS 和 TargetFrameworkMoniker 的属性。 内容的格式为属性名称：属性值。 |
| \<元名称="微软.帮助.主题版本内容"[主题版本号]"/> | 指定目录中存在多个版本的主题的此版本。 由于Microsoft.Help.Id不保证是唯一的，因此当目录中存在多个主题版本时，例如，当目录包含 .NET Framework 3.5 的主题和 .NET Framework 4 的主题且两者具有相同的Microsoft.Help.Id时，需要此标记。 |
| \<元名="自品牌"内容"[真实或FALSE]"/> | 指定此主题是使用帮助库管理器启动品牌包还是特定于主题的品牌包。 此标记必须为 TRUE 或 FALSE。 如果为 TRUE，则关联主题的品牌包将覆盖帮助库管理器启动时设置的品牌包，以便即使主题与其他内容的呈现不同，也会按预期呈现。 如果是 FALSE，则根据帮助库管理器启动时设置的品牌包呈现当前主题。 默认情况下，帮助库管理器假定自品牌为 false，除非自品牌变量声明为 TRUE;否则，帮助库管理器假定自品牌为 false。因此，您不必声明\<元名称="自品牌"内容="FALSE"/>。 |

## <a name="create-a-branding-package"></a>创建品牌包

Visual Studio 版本包含许多不同的视觉工作室产品，包括可视化工作室合作伙伴的隔离和集成外壳。  这些产品中的每一个都需要一定程度的基于主题的帮助内容品牌支持，这是产品独有的。  例如，Visual Studio 主题需要具有一致的品牌展示，而包装 ISO Shell 的 SQL Studio 需要为每个主题提供自己独特的帮助内容品牌。  集成的壳牌合作伙伴可能希望他们的帮助主题位于父 Visual Studio 产品帮助内容中，同时保持自己的主题品牌。

品牌包由包含帮助查看器的产品安装。  对于视觉工作室产品：

- 帮助查看器 2.3\<应用根目录（例如：C：程序文件 （x86）\Microsoft 帮助查看器\v2.3）中安装了回退品牌包（Branding_区域设置>.mshc）。  这用于未安装产品品牌包（未安装任何内容）或已安装的品牌包已损坏的情况。  使用应用根回退品牌包时，将忽略 Visual Studio 元素（徽标和反馈）。

- 从内容包服务安装 Visual Studio 内容时，还会安装品牌包（这是首次安装内容方案）。  如果品牌包有更新，则在下一次内容更新或其他包安装操作发生时将安装更新。

Microsoft 帮助查看器支持基于主题元数据的主题品牌。

- 当主题元数据定义自品牌 = true 时，呈现主题原样，不执行任何操作（至于品牌）。

- 当主题元数据定义自品牌 = false 时，请使用与主题供应商元数据值关联的品牌包。

- 当主题元数据定义名称="Microsoft.Help.Topicvendor"内容*\<供应商 MSHA>中的品牌包名称时，请使用内容值中定义的品牌包。

- 在可视化工作室目录中，有品牌包的优先应用。  首先应用 Visual Studio 默认品牌，然后，如果在主题元数据中定义并受关联的品牌包（如安装 msha 中定义）支持，则供应商定义的品牌将应用为覆盖。

品牌元素通常分为三个主要类别：

- 标题元素（示例包括反馈链接、条件免责声明文本、徽标）

- 内容行为（示例包括展开/折叠控件文本元素和代码段元素）

- 页脚元素（示例版权）

被视为品牌元素的项目包括（本规范中详细规定）：

- 目录/产品徽标（示例，视觉工作室）

- 反馈链接和电子邮件元素

- 免责声明文本

- 版权文本

可视化工作室帮助查看器品牌包中的支持文件包括：

- 图形（徽标、图标等）

- 品牌.js - 支持内容行为的脚本文件

- 品牌.xml - 跨目录内容一致使用的字符串。  注意：对于品牌中的 Visual Studio 本地化文本元素，请包括\<_locID\">的唯一值"

- 品牌.css - 表示一致性的样式定义

- 打印.css - 用于一致打印演示文稿的样式定义

如上所述，品牌包与主题相关联：

- 在元数据中定义自品牌 = false 时，主题将继承目录品牌包

- 或者，当自品牌 = false，并且在 MSHA 中定义了唯一的品牌包，并在安装内容时可用

对于实现自定义品牌包（VSP 内容、自品牌=True）的 VSP，一种方法是从回退品牌包开始（随帮助查看器一起安装），并根据需要更改文件的名称。  Branding_\<区域设置>.mshc 文件是一个 zip 文件，文件扩展名更改为 .mshc，因此只需将扩展名从 .mshc 更改为 .zip 并提取内容即可。  请参阅下文，了解品牌包元素并根据需要进行修改（例如，将徽标更改为 VSP 徽标，以及品牌.xml 文件中对徽标的引用、根据 VSP 细节更新品牌.xml 等）。

完成所有修改后，创建包含所需品牌元素的 zip 文件，并将扩展名更改为 .mshc。

要关联自定义品牌包，请创建 MSHA，其中包含对品牌 mshc 文件的引用以及内容 mshc（包含主题）。  有关如何创建基本 MSHA，请参阅下面的"MSHA"。

当主题包含\<元名称\"Microsoft.Help.Help.自品牌"内容\"false"/>时，Branding.xml 文件包含用于一致呈现主题中特定项目的元素列表。  下面列出了"品牌.xml"文件中元素的可视化工作室列表。  此列表旨在用作 ISO 壳牌采用者的模板，他们在此修改这些元素（例如徽标、反馈和版权），以满足他们自己的产品品牌需求。

注意："{n}"指定的变量具有代码依赖项 - 删除或更改这些值将导致错误，并可能导致应用程序崩溃。 可视化工作室品牌包中包括本地化标识符（示例_locID="代码段.n"）。

**品牌.xml**

| | |
| - | - |
| 功能： | **可折叠区域** |
| 使用： | 展开折叠内容控制文本 |
| **元素** | **价值** |
| 展开文本 | 展开 |
| 折叠文本 | 折叠 |
| 功能： | **代码段** |
| 使用： | 代码段控制文本。  注意：具有"非中断"空间的代码片段内容将更改为空格。 |
| **元素** | **价值** |
| 复制到剪贴板 | 复制到剪贴板 |
| 查看彩色文本 | 查看着色 |
| 组合VBTab显示语言 | 视觉基础（示例） |
| VB 声明 | 声明 |
| VB使用 | 使用情况 |
| 功能： | **反馈、页脚和徽标** |
| 使用： | 提供反馈控制，以便客户通过电子邮件提供有关当前主题的反馈。  内容的版权文本。  徽标定义。 |
| **元素** | **值（可以修改这些字符串以满足内容采用者的需求。** |
| 版权 | © 2013 微软公司。 保留所有权利。 |
| 发送反馈 | \<href=">{0}{1}向微软发送关于\<此主题的反馈/>。 |
| 反馈链接 | |
| 徽标标题 | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| 徽标文件名称 | vs_logo_bk.gif |
| 标志文件名称HC | vs_logo_wh.gif |
| 功能： | **免责声明** |
| 使用： | 一组针对计算机翻译内容的特定于案例的免责声明。 |
| **元素** | **价值** |
| MT_Editable | 本文已翻译为机器。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| MT_NonEditable | 本文已翻译为机器。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| MT_QualityEditable | 本文已手动翻译。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| MT_QualityNonEditable | 本文已手动翻译。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| MT_BetaContents | 本文已翻译为初步版本。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| MT_BetaRecycledContents | 本文已手动翻译为初步版本。 如果您有互联网连接，请选择"联机查看此主题"以可编辑模式查看此页面，同时使用原始英语内容。 |
| 功能： | **链接表** |
| 使用： | 支持在线主题链接 |
| **元素** | **价值** |
| 链接表标题 | 链接表 |
| 主题EnuLink文本 | 查看计算机上可用的本\<主题的英文版本 />。 |
| 主题在线链接文本 | 查看此主题\<href="{0} {1} ">\<在线 /> |
| 在线文本 | 联机 |
| 功能： | **视频音频控制** |
| 使用： | 显示视频内容的元素和文本 |
| **元素** | **价值** |
| 不支持多媒体 | 必须安装 IE9 或更高支持{0}内容。 |
| 视频文本 | 显示视频 |
| 音频文本 | 流音频 |
| 在线视频链接文本 | \<p>要查看与此主题关联的视频，请单击{0}\<href="{1}">{2}此处\</>。\</p> |
| 在线音频链接文本 | \<p>要收听与此主题关联的音频，请单击{0}\<href=">{1}{2}此处\</>。\</p> |
| 功能： | **内容未安装控制** |
| 使用： | 用于呈现内容未安装内容的文本元素（字符串） |
| **元素** | **价值** |
| 内容未安装标题 | 您的计算机上未找到任何内容。 |
| 内容未安装 下载内容文本 | \<p>要将内容下载到\<您的计算机，>单击{0}"{1}管理"选项卡\</>"\</p> |
| 内容未安装文本 | \<p>计算机上未安装任何内容。 有关本地帮助内容安装，请与管理员联系。\</p> |
| 功能： | **主题未找到控件** |
| 使用： | 用于呈现主题"未找到.htm"的文本元素（字符串） |
| **元素** | **价值** |
| 主题未找到标题 | 在计算机上找不到请求的主题。 |
| 主题未找到查看在线文本 | \<p>您请求的主题在计算机上找不到\<，但您可以创建 href="{0}">{1}联机\</>查看主题。\</p> |
| 主题 未找到下载内容文本 | \<p>查看导航窗格，了解指向类似主题的链接\<，或"href"">{0}{1}单击"管理\<"选项卡/>将内容下载到计算机。\</p> |
| 主题未找到文本 | \<p>您请求的主题在计算机上找不到。\</p> |
| 功能： | **主题损坏的控制** |
| 使用： | 用于渲染主题损坏.htm 的文本元素（字符串） |
| **元素** | **价值** |
| 主题已损坏的标题 | 无法显示请求的主题。 |
| 主题已损坏查看在线文本 | \<p>帮助查看器无法显示请求的主题。 主题的内容或基础系统依赖项中可能存在错误。\</p> |
| 功能： | **主页控件** |
| 使用： | 支持显示帮助查看器顶级节点内容的文本。 |
| **元素** | **价值** |
| 主页标题 | 帮助查看者主页 |
| 主页简介 | \<p>欢迎加入 Microsoft 帮助查看器，这是使用 Microsoft 工具、产品、技术和服务的每个人的重要信息来源。 帮助查看器允许您访问访问访问方式和参考信息、示例代码、技术文章等。 要查找所需的内容，请浏览目录、使用全文搜索或使用关键字索引浏览内容。\</p> |
| 主页内容安装文本 | \<p \<>br />\<使用{0}href=" {1} \<>管理内容/>选项卡执行以下操作\<：ul \<>li>将内容添加到您的计算机。\</li \<>li>检查本地内容的更新。\</li \<>li>从您的计算机中删除内容。\</li \<>/ul>\</p> |
| 主页已安装图书 | 已安装的书籍 |
| 主页 无图书已安装 | 您的计算机上未找到任何内容。 |
| 主页帮助设置 | 帮助内容设置 |
| 主页帮助设置文本 | \<p>您当前的设置是本地帮助。 帮助查看器显示计算机上已安装的内容。\<br />要更改"帮助"内容的来源，请在 Visual Studio\<菜单栏上{0}选择"跨样式"">\<帮助，设置帮助首选项/跨>。\<br />\</p> |
| 兆 字节 | MB |

**品牌.js**

品牌.js 文件包含 Visual Studio 帮助查看器品牌元素使用的 JavaScript。  下面是品牌元素和支持的 JavaScript 函数的列表。  此文件要本地化的所有字符串都在此文件顶部的"可本地化字符串"部分定义。  已为品牌.js 文件中的 loc 字符串创建了 ICL 文件。

||||
|-|-|-|
|**品牌功能**|**JavaScript 函数**|**说明**|
|无 功。。。||定义变量|
|获取用户代码语言|设置用户首选项|将索引 # 映射到代码语言|
|设置和获取 Cookie 值|得到饼干，设置饼干||
|继承成员|更改成员标签|展开/折叠继承成员|
|当自品牌=假|上载荷|读取查询字符串以检查该字符串是否为打印请求。  设置所有代码段以集中用户首选选项卡。 如果是打印请求，则设置为"打印机友好"设置为 true。 检查对比度过高模式。|
|代码段|添加特定文本语言标记集||
||从 Devlang 获取索引||
||更改选项卡||
||设置代码片段朗||
||设置电流朗||
||复制到剪贴板||
|可折叠区域|添加到可折叠控制集|将所有可折叠控件对象写入列表。|
||CA_Click|基于可折叠区域的状态，定义要呈现的图像和文本|
|对徽标的对比支持|是黑色背景（）|调用以确定背景是否为黑色。  仅在高对比度模式下准确。|
||是高对比度（）|使用彩色范围检测高对比度模式|
||上高对比度（黑色）|检测到高对比度时调用|
|LST 功能|||
||添加放大缩小字体功能 放大缩小字体功能||
||更新 LST（电流朗）||
||获取Devlang从代码片段（朗）||
|多媒体功能|标题（开始、结束、文本、样式）||
||查找所有媒体控制（规范化 ID）||
||获取活动播放器（规范化 ID）||
||标题OnOff（id）||
||到秒（t）||
||获取所有评论（节点）||
||样式更正（样式名称、样式值）||
||显示CC（id）||
||副标题（ID）||

**HTM 文件**

品牌包包含一组 HTM 文件，这些文件支持将关键信息传达给帮助内容用户的方案，例如，主页包含描述已安装的内容集的部分，以及告知用户在本地主题集中找不到主题时告知用户的页面。 每个产品都可以修改这些 HTM 文件。  ISO 壳牌供应商能够采用默认品牌包，并更改这些页面的行为和内容，以满足其需求。  这些文件引用其各自的品牌包，以便品牌标签从品牌.xml 文件中获取相应的内容。

||||
|-|-|-|
|**文件**|**使用**|**显示的内容源**|
|主页.htm|这是一个页面，显示当前安装的内容，以及适合向用户展示其内容的任何其他消息。  此文件具有附加的元数据属性"Microsoft.Help.Id"内容="-1"，该属性将此内容置于本地内容 TOC 的顶部。||
||<META_HOME_PAGE_TITLE_ADD/>|品牌.xml，标记\<主页标题>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD />|品牌.xml，标记\<主页介绍>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD/>|品牌.xml，标记\<主页内容安装文本>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD/>|标题部分品牌.xml\<标签 HomePage 安装簿>，从应用程序生成\<的数据，HomePageNoBooks 安装>未安装书籍。|
||<HOME_PAGE_SETTINGS_SECTION_ADD/>|标题部分品牌.xml\<标签主页帮助设置>，节文本\<主页帮助设置文本>。|
|主题损坏.htm|当本地集中存在主题，但由于某种原因无法显示（损坏的内容）。||
||<META_TOPIC_CORRUPTED_TITLE_ADD/>|品牌.xml，标签\<主题损坏标题>|
||<TOPIC_CORRUPTED_SECTION_ADD/>|品牌.xml，标签\<主题损坏查看在线文本>|
|主题未发现.htm|在本地内容集中找不到主题，也联机不可用||
||<META_TOPIC_NOT_FOUND_TITLE_ADD/>|品牌.xml，标签\<主题未找到标题>|
||<META_TOPIC_NOT_FOUND_ID_ADD/>|品牌.xml，标签\<主题未找到查看在线文本> \<+ 主题未找到下载内容文本>|
||<TOPIC_NOT_FOUND_SECTION_ADD/>|品牌.xml，标签\<主题未找到文本>|
|内容未安装.htm|当产品未安装本地内容时。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD/>|品牌.xml，标记\<内容未安装标题>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD/>|品牌.xml，标记\<内容未安装下载内容文本>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD/>|品牌.xml，标记\<内容未安装文本>|

**CSS 文件**

可视化工作室帮助查看器品牌包包含两个 css 文件，以支持一致的可视化工作室帮助内容演示文稿：

- 品牌.css - 包含用于渲染自品牌\false 的 css 元素

- 打印机.css - 包含用于渲染自品牌=false 的 cs 元素

Branding.css 文件包括 Visual Studio 主题演示文稿的定义（警告是Branding_\<区域设置中包含的品牌.css>.mshc 从包服务可能会更改）。

**图形文件**

可视化工作室内容显示视觉工作室徽标以及其他图形。  "可视化工作室帮助查看器"品牌包中的图形文件的完整列表如下所示。

||||
|-|-|-|
|**文件**|**使用**|**示例**|
|清除.gif|用于渲染可折叠区域||
|footer_slice.gif|页脚演示||
|info_icon.gif|显示信息时使用|免责声明|
|online_icon.gif|此图标将与联机链接关联||
|选项卡左BD.gif|用于呈现代码段容器||
|tabRightBD.gif|用于呈现代码段容器||
|vs_logo_bk.gif|用于品牌.xml 标记\<LogoFilename>中定义的正常对比度徽标引用。  对于 Visual Studio 产品，徽标名称为 vs_logo_bk.gif。||
|vs_logo_wh.gif|用于品牌.xml 标签\<LogoFileNameHC>中定义的正常高徽标引用。  对于 Visual Studio 产品，徽标名称为 vs_logo_wh.gif。||
|ccOff.png|字幕图形||
|ccOn.png|字幕图形||
|图像Sprite.png|用于渲染可折叠区域|展开或折叠图形|

## <a name="deploy-a-set-of-topics"></a>部署一组主题

这是一个简单而快速的教程，用于创建由 MSHA 文件和包含主题的驾驶室或 MSHC 集组成的帮助查看器内容部署集。 MSHA 是一个 XML 文件，用于描述一组驾驶室或 MSHC 文件。 帮助查看器可以读取 MSHA 以获取内容列表（。CAB 或 。可用于本地安装的 MSHC 文件）。

这只是描述帮助查看器 MSHA 非常基本的 XML 架构的入门部分。  此简要概述和示例帮助内容安装程序.msha 下方有一个示例实现。

MSHA 的名称（出于此引瑟）而言，是 HelpContentSetup.msha（文件的名称可以是任何内容，具有扩展名。MSHA）。 帮助内容设置.msha（下面的示例）应包含可用的驾驶室或 MSHC 的列表。  文件类型必须在 MSHA 中保持一致（不支持 MSHA 和 CAB 文件类型的组合）。 对于每个 CAB 或 MSHC，应该有\<一个 div 类="包">...\</div>（参见下面的示例）。

注意：在下面的实施示例中，我们包括了品牌包。 这对于获取所需的 Visual Studio 内容呈现元素和内容行为至关重要。

示例帮助内容安装程序.msha 文件：（将"内容集名称 1"和"内容集名称 2"等替换为文件名。

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

1. 创建本地文件夹，如"C：\sample内容"

2. 在此示例中，我们将使用 MSHC 文件来包含主题。  MSHC 是一个 zip，文件扩展名从 .zip 更改为 。MSHC。

3. 将下面的帮助内容安装程序.msha 创建为文本文件（记事本用于创建文件），并将其保存到上述指定文件夹（请参阅步骤 1）。

类"品牌"存在且是唯一的。 品牌 mshc 包含在此入门中，以便已安装的内容具有品牌，并且 MSHC 中包含的内容行为将包含品牌包中包含的相应支持元素。 如果没有这一点，当系统查找不属于翻录（已安装）内容的支持项时，将导致错误。

要获取 Visual Studio 品牌包，请将 Branding_en-US.mshc 文件（C：*程序文件 （x86）\Microsoft 帮助查看器\v2.3]复制到您的工作文件夹。

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

使用和扩展上述步骤将使 VSP 能够为可视化工作室帮助查看器部署其内容集。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>向可视化工作室外壳添加帮助（集成和隔离）

**简介**

本演练演示如何将帮助内容合并到 Visual Studio 外壳应用程序中，然后部署它。

**要求**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [视觉工作室 2013 孤立壳牌红人](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**概述**

命令[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]行程序是 IDE[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]的版本，您可以基于该版本来建立应用程序。 此类应用程序包含隔离外壳以及您创建的扩展。 使用[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]SDK 中包含的隔离外壳项目模板生成扩展。

创建基于孤立外壳的应用程序及其帮助的基本步骤：

1. 获取[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]ISO 外壳可再分发（微软下载）。

2. 在 Visual Studio 中，创建基于隔离外壳的帮助扩展，例如，本演练稍后将介绍的 Contoso 帮助扩展。

3. 将扩展和 ISO Shell 可再分发包装到部署 MSI（应用程序设置）。 本演练不包括设置步骤。

创建可视化工作室内容存储。 对于集成的外壳方案，将 Visual Studio12 更改为产品目录名称，如下所示：

- 创建文件夹 C：\程序数据\微软\帮助库2_目录\VisualStudio15。

- 创建名为 CatalogType.xml 的文件并将其添加到文件夹中。 该文件应包含以下代码行：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

定义注册表中的内容存储。 对于集成外壳，将 VisualStudio15 更改为产品目录名称：

- HKLM_SOFTWARE_Wow6432Node_微软_帮助\v2.3_目录_VisualStudio15

   键：位置路径字符串值：C：\程序数据\微软\帮助库2_目录_VisualStudio15]

- HKLM_SOFTWARE_Wow6432Node_微软_帮助\v2.3_目录_VisualStudio15_en-US

   键：目录名称字符串值：[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]文档

**创建项目**

要创建隔离的 Shell 扩展：

1. 在视觉工作室中，在 **"文件**"下，选择 **"新项目**"，在 **"其他项目类型"** 下选择 **"扩展性**"，然后选择 **"视觉工作室外壳隔离**"。 命名项目`ContosoHelpShell`），以基于可视化工作室隔离外壳模板创建扩展性项目。

2. 在解决方案资源管理器中，在 ContosoHelpShellUI 项目中，在"资源文件"文件夹中打开应用程序命令.vsct。 确保此行已注释掉（搜索"No_Help"）：`<!-- <define name="No_HelpMenuCommands"/> -->`

3. 选择要编译和运行**调试**的 F5 键。 在隔离 Shell IDE 的实验实例中，选择 **"帮助"** 菜单。 确保显示 **"查看帮助**"、**添加和删除帮助内容**以及**设置帮助首选项**命令。

4. 在解决方案资源管理器中，在 ContosHelpShell 项目中，在"壳体自定义"文件夹中打开 ContosoHelpShell.pkgdef。 要定义 Contoso 帮助目录，请添加以下行：

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. 在解决方案资源管理器中，在 ContosHelpShell 项目中，在"壳体自定义"文件夹中打开 ContosoHelpShell.应用程序.pkgdef。 要启用 F1 帮助，添加以下行：

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

6. 在"解决方案资源管理器"中，在 ContosoHelpShell 解决方案的上下文菜单中，选择 **"属性"** 菜单项。 在 **"配置属性**"下，选择**配置管理器**。 在 **"配置"** 列中，将每个"调试"值更改为"释放"。

7. 生成解决方案。 这将在发布文件夹中创建一组文件，将在下一节中使用。

要测试此项，就像已部署一样：

1. 在要部署到的计算机上，安装下载的（从上面）ISO 外壳。

2. 在 #程序\\文件 （x86）\\中创建一个`Contoso`文件夹，并命名为 它。

3. 将内容从 ContosoHelpShell 版本文件夹复制到\\[程序文件 （x86）\Contoso] 文件夹。

4. 通过在 **"开始"** 菜单中选择`Regedit`**"运行**"并输入 启动注册表编辑器。 在注册表编辑器中，选择 **"文件**"，然后**导入**。 浏览到 ContosoHelpShell 项目文件夹。 在 ContosoHelpShell 子文件夹中，选择 ContosoHelpShell.reg。

5. 创建内容存储：

    对于 ISO 外壳 - 创建 Contoso 内容存储 C：\程序数据\微软_帮助库2_目录\ContosoDev12

    对于[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]集成外壳，创建文件夹 C：\程序数据\微软\帮助库2_目录\VisualStudio15

6. 创建目录类型.xml 并添加到内容存储（上一步），其中包含：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 添加以下注册表项：

    HKLM_SOFTWARE_Wow6432Node_微软_帮助\v2.3_目录_VisualStudio15键：位置路径字符串值：

    对于 ISO 外壳：

    C：程序数据微软帮助图书馆2目录视觉工作室15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]集成外壳：

    C：程序数据微软帮助图书馆2目录视觉工作室15en-美国

    键：目录名称字符串值：[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]文档。 对于 ISO 外壳，这是目录的名称。

8. 将内容（驾驶室或 MSHC 和 MSHA）复制到本地文件夹。

9. 用于测试内容存储的集成外壳命令行。 对于 ISO 外壳，根据需要更改目录和启动应用值以匹配产品。

     "C：_程序文件 （x86）\微软帮助查看器\v2.3_HlpViewer.exe" /目录名称 VisualStudio15 /帮助查询方法="页&id_ContosoTopic0" /启动应用程序微软，VisualStudio，12.0

10. 启动 Contoso 应用程序（从 Contoso 应用根目录）。 在 ISO 外壳中，选择 **"帮助"** 菜单项，并将 **"设置帮助首选项"** 更改为 **"使用本地帮助**"。

11. 在 shell 中，选择 **"帮助"** 菜单项，然后**查看帮助**。 本地帮助查看器应启动。 选择"**管理内容**"选项卡。在 **"安装源**"下，选择 **"磁盘**"选项按钮。 选择 **...** 按钮并浏览到包含 Contoso 内容的本地文件夹（复制到上述步骤中的本地文件夹）。 选择帮助内容设置.msha。 康托索现在应该在书选中作为一本书出现。 选择 **"添加**"，然后选择 **"更新**"按钮（右下角）。

12. 在 Contoso IDE 中，选择 F1 键以测试 F1 功能。

## <a name="additional-resources"></a>其他资源

有关运行时 API，请参阅[Windows 帮助 API](/previous-versions/windows/desktop/helpapi/helpapi-portal)。

有关如何利用帮助 API 的详细信息，请参阅[帮助查看器代码示例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)。

您可以提交[有关开发人员社区的](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)功能建议。
