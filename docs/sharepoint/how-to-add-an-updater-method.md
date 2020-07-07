---
title: 如何：添加更新程序方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], updating data
- BDC [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating data
- Business Data Connectivity service [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating entity instances
- BDC [SharePoint development in Visual Studio], updating entity instances
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c76373c710908a8ae7edc49c4e26ff7e94336a6d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014981"
---
# <a name="how-to-add-an-updater-method"></a>如何：添加更新程序方法
  您可以通过创建一种*更新方法，* 使用户能够更新 SharePoint 外部列表中的业务数据。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-an-updater-method"></a>创建更新方法

1. 在 BDC 设计器中选择一个实体。

2. 在菜单栏上，选择 "**查看**  >  **其他 Windows**  >  **BDC 方法详细信息**"。

    “BDC 方法详细信息”窗口将打开。 有关此窗口的详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 "**添加方法**" 列表中，选择 "**创建更新方法**"。

    Visual Studio 将以下元素添加到模型中。 这些元素出现在 "BDC 方法详细信息" 窗口中。

   - 名为**Update**的方法。

   - 方法的输入参数。

   - 参数的类型描述符。 默认情况下，Visual Studio 使用为 Finder 方法（例如： Contact）定义的实体类型描述符。

   - 方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

   > [!NOTE]
   > 如果实体类型的标识符表示数据库表中的字段（该字段不是自动生成的），请将 "**预生成更新字段**" 属性设置为 " **True**"。

4. 在**解决方案资源管理器**中，打开为实体生成的服务代码文件的快捷菜单，然后选择 "**查看代码**"。

    实体服务代码文件将在**代码编辑器**中打开。 有关该文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到更新方法来更新数据。 下面的示例更新 AdventureWorks 示例数据库中的联系人信息，以便 SQL Server。

   > [!NOTE]
   > 将字段的值替换 `ServerName` 为服务器的名称。

    [!code-csharp[SP_BDC#5](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#5)]
    [!code-vb[SP_BDC#5](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#5)]

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
