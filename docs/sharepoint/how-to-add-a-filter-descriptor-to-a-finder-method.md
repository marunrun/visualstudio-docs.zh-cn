---
title: 如何：向 Finder 方法添加筛选器描述符 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], filter descriptors
- Business Data Connectivity service [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], filter descriptors
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 228afb2f49f4d528fa9b806e9bf8d2531f7de901
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016737"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>如何：向 Finder 方法添加筛选器描述符
  筛选器描述符允许模型的使用者在执行之前将值传递给方法。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 常见的一种情况是，SharePoint 中的用户想要检索符合某些条件的外部内容类型的实例。 可以通过向 Finder 方法添加筛选器描述符来支持此方案。

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>向 Finder 方法添加筛选器描述符

1. 在 " **BDC 方法详细信息**" 窗口中，展开 Finder 方法的节点，展开 "**参数**" 节点，然后添加一个输入参数。 有关详细信息，请参阅[如何：向方法中添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)。

2. 在 "**方法详细信息**" 窗口中，选择参数的类型描述符。

3. 在菜单栏上，选择 "**查看**  >  **属性窗口**"。

4. 在 "**属性**" 窗口中，将 "**类型名称**" 属性设置为适用于筛选器的数据类型。

     例如，筛选器可以使用订单日期来限制该方法返回的销售订单数。 若要支持该筛选器，必须将类型描述符的**Type Name**属性**设置为 system.string。**

5. 在 "**方法详细信息**" 窗口中，展开 "**筛选器描述符**" 节点。

6. 在 "**添加筛选器描述符**" 列表中，选择 "**创建筛选器描述符**"。

     **筛选器描述符**节点下将显示一个新的筛选器描述符。

7. 在菜单栏上，选择 "**查看**  >  **属性窗口**"。

8. 在 "**属性**" 窗口中，选择 "**类型**" 属性。

9. 在显示的 "**类型**" 属性的列表中，选择所需的筛选模式。

     例如，若要创建一个使用订单日期来限制在 Finder 方法中返回的销售订单数的筛选器，请选择 "**比较**"。 比较筛选器可确保 finder 方法仅返回满足特定条件的实例。 有关每个筛选模式的详细信息，请参阅[BDC 支持的筛选器类型](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))。

10. 在 "**属性**" 窗口中，选择 "**关联的类型描述符**" 属性。

11. 在 "**关联的类型描述符**" 属性显示的列表中，选择之前在此过程中创建的类型描述符。 这会将筛选器与 Finder 方法的输入参数相关联。

12. 向返回数据的 Finder 方法添加代码。 您可以使用输入参数作为选择查询中的条件。

     下面的示例返回具有指定订单日期的销售订单。

    > [!NOTE]
    > 将字段的值替换 `ServerName` 为服务器的名称。

     [!code-csharp[SP_BDC#11](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#11)]
     [!code-vb[SP_BDC#11](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#11)]

## <a name="see-also"></a>另请参阅
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
