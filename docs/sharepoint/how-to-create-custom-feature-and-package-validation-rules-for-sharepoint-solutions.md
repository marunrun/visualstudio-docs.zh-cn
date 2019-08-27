---
title: SharePoint 解决方案：创建自定义功能，包验证规则
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
- SharePoint development in Visual Studio, validation rules
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a10118a0c83f9e17e32efd293a9a824e38a0942a
ms.sourcegitcommit: cc5fd59e5dc99181601b7db8b28d7f8a83a36bab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66835927"
---
# <a name="how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions"></a>如何：创建自定义功能和包验证规则为 SharePoint 解决方案
  可以创建自定义验证规则来验证由 Visual Studio 生成的解决方案包。 可以在整个功能或包上执行完全验证，通过选择**Validate**从包中的新功能的上下文菜单**PackagingExplorer**。 将新的 SharePoint 项目项或功能添加到项目，以确定包或功能将会处于有效状态时执行部分验证。

### <a name="to-create-a-custom-package-validation-rule"></a>若要创建自定义包验证规则

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建一个类实现以下接口之一：

    - 若要创建的包验证规则，实现<xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule>接口。

    - 若要创建功能验证规则，实现<xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule>接口。

4. 添加<xref:System.ComponentModel.Composition.ExportAttribute>到类。 此特性使 Visual Studio 能够发现和加载你的验证规则。 传递<xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule>或<xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule>特性构造函数的类型。

## <a name="example"></a>示例
 下面的代码示例演示如何创建自定义功能验证规则。

 [!code-vb[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb#1)]
 [!code-csharp[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint.

- System.ComponentModel.Composition.

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[在 Visual Studio 工具部署 SharePoint 扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
