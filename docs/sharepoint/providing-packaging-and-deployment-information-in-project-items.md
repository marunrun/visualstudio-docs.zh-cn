---
title: 在项目项中的打包和部署信息
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
ms.openlocfilehash: a9af945ff377b30925a51875db205bcd882f4585
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177708"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>提供在项目项中的打包和部署信息
  中的所有 SharePoint 项目项[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]具有可用于项目部署到 SharePoint 时提供额外的数据的属性。 这些属性如下所示：

- 功能属性

- 功能接收器

- 项目输出引用

- 安全控件项

  这些属性将显示在**属性**窗口。

## <a name="feature-properties"></a>功能属性
 使用**功能属性**属性指定的功能使用的数据。 功能属性数据是一组值 （以键/值对的形式存储），它将部署到 SharePoint 时，将包含与某个功能。 部署功能后，可在代码中访问属性值。

 当您将功能属性值添加到项目项时，将值添加为项的功能清单中的元素。 在业务数据连接 (BDC) 模型项目中，例如，ModelFileName 功能属性显示为：

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 设置功能属性值后，它将作为项目的 FeatureProperty 元素中添加 *.spdata*文件。 有关访问在 SharePoint 中的属性的信息，请参阅[SPFeaturePropertyCollection 类](http://go.microsoft.com/fwlink/?LinkId=177391)。

 从所有项目项的完全相同的功能属性值时，将合并功能清单中。 但是，如果两个不同的项目项不匹配的值与指定的相同的功能属性键，则发生验证错误。

 若要将功能属性添加直接到功能文件 ( *.feature*)，调用[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 对象模型方法<xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A>。 如果使用此方法，请注意，在功能属性中添加相同的功能属性值相同的规则也适用于直接添加到功能文件的属性。

## <a name="feature-receiver"></a>功能接收器
 功能接收器是对项目项发生某些事件时执行的代码包含的功能。 例如，可以定义该功能是安装、 激活，或升级时执行的功能接收器。 添加功能接收器是将其添加直接向一项功能，如中所述的一种方法[演练：添加功能事件接收器](../sharepoint/walkthrough-add-feature-event-receivers.md)。 另一种方法是一个功能接收器类名称和中的程序集引用**功能接收器**属性。

### <a name="direct-method"></a>直接方法
 当直接将功能接收器添加到一项功能时，代码文件将位于下**功能**在解决方案资源管理器中的节点。 生成 SharePoint 解决方案时，该代码将编译为程序集，并将部署到 SharePoint。 默认情况下，功能属性**接收器程序集**并**接收器类**引用类名称和程序集。

### <a name="reference-method"></a>Reference 方法
 功能接收器添加另一种方法是使用**功能接收器**引用功能接收器程序集的项目项的属性。 功能接收器属性值具有两个子属性：**程序集**并**类名**。 程序集必须使用其完全限定，"强"名称和类名必须是完整类型名称。 有关详细信息，请参阅[具有强名称的程序集](http://go.microsoft.com/fwlink/?LinkID=169573)。 将解决方案部署到 SharePoint 之后, 该功能使用引用的功能接收器来处理功能的事件。

 在解决方案生成时间，该功能的功能中的接收方属性值和其项目合并在一起以 SharePoint 解决方案的功能清单中设置的功能元素的 ReceiverAssembly 和 receiverclass 的属性特性 ( *.wsp*) 文件。 因此，如果同时指定了项目项和功能的程序集和类名属性值，则项目项和功能属性值必须匹配。 如果值不匹配，将收到验证错误。 如果您希望项目项引用的功能接收器程序集不是其功能使用，将其移到另一项功能。

 如果引用已不在服务器的功能接收器程序集，还必须在包中包括的程序集文件本身[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]不会为您添加它。 在部署此功能时，程序集文件复制到系统的[!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)]或 SharePoint 物理目录的 Bin 文件夹。 有关详细信息，请参阅如何：[如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关功能接收器的详细信息，请参阅[功能事件接收器](http://go.microsoft.com/fwlink/?LinkID=169574)并[功能事件](http://go.microsoft.com/fwlink/?LinkID=169575)。

## <a name="project-output-references"></a>项目输出引用
 项目输出引用属性指定一个依赖项，例如您的项目项都需要运行的程序集。 例如，假设您的解决方案具有 BDC 项目和一个项目。 如果 BDC 项目类项目输出程序集上具有依赖项，则可以引用 BDC 项目的项目输出引用属性中的程序集。 当打包 BDC 项目时，包中包含依赖程序集。

 项目输出引用通常是程序集，但在某些情况下 （例如 Silverlight 项目） 可以是其他文件类型。

 有关详细信息，请参阅[如何：添加项目输出引用](../sharepoint/how-to-add-a-project-output-reference.md)。

## <a name="safe-control-entries"></a>安全控件项
 SharePoint 提供了一种安全机制，称为安全控件项，以限制到特定控件的不受信任用户的访问。 根据设计，SharePoint 允许不受信任的用户上传并在 SharePoint 服务器上创建 ASPX 页。 若要防止这些用户将不安全代码添加到 ASPX 页，SharePoint 会限制其访问权限*安全控件*。 安全控件是 ASPX 控件和指定为安全的 Web 部件，并且由你的站点上的任何用户。 有关详细信息，请参阅[步骤 4:将 Web 部件添加到安全控件列表](http://go.microsoft.com/fwlink/?LinkID=171014)。

 中的每个 SharePoint 项目项[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]具有一个名为属性**安全控件项**具有两个布尔子属性：**安全**并**安全应对脚本**。 “安全”属性指定不受信任的用户是否能访问控件。 安全应对脚本属性指定是否不受信任的用户可以查看和更改控件的属性。

 安全控件项集进行引用。 通过输入项目项中的安全控件项添加到项目的程序集**安全控件项**属性。 但是，您还可以向项目的程序集通过添加安全控件项**高级**选项卡**包设计器**时向包中添加其他程序集。 有关详细信息，请参阅[如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)或[Web 部件程序集注册为安全控件](http://go.microsoft.com/fwlink/?LinkID=171013)。

### <a name="xml-entries-for-safe-controls"></a>XML 项的安全控件
 时安全控件项添加到项目项或对项目的程序集时，引用写入包清单采用以下格式：

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
- [包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
