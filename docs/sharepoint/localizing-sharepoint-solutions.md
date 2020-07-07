---
title: 本地化 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.Project.GlobalAndFeatureResource
- VS.SharePoint.Project.AddResourceDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalizing [SharePoint development in Visual Studio]
- localizing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0a7b04ab1f77eba15f2bc617f89514a8d0952674
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017146"
---
# <a name="localize-sharepoint-solutions"></a>本地化 SharePoint 解决方案

  准备应用程序以使其可在全球范围内使用的过程称为本地化。 本地化是将资源转换为特定区域性。 有关详细信息，请参阅[全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)。 本主题提供有关如何本地化 SharePoint 解决方案的概述。

 若要本地化解决方案，请从代码中删除硬编码的字符串，并将它们抽象到资源文件中。 资源文件是扩展名为 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] *.resx*的基于的文件。 资源文件包含解决方案中使用的字符串的翻译版本。 有关详细信息，请参阅[应用程序中的资源](/previous-versions/dotnet/netframework-4.0/f45fce5x(v=vs.100))。

> [!NOTE]
> 仅将字符串资源添加到 SharePoint 解决方案资源文件。 尽管资源编辑器可用于添加非字符串资源，但非字符串资源不会部署到 SharePoint。

## <a name="resource-files"></a>资源文件
 有三种类型的资源文件：默认、非特定语言和特定语言。

|资源文件类型|说明|
|------------------------|-----------------|
|默认|默认资源文件也称为 "回退资源"，其中包含为默认区域性（例如英语）本地化的字符串。 如果找不到指定语言的本地化资源文件，则使用这些文件。 默认资源没有单独的文件，它们存储在主应用程序程序集中。|
|非特定语言|一种资源文件，其中包含针对某种语言（而不是特定区域性）本地化的字符串。 例如，"fr" 表示法语。|
|特定于语言|一种资源文件，其中包含针对某种语言和区域性本地化的字符串。 例如，加拿大法语的 "fr-CA"。|

 有关详细信息，请参阅[用于本地化的资源的分层组织](../ide/globalizing-and-localizing-applications.md)。

 若要在中开发的 SharePoint 项目中指定默认资源文件 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，请在添加资源文件时在 "**添加资源**" 对话框的 "区域性" 列表中选择 "**固定语言（固定国家/地区）** "。

## <a name="localize-visual-studio-sharepoint-solutions"></a>本地化 Visual Studio SharePoint 解决方案
 本地化解决方案时，应考虑解决方案向用户显示的所有文本信息。 必须转换信息性消息、错误消息和 [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] 字符串，并将这些翻译放在资源文件中。

 资源文件中的每个字符串都具有唯一的标识符。 为每个资源文件中的已翻译字符串使用相同的标识符。 例如，如果 "String1" 是默认资源文件中第一个字符串的标识符，则为特定于语言的资源文件中的第一个字符串使用相同的标识符。

 在 SharePoint 应用程序中，通常有三个区域需要本地化 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ：功能、ASPX 页标记和代码。 出于说明目的，以下部分假设你有一个要本地化为德语和日语的 SharePoint 解决方案。 默认语言为英语。

### <a name="localize-features"></a>本地化功能
 若要本地化功能，必须将功能的硬编码标题和说明替换为在本地化资源文件中引用已翻译标题和字符串的表达式。 在的**功能设计器**中进行此更改 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 有关详细信息，请参阅[如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)。

 若要将英语功能本地化为德语和日语，请向项目添加三个资源文件项目项：一个用于英语，一个用于德语，另一个用于日语。 功能资源文件不能用于本地化 ASPX 标记或代码;需要单独的资源文件。

 创建功能资源文件后，向其中添加已翻译的字符串。 使用以下格式的表达式访问本地化字符串：

```aspx-csharp
$Resources:String ID
```

 中的功能资源 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 始终命名为资源。 如果选择了不使用固定语言的语言，则会将区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 添加到资源文件名。 例如，如果添加了一个固定语言（默认）功能资源文件，则该文件称为 *.resources*。 如果通过选择日语（日本）的区域性来添加特定于语言的功能资源，则该文件将被称为 " *ja-jp*"。 功能资源文件名是自动分配的，无法更改。

 功能资源的作用域是其所添加到的功能的本地。 若要创建可供解决方案中的任何功能或元素文件使用的资源，请添加 "**全局资源文件**" 项目项，而不是功能资源文件。 "**全局资源文件**" 项目项位于 "**添加新项**" 对话框的 " **SharePoint** " 下的 " **2010** " 文件夹中。 全局资源文件部署到 SharePoint 根文件夹的 \Resources 文件夹。

### <a name="localize-aspx-page-markup"></a>本地化 ASPX 页标记
 若要对页面进行本地化 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ，请将三个资源文件项目项添加到项目中：一个用于英语，一个用于德语，另一个用于日语。 如果除了标记之外还不必本地化代码，可以添加全局资源文件。

 提供默认语言资源文件的名称。 为本地化的资源文件指定附加了特定于语言的区域性的相同名称 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 。 例如， *MyAppResources.de-* 将德语和*MyAppResources For .resx*用于日语。

 将每个资源文件的 "**部署类型**" 属性设置为 " **AppGlobalResource**"。 这会使资源文件部署到 App_GlobalResources 文件夹，在该文件夹中，这些资源文件可用于解决方案中的所有 ASPX 页和控件。 App_GlobalResources 文件夹位于 C:\inetpub\wwwroot\wss\VirtualDirectories \\<端口号 \> \ App_GlobalResources 中。

> [!NOTE]
> 如果使用非全局资源文件，请将它们移到项目项文件夹，以启用部署类型属性和其他特定于 SharePoint 的属性。

 ASPX 标记资源文件也可用于本地化代码。 如果使用资源来本地化除 ASPX 标记之外的代码，请将每个文件的 "生成操作" 属性设置保留为嵌入资源，以使资源编译到附属程序集中。 但是，如果你只使用资源文件来本地化标记，则可以选择将生成操作更改为内容，以防止将文件编译到主应用程序程序集中。

 将 ASPX 页中的所有硬编码属性字符串替换为以下格式的表达式，并将其控件标记为：

```aspx-csharp
<asp:<class> runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 例如：

```aspx-csharp
<asp:Button ID="btn1" runat="server" onclick="btn1_Click" Text="<%$Resources:Resource1,String7%>"></asp:Button>
```

 对于 ASPX 作为文本，请使用以下格式的表达式：

```aspx-csharp
<asp:literal ID="<ID>" runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 例如：

```aspx-csharp
<asp:literal ID="Literal1" runat="server" Text="<%$Resources:Resource1, String9%>" />
```

 有关详细信息，请参阅[如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)。

### <a name="localize-code"></a>本地化代码
 除了本地化功能字符串和标记外 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ，还必须本地化出现在解决方案代码中的消息字符串和错误字符串。 本地化的信息性消息和错误消息包含在附属程序集中。 附属程序集包含对用户可见的字符串，如诸如 [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] 异常之类的文本和输出消息。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]使用标准 .NET Framework 中心和辐射模型。 中心程序集或主程序集包含默认语言资源。 轮辐程序集或附属程序集包含特定于语言的资源。 有关详细信息，请参阅[打包和部署资源](/previous-versions/dotnet/netframework-4.0/sb6a8618(v=vs.100))。 附属程序集是从资源（*.resx*）文件编译的。 将特定于语言的资源文件添加到项目和解决方案包时，会将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 资源文件编译为名为 *{project Name} .resources.dll*的附属程序集。

 与 ASPX 标记一样，通过将单独的资源文件项目项添加到项目来本地化 SharePoint 应用程序代码;一个用于默认语言，另一个用于每种本地化语言。 不过，如前文所述，如果你已有用于本地化 ASPX 标记的资源文件，则可以重复使用它们来本地化代码。 如果需要创建资源文件，请为默认语言资源文件指定一个以 *.resx*扩展名追加的选项名称。 将已本地化的资源文件命名为与特定语言区域性一起附加的相同名称 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 。 将每个资源文件的 "生成操作" 属性设置为 "嵌入的资源"，以便能够创建附属资源程序集。

 若要创建附属程序集，请生成项目，然后通过**包设计器**的 "**高级**" 选项卡将文件添加为其他程序集。 添加程序集时，请在位置路径前面添加区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 文件夹，如*取消反 \\ 工程项名称} .resources.dll*。 这允许包包含同名的文件。

 在代码中，使用以下语法将硬编码字符串替换为对方法的调用 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> ：

```aspx-csharp
HttpContext.GetGlobalResourceObject("<Resource File Name>", "<String ID>")
```

 有关详细信息，请参阅[如何：本地化代码](../sharepoint/how-to-localize-code.md)。

#### <a name="web-part-code-localization"></a>Web 部件代码本地化
 Web 部件包括自定义属性编辑器功能，其中包括使用硬编码字符串的代码属性，如 WebDisplayName、Category 和 WebDescription。 若要替换这些特性的字符串值，请创建一个派生自该特性的类的单独的类。 在这些类中，设置特性的属性。 特性属性取决于基类。 例如，WebDisplayName 特性属性是 DisplayNameValue，WebDescription 特性属性为 DescriptionValue。

 在派生类中，引用资源文件中的字符串 ID 和 ResourceManager 对象，以获取字符串 ID 的本地化值。 将此值返回到属性编辑器属性。

## <a name="see-also"></a>另请参阅
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
