---
title: 创建 SharePoint 的网站栏、内容类型和列表 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.ContentTypeSetting
- VS.SharePointTools.ContentTypeDesigner.CommonPropertiesPage
- VS.SharePointTools.ListDesigner.CreatingLists
- VS.SharePointTools.ListDesigner.ListPage
- VS.SharePointTools.ListDesigner.ViewPage
- VS.SharePointTools.ListDesigner.CommonPropertiesPage
- VS.SharePointTools.ContentTypeDesigner.ColumnsPage
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 538d82794fcecb91e4f13ab6d7718d0bf407b86f
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984515"
---
# <a name="create-site-columns-content-types-and-lists-for-sharepoint"></a>创建 SharePoint 的网站栏、内容类型和列表
  Visual Studio 为许多不同的基本 SharePoint 项（包括*列表*和*内容类型*）提供项目项模板，这两者都可以包含网站列（或*字段*）。 用于内容类型和列表的新设计器可更简单地创建这些项。

## <a name="site-columns"></a>网站栏
 网站栏是您可以向 SharePoint 项目添加的一种最基本元素。 网站栏表示数据的类型，例如联系人列表中某一联系人的电话号码、注释或者所在城市的名称。

 新网站栏项目项模板使创建网站栏比使用 Visual Studio 的早期版本更容易。 创建新的网站列后，您可以修改网站列的 "*元素 .xml* " 文件中的 xml，以包含所需的信息，例如其显示名称、数据类型以及您希望网站列出现在 SharePoint 中的组。 有关站点列的详细信息，请参阅[列简介](/previous-versions/office/developer/sharepoint-2010/ms450825(v=office.14))。

## <a name="content-types-and-lists"></a>内容类型和列表
 内容类型和列表是 SharePoint 中常用的元素。

 内容类型定义 SharePoint 列表或文档库中的元数据、工作流和项类别的行为。 例如，可以为联系人列表或任务列表中的信息创建内容类型。 联系人内容类型可以包含多个栏，例如“姓名”、“电子邮件”、“电话号码”和“地址”。 您定义的站点级别的内容类型独立于站点中的任何列表或文档库。 在 SharePoint 网站上，您可以对不同列表或文档库使用同一内容类型。 您还可以对同一列表或文档库使用多个内容类型。

 列表是 SharePoint 中可与其他人共享的信息的集合。 列表由多行包含数据的栏组成。 列表的一些示例包括：任务列表、联系人列表和公告列表。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的新内容类型和列表设计器使创建站点内容类型和列表比使用 Visual Studio 的早期版本更容易、更直观。 UI 允许您以熟悉的方式可视化构造内容类型和列表，并能够排序和分组列表中的数据以及使用组标题。 有关内容类型的详细信息，请参阅[内容类型](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))。 有关列表的详细信息，请参阅[列出窗体](/previous-versions/office/developer/sharepoint-2010/aa543232(v=office.14))和[列表视图](/previous-versions/office/developer/sharepoint-2010/ff604021(v=office.14))。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[演练：为 SharePoint 创建网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|演示如何创建网站栏以用于自定义内容类型。 此内容类型随后将用于自定义列表。|

## <a name="see-also"></a>请参阅
- [在 SharePoint 2010 上开始开发](/sharepoint/dev/)
