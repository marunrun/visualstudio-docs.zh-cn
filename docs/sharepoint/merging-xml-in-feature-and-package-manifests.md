---
title: 合并功能和包清单中的 XML |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1378cddbc9770af923a98f1b7083a8792874b5b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840558"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>合并功能和包清单中的 XML
  功能和包是由 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 清单文件定义的。 这些打包的清单是由设计器生成的数据和 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 由用户在清单模板中输入的自定义数据的组合。 打包时，会 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句与提供程序合并， [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 以形成打包的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 清单文件。 在将 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 文件部署到 SharePoint 并使清单文件更小且更有效的情况下，将合并类似元素，其中包含在合并异常之后的异常。

## <a name="modify-the-manifests"></a>修改清单
 在禁用功能或包设计器之前，不能直接修改打包的清单文件。 但是，您可以 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 通过功能和包设计器或编辑器将自定义元素手动添加到清单模板 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 。 有关详细信息，请参阅 [如何：自定义 Sharepoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md) 和 [如何：自定义 sharepoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

## <a name="feature-and-package-manifest-merge-process"></a>功能和包清单合并过程
 结合使用自定义元素和设计器提供的元素时， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用以下过程。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 检查每个元素是否具有唯一的键值。 如果元素没有唯一的键值，则会将其追加到打包的清单文件。 同样，具有多个键的元素也无法合并。 因此，它们将追加到清单文件中。

 如果元素具有唯一键，则 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将比较设计器和自定义键的值。 如果值匹配，它们将合并为单个值。 如果这些值不同，则会丢弃设计器键值，并使用自定义键值。 集合也将合并。 例如，如果设计器生成的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 和自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 都包含一个程序集集合，则打包的清单只包含一个程序集集合。

## <a name="merge-exceptions"></a>合并异常
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将大多数设计器 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素与类似的自定义元素组合在一起 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ，只要它们具有单个唯一的标识属性即可。 但是，某些元素缺少合并所需的唯一标识符 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 。 这些元素称为 *合并异常*。 在这些情况下，不 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素与设计器提供的元素合并在一起 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ，而是将它们追加到打包的清单文件中。

 下面是功能和包清单文件的合并异常列表 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 。

|Designer|XML 元素|
|--------------|-----------------|
|功能设计器|ActivationDependency|
|功能设计器|UpgradeAction|
|包设计器|SafeControl|
|包设计器|CodeAccessSecurity|

## <a name="feature-manifest-elements"></a>功能清单元素
 下表列出了可以合并的所有功能清单元素及其用于匹配的唯一键。

|元素名称|唯一键|
|------------------|----------------|
|功能 (所有属性) |*特性名称* (功能元素的每个特性名称都是唯一键。 ) |
|ElementFile|位置|
|ElementManifests/ElementManifest|位置|
|属性/属性|密钥|
|CustomUpgradeAction|名称|
|CustomUpgradeActionParameter|名称|

> [!NOTE]
> 由于修改 CustomUpgradeAction 元素的唯一方法是在自定义编辑器中进行 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ，因此不合并的效果很低。

## <a name="package-manifest-elements"></a>包清单元素
 下表列出了可以合并的所有包清单元素及其用于匹配的唯一键。

|元素名称|唯一键|
|------------------|----------------|
|解决方案 (所有属性) |*属性名称* (解决方案元素的每个属性名称都是唯一键。 ) |
|ApplicationResourceFiles/ApplicationResourceFile|位置|
|程序集/程序集|位置|
|ClassResources/ClassResource|位置|
|DwpFiles/DwpFile|位置|
|FeatureManifests/FeatureManifest|位置|
|资源/资源|位置|
|RootFiles/RootFile|位置|
|SiteDefinitionManifests/SiteDefinitionManifest|位置|
|WebTempFile|位置|
|与 templatefiles/TemplateFile|位置|
|SolutionDependency|SolutionID|

## <a name="manually-add-deployed-files"></a>手动添加已部署文件
 某些清单元素（例如 ApplicationResourceFile 和 DwpFiles）指定包含文件名的位置。 但是，将文件名条目添加到清单模板不会将基础文件添加到包中。 您必须将该文件添加到项目中，以将其包含在包中，并相应地设置其 "部署类型" 属性。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
