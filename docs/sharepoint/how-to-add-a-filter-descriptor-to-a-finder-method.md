---
title: 如何：将筛选器描述符添加到 Finder 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: fceb6270aea9da5af1a53adf7560df7dd3702349
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63418313"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>如何：将筛选器描述符添加到 Finder 方法
  筛选器描述符，它们执行之前将值传递给方法的模型的使用者。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 一种常见方案是在 SharePoint 中的用户想要检索的外部内容类型与某个条件匹配的实例。 可以通过将筛选器描述符添加到 Finder 方法来支持此方案。

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>若要将筛选器描述符添加到 Finder 方法

1. 在中**BDC 方法详细信息**窗口中，展开的 Finder 方法节点，展开**参数**节点，然后添加一个输入的参数。 有关详细信息，请参阅[如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)。

2. 在中**方法的详细信息**窗口中，选择该参数的类型描述符。

3. 在菜单栏上依次选择**视图** > **属性窗口**。

4. 在中**属性**窗口中，将**类型名称**属性设置为适当的筛选器的数据类型。

     例如，筛选器可能使用订单日期来限制由方法返回的销售订单数。 若要支持该筛选器**类型名称**类型描述符的属性必须设置为**System.DateTime**。

5. 在中**方法的详细信息**窗口中，展开**筛选器描述符**节点。

6. 在中**添加筛选器描述符**列表中，选择**创建筛选器描述符**。

     新的筛选器描述符显示下方**筛选器描述符**节点。

7. 在菜单栏上依次选择**视图** > **属性窗口**。

8. 在中**属性**窗口中，选择**类型**属性。

9. 在列表中为显示**类型**属性中，选择所需的筛选模式。

     例如，若要创建的筛选器，使用订单日期限制的 Finder 方法中返回的销售订单数，请选择**比较**。 比较筛选器可确保 finder 方法返回满足特定条件的实例。 有关每种筛选模式的详细信息，请参阅[类型的筛选器受 BDC](http://go.microsoft.com/fwlink/?LinkId=169287)。

10. 在中**属性**窗口中，选择**关联的类型描述符**属性。

11. 在列表中为显示**关联的类型描述符**属性中，选择您在此过程前面创建的类型描述符。 这与筛选器相关的 Finder 方法的输入参数。

12. 将代码添加到返回数据的 Finder 方法。 为 select 查询中的条件，可以使用输入的参数。

     以下示例返回具有指定的订单日期的销售订单。

    > [!NOTE]
    > 值替换为`ServerName`字段与服务器的名称。

     [!code-csharp[SP_BDC#11](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#11)]
     [!code-vb[SP_BDC#11](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#11)]

## <a name="see-also"></a>请参阅
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
