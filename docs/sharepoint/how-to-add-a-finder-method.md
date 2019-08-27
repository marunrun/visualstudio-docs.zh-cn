---
title: 如何：添加 Finder 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 49f494fa2c0fb35f7d2a65dc2ccb6b6d2d761cbe
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63428728"
---
# <a name="how-to-add-a-finder-method"></a>如何：添加 Finder 方法
  若要启用业务数据连接 (BDC) 服务，以显示 web 部件或列表中的实体的列表，必须创建*Finder*方法。 查找程序方法是一种特殊的方法返回的实体实例的集合。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-finder-method"></a>若要创建 Finder 方法

1. 上**BDC 设计器**，选择实体。

    有关详细信息，请参阅[如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上依次选择**视图** > **其他 Windows** > **BDC 方法详细信息**。

    **BDC 方法详细信息**窗口随即打开。 有关详细信息**BDC 方法详细信息**窗口中，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**添加一个方法**列表中，选择**创建 Finder 方法**。

    Visual Studio 将添加一个方法，返回参数和类型描述符。

4. 将类型描述符配置为实体集合类型描述符。 有关如何创建实体集合类型描述符的详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 无需执行此步骤中，如果特定的 Finder 方法添加到实体。 Visual Studio 将使用特定的 Finder 方法中定义的类型描述符。

5. 在中**解决方案资源管理器**，打开实体，已生成的服务代码文件的快捷菜单，然后选择**查看代码**。 有关服务代码文件的详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

6. 将代码添加到 Finder 方法。 这段代码执行下列任务：

   - 从数据源检索数据。

   - 向 BDC 服务返回实体的列表。

     下面的示例返回一系列`Contact`通过用于 SQL Server 的 AdventureWorks 示例数据库中的数据的实体。

   > [!NOTE]
   > 值替换为`ServerName`字段与服务器的名称。

    [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
    [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="see-also"></a>请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
