---
title: 本地化 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 90da60cb904ba6e3db2be3805256fcf4eb9122ee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444345"
---
# <a name="localize-sharepoint-solutions"></a>本地化 SharePoint 解决方案

  准备你的应用程序，以便可以全球范围内使用的过程称为本地化。 本地化将资源翻译为特定区域性。 有关详细信息，请参阅[Globalizing and Localizing Applications](../ide/globalizing-and-localizing-applications.md)。 本主题提供有关如何本地化 SharePoint 解决方案的概述。

 若要本地化解决方案，您从代码中移除硬编码的字符串，它们提取到资源文件。 资源文件是[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]-基于使用的文件 *.resx*扩展。 资源文件包含你的解决方案中使用的字符串的翻译的版本。 有关详细信息，请参阅[应用程序中的资源](http://go.microsoft.com/fwlink/?LinkID=155844)。

> [!NOTE]
> 将只有字符串资源添加到 SharePoint 解决方案资源文件。 尽管资源编辑器，您可以添加非字符串资源，但非字符串资源不会部署到 SharePoint。

## <a name="resource-files"></a>资源文件
 有三种类型的资源文件： 默认、 非特定语言和特定于语言的。

|资源文件类型|描述|
|------------------------|-----------------|
|默认|也称为回退资源，默认资源文件包含针对默认区域性，例如英语本地化的字符串。 如果找不到指定语言的本地化的资源文件，则使用它们。 默认资源没有单独的文件，它们存储在主应用程序程序集。|
|非特定语言|包含针对一种语言，而不是特定区域性本地化的字符串的资源文件。 例如，"fr"表示法语。|
|特定于语言的|包含针对某种语言和区域性本地化的字符串的资源文件。 例如，"FR-CA"表示加拿大法语。|

 有关详细信息，请参阅[层次结构的组织资源的本地化](http://go.microsoft.com/fwlink/?LinkId=178360)。

 若要在开发中的 SharePoint 项目中指定默认资源文件[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，选择**固定语言 （固定国家/地区）** 中的区域性列表**添加资源**对话框时您添加资源文件。

## <a name="localize-visual-studio-sharepoint-solutions"></a>本地化 Visual Studio SharePoint 解决方案
 在本地化解决方案，应考虑的所有文本向用户显示你的解决方案的信息。 信息性消息、 错误消息和[!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)]必须转换字符串，并且这些翻译放在资源文件。

 在资源文件中的每个字符串都有唯一标识符。 每个资源文件中的已翻译字符串使用相同的标识符。 例如，如果"String1"是默认资源文件中的第一个字符串的标识符，特定于语言的资源文件中的第一个字符串使用相同的标识符。

 有三个区域，您通常本地化中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 应用程序： 功能、 ASPX 页面标记和代码。 为便于说明，以下各节假定您有你想要本地化为德语和日语的 SharePoint 解决方案。 默认语言为英语。

### <a name="localize-features"></a>本地化功能
 若要本地化功能，必须以替换引用的已翻译的标题和已本地化的资源文件中字符串的表达式的硬编码的标题和说明的功能。 进行此更改中的**功能设计器**中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关详细信息，请参阅[如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)。

 若要将英语功能本地化为德语和日语，您将三个资源文件项目项添加到你的项目： 一个用于英语、 德语和日语。 功能资源文件不能用于本地化 ASPX 标记或代码;需要为其单独的资源文件。

 创建功能资源文件后，向其添加已翻译的字符串。 访问本地化的字符串采用以下格式的表达式：

```aspx-csharp
$Resources:String ID
```

 中的功能资源[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]始终命名为资源。 如果您选择一种语言而非固定语言，则区域性[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]添加到资源文件名称。 例如，如果添加固定语言 （默认值） 功能资源文件，则将调用*Resources.resx*。 如果通过选择日语 （日本） 区域性添加特定于语言的功能资源，该文件称为*Resources.ja JP.resx*。 功能资源文件的名称自动分配，并且不能进行更改。

 范围的功能资源是本地的添加到功能。 若要创建可以由解决方案中的任何功能或元素文件使用的资源，请添加**全局资源文件**而不是功能资源文件的项目项。 **全局资源文件**项目项位于**2010年**下的文件夹**SharePoint**中**添加新项**对话框。 全局资源文件部署到 SharePoint 根文件夹的 \Resources 文件夹。

### <a name="localize-aspx-page-markup"></a>本地化 ASPX 页面标记
 若要本地化[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]页，将三个资源文件项目项添加到你的项目： 一个用于英语、 德语和日语。 如果不需要本地化除了标记以外的代码，则可以改为添加全局资源文件。

 提供的默认语言资源文件的名称。 为相同的名称附加有特定于语言的区域性的本地化的资源文件[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如， *MyAppResources.de-DE.resx*德语和*用于日语*日语。

 设置**部署类型**到每个资源文件的属性**AppGlobalResource**。 这会导致要部署到 App_GlobalResources 文件夹，其中它们可供所有 ASPX 页面和控件在解决方案中的资源文件。 App_GlobalResources 文件夹位于 C:\inetpub\wwwroot\wss\VirtualDirectories\\< 端口号\>\App_GlobalResources。

> [!NOTE]
> 如果使用非全局资源文件，请将它们移到项目项文件夹，若要启用的部署类型属性和其他特定于 SharePoint 的属性。

 此外可以使用 ASPX 标记资源文件来本地化代码。 如果使用的资源来本地化除 ASPX 标记之外的代码，生成操作属性将设置保留的每个文件为嵌入的资源，以便将资源编译到附属程序集。 但是，如果使用的资源文件来本地化标记，你可以选择更改生成操作以防止文件被编译到主应用程序程序集的内容。

 ASPX 页面和控件标记中的所有硬编码属性字符串替换为以下格式的表达式：

```aspx-csharp
<asp:<class> runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 例如：

```aspx-csharp
<asp:Button ID="btn1" runat="server" onclick="btn1_Click" Text="<%$Resources:Resource1,String7%>"></asp:Button>
```

 对于文本形式的 ASPX，采用以下格式使用的表达式：

```aspx-csharp
<asp:literal ID="<ID>" runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 例如：

```aspx-csharp
<asp:literal ID="Literal1" runat="server" Text="<%$Resources:Resource1, String9%>" />
```

 有关详细信息，请参阅[如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)。

### <a name="localize-code"></a>本地化代码
 除了本地化功能字符串和[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]标记中，您还必须本地化消息字符串和解决方案代码中出现的错误字符串。 本地化信息和错误消息包含在附属程序集中。 附属程序集包含的用户均可见，如字符串[!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)]文本和输出消息，如异常。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用标准.NET Framework 集散模型。 中心或主程序程序集包含的默认语言资源。 辐射或附属程序集包含特定于语言的资源。 有关详细信息，请参阅[打包和部署资源](http://go.microsoft.com/fwlink/?LinkId=179280)。 编译从资源的附属程序集 (*.resx*) 文件。 在将特定于语言的资源文件添加到你的项目和解决方案包时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将资源文件编译到附属程序集名为 *{Project Name}.resources.dll*。

 与 ASPX 标记一样本地化 SharePoint 应用程序代码通过将单独的资源文件项目项添加到你的项目;一个默认语言，一个用于每个本地化语言。 但是，如前所述，如果已有用于本地化 ASPX 标记的资源文件，您可以重复使用它们来本地化代码。 如果需要创建资源文件，为默认语言资源文件追加与所选的命名 *.resx*扩展。 本地化的资源文件命名相同的名称附加有特定于语言的区域性[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 设置为嵌入的资源可用于创建附属资源程序集的每个资源文件的 Build Action 属性。

 若要创建附属程序集，生成项目，然后将文件添加为通过其他程序集**高级**选项卡**包设计器**。 在添加程序集时，前面添加区域性[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]文件夹在位置路径，如*DE-DE\\{项目项名称}.resources.dll*。 这允许包包含具有相同名称的文件。

 在代码中，将对的调用替换为硬编码的字符串<xref:System.Web.HttpContext.GetGlobalResourceObject%2A>方法使用以下语法：

```aspx-csharp
HttpContext.GetGlobalResourceObject("<Resource File Name>", "<String ID>")
```

 有关详细信息，请参阅[如何：本地化代码](../sharepoint/how-to-localize-code.md)。

#### <a name="web-part-code-localization"></a>Web 部件代码本地化
 Web 部件包括自定义属性编辑器功能，其中包括使用硬编码的字符串，例如 WebDisplayName、 Category 和 WebDescription 代码属性。 若要替换这些属性的字符串值，请创建单独的类派生特性的类。 在这些类中，设置该属性的属性。 特性属性依赖于类的基类。 例如，WebDisplayName 特性属性为 DisplayNameValue，WebDescription 特性属性为 DescriptionValue。

 在派生类中，引用的字符串 ID 从资源文件和 ResourceManager 对象，若要获取的本地化的值的字符串 id。 此值返回到属性编辑器特性。

## <a name="see-also"></a>请参阅
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：使用资源文件指定本地化的名称、 属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
