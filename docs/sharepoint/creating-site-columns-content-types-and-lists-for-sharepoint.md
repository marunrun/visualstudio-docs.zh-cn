---
title: 为 SharePoint 创建站点栏、 内容类型和列表 |Microsoft Docs
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
ms.openlocfilehash: 8cecb3e78cea90b927dc6b67b5b4a2cb50bfa87c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62581091"
---
# <a name="create-site-columns-content-types-and-lists-for-sharepoint"></a>为 SharePoint 创建站点栏、 内容类型和列表
  Visual Studio 为许多不同基本 SharePoint 项，包括提供项目项模板*列出了*并*内容类型*，这两种可结合网站栏 (或*字段*)。 用于内容类型和列表的新设计器可更简单地创建这些项。

## <a name="site-columns"></a>网站栏
 网站栏是您可以向 SharePoint 项目添加的一种最基本元素。 网站栏表示数据的类型，例如联系人列表中某一联系人的电话号码、注释或者所在城市的名称。

 新网站栏项目项模板使创建网站栏比使用 Visual Studio 的早期版本更容易。 创建一个新的站点列之后, 您可以修改网站栏中的 XML *Elements.xml*文件以包含所需信息，例如其显示名称、 其数据类型和想要站点列中显示的组SharePoint。 有关站点列的详细信息，请参阅[简介列](http://go.microsoft.com/fwlink/?LinkId=224996)。

## <a name="content-types-and-lists"></a>内容类型和列表
 内容类型和列表是 SharePoint 中常用的元素。

 内容类型定义 SharePoint 列表或文档库中的元数据、工作流和项类别的行为。 例如，可以为联系人列表或任务列表中的信息创建内容类型。 联系人内容类型可以包含多个栏，例如“姓名”、“电子邮件”、“电话号码”和“地址”。 您定义的站点级别的内容类型独立于站点中的任何列表或文档库。 在 SharePoint 网站上，您可以对不同列表或文档库使用同一内容类型。 您还可以对同一列表或文档库使用多个内容类型。

 列表是 SharePoint 中可与其他人共享的信息的集合。 列表由多行包含数据的栏组成。 列表的一些示例包括：任务列表、联系人列表和公告列表。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的新内容类型和列表设计器使创建站点内容类型和列表比使用 Visual Studio 的早期版本更容易、更直观。 UI 允许您以熟悉的方式可视化构造内容类型和列表，并能够排序和分组列表中的数据以及使用组标题。 有关内容类型的详细信息，请参阅[内容类型](http://go.microsoft.com/fwlink/?LinkId=224997)。 有关列表的详细信息，请参阅[的列表窗体](http://go.microsoft.com/fwlink/?LinkId=224998)并[列表视图](http://go.microsoft.com/fwlink/?LinkId=224999)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|演示如何创建网站栏以用于自定义内容类型。 此内容类型随后将用于自定义列表。|

## <a name="see-also"></a>请参阅
- [SharePoint 2010 开发入门](http://go.microsoft.com/fwlink/?LinkId=225000)
