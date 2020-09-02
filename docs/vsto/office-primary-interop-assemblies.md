---
title: Office 主互操作程序集
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies
- assemblies [Office development in Visual Studio], primary interop assemblies
- Office primary interop assemblies
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f4677cd2d178781d79b11ac3b1010a76fd6fcf00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985717"
---
# <a name="office-primary-interop-assemblies"></a>Office 主互操作程序集

若要在 Office 项目中使用 Microsoft Office 应用程序的功能，你必须使用该应用程序的主互操作程序集 (PIA)。 PIA 使托管代码可与 Microsoft Office 应用程序基于 COM 的对象模型进行交互。

[!include[Add-ins note](includes/addinsnote.md)]

创建新的 Office 项目时，Visual Studio 会添加对生成该项目所需的 PIA 的引用。 在某些情况下，你可能需要添加对其他 PIA 的引用（例如，如果你希望在 Microsoft Office Excel 项目中使用 Microsoft Office Word 的功能）。

本主题描述在 Office 项目中使用 Microsoft Office PIA 的以下方面：

- [分隔主互操作程序集以生成和运行项目](#separateassemblies)

- [在单个项目中使用多个 Microsoft Office 应用程序的功能](#usingfeatures)

- [Microsoft Office 应用程序的主互操作程序集的完整列表](#pialist)

有关主互操作程序集的详细信息，请参阅 [主互操作程序集](/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))。

<a name="separateassemblies"></a>

## <a name="separate-primary-interop-assemblies-to-build-and-run-projects"></a>分隔主互操作程序集以生成和运行项目

Visual Studio 在开发计算机上使用不同的 PIA 集。 这些不同的程序集位于下列位置：

- Program files 目录中的文件夹

  当你编写代码和生成项目时，将使用这些程序集副本。 Visual Studio 会自动安装这些程序集。

- 全局程序集缓存

  这些程序集副本在某些开发任务期间（例如在运行或调试项目时）使用。 Visual Studio 不会安装和注册这些程序集；你必须自己安装和注册。

### <a name="primary-interop-assemblies-in-the-program-files-directory"></a>Program files 目录中的主互操作程序集

安装 Visual Studio 时，会将 PIA 自动安装到文件系统中全局程序集缓存之外的某个位置。 创建新项目时，Visual Studio 会自动将对这些 PIA 副本的引用添加到你的项目中。 Visual Studio 使用这些 PIA 副本（而非全局程序集缓存中的程序集）在开发和生成项目时解析类型引用。

这些 PIA 副本帮助 Visual Studio 避免在全局程序集缓存中注册 PIA 的不同版本时可能发生的多种开发问题。

从 Visual Studio 2017 开始，这些 Pia 副本安装在开发计算机上的下列共享位置：

- `%ProgramFiles%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\`

- `%ProgramFiles(x86)%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\`64 位操作系统上的 (或) 

> [!NOTE]
> 对于较旧版本的 Visual Studio，这些 Pia 将安装到 `%ProgramFiles%` 该版本的 Visual studio 文件夹下的 Office\PIA 文件夹的 Visual Studio Tools。
> 例如： `%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Visual Studio Tools for Office\PIA\`

### <a name="primary-interop-assemblies-in-the-global-assembly-cache"></a>全局程序集缓存中的主互操作程序集

若要执行某些开发任务，必须在开发计算机上的全局程序集缓存中安装并注册 PIA。 通常，在开发计算机上安装 Office 时会自动安装 PIA。 有关详细信息，请参阅 [配置计算机以开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

若要运行 Office 解决方案，无需在最终用户计算机上安装 Office PIA。 有关详细信息，请参阅 [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)。

<a name="usingfeatures"></a>

## <a name="use-features-of-multiple-microsoft-office-applications-in-a-single-project"></a>在单个项目中使用多个 Microsoft Office 应用程序的功能

Visual Studio 中的每个 Office 项目模板旨在与单个 Microsoft Office 应用程序配合使用。 若要使用多个 Microsoft Office 应用程序的功能，或者使用 Visual Studio 中没有项目的应用程序或组件的功能，必须添加对所需 PIA 的引用。

在大多数情况下，应添加对 Visual Studio 安装在目录下的 Pia 的引用 `%ProgramFiles(x86)%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\` 。 这些版本的程序集显示在 "**引用管理器**" 对话框的 "**框架**" 选项卡上。 有关详细信息，请参阅 [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)。

如果你在全局程序集缓存中安装并注册了 PIA，则这些版本的程序集显示在 **“引用管理器”** 对话框的 **“COM”** 选项卡上。 你应当避免添加对这些版本的程序集的引用，因为使用它们时可能会出现某些开发问题。 例如，如果你在全局程序集缓存中注册了 PIA 的不同版本，则项目将自动绑定到你最后一次注册的程序集版本，即使在 **“引用管理器”** 对话框的 **“COM”** 选项卡上指定了其他程序集版本也是如此。

> [!NOTE]
> 添加一个引用某些程序集的程序集时，这些被引用的程序集将自动添加到项目中。 例如， `Office.dll` `Microsoft.Vbe.Interop.dll` 当你添加对 Word、Excel、Outlook、Microsoft Forms 或 Graph 程序集的引用时，将自动添加对和程序集的引用。

<a name="pialist"></a>

## <a name="primary-interop-assemblies-for-microsoft-office-applications"></a>Microsoft Office 应用程序的主互操作程序集

下表列出了可用于、和的主互操作程序集 [!INCLUDE[Office_16_short](../vsto/includes/office-16-short-md.md)] [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 。

<br/>

|Office 应用程序或组件|主互操作程序集名称|
|-------------------------------------|-----------------------------------|
|Microsoft Access 14.0 对象库<br /><br /> Microsoft Access 15.0 对象库|Microsoft.Office.Interop.Access.dll|
|Microsoft Office 14.0 Access 数据库引擎对象库<br /><br /> Microsoft Office 15.0 Access 数据库引擎对象库|Microsoft.Office.Interop.Access.Dao.dll|
|Microsoft Excel 14.0 对象库<br /><br /> Microsoft Excel 15.0 对象库|[Microsoft.Office.Interop.Excel.dll](/dotnet/api/microsoft.office.interop.excel?view=excel-pia)|
|Microsoft Graph 14.0 对象库（PowerPoint、Access 和 Word 将该对象库用于图形）<br /><br /> Microsoft Graph 15.0 对象库|Microsoft.Office.Interop.Graph.dll|
|Microsoft InfoPath 2.0 类型库（仅用于 InfoPath 2007）|[Microsoft.Office.Interop.InfoPath.dll](/dotnet/api/microsoft.office.interop.infopath?view=infopath-form)|
|Microsoft InfoPath XML 互操作程序集（仅用于 InfoPath 2007）|Microsoft.Office.Interop.InfoPath.Xml.dll|
|Microsoft Office 14.0 对象库（Office 共享的功能）<br /><br /> Microsoft Office 15.0 对象库（Office 共享的功能）|office.dll|
|Microsoft Office Outlook 视图控件（在网页和应用程序中可用来访问收件箱）|Microsoft.Office.Interop.OutlookViewCtl.dll|
|Microsoft Outlook 14.0 对象库<br /><br /> Microsoft Outlook 15.0 对象库|[Microsoft.Office.Interop.Outlook.dll](/dotnet/api/microsoft.office.interop.outlook?view=outlook-pia)|
|Microsoft PowerPoint 14.0 对象库<br /><br /> Microsoft PowerPoint 15.0 对象库|Microsoft.Office.Interop.PowerPoint.dll|
|Microsoft Project 14.0 对象库<br /><br /> Microsoft Project 15.0 对象库|[Microsoft.Office.Interop.MSProject.dll](/dotnet/api/microsoft.office.interop.msproject?view=office-project-server)|
|Microsoft Publisher 14.0 对象库<br /><br /> Microsoft Publisher 15.0 对象库|Microsoft.Office.Interop.Publisher.dll|
|Microsoft SharePoint Designer 14.0 Web 对象引用库|Microsoft.Office.Interop.SharePointDesigner.dll|
|Microsoft SharePoint Designer 14.0 Page 对象引用库|Microsoft.Office.Interop.SharePointDesignerPage.dll|
|Microsoft 智能标记2.0 类型库 **注意：**  在和中已弃用智能标记 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)] 。|Microsoft.Office.Interop.SmartTag.dll|
|Microsoft Visio 14.0 类型库<br /><br /> Microsoft Visio 15.0 类型库|Microsoft.Office.Interop.Visio.dll|
|Microsoft Visio 14.0 Save As Web 类型库<br /><br /> Microsoft Visio 15.0 Save As Web 类型库|Microsoft.Office.Interop.Visio.SaveAsWeb.dll|
|Microsoft Visio 14.0 绘图控件类型库<br /><br /> Microsoft Visio 15.0 绘图控件类型库|Microsoft.Office.Interop.VisOcx.dll|
|Microsoft Word 14.0 对象库<br /><br /> Microsoft Word 15.0 对象库|[Microsoft.Office.Interop.Word.dll](/dotnet/api/microsoft.office.interop.word?view=word-pia)|
|Microsoft Visual Basic for Applications Extensibility 5.3|Microsoft.Vbe.Interop.dll|

### <a name="binding-redirect-assemblies"></a>绑定重定向程序集

在全局程序集缓存中安装并注册 Office PIA（通过 Office，或通过为 PIA 安装可再发行组件包）时，绑定重定向程序集也只会安装在全局程序集缓存中。 这些程序集有助于确保在运行时加载主互操作程序集的正确版本。

例如，当引用 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 程序集的解决方案在装有同一主互操作程序集的 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 版本的计算机上运行时，绑定重定向程序集会指示 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] 运行时加载 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 版本的主互操作程序集。

有关详细信息，请参阅 [如何：启用和禁用自动绑定重定向](/dotnet/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection)。

## <a name="see-also"></a>另请参阅

- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [InfoPath 解决方案](../vsto/infopath-solutions.md)
- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)
- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)
- [项目解决方案](../vsto/project-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [Visual Studio 中的常规参考 &#40;Office 开发&#41;](../vsto/general-reference-office-development-in-visual-studio.md)
