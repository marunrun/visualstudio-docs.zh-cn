---
title: 创建实体之间的关联 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Association_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ee767ded0687baa09653bd82785b68bee7fa0ebd
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981090"
---
# <a name="create-an-association-between-entities"></a>创建实体之间的关联
  您可以通过创建关联来定义业务数据连接（BDC）模型中的实体之间的关系。 Visual Studio 生成的方法为模型的使用者提供有关每个关联的信息。 SharePoint Web 部件、列表或自定义应用程序可以使用这些方法在用户界面 (UI) 中显示数据关系。

## <a name="create-an-association"></a>创建关联
 通过在 Visual Studio 的 **"工具箱**" 中选择 "**关联**" 控件，选择第一个实体（称为 "源" 实体），然后选择第二个实体（称为 "目标" 实体），创建关联。 您可以在 "**关联编辑器**" 中定义关联的详细信息。 有关详细信息，请参阅[如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)。

## <a name="association-methods"></a>关联方法
 SharePoint 业务数据 web 部件等应用程序通过调用实体的服务类中的方法来使用关联。 您可以通过在 "**关联编辑器**" 中选择来向实体的服务类添加方法。

 默认情况下，"**关联编辑器**" 向源实体和目标实体添加关联导航方法。 源实体中的关联导航方法使使用者能够检索目标实体的列表。 目标实体中的关联导航方法使使用者能够检索与目标实体相关的源实体。

 您必须将代码添加到这些方法中的每个方法才能返回相应的信息。 你还可以添加其他类型的方法来支持更高级的方案。 有关上述每种方法的详细信息，请参阅[支持的操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))。

## <a name="types-of-associations"></a>关联类型
 可以在 BDC 设计器中创建两种类型的关联：基于外键的关联和外部无键关联。

### <a name="foreign-key-based-association"></a>基于外键的关联
 可以通过将源实体中的标识符与目标实体中定义的类型描述符关联来创建基于外键的关联。 此关系使模型的使用者可以为其用户提供增强的 UI。 例如，在 Outlook 中允许用户创建可在下拉列表中显示客户的销售订单的窗体;或 SharePoint 中的销售订单列表，使用户能够打开客户的个人资料页。

 若要创建基于外键的关联，请关联共享同一名称和类型的标识符和类型描述符。 例如，可以在 `Contact` 实体与 `SalesOrder` 实体之间创建基于外键的关联。 `SalesOrder` 实体将 `ContactID` 类型说明符作为查找器的返回参数或特定查找器方法的一部分返回。 这两个类型说明符都显示在 "**关联编辑器**" 中。 若要在 `Contact` 实体和 `SalesOrder` 实体之间创建基于外键的关系，请选择其中每个字段旁边的 `ContactID` 标识符。

 将代码添加到源实体的关联导航器方法，该方法返回目标实体的集合。 下面的示例返回联系人的销售订单。

 [!code-csharp[SP_BDC#7](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#7)]
 [!code-vb[SP_BDC#7](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#7)]

 向返回源实体的目标实体的关联导航器方法添加代码。 下面的示例返回与销售订单相关的联系人。

 [!code-csharp[SP_BDC#8](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#8)]
 [!code-vb[SP_BDC#8](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#8)]

### <a name="foreign-keyless-association"></a>外无键关联
 你可以创建一个关联，而无需将标识符映射到字段类型描述符。 当源实体与目标实体没有直接关系时，创建这种关联。 例如，`SalesOrderDetail` 表没有映射到 `Contact` 表中的主键的外键。

 如果要在与 `Contact`相关的 `SalesOrderDetail` 表中显示信息，则可以在 `Contact` 实体和 `SalesOrderDetail` 实体之间创建外部无键关联。

 在 `Contact` 实体的关联导航方法中，通过联接表或通过调用存储过程来返回 `SalesOrderDetail` 实体。

 下面的示例通过联接表来返回所有销售订单的详细信息。

 [!code-csharp[SP_BDC#9](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#9)]
 [!code-vb[SP_BDC#9](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#9)]

 在 `SalesOrderDetail` 实体的关联导航方法中，返回相关的 `Contact`。 下面的示例演示这一操作。

 [!code-csharp[SP_BDC#10](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs#10)]
 [!code-vb[SP_BDC#10](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb#10)]

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)
