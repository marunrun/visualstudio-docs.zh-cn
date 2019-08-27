---
title: 合并功能和包中的 XML 清单 |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63429288"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>在功能和包清单中合并 XML
  通过定义功能和包[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]清单文件。 这些打包的清单是从设计器和自定义生成的数据组合[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]清单模板中输入的用户。 在打包时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]合并自定义[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]语句与设计器提供[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]形成打包[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]清单文件。 类似的元素合并异常更高版本中所示的异常进行合并，以避免[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]验证错误后将文件部署到 SharePoint，并使清单文件较小、 更高效。

## <a name="modify-the-manifests"></a>修改清单
 不能直接修改打包的清单文件，直到你禁用的功能或包设计器。 但是，您可以手动添加自定义[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]元素与清单模板通过功能和包设计器或[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]编辑器。 有关详细信息，请参阅[如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)和[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

## <a name="feature-and-package-manifest-merge-process"></a>功能和包清单合并进程
 合并提供设计器的元素，以及自定义元素时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将使用下列过程。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 检查每个元素是否具有唯一的键值。 如果元素没有唯一的键值，则会将其追加到打包的清单文件。 同样，具有多个键的元素也无法合并。 因此，它们被追加到清单文件。

 如果元素具有一个唯一密钥，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将设计器和自定义密钥的值进行比较。 如果值匹配，它们合并到单个值。 如果值不同，设计器的密钥值将被丢弃，而使用自定义密钥值。 集合也将合并。 例如，如果设计器生成[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]和自定义[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]同时包含程序集集合，打包的清单包含只有一个程序集集合。

## <a name="merge-exceptions"></a>合并异常
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 合并大多数设计器[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]以及类似的自定义元素[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]元素，只要它们具有唯一的标识属性。 但是，某些元素缺少所需的唯一标识符[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]合并。 这些元素称为*合并异常*。 在这些情况下，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]不会合并自定义[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]元素与设计器提供[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]元素，但改为将它们追加到打包的清单文件。

 下面是一系列功能和包的合并异常[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]清单文件。

|Designer|XML 元素|
|--------------|-----------------|
|功能设计器|ActivationDependency|
|功能设计器|UpgradeAction|
|包设计器|SafeControl|
|包设计器|CodeAccessSecurity|

## <a name="feature-manifest-elements"></a>功能清单元素
 下表是可以合并的所有功能清单元素和用于匹配其唯一键的列表。

|元素名称|唯一键|
|------------------|----------------|
|功能 （所有属性）|*属性名称*（功能元素的每个特性名称是唯一键。）|
|ElementFile|位置|
|ElementManifests/ElementManifest|位置|
|属性/属性|键|
|CustomUpgradeAction|名称|
|CustomUpgradeActionParameter|名称|

> [!NOTE]
> 因为修改 CustomUpgradeAction 元素的唯一方法是在自定义[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]编辑器中，未合并的效果较低。

## <a name="package-manifest-elements"></a>包清单元素
 下表是可以合并的所有包清单元素和用于匹配其唯一键的列表。

|元素名称|唯一键|
|------------------|----------------|
|解决方案 （所有属性）|*属性名称*（解决方案元素的每个特性名称是唯一键。）|
|ApplicationResourceFiles/ApplicationResourceFile|位置|
|程序集/程序集|位置|
|ClassResources/ClassResource|位置|
|DwpFiles/DwpFile|位置|
|FeatureManifests/FeatureManifest|位置|
|资源/资源|位置|
|RootFiles/RootFile|位置|
|SiteDefinitionManifests/SiteDefinitionManifest|位置|
|WebTempFile|位置|
|TemplateFiles/TemplateFile|位置|
|SolutionDependency|SolutionID|

## <a name="manually-add-deployed-files"></a>手动添加部署的文件
 一些清单元素，如 ApplicationResourceFile 和 DwpFiles，指定包含文件名的位置。 但是，将文件名称条目添加到清单模板不添加基础文件到包。 必须将文件添加到项目，以将其包括在包中并相应地设置其部署类型属性。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
