---
title: 打包资源管理器：添加和删除功能和包的项
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 0f01ecb67cb82ffe325ea471ad5fb5913c8e4d28
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401564"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>如何：添加和删除功能和包项使用打包资源管理器
  若要配置要部署的 SharePoint 项和功能的程序包，可以使用打包资源管理器。 .Wsp 文件中，可以调整的 SharePoint 项目项和功能。

 或者，可以使用打包设计器来查看和重新排列要更改的激活顺序的功能。 有关详细信息，请参阅[如何：添加和删除使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

## <a name="open-the-packaging-explorer"></a>打开打包资源管理器
 您可以使用以下过程打开打包资源管理器，如果你的 Visual Studio 解决方案包含至少一个 SharePoint 项目。 或者，打包资源管理器将自动打开功能或包设计器中查看时。 关闭所有的功能和包设计器后，打包资源管理器也会关闭。

#### <a name="to-open-the-packaging-explorer"></a>若要打开打包资源管理器

1. 在菜单栏上依次选择**视图** > **其他 Windows** > **打包资源管理器**。

     **打包资源管理器**将出现在**工具箱**。

## <a name="adding-a-feature-to-a-package"></a>向包中添加一项功能
 通过使用打包资源管理器，可以向包添加新的和现有功能。

#### <a name="to-add-a-sharepoint-feature"></a>若要添加的 SharePoint 功能

1. 打开**打包资源管理器**，打开项目的快捷菜单，然后选择**添加功能**。

#### <a name="to-move-an-existing-sharepoint-feature"></a>若要将现有的 SharePoint 功能

1. 打开**打包资源管理器**，然后执行以下步骤之一：

    - 拖动**功能**从一个项目到另一个项目。

    - 对于每项功能打开快捷菜单，选择**剪切**，打开你想要移动功能，然后选择该项目的快捷菜单**粘贴**。

    > [!NOTE]
    > 如果解决方案中包含多个 SharePoint 项目，请使用此过程。

## <a name="validate-a-feature-or-package"></a>验证功能或包
 可以通过验证文件中标识的 SharePoint 功能和包中的潜在问题。 在输出窗口和错误列表窗口中显示警告和错误。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>若要验证的 SharePoint 功能或包

1. 打开**打包资源管理器**。

2. 功能或包中，打开快捷菜单，然后选择**验证**。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
