---
title: 如何：添加 Finder 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 1fa8f8eb34943cc17bc6cabca8e93ea7569a7ba6
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016724"
---
# <a name="how-to-add-a-finder-method"></a>如何：添加 Finder 方法
  若要使业务数据连接（BDC）服务能够显示 web 部件或列表中实体的列表，则必须创建*Finder*方法。 Finder 方法是一种特殊方法，它返回实体实例的集合。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-finder-method"></a>创建 Finder 方法

1. 在**BDC 设计器**中选择一个实体。

    有关详细信息，请参阅[如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上，选择 "**查看**  >  **其他 Windows**  >  **BDC 方法详细信息**"。

    此时将打开 " **BDC 方法详细信息**" 窗口。 有关 " **Bdc 方法详细**信息" 窗口的详细信息，请参阅[bdc 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 "**添加方法**" 列表中，选择 "**创建 Finder 方法**"。

    Visual Studio 将添加方法、返回参数和类型描述符。

4. 将类型描述符配置为实体集合类型描述符。 有关如何创建实体集合类型描述符的详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 如果已将特定的 Finder 方法添加到实体，则无需执行此步骤。 Visual Studio 使用您在特定 Finder 方法中定义的类型描述符。

5. 在**解决方案资源管理器**中，打开为实体生成的服务代码文件的快捷菜单，然后选择 "**查看代码**"。 有关服务代码文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

6. 向 Finder 方法添加代码。 此代码执行以下任务：

   - 从数据源中检索数据。

   - 返回 BDC 服务的实体列表。

     下面的示例 `Contact` 通过使用 SQL Server 的 AdventureWorks 示例数据库中的数据，返回实体的集合。

   > [!NOTE]
   > 将字段的值替换 `ServerName` 为服务器的名称。

    [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
    [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
