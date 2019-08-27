---
title: 项模板/项目模板的 SharePoint 项目项
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
ms.openlocfilehash: 8f41783689e572ca823788e1a8dbcf772f07e924
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177616"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>创建项模板和用于 SharePoint 项目项的项目模板

在定义的自定义 SharePoint 项目项类型时，可以将其与项模板或项目模板。 这种关联允许其他开发人员使用 Visual Studio 中的项目项。 此外可以创建模板向导。

例如，Visual Studio 不包括项目模板或项模板将字段添加到 SharePoint 站点。 可以定义 SharePoint 项目项类型表示的字段，然后构造其他开发人员可用于将字段项添加到 SharePoint 项目项模板。 或者，您可以构建项目模板，以便开发人员可以创建新的 SharePoint 项目具有字段项。 在这两种情况下，你还可以提供开发人员使用你的模板时，将显示一个向导。 此向导可以从开发人员配置新项目收集的信息。

项模板和项目模板是 *.zip*包含 Visual Studio 用来创建项目项或项目的文件的文件。 有关项模板和项目模板的基础知识的详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-item-templates"></a>创建项模板
 创建 SharePoint 项目项的项模板时，有一些始终是必需的文件和可能使用的某些类型的项目项的可选文件。 有关演示如何定义 SharePoint 项目项类型并为其创建项模板的演练，请参阅[演练： 使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

 下表列出了所需的文件以创建 SharePoint 项目项的项模板。

|所需文件|描述|
|-------------------|-----------------|
|*.Spdata*文件|此 XML 文件指定的内容和项目项的默认行为。 此文件必须包括在项模板。 详细了解的内容 *.spdata*文件，请参阅[SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。|
|一个 *.vstemplate*文件。|此文件中显示模板所需的信息提供 Visual Studio**添加新项**对话框中，并从模板创建项目项。 此文件必须包括在项模板。 有关详细信息，请参阅[Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|Visual Studio 的扩展插件程序集，实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>接口。|此程序集定义项目项的运行的时的行为。 此程序集必须包含带有项模板 VSIX 包中。 有关详细信息，请参阅[定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)并[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。|

 下表列出了一些最常见的可选文件可以包括在项模板。 某些类型的项目项可能需要此处未列出的其他文件。

| 可选文件 | 描述 |
|----------------------| - |
| *Elements.xml* | 一个*Feature 元素*文件。 此文件定义的 UI 和行为的自定义项创建的项目项。 每种类型的自定义项，如列表实例、 内容类型或自定义操作，有不同的架构，用于定义此文件的内容。 有关详细信息，请参阅[构建基块：功能](http://go.microsoft.com/fwlink/?LinkId=169183)并[功能架构](http://go.microsoft.com/fwlink/?LinkId=169192)。 |
| *Schema.xml* | 列表定义架构文件。 有关详细信息，请参阅[构建基块：列表和文档库](http://go.microsoft.com/fwlink/?LinkId=177792)并[Schema.xml](http://go.microsoft.com/fwlink/?LinkId=177793)。 |
| *.webpart* | 一个*Web 部件定义*文件。 此文件包含 Web 部件的属性设置。 有关详细信息，请参阅[构建基块：Web 部件](http://go.microsoft.com/fwlink/?LinkId=177791)。 |
| *.ascx* | ASP.NET 用户控件文件。 此文件定义可视 Web 部件的 UI。 |
| *.aspx* | ASP.NET 页文件。 此文件包含定义应用程序页上的 XML 标记。 |
| *.cs*或 *.vb*文件 | 这些代码文件定义有一个编程模型，可以从 Visual C# 或 Visual Basic 代码，如应用程序页、 Web 部件和工作流访问的 SharePoint 自定义的行为。 |

## <a name="create-project-templates"></a>创建项目模板
 创建 SharePoint 项目模板，请时始终是必需的并可选文件，某些类型的项目可能会使用一些文件。 通常情况下，SharePoint 项目包含至少一个 SharePoint 项目项。 但是，这不是必需的。 例如，可以定义旨在仅用于部署在其他项目中创建 SharePoint 解决方案的 SharePoint 项目模板。

 有关演示如何定义 SharePoint 项目项类型并为其创建的项目模板的演练，请参阅[演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。

 下表列出了必须在 SharePoint 项目模板中包含的文件。

|所需文件|描述|
|-------------------|-----------------|
|一个 *.vstemplate*文件|此文件中显示模板所需的信息提供 Visual Studio**新的项目**对话框中，并从模板创建一个项目。 有关详细信息，请参阅[Visual Studio 模板元数据文件](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\))。|
|一个 *.csproj*或 *.vbproj*文件|这是项目文件。 它定义的内容和项目的配置设置。|
|*Package.package*|此文件定义项目的部署包。 当您使用包设计器为你的项目自定义解决方案包时，Visual Studio 将在此文件中存储解决方案包有关的数据。<br /><br /> 创建自定义 SharePoint 项目模板时，我们建议包括仅在最小所需的内容*Package.package*文件，并使用中的 Api 配置解决方案包<xref:Microsoft.VisualStudio.SharePoint.Packages>与项目模板关联的扩展中的命名空间。 如果这样做，你的项目模板防止将来的更改的结构*Package.package*文件。 有关示例，演示如何创建*Package.package*文件具有的最低要求的内容，请参阅[演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果你想要修改*Package.package*直接文件中，您可以通过使用中的架构来验证内容 *%Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\PackageModelSchema.xsd*.|
|*Package.Template.xml*|此文件提供了基础解决方案指令清单文件 (*manifest.xml*) 的 SharePoint 解决方案包 ( *.wsp*) 从项目生成。 如果你想要指定不应由您的项目类型的用户更改某些行为，可以添加到此文件的内容。 有关详细信息，请参阅[构建基块：解决方案](http://go.microsoft.com/fwlink/?LinkId=169186)并[解决方案架构](http://go.microsoft.com/fwlink/?LinkId=177794)。<br /><br /> Visual Studio 生成时从项目的解决方案包，合并的内容*Package.package*并*Package.Template.xml*到解决方案文件清单文件。 有关生成解决方案包的详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

 下表列出了可以在项目模板中包含的可选文件。

|可选文件|描述|
|-------------------|-----------------|
|SharePoint 项目项|可以包含一个或多个.spdata 文件，用于定义 SharePoint 项目项类型。 每个 *.spdata*文件必须具有匹配<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>VSIX 包项目模板中包括的扩展程序集中实现。 有关详细信息，请参阅[创建项模板](#create-item-templates)。<br /><br /> 通常情况下，SharePoint 项目包含至少一个 SharePoint 项目项。 但是，这不是必需的。|
|*\<featureName>.feature*|此文件定义了一项 SharePoint 功能，用于部署的多个项目项进行分组。 当功能设计器用于在项目中自定义功能时，Visual Studio 将在此文件中存储有关功能的数据。 如果你想要将项目项分组为不同的功能，可以包括多个 *.feature*文件。<br /><br /> 创建自定义 SharePoint 项目模板时，我们建议在每个包含的最小所需的内容 *.feature*文件，并使用中的 Api 配置功能<xref:Microsoft.VisualStudio.SharePoint.Features>中的命名空间与项目模板关联的扩展。 如果这样做，你的项目模板防止将来的更改的结构 *.feature*文件。 有关示例，演示如何创建 *.feature*文件具有的最低要求的内容，请参阅[演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。<br /><br /> 如果你想要修改 *.feature*直接文件中，您可以通过使用中的架构来验证内容 *%Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\FeatureModelSchema.xsd*。|
|*\<featureName>.Template.xml*|此文件提供了基础功能清单文件 (*Feature.xml*) 从项目生成的每项功能。 如果你想要指定不应由您的项目类型的用户更改某些行为，可以添加到此文件的内容。 有关详细信息，请参阅[构建基块：功能](http://go.microsoft.com/fwlink/?LinkId=169183)并[Feature.xml](http://go.microsoft.com/fwlink/?LinkId=177795)文件。<br /><br /> Visual Studio 生成时从项目的解决方案包，将每个对的内容合并 *\<featureName >.feature*文件并 *\<功能名 >。Template.xml*文件到一项功能清单文件。 有关生成解决方案包的详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>创建项模板和项目模板中的向导
 定义 SharePoint 项目项类型并将其关联的项或项目模板后，您还可以创建一个向导。 向导将显示当开发人员使用项模板将 SharePoint 项目项添加到项目，或开发人员使用的项目模板来创建一个包含 SharePoint 项目项的新项目时。 若要从开发人员收集信息并初始化新的 SharePoint 项目项，可以使用该向导。

 有关演练，演示如何创建项模板和项目模板中的向导，请参阅[演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)和[演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
