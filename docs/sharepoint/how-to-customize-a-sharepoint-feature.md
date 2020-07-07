---
title: 如何：自定义 SharePoint 功能 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a330f3c4cbe1e410ddc6a1612796c92eeda281b8
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016896"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>如何：自定义 SharePoint 功能
  您可以使用 Visual Studio 中的功能设计器来创建和自定义 SharePoint 功能。 例如，可以设置功能范围并将其他功能添加为依赖项。 默认情况下，当你在解决方案资源管理器或 SharePoint 包资源管理器中添加新功能时，将打开功能设计器。

## <a name="opening-the-feature-designer"></a>打开功能设计器
 可以使用功能设计器向功能中添加或删除 SharePoint 项目项。

#### <a name="to-open-the-feature-designer"></a>打开功能设计器

1. 在**解决方案资源管理器**中，展开 "**功能**"。

2. 双击 " *Feature1* " 项，或打开 " *Feature1* " 项的快捷菜单，然后选择 "**视图设计器**"。

## <a name="view-the-packaged-manifest-file"></a>查看打包的清单文件
 可以使用功能设计器来修改和生成功能的打包清单文件（*feature.xml*）。 然后，你可以在 Visual Studio 中查看此文件的 XML 代码。

#### <a name="to-view-the-packaged-manifest-file"></a>查看打包的清单文件

1. 在**功能设计器**中，选择 "**清单**" 选项卡。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>使用解决方案资源管理器查看打包的清单文件

1. 在**解决方案资源管理器**中，选择 "**显示所有文件**" 图标。

2. 展开 "功能"，展开 "功能名"，展开 "功能"，然后打开* \<FeatureName>.Template.xml*文件。

    > [!NOTE]
    > 当你打开功能模板清单 XML 文件时，将自动验证这些文件并忽略在 "错误列表" 窗口中显示的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 您可以在 Visual Studio XML 编辑器或 "清单模板" 窗格中更改功能清单文件的 XML 代码。 对 XML 代码所做的任何更改都将合并到该功能的打包清单文件中。 例如，你可能想要更改清单模板以自定义功能属性。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>使用 "XML 编辑器" 更改清单模板

1. 在**功能设计器**中，选择 **"清单**" 选项卡，展开 "**编辑选项**" 节点，然后选择 "**在 XML 编辑器中打开**" 链接。

     对 XML 所做的更改将合并到打包的清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>使用 "清单模板" 窗格更改清单模板

1. 在**功能设计器**中，选择 "**清单**" 选项卡，展开 "**编辑选项**" 节点，然后更改出现在 "清单模板" 窗格中的 XML。

     已打包的 "**打包清单**" 窗格的预览中将显示对 XML 所做的更改。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 您可以禁用功能设计器并手动创建*feature.xml*文件。 第一次执行此过程时，功能设计器中的当前设置将保存到功能模板 XML 文件中。 然后，您可以修改或覆盖 XML 代码。

> [!NOTE]
> 如果在禁用功能设计器的情况下添加或删除 XML 文件中的 SharePoint 项目项，则不会打包这些项目项。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>通过禁用设计器覆盖打包的清单文件

1. 在**功能设计器**中，选择 "**清单**" 选项卡。

2. 展开 "**编辑选项**" 节点，选择 "**覆盖生成的 XML 并在 xml 编辑器中编辑清单**" 链接，然后选择 "**是"** 按钮。

     模板将更新为当前打包的清单文件。

## <a name="enable-the-feature-designer"></a>启用功能设计器
 您可以重新启用功能设计器以自定义*feature.xml*文件。

#### <a name="to-re-enable-the-designer"></a>重新启用设计器

1. 在**功能设计器**中，选择 "**放弃清单编辑并重新启用设计器"** 链接，然后选择 "**是"** 按钮。

2. 模板会刷新为原始文本，对 XML 所做的任何更改都将丢失。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
