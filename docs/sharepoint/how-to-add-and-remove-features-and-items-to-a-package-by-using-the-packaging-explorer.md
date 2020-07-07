---
title: 打包资源管理器：添加 & 删除 & 项到包的功能
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackagingExplorer
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
ms.openlocfilehash: c3ea7e30737855cbbb9434e8763f4903d80b82da
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014553"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>如何：使用打包资源管理器在包中添加和移除功能和项
  若要将包配置为部署 SharePoint 项和功能，可以使用 "打包资源管理器"。 可以在 .wsp 文件中调整 SharePoint 项目项和功能。

 或者，您可以使用打包设计器来查看和重新排列功能，以更改激活顺序。 有关详细信息，请参阅[如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

## <a name="open-the-packaging-explorer"></a>打开 "打包资源管理器"
 如果你的 Visual Studio 解决方案至少具有一个 SharePoint 项目，则可以使用以下过程打开 "打包资源管理器"。 或者，当你查看功能或包设计器时，将自动打开 "打包资源管理器"。 关闭所有功能和包设计器后，"打包资源管理器" 也会关闭。

#### <a name="to-open-the-packaging-explorer"></a>打开 "打包资源管理器"

1. 在菜单栏上，选择 "**查看**  >  **其他 Windows**  >  **打包资源管理器**"。

     "**打包资源管理器**" 将出现在**工具箱**中。

## <a name="adding-a-feature-to-a-package"></a>向包中添加功能
 您可以使用 "打包资源管理器" 将新功能和现有功能添加到包。

#### <a name="to-add-a-sharepoint-feature"></a>添加 SharePoint 功能

1. 打开 "**打包资源管理器**"，打开项目的快捷菜单，然后选择 "**添加功能**"。

#### <a name="to-move-an-existing-sharepoint-feature"></a>移动现有 SharePoint 功能

1. 打开 "**打包资源管理器**"，然后执行以下步骤之一：

    - 将一个**功能**从一个项目拖动到另一个项目。

    - 打开某个功能的快捷菜单，选择 "**剪切**"，打开要将该功能移动到的项目的快捷菜单，然后选择 "**粘贴**"。

    > [!NOTE]
    > 如果解决方案中包含多个 SharePoint 项目，请使用此过程。

## <a name="validate-a-feature-or-package"></a>验证功能或包
 您可以通过验证文件来识别 SharePoint 功能和包中的潜在问题。 警告和错误将显示在 "输出" 窗口和 "错误列表" 窗口中。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>验证 SharePoint 功能或包

1. 打开 "**打包资源管理器**"。

2. 打开功能或包的快捷菜单，然后选择 "**验证**"。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
