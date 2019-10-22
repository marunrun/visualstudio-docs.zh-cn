---
title: JavaScript IntelliSense | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript]
- <reference> JavaScript XML tag
- JavaScript Code Editor
- XML code comments, JavaScript IntelliSense
- reference JavaScript XML tag
- JavaScript, IntelliSense
- code comments, JavaScript IntelliSense
- JavaScript, reference groups
- JavaScript Editor
- reference directives [JavaScript]
- JavaScript, XML documentation comments
- reference groups [JavaScript]
- JavaScript, reference directives
- IntelliSense [JavaScript], about
- IntelliSense extensibility [JavaScript]
- XML documentation comments [JavaScript]
ms.assetid: af1a3171-c9d8-45a3-9c96-a763e3b163ef
caps.latest.revision: 67
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 39c90a8550736c945f04467e9366a73039cfa2b1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670477"
---
# <a name="javascript-intellisense"></a>JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IntelliSense 可在你编码时提供信息，从而有助于较快地编写代码，而且编写的代码错误较少。 在 JavaScript 编辑器中使用客户端脚本时，IntelliSense 将根据当前的上下文列出可用的对象、函数、属性和参数。 可以从 IntelliSense 提供的弹出列表中选择编码选项以完成代码。

 使用 IntelliSense 可以比较轻松地完成以下任务：

- 查找成员信息。

- 将语言元素直接插入代码中。

- 维护上下文，而不必脱离代码编辑器。

- 利用 XML 文档注释和 JavaScript IntelliSense 扩展性支持自定义 IntelliSense。

  本主题包含以下各节：

- [确定 IntelliSense 上下文](#DeterminingIntelliSenseContext)

- [处理 Intellisense 信息](#ProcessingIntelliSenseInformation)

- [JavaScript IntelliSense 功能](#Features)

- [JavaScript IntelliSense 扩展性](#Extensibility)

- [JavaScript 验证](#Validation)

  有关 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 的 IntelliSense 功能的详细信息，请参阅[使用 IntelliSense](../ide/using-intellisense.md)。

## <a name="DeterminingIntelliSenseContext"></a>确定 IntelliSense 上下文
 JavaScript IntelliSense 根据与当前脚本上下文相关的所有脚本提供编码选项。 这包括当前文件中的脚本元素。 它还包括从脚本中直接或间接引用的任何代码，例如脚本文件引用、程序集脚本引用、服务引用以及与页面关联的引用。

 当前的脚本上下文是根据以下项创建的：

- 在活动文档的所有脚本块中定义的函数。 在具有以下文件扩展名的文件中支持内联脚本块：.aspx、.ascx、.master、.html 和 .htm。

- 具有指向其他脚本文件的 `src` 属性的 `script` 元素。 目标脚本文件必须具有文件扩展名 .js。

- 通过使用 `reference` 指令引用其他 JavaScript 文件的 JavaScript 文件。

- 全局对象、IntelliSense 扩展或延迟加载的脚本文件的引用组。

- 对 XML Web 服务的引用。

- <xref:System.Web.UI.ScriptManager> 和 <xref:System.Web.UI.ScriptManagerProxy> 控件（如果 Web 应用程序是启用 AJAX 的 ASP.NET 应用程序）。

- [!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)]（如果正在使用支持 AJAX 的 ASP.NET Web 应用程序）。

    > [!NOTE]
    > HTML 元素的事件处理程序特性中的脚本或者在 `href` 特性中定义的脚本不支持 IntelliSense。

## <a name="ProcessingIntelliSenseInformation"></a>处理 Intellisense 信息
 为提供 JavaScript IntelliSense，该语言服务将执行以下操作：

- 创建相关的 JavaScript 文件列表，这些文件基于活动文档中的引用以及所引用文件中的递归检查脚本引用。

- 遍历此列表并从每个文件中收集类型信息和其他相关数据。

- 聚合数据并将其传递给 JavaScript Language Service，该服务可向 IntelliSense 提供类型信息和数据。

- 监视文件是否发生了可能影响 IntelliSense 列表的变化，并根据需要更新列表。 关于远程存储（例如使用 HTTP 引用的存储）的脚本不接受监视。

## <a name="Features"></a>JavaScript IntelliSense 功能
 JavaScript IntelliSense 支持以下对象：

- [文档对象模型 (DOM) 元素](#HTMLDom)

- [内部对象](#IntrinsicObjects)

- [用户定义的变量、函数和对象](#UserDefined)

- 使用引用（例如[脚本引用](#Script)、[引用指令](#ReferenceDirectives)和[引用组](#ReferenceGroups)）的外部文件中定义的对象。

- 从 Visual Studio 下载的远程文件中定义的对象。

- [XML 文档注释](#XMLDocComments)中指定的对象，例如参数和字段。

- 使用标准 JavaScript 注释标记 (//) 描述的对象。 有关详细信息，请参阅[扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)。

- 使用 [JavaScript IntelliSense 扩展性](#Extensibility)机制支持的对象。 有关详细信息，请参阅[扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)。

- [ASP.NET AJAX 对象](#ASPNet)

  IntelliSense 无法确定对象的类型时，将使用活动文档中的标识符提供语句结束选项。 有关详细信息，请参阅[标识符的语句完成](../ide/statement-completion-for-identifiers.md)。

### <a name="HTMLDom"></a>HTML DOM 元素
 JavaScript IntelliSense 为诸如 `body`、`form` 和 `div` 之类的动态 HTML (DHTML) DOM 元素提供编程引用。 IntelliSense 只显示包括在当前文档和母版页中的元素。 JavaScript IntelliSense 还支持 `window` 和 `document` 对象及其成员。

### <a name="IntrinsicObjects"></a>内部对象
 JavaScript IntelliSense 为 `Array`、`String`、`Math`、`Date` 和 `Number` 等内部对象提供编程引用。 有关内部对象的详细信息，请参阅[标准内置对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)。

### <a name="UserDefined"></a> 用户定义的变量、函数和对象
 更改 JavaScript 文件时，[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 将扫描打开和引用的文档，以确定所有可用的代码资源。 这包括已创建的变量、函数和对象。 然后 JavaScript IntelliSense 便可使用这些资源。

 有关用户定义的变量、函数和对象的详细信息，请参阅 MSDN 网站上的[创建自己的对象](http://go.microsoft.com/fwlink/?LinkId=108671)。

### <a name="External"></a> 外部文件引用
 你可以包含各种类型的外部文件引用，以便在你的代码中实现 IntelliSense 支持。 外部文件引用可能是脚本引用、引用指令，或可使用引用组指定。

#### <a name="Script"></a> 脚本引用
 你可以引用包括脚本代码的外部文件，而不用在页中编写所有客户端脚本。 这样，可以比较轻松地在页之间重复使用代码，而且客户端脚本可以由浏览器进行缓存。

 如果不处理支持 ASP.NET AJAX 的网页，则可以通过在 `src` 元素开始标记中使用 `script` 特性来引用外部脚本文件。 `src` 特性指定包含源代码或数据的外部文件的 URL。

 以下示例显示在 <`script`> 标志中使用 `src` 特性引用脚本文件的标记。

```html
<script type="text/javascript" src="~/Scripts/JavaScript.js">

</script>
```

 如果要处理支持 ASP.NET AJAX 的网页，则可以通过使用 <xref:System.Web.UI.ScriptReference> 控件的 <xref:System.Web.UI.ScriptManager> 对象来引用脚本文件。

 下面的示例显示了在 <xref:System.Web.UI.ScriptReference> 控件中使用 <xref:System.Web.UI.ScriptManager> 对象来引用脚本文件的标记。

```html
<asp:ScriptManager ID="ScriptManager1" runat="server">
  <Scripts>
    <asp:ScriptReference Path="~/Scripts/JavaScript.js" />
  </Scripts>
</asp:ScriptManager>
```

 IntelliSense 还支持以资源形式嵌入在 ASP.NET AJAX Web 应用程序中的程序集内的脚本文件。 有关嵌入的脚本资源的详细信息，请参阅[演练：将 JavaScript 文件作为资源嵌入到程序集中](https://msdn.microsoft.com/library/d8cb78cd-95a9-4dc6-92df-391866817e89)。

#### <a name="ReferenceDirectives"></a> 引用指令
 通过使用 `reference` 指令，[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 能够在当前正编辑的脚本与其他脚本之间建立关系。 通过使用 `reference` 指令，可以在当前脚本文件的脚本上下文中包括一个脚本文件。 这使 IntelliSense 能够在你进行编码时引用在外部定义的函数、类型和字段。

 你可以以 XML 注释的形式创建一个 `reference` 指令。 此指令必须在文件中任何脚本之前声明。 `reference` 指令可以包括基于磁盘的脚本引用、基于程序集的脚本引用、基于服务的脚本引用或基于页面的脚本引用。

 下面的示例演示如何使用基于磁盘的引用指令。 在第一个示例中，该语言服务在包含项目文件（例如 .jsproj）的同一文件夹中查找文件。

 `/// <reference path="ScriptFile1.js" />`

 `/// <reference path="Scripts/ScriptFile2.js" />`

 `/// <reference path="../ScriptFile3.js" />`

 `/// <reference path="~/Scripts/ScriptFile4.js" />`

 下面的示例演示如何创建对基于程序集的脚本的引用。

 `/// <reference name "Ajax.js" assembly="System.Web.Extensions, ..." />`

 下面的示例演示如何引用基于服务的脚本：

 `/// <reference path="MyService.asmx" />`

 `/// <reference path="Services/MyService.asmx" />`

 `/// <reference path="../MyService.asmx" />`

 `/// <reference path="~/Services/MyService.asmx" />`

> [!NOTE]
> 包含在 Web 应用程序项目 (WAP) 内的 Web 服务 (.asmx) 文件中的脚本不支持 JavaScript IntelliSense。

 下面的示例演示如何引用基于页面的脚本。

 `/// <reference path="Default.aspx" />`

 `/// <reference path="Admin/Default.aspx" />`

 `/// <reference path="../Default.aspx" />`

 `/// <reference path="~/Admin/Default.aspx" />`

 下面的规则适用于 `reference` 指令。

- `reference` XML 注释必须在任何脚本之前声明。

- 必须将 XML 注释语法与三个斜杠一起使用。 用标准注释语法（两个斜杠）进行的引用将被忽略。

- 对于每个指令，只能指定一个文件或资源。

- 不允许存在多个对基于页面的脚本的引用。

- 如果指定了一个页面引用，则不允许执行其他类型的引用指令。

- 文件名使用相对路径。 可以使用波形符运算符 (`~`) 创建相对于应用程序根目录的路径。

- 绝对路径将被忽略。

- 将不处理引用的页面中的引用指令，也就是说，不为页面对引用指令进行递归式解析。 只包括页面直接引用的脚本。

#### <a name="ReferenceGroups"></a> 引用组
 你可以使用预定义的引用组指定特殊的 IntelliSense .js 文件位于不同 JavaScript 项目的范围内。 可用引用组类型如下：

- 隐式 (Windows)，用于使用 JavaScript 的 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用。 包含在该组中的文件位于代码编辑器中为指定类型的项目打开的每个 .js 文件的范围中。

- 隐式 (Web)，用于 HTML5 项目。 包含在该组中的文件位于代码编辑器中为这些项目类型打开的每个 .js 文件的范围中。

- 专用工作线程引用组，用于 HTML5 Web 工作线程。 该组中指定的文件位于显式引用专用工作线程引用组的 .js 文件的范围中。

- 一般类型，用于其他 JavaScript 项目类型。

  在大多数情况下，你不必修改引用组。 但是，如果要更改，可使用 JavaScript 代码编辑器的配置选项，指定引用组中包含的文件。 有关使用此功能的说明，请参阅[选项、文本编辑器、JavaScript、IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md)。

> [!TIP]
> IntelliSense 引用通常用于为全局对象以及 IntelliSense [扩展](#Extensibility)提供 IntelliSense 支持。 你还可以对必须在运行时使用脚本加载程序加载的脚本使用该功能。

### <a name="remote-file-references"></a>远程文件引用
 你可以指示 Visual Studio 下载 JavaScript 文件所引用的远程 JavaScript 文件，以便为远程文件或库提供 IntelliSense 支持。 当你使用该功能时，文件会在你将其作为引用包含到 JavaScript 文件中时进行下载。

> [!NOTE]
> 除 Web 项目外，该功能仅适用于在项目上下文外部打开的 JavaScript 文件。 对于 Web 项目，默认下载你的项目中所引用的远程文件。

 有关使用此功能的说明，请参阅[选项、文本编辑器、JavaScript、IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md)。

> [!WARNING]
> 如果你启用该功能后发现代码编辑器速度降低，我们建议你将其禁用。

### <a name="XMLDocComments"></a> XML 文档注释
 XML 文档注释是添加到脚本中的代码元素的文本说明。 引用注释的脚本时，IntelliSense 中将显示这些文本说明。 例如，你可提供有关函数的参数和返回值的信息。 XML 文档注释只能从引用的文件、程序集和服务中提供。 有关详细信息，请参阅 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)和[创建 XML 文档注释](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)。

 IntelliSense 可以在以下方案中显示 XML 文档注释：

- 一个引用另一个 .js 文件的 .js 文件。

- 一个引用 .aspx 文件的 .js 文件。

- 一个引用 .js 文件的 .aspx 文件。

  当一个 .aspx 文件引用另一个 .aspx 文件时，IntelliSense 不可用。

### <a name="ASPNet"></a> ASP.NET AJAX 对象
 ASP.NET AJAX 也支持 JavaScript IntelliSense。 ASP.NET AJAX 包含一个客户端框架，该框架将扩展可用于 ECMAScript (JavaScript) 的标准类型。 为使 JavaScript IntelliSense 能够提供有关 ASP.NET AJAX 对象的详细信息，XML 文档注释已添加到整个 [!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)] 中。 使用包含在 ASP.NET AJAX 库中的类型和成员时，将会显示这些 XML 文档注释。

> [!NOTE]
> JavaScript IntelliSense 不显示私有成员。 在 ASP.NET AJAX 中用以下划线 (_) 开头的成员来表示私有成员。

## <a name="Extensibility"></a> JavaScript IntelliSense 扩展性
 使用 JavaScript Language Service 提供的对象和函数，你将能够改变使用第三方库的开发人员的 IntelliSense 体验。 当默认语言服务无法提供你需要提供给客户的所有信息时，这些功能尤为有用。 有关详细信息，请参阅[扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)。

## <a name="Validation"></a> JavaScript 验证
 JavaScript 脚本验证总是在后台进行。 当 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 检测到 JavaScript 代码的语法错误时，将通过以下方式提供反馈：

- 编辑器中带下划线的元素。 红色的波浪下划线指出了错误。 如果将鼠标指针停留在错误上，工具提示会显示错误说明。

- “错误列表”  窗口。 “错误列表”  窗口显示错误说明、出错的文件、行号和列号以及项目。 若要显示“错误列表”  窗口，请在“视图”  菜单中单击“错误列表”  。

- “输出”窗口将显示未加载的引用。

## <a name="see-also"></a>另请参阅
- [使用 IntelliSense](../ide/using-intellisense.md)
- [创建 XML 文档注释](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)
- [扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)
- [适用于标识符的语句结束](../ide/statement-completion-for-identifiers.md)
- [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
- [关于 DHTML 对象模型](http://go.microsoft.com/fwlink/?LinkID=92344)
- [列表成员](https://msdn.microsoft.com/1b9cc469-9cd4-4d42-9999-1f9479635ff8)
- [SRC 特性|src 属性](http://go.microsoft.com/fwlink/?LinkId=92345)