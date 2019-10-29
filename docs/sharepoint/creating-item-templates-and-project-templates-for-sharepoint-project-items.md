---
title: SharePoint 项目项的项模板/项目模板
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- .spdata files
- projects [SharePoint development in Visual Studio], creating custom templates
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, creating custom project and item templates
- project items [SharePoint development in Visual Studio], creating custom templates
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65bbd58bf9b3e0b399603a083615daccc382a98f
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981166"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>为 SharePoint 项目项创建项模板和项目模板

定义自定义 SharePoint 项目项类型时，可以将其与项模板或项目模板相关联。 此关联使其他开发人员可以使用 Visual Studio 中的项目项。 你还可以为模板创建向导。

例如，Visual Studio 不包括用于向 SharePoint 站点添加字段的项目模板或项模板。 您可以定义一个表示字段的 SharePoint 项目项类型，然后构造一个其他开发人员可用于向 SharePoint 项目添加字段项的项模板。 或者，您可以构造项目模板，使开发人员能够创建具有字段项的新 SharePoint 项目。 在这两种情况下，你还可以提供当开发人员使用你的模板时显示的向导。 此向导可以收集开发人员提供的信息来配置新项或项目。

项模板和项目模板为 *.zip*文件，其中包含 Visual Studio 用来创建项目项或项目的文件。 有关项模板和项目模板基础的详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-item-templates"></a>创建项模板
 为 SharePoint 项目项创建项模板时，某些始终需要的文件以及某些类型的项目项可能会使用的可选文件。 有关演示如何定义 SharePoint 项目项类型并为其创建项模板的演练，请参阅[演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

 下表列出了为 SharePoint 项目项创建项模板所需的文件。

|所需文件|描述|
|-------------------|-----------------|
|*Spdata*文件|此 XML 文件指定项目项的内容和默认行为。 此文件必须包含在项模板中。 有关*spdata*文件的内容的详细信息，请参阅[SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。|
|*.Vstemplate*文件。|此文件为 Visual Studio 提供了在 "**添加新项**" 对话框中显示模板以及从模板创建项目项所需的信息。 此文件必须包含在项模板中。 有关详细信息，请参阅[Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的 Visual Studio 扩展程序集。|此程序集定义项目项的运行时行为。 此程序集必须包含在具有项模板的 VSIX 包中。 有关详细信息，请参阅[在 Visual Studio 中定义 sharepoint 工具](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)的[自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)和部署扩展。|

 下表列出了可以包含在项模板中的一些最常见的可选文件。 某些类型的项目项可能需要此处未列出的其他文件。

| 可选文件 | 描述 |
|----------------------| - |
| *元素 .xml* | *功能元素*文件。 此文件定义由项目项创建的自定义项的 UI 和行为。 每种类型的自定义（例如，列表实例、内容类型或自定义操作）都有不同的架构，用于定义此文件的内容。 有关详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))和[功能架构](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))。 |
| *Schema .xml* | 列表定义的架构文件。 有关详细信息，请参阅[构建基块：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))和[架构 .xml](/previous-versions/office/developer/sharepoint-2010/ms459356(v=office.14))。 |
| *webpart* | *Web 部件定义*文件。 此文件包含 Web 部件的属性设置。 有关详细信息，请参阅[构建基块： Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。 |
| *.ascx* | ASP.NET UserControl 文件。 此文件定义可视 Web 部件的 UI。 |
| *.aspx* | ASP.NET 页面文件。 此文件包含定义应用程序页的 XML 标记。 |
| *.cs*或 *.vb*文件 | 这些代码文件定义 SharePoint 自定义的行为，这些自定义项具有可从视觉对象C#或 Visual Basic 代码访问的编程模型，如应用程序页、Web 部件和工作流。 |

## <a name="create-project-templates"></a>创建项目模板
 创建 SharePoint 项目模板时，某些文件始终是必需的，并且是某些类型的项目可能会使用的可选文件。 通常，SharePoint 项目包含至少一个 SharePoint 项目项。 但这不是必需的。 例如，你可以定义一个 SharePoint 项目模板，该模板旨在仅用于部署在其他项目中创建的 SharePoint 解决方案。

 有关演示如何定义 SharePoint 项目项类型并为其创建项目模板的演练，请参阅[演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。

 下表列出了必须包含在 SharePoint 项目模板中的文件。

|所需文件|描述|
|-------------------|-----------------|
|*.Vstemplate*文件|此文件为 Visual Studio 提供了在 "**新建项目**" 对话框中显示模板以及从模板创建项目所需的信息。 有关详细信息，请参阅[Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|*.Csproj*或 *.vbproj*文件|这是项目文件。 它定义项目的内容和配置设置。|
|*Package. package*|此文件定义项目的部署包。 使用包设计器自定义项目的解决方案包时，Visual Studio 会将有关解决方案包的数据存储在此文件中。<br /><br /> 当你创建自定义 SharePoint 项目模板时，我们建议你仅在*包*文件中包含所需的最少内容，并且通过使用扩展中的 <xref:Microsoft.VisualStudio.SharePoint.Packages> 命名空间中的 api 来配置解决方案包，与项目模板关联。 如果执行此操作，你的项目模板将受到保护，以防止将来更改包文件的结构 *。* 有关演示如何创建*包*的示例，请参阅 "[演练：使用项目模板创建网站栏项目项，第1部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)"。<br /><br /> 如果要直接修改*包*文件，可以使用 *% Program Files （x86）% \ Microsoft Visual Studio 11.0 \ Xml\Schemas\PackageModelSchema.xsd*中的架构验证内容。|
|*Package .xml*|此文件为从项目生成的 SharePoint 解决方案包（ *.wsp*）提供解决方案清单文件（*manifest*）的基础。 如果您想要指定不打算由您的项目类型的用户更改的某些行为，则可以向此文件中添加内容。 有关详细信息，请参阅[构建基块：解决方案](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))和[解决方案架构](/sharepoint/dev/schema/solution-schema)。<br /><br /> 从项目中生成解决方案包时，Visual Studio 会将*package*和 package *.xml*文件的内容合并到解决方案清单文件中。 有关生成解决方案包的详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

 下表列出了可在项目模板中包含的可选文件。

|可选文件|描述|
|-------------------|-----------------|
|SharePoint 项目项|可以包含一个或多个定义 SharePoint 项目项类型的 spdata 文件。 每个*spdata*文件必须在包含在项目模板的 VSIX 包中的扩展程序集中具有匹配的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现。 有关详细信息，请参阅[创建项模板](#create-item-templates)。<br /><br /> 通常，SharePoint 项目包含至少一个 SharePoint 项目项。 但这不是必需的。|
|*\<功能功能 > 功能*|此文件定义用于对多个项目项进行分组以进行部署的 SharePoint 功能。 使用功能设计器自定义项目中的功能时，Visual Studio 会将有关此功能的数据存储在此文件中。 如果要将项目项分组到不同的功能，则可以包含多个*特性*文件。<br /><br /> 当你创建自定义 SharePoint 项目模板时，我们建议你仅在每个 *. 功能*文件中包含最少的必需内容，并通过使用与关联的扩展中的 <xref:Microsoft.VisualStudio.SharePoint.Features> 命名空间中的 api 来配置功能项目模板。 如果执行此操作，则会保护项目模板，使其不会在将来对*功能*文件的结构进行更改。 有关演示如何使用所需的最少内容创建 *. 功能*文件的示例，请参阅[演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果要直接修改*功能*文件，可使用 *% Program Files （x86）% \ Microsoft Visual Studio 11.0 \ Xml\Schemas\FeatureModelSchema.xsd*中的架构验证内容。|
|*\<功能功能 >。Template .xml*|此文件为从项目生成的每个功能提供功能清单文件（*feature*）的基础。 如果您想要指定不打算由您的项目类型的用户更改的某些行为，则可以向此文件中添加内容。 有关详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))和[功能 .xml](/sharepoint/dev/schema/feature-xml-files)文件。<br /><br /> 从项目生成解决方案包时，Visual Studio 会合并每对 *\<功能，> 功能*文件和\<功能名 > 的内容 *。将模板 .xml*文件导入到功能清单文件中。 有关生成解决方案包的详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>为项模板和项目模板创建向导
 定义 SharePoint 项目项类型并将其与项或项目模板关联后，还可以创建一个向导。 当开发人员使用项模板将 SharePoint 项目项添加到项目时，或者当开发人员使用项目模板创建包含 SharePoint 项目项的新项目时，该向导将显示。 此向导可用于从开发人员收集信息并初始化新的 SharePoint 项目项。

 有关演示如何为项模板和项目模板创建向导的演练，请参阅[演练：使用项模板创建自定义操作项目项、第2部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)和[演练：使用项目创建网站栏项目项模板，第2部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项（第2部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
