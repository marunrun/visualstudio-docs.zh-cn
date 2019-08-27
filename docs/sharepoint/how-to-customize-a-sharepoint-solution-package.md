---
title: 如何：自定义 SharePoint 解决方案包 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0aa124d25e279b7e44292645d81d80829f5d3f8f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63420200"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>如何：自定义 SharePoint 解决方案包
  在包设计器可用于创建和自定义包 (*.wsp*)。 例如，可以添加 SharePoint 项目项和功能，指定是否 Web 服务器是重置时部署解决方案，并设置部署服务器类型。

## <a name="open-the-package-designer"></a>打开包设计器

#### <a name="to-open-the-package-designer"></a>若要打开包设计器

- 在中**解决方案资源管理器**，双击**包**，或选择**视图设计器**上的快捷菜单**包**。

## <a name="view-the-packaged-manifestffile"></a>查看打包的 manifestfFile
 在包设计器可用于修改并生成打包的清单文件。 然后，您可以在 Visual Studio 中查看此文件的 XML 代码。

#### <a name="to-view-the-xml-source-file"></a>若要查看 XML 源文件

1. 在中**包设计器**，选择**清单**。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>若要使用解决方案资源管理器查看打包的清单文件

1. 在“解决方案资源管理器”中，选择“显示所有文件”。

2. 展开包中，展开 Package.package，，然后打开*Package.Template.xml*文件。

    > [!NOTE]
    > 当打开包模板的清单 XML 文件时，将自动验证这些文件，并可以忽略在错误列表窗口中显示的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 你可以在 Visual Studio XML 编辑器或清单模板窗格中打包的清单文件的 XML 代码。 对 XML 代码的任何更改将合并到包打包的清单文件。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>若要使用 XML 编辑器更改清单模板

1. 在中**包设计器**，选择**清单**选项卡上，展开**编辑选项**节点，然后选择**XML 编辑器中打开**链接。

     对 XML 的更改将合并到打包的清单文件。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>若要使用清单模板窗格中更改清单模板

1. 在中**包设计器**，选择**清单**选项卡上，展开**编辑选项**节点，然后再更改的清单模板窗格中显示的 XML。

     对 XML 的更改显示在**预览打包的清单**窗格。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 可以禁用包设计器，并创建*manifest.xml*手动文件。 第一次执行此过程中，在包设计器中的当前设置保存到包模板 XML 文件。 然后，可以修改或覆盖的 XML 代码。

> [!NOTE]
> 如果添加或禁用包设计器时，删除在 XML 文件中的 SharePoint 项目项和功能，不会打包到这些项目项和功能。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>若要通过禁用设计器覆盖打包的清单文件

1. 在中**包设计器**，选择**清单**选项卡。

2. 展开**编辑选项**节点，选择**在 XML 编辑器中的覆盖生成的 XML 和编辑清单**链接，，然后选择**是**按钮。

     该模板将更新为当前打包的清单文件。

## <a name="enable-the-package-designer"></a>启用包设计器
 你可以在包设计器自定义*manifest.xml*文件。

#### <a name="to-re-enable-the-designer"></a>若要重新启用设计器

1. 在中**包设计器**，选择**放弃清单编辑和重新启用设计器**链接，，然后选择**是**按钮。

     模板刷新并显示原始文本和 XML 的任何更改都将丢失。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
