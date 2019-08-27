---
title: 如何：添加项目输出引用 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 2ae3965647416d7a8e11cf0ea5e24cef1e54a09b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967248"
---
# <a name="how-to-add-a-project-output-reference"></a>如何：添加项目输出引用
  若要部署到 SharePoint 的非 SharePoint 项目程序集 （或在 Silverlight 项目中的.xap 文件），将其添加为项目输出引用。

 此过程将创建两个项目之间解决方案生成依赖项。 构建和部署 SharePoint 项目之前生成项目输出引用与关联的项目。

### <a name="to-add-a-project-output-reference"></a>若要添加项目输出引用

1. 加载包含至少一个 SharePoint 项目和一个非 SharePoint 项目的解决方案。

2. 在中**解决方案资源管理器**，选择 SharePoint 项目节点中的项。

3. 在中**属性**窗口中，选择**项目输出引用**属性，然后选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP。NET 移动设计器椭圆")) 旁边的按钮。

4. 在中**项目输出引用**对话框框中，选择**添加**按钮。

5. 在属性窗格中，选择箭头旁边**部署类型**属性，然后选择适当的值所引用，如非 SharePoint 项**ElementFile**。

6. 选择箭头旁边**项目名称**，选择非 SharePoint 项目项的名称，然后选择**确定**按钮。

## <a name="see-also"></a>请参阅
- [提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
