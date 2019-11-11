---
title: 打包 & 项目项中的部署信息
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SafeControlEntries
- VS.SharePointTools.Project.ProjectOutputReference
- VS.SharePointTools.Project.FeatureProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature properties
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
- feature properties [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature receiver
- feature receiver [SharePoint development in Visual Studio]
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: db805c308fd245554824997b24236eb2e2d80e62
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984204"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>在项目项中提供打包和部署信息
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的所有 SharePoint 项目项都具有一些属性，这些属性可用于在将项目部署到 SharePoint 时提供附加数据。 这些属性如下所示：

- 功能属性

- 功能接收器

- 项目输出引用

- 安全控件项

  这些属性将显示在 "**属性**" 窗口中。

## <a name="feature-properties"></a>功能属性
 使用 "**功能属性**" 属性可指定功能使用的数据。 功能属性数据是一组值（存储为键/值对），在功能部署到 SharePoint 时包含在其中。 部署功能后，可在代码中访问属性值。

 向项目项添加功能属性值时，会将值作为元素添加到项的功能清单中。 例如，在业务数据连接（BDC）模型项目中，ModelFileName 功能属性显示为：

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 设置功能属性值后，它将作为 FeatureProperty 元素添加到项目的*spdata*文件中。 有关访问 SharePoint 中的属性的信息，请参阅[SPFeaturePropertyCollection 类](/previous-versions/office/sharepoint-server/ms461895(v=office.15))。

 所有项目项中的相同功能属性值将合并到功能清单中。 但是，如果两个不同的项目项指定了与不匹配的值相同的功能属性键，则会发生验证错误。

 若要直接向功能文件（ *. 功能*）添加功能属性，请调用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 对象模型方法 <xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A>。 如果使用此方法，请注意，与在功能属性中添加相同的功能属性值有关的相同规则也适用于直接添加到功能文件中的属性。

## <a name="feature-receiver"></a>功能接收器
 功能接收器是在项目项的包含功能中发生特定事件时执行的代码。 例如，你可以定义在安装、激活或升级功能时执行的功能接收器。 添加功能接收器的一种方法是将其直接添加到功能，如[演练：添加功能事件接收器](../sharepoint/walkthrough-add-feature-event-receivers.md)中所述。 另一种方法是在**功能接收器**属性中引用功能接收器类名称和程序集。

### <a name="direct-method"></a>直接方法
 直接将功能接收器添加到功能时，会在解决方案资源管理器的**功能**节点下放置一个代码文件。 生成 SharePoint 解决方案时，代码将编译到一个程序集中并部署到 SharePoint。 默认情况下，功能属性 "**接收方程序集**" 和 "**接收方" 类**引用类名称和程序集。

### <a name="reference-method"></a>Reference 方法
 添加功能接收器的另一种方法是使用项目项的**功能接收器**属性来引用功能接收器程序集。 功能接收器属性值具有两个子属性：**程序集**和**类名**。 程序集必须使用其完全限定的 "强" 名称并且类名必须是完整的类型名称。 有关详细信息，请参阅[具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/wd40t7ad(v=vs.100))。 将解决方案部署到 SharePoint 后，该功能将使用引用的功能接收器来处理功能事件。

 在解决方案生成时，功能中的功能接收器属性值和其项目一起合并，以设置 SharePoint 解决方案（ *.wsp*）文件的功能清单中功能元素的 ReceiverAssembly 和 ReceiverClass 属性。 因此，如果同时指定了项目项和功能的程序集和类名称属性值，则项目项和功能属性值必须匹配。 如果值不匹配，您将收到验证错误。 如果希望项目项引用功能接收器程序集而不是其功能使用的程序集，请将其移到另一项功能。

 如果引用的功能接收器程序集尚未在服务器上，则还必须将程序集文件本身包含在包中;[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不会为你添加该功能。 部署此功能时，会将程序集文件复制到系统的 [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] 或 SharePoint 物理目录中的 Bin 文件夹。 有关详细信息，请参阅如何：[如何：添加和移除附加程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关功能接收器的详细信息，请参阅[功能事件接收器](/previous-versions/office/developer/sharepoint-2007/bb862634(v=office.12))和[功能事件](/previous-versions/office/developer/sharepoint-2010/ms469501(v=office.14))。

## <a name="project-output-references"></a>项目输出引用
 "项目输出引用" 属性指定项目项需要运行的依赖项（如程序集）。 例如，假设您的解决方案具有 BDC 项目和类项目。 如果 BDC 项目依赖于类项目输出的程序集，则可以在 BDC 项目的 "项目输出引用" 属性中引用该程序集。 打包 BDC 项目后，该依赖程序集将包含在包中。

 项目输出引用通常是程序集，但在某些情况下（如 Silverlight 项目）可以是其他文件类型。

 有关详细信息，请参阅[如何：添加项目输出引用](../sharepoint/how-to-add-a-project-output-reference.md)。

## <a name="safe-control-entries"></a>安全控件项
 SharePoint 提供了一个称为安全控制项的安全机制，用于限制不受信任的用户对某些控件的访问。 按照设计，SharePoint 允许不受信任的用户在 SharePoint 服务器上上传和创建 ASPX 页。 为了防止这些用户向 ASPX 页添加不安全代码，SharePoint 限制了对*安全控件*的访问。 安全控件是将 ASPX 控件和 Web 部件指定为安全的，并可由网站上的任何用户使用。 有关详细信息，请参阅[步骤4：将 Web 部件添加到安全控件列表](/previous-versions/office/developer/sharepoint-2007/ms581321(v=office.12))。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的每个 SharePoint 项目项都具有一个名为**安全控件项**的属性，该属性具有两个布尔子属性： **safe**和**safe for Script**。 “安全”属性指定不受信任的用户是否能访问控件。 "安全应对脚本" 属性指定不受信任的用户是否可以查看和更改控件的属性。

 安全控件项是根据程序集引用的。 通过在项目项的 "**安全控件项**" 属性中输入安全控件项，可以将这些项添加到项目的程序集。 但是，在将其他程序集添加到包时，还可以通过**包设计器**中的 "**高级**" 选项卡，将安全控件项添加到项目的程序集。 有关详细信息，请参阅[如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)或[将 Web 部件程序集注册为安全控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

### <a name="xml-entries-for-safe-controls"></a>安全控件的 XML 项
 将安全控件项添加到项目项或项目的程序集时，引用将按以下格式写入包清单：

```xml
<Assemblies>
    <Assembly Location="<assembly name>.dll"
      DeploymentTarget="<'GlobalAssemblyCache' or 'WebApplication'">>
        <SafeControls>
            <SafeControl Assembly="<assembly name>.dll" Namespace=
              "<SharePoint project name>" Safe="<true/false>"
                TypeName="<control name>"
                SafeAgainstScript="<true/false>" />
        </SafeControls>
    </Assembly>
</Assemblies>
```

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [使用模块在解决方案中包括文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
