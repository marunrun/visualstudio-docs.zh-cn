---
title: 如何：添加 Deleter 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], removing data
- BDC [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], removing data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c9d005ef8bade9f83027c216d875d24aad602449
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63418353"
---
# <a name="how-to-add-a-deleter-method"></a>如何：添加 Deleter 方法
  可以启用最终用户可以向模型添加 Deleter 方法从 SharePoint 站点上的外部列表中删除数据记录。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-deleter-method"></a>若要创建 Deleter 方法

1. 上**BDC 设计器**，选择实体。

2. 在菜单栏上依次选择**视图** > **其他 Windows** > **BDC 方法详细信息**。

    **BDC 方法详细信息**窗口随即打开。 有关此窗口的详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**添加一个方法**列表中，选择**创建 Deleter 方法**。

    Visual Studio 将以下元素添加到模型。 这些元素出现在**BDC 方法详细信息**窗口。

   - 一个名为方法**删除**。

   - 方法的输入的参数。

   - 参数类型描述符。

   - 方法实例的方法。

     有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 在中**解决方案资源管理器**，打开实体，已生成的服务代码文件的快捷菜单，然后选择**查看代码**。

    实体服务代码文件将在代码编辑器中打开。 有关实体服务代码文件的详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到要删除的记录的删除器方法。 下面的示例使用 AdventureWorks 示例数据库的 SQL Server 从销售订单删除行项。

   > [!NOTE]
   > 此示例中的方法使用两个输入的参数。

   > [!NOTE]
   > 值替换为`ServerName`字段与服务器的名称。

    [!code-csharp[SP_BDC#6](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs#6)]
    [!code-vb[SP_BDC#6](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb#6)]

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
