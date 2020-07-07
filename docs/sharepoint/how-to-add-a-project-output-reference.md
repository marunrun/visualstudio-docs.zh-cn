---
title: 如何：添加项目输出引用 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bea0f39ae161d8b695f872cb634c35d0cb205c91
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016747"
---
# <a name="how-to-add-a-project-output-reference"></a>如何：添加项目输出引用
  若要将非 SharePoint 项目程序集（或 Silverlight 项目中的 .xap 文件）部署到 SharePoint，请将其添加为项目输出引用。

 此过程将在两个项目之间创建一个解决方案生成依赖项。 与项目输出引用关联的项目在生成和部署 SharePoint 项目之前生成。

### <a name="to-add-a-project-output-reference"></a>添加项目输出引用

1. 加载包含至少一个 SharePoint 项目和一个非 SharePoint 项目的解决方案。

2. 在**解决方案资源管理器**中，选择 SharePoint 项目节点中的项。

3. 在 "**属性**" 窗口中，选择 "**项目输出引用**" 属性，然后选择它旁边的省略号（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮。

4. 在 "**项目输出引用**" 对话框中，选择 "**添加**" 按钮。

5. 在 "属性" 窗格中，选择 "**部署类型**" 属性旁边的箭头，然后为所引用的非 SharePoint 项选择适当的值，例如**ElementFile**。

6. 选择 "**项目名称**" 旁边的箭头，选择非 SharePoint 项目项的名称，然后选择 **"确定"** 按钮。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
