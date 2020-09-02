---
title: 如何：自定义 SharePoint 解决方案包 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 77b66160d489f711b5588fdcdd024d13769d734f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016873"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>如何：自定义 SharePoint 解决方案包
  您可以使用包设计器来创建和自定义包 (*.wsp*) 。 例如，你可以添加 SharePoint 项目项和功能，指定是否在部署解决方案时重置 Web 服务器，并设置部署服务器类型。

## <a name="open-the-package-designer"></a>打开包设计器

#### <a name="to-open-the-package-designer"></a>打开包设计器

- 在**解决方案资源管理器**中，双击 "**包**"，或在 "**包**" 的快捷菜单上选择 "**查看设计器**"。

## <a name="view-the-packaged-manifestffile"></a>查看打包的 manifestfFile
 你可以使用包设计器来修改和生成打包的清单文件。 然后，你可以在 Visual Studio 中查看此文件的 XML 代码。

#### <a name="to-view-the-xml-source-file"></a>查看 XML 源文件

1. 在 **包设计器**中，选择 " **清单**"。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>使用解决方案资源管理器查看打包的清单文件

1. 在“解决方案资源管理器”中，选择“显示所有文件”********。

2. 展开 "包"，展开 "包"，然后打开 *Package.Template.xml* 文件。

    > [!NOTE]
    > 当你打开包模板的清单 XML 文件时，将自动验证这些文件，你可以忽略出现在 "错误列表" 窗口中的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 您可以在 Visual Studio XML 编辑器或 "清单模板" 窗格中更改打包清单文件的 XML 代码。 对 XML 代码所做的任何更改都将合并到包的打包清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>使用 "XML 编辑器" 更改清单模板

1. 在 **包设计器**中，选择 **"清单** " 选项卡，展开 " **编辑选项** " 节点，然后选择 " **在 XML 编辑器中打开** " 链接。

     对 XML 所做的更改将合并到打包的清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>使用 "清单模板" 窗格更改清单模板

1. 在 **包设计器**中，选择 " **清单** " 选项卡，展开 " **编辑选项** " 节点，然后更改出现在 "清单模板" 窗格中的 XML。

     已打包的 " **打包清单** " 窗格的预览中将显示对 XML 所做的更改。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 您可以禁用包设计器并手动创建 *manifest.xml* 文件。 第一次执行此过程时，包设计器中的当前设置将保存到包模板 XML 文件中。 然后，您可以修改或覆盖 XML 代码。

> [!NOTE]
> 如果在禁用包设计器的同时添加或删除 XML 文件中的 SharePoint 项目项和功能，则不会打包这些项目项和功能。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>通过禁用设计器覆盖打包的清单文件

1. 在 **包设计器**中，选择 " **清单** " 选项卡。

2. 展开 " **编辑选项** " 节点，选择 " **覆盖生成的 XML 并在 xml 编辑器中编辑清单** " 链接，然后选择 " **是"** 按钮。

     模板将更新为当前打包的清单文件。

## <a name="enable-the-package-designer"></a>启用包设计器
 您可以重新启用包设计器以自定义 *manifest.xml* 文件。

#### <a name="to-re-enable-the-designer"></a>重新启用设计器

1. 在 **包设计器**中，选择 " **放弃清单编辑并重新启用设计器"** 链接，然后选择 " **是"** 按钮。

     模板会刷新为原始文本，对 XML 所做的任何更改都将丢失。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
