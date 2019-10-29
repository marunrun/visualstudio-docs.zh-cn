---
title: 如何：创建实体之间的关联 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- AssociationGroupTool
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
ms.openlocfilehash: cba9d712e2bcfa90ae37d47e3c518697f10b6add
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981836"
---
# <a name="how-to-create-an-association-between-entities"></a>如何：创建实体之间的关联
  您可以通过创建关联来定义业务数据连接（BDC）模型中的实体之间的关系。 Visual Studio 生成的方法为模型的使用者提供有关每个关联的信息。 SharePoint Web 部件、列表或自定义应用程序可以使用这些方法在用户界面 (UI) 中显示数据关系。

 可以在 BDC 设计器中创建两种类型的关联：基于外键的关联和外部无键关联。 有关详细信息，请参阅[创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)。

### <a name="to-create-an-association-between-entities"></a>创建实体之间的关联

1. 在 "**工具箱**" 的 " **BusinessDataConnectivity** " 选项卡上，选择 "**关联**" 项。

2. 在 BDC 设计器中，选择源实体，然后选择目标实体。

     此时将显示 "**关联编辑器**"。

3. 如果要创建基于外键的关联，请选中 "**为外键关联**" 复选框。

    1. 在 "**标识符映射**" 表的 "**源 ID** " 列中，选择出现在 "**字段**" 列中的每个匹配类型描述符旁边的标识符。

         例如，在 "**源 ID** " 列中，选择 `ReadList.salesOrderList.SalesOrderList.SalesOrder.ContactID` 类型描述符和 `ReadItem.salesOrder.SalesOrder.ContactID` 类型描述符旁 `ContactID`。

4. 如果要创建外部无键关联，请清除 "**为外键关联**" 复选框。

5. 选择 **“确定”** 按钮。

6. 在 BDC 设计器中，表示关联的行出现在源实体和目标实体之间。

     Visual Studio 将关联导航器方法添加到目标实体的服务类和源实体的服务类。 有关关联导航方法的详细信息，请参阅[支持的操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))。

7. 在源实体的关联导航器方法中，添加返回目标实体集合的代码。

8. 在目标实体的关联导航器方法中，添加返回相关源实体的代码。

     有关关联导航器方法的示例，请参阅[创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)。

## <a name="see-also"></a>请参阅
- [创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [演练：使用业务数据在 SharePoint 中创建外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
