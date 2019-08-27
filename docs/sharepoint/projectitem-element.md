---
title: ProjectItem 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2768a2e55b3e38158f2ef6b856a653a1a2c12dfa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562398"
---
# <a name="projectitem-element"></a>ProjectItem 元素
  表示 SharePoint 项目项。 此元素的必需的根元素的 *.spdata*文件。

## <a name="syntax"></a>语法

```xml
<ProjectItem DefaultFile = "File that opens in the editor when you open the project item"
    FeatureReceiverClass = "Class that implements a feature receiver for the project item"
    FeatureReceiverAssembly = "Assembly that defines a feature receiver for the project item"
    SupportedTrustLevels = "Trust levels that the project item supports"
    SupportedDeploymentScopes = "Deployment scopes that the project item supports"
    Type="Identifier for the project item">
  <Files>...</Files>
  <ProjectItemFolder>...</ProjectItemFolder>
  <SafeControls>...</SafeControls>
  <FeatureProperties>...</FeatureProperties>
  <ExtensionData>...</ExtensionData>
</ProjectItem>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|**DefaultFile**|可选**xs： 字符串**属性。<br /><br /> 包括文件名称，打开中的 SharePoint 项目项时，在 Visual Studio 编辑器中打开的文件的相对路径**解决方案资源管理器**。 该路径是相对于包含文件夹 *.spdata*文件。|
|**FeatureReceiverClass**|可选**xs: string**属性。<br /><br /> 功能接收器类的此 SharePoint 项目项的完全限定的名称。 有关功能接收器的详细信息，请参阅[提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。|
|**FeatureReceiverAssembly**|可选**xs: string**属性。<br /><br /> 指定定义此 SharePoint 项目项的功能接收器的程序集的完全限定的名称。 有关功能接收器的详细信息，请参阅[提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。 有关完全限定的程序集名称的详细信息，请参阅[程序集名称](/dotnet/framework/app-domains/assembly-names)。|
|**SupportedTrustLevels**|可选**xs: string**属性。<br /><br /> 指定此 SharePoint 项目项支持的信任级别。 此值可以是下列字符串之一：沙盒解决方案，FullTrust，或全部。 值 All 指定 Sandboxed 和 FullTrust。<br /><br /> 中的自定义 SharePoint 项目项类型，此属性的值对应的值分配给<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A>属性的实现中<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法。 如果指定此属性的不同值时，Visual Studio 将覆盖的值，以便指定要在中指定的信任级别相同<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A>属性。|
|**SupportedDeploymentScopes**|可选**xs: string**属性。<br /><br /> 指定此 SharePoint 项目项支持部署范围。 此值是由逗号分隔字符串，包含一个或多个以下字符串：场、 站点、 Web、 web 应用程序或包。 例如： `Web, Site`<br /><br /> 中的自定义 SharePoint 项目项类型，此属性的值对应的值分配给<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A>属性的实现中<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法。 如果指定此属性的不同值时，Visual Studio 将覆盖的值，以便指定要在中指定的信任级别相同<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A>属性。|
|**Type**|所需**xs: string**属性。<br /><br /> SharePoint 项目项的标识符。 中的自定义 SharePoint 项目项类型，标识符是传递给字符串<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。<br /><br /> Visual Studio 附带的内置 SharePoint 项目项的标识符的列表，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|可选元素。<br /><br /> 表示 SharePoint 项目项与相关联的自定义数据项的集合。<br /><br /> 您可只包含一个**ExtensionData**元素。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|可选元素。<br /><br /> 表示部署到 SharePoint 时，包含与某个功能的属性值的集合。<br /><br /> 您可只包含一个**FeatureProperties**元素。|
|[文件](../sharepoint/files-element.md)|可选**FileCollectionType**元素。<br /><br /> 指定要部署使用 SharePoint 项目项，如功能元素文件和依赖的非 SharePoint 项目的输出的文件。<br /><br /> 包括**文件**或**ProjectItemFolder**元素，但不可同时使用两者。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|可选**ProjectItemFolderType**元素。<br /><br /> 表示映射的文件夹。<br /><br /> 包括**文件**或**ProjectItemFolder**元素，但不可同时使用两者。|
|[SafeControls](../sharepoint/safecontrols-element.md)|可选元素。<br /><br /> 表示的 ASPX 控件和指定为安全的任何用户访问 SharePoint 站点上任何 ASPX 页上的 Web 部件的集合。<br /><br /> 您可只包含一个**SafeControls**元素。|

### <a name="parent-elements"></a>父元素
 无。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
[SharePoint 项目项架构 rseference](../sharepoint/sharepoint-project-item-schema-reference.md)
