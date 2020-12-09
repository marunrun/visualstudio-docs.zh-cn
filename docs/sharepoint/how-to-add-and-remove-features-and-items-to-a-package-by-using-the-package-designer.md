---
title: 包设计器：添加 & 删除包的功能和项
titleSuffix: ''
description: 查看如何使用 Visual Studio 中的包设计器在 SharePoint 包中添加和移除功能和项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 45c8da30a059599a291b18155dc48c4521d6d875
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914941"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>如何：使用包设计器在包中添加和移除功能和项
  创建 SharePoint 解决方案时，Visual Studio 会将默认 SharePoint 功能添加到解决方案中的包。 在最终部署之前，您可以添加和删除 SharePoint 项目项和功能来修改 SharePoint 包。

 或者，可以使用 "打包资源管理器" 添加和删除 SharePoint 项目项。 你还可以查看和更改放置在包 ( .wsp) 中的 SharePoint 项目项和功能的层次结构。 有关详细信息，请参阅 [如何：使用打包资源管理器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

## <a name="add-features-to-a-sharepoint-package"></a>向 SharePoint 包添加功能
 您可以使用包设计器将功能添加到 SharePoint 包。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>用包设计器添加 SharePoint 功能

1. 打开 **包设计器**。

    有关详细信息，请参阅 [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 通过执行以下一个或多个步骤来添加一个或多个 SharePoint 功能：

   1. 双击解决方案列表中要添加的 **项** 中的每一项。

   2. 选择要添加的项目，然后选择 " **添加** " 按钮 ( # A0) 。

   3. 选择 " **全部添加** " 按钮 ( # A2) 一次添加所有项。

      例如，您可以双击 **解决方案列表项** 中的项以将其添加到 "包" 列表中的 **项** 。

      SharePoint 项目项和功能显示在包列表的 **项** 中。

## <a name="remove-features-from-a-sharepoint-package"></a>从 SharePoint 包删除功能
 您可以使用包设计器删除 SharePoint 包的功能。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>用包设计器删除 SharePoint 功能

1. 在 " **包中的项** " 列表中，选择要删除的项，然后选择 " **删除** ( # A0) " 按钮，或选择 " **全部删除** " 按钮 ( # A3) 删除所有项。

     SharePoint 项显示在解决方案列表中的 **项** 上。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：创建包](/previous-versions/ee231585(v=vs.110))