---
title: 包设计器：添加和删除功能和包项
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerDesign
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
ms.openlocfilehash: fbd44bbf3b337815c8c72cea66dd4d56fc645ade
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401611"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>如何：添加和删除使用包设计器的功能和包项
  创建 SharePoint 解决方案时，Visual Studio 会将默认的 SharePoint 功能添加到解决方案中的包。 然后才能最终部署，可以添加和删除 SharePoint 项目项和修改 SharePoint 包的功能。

 或者，可以使用打包资源管理器添加和删除 SharePoint 项目项。 您还可以查看和更改层次结构的 SharePoint 项目项和放入包 (.wsp) 的功能。 有关详细信息，请参阅[如何：添加和删除使用打包资源管理器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

## <a name="add-features-to-a-sharepoint-package"></a>将功能添加到 SharePoint 包
 在包设计器可用于将功能添加到 SharePoint 包。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>若要使用包设计器添加 SharePoint 功能

1. 打开**包设计器**。

    有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 通过执行一个或多个以下步骤添加一个或多个 SharePoint 功能：

   1. 双击中的每一项**解决方案中的项**你想要添加的列表。

   2. 选择你想要添加，，然后选择的项**添加**按钮 (>)。

   3. 选择**全部添加**按钮 (>>) 若要同时添加所有项。

      例如，你可以双击中的项**解决方案中的项**列表，以将其添加到**包中的项**列表。

      在显示的 SharePoint 项目项和功能**包中的项**列表。

## <a name="remove-features-from-a-sharepoint-package"></a>从 SharePoint 包中删除功能
 在包设计器可用于向 SharePoint 包删除功能。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>若要使用包设计器删除 SharePoint 功能

1. 在中**包中的项**列表中，选择你想要删除，然后选择的项**删除**(<) 按钮，或选择**全部删除**按钮 (<<) 若要删除所有项。

     SharePoint 项出现在**解决方案中的项**列表。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：创建包](https://msdn.microsoft.com/b24be45c-e91d-49bb-afb0-7b265404214b)
