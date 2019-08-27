---
title: 如何：添加 Updater 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 8204b13aa0405d01590e4aeb0fe43a92b41c226f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431260"
---
# <a name="how-to-add-an-updater-method"></a>如何：添加 Updater 方法
  可以让用户可以通过创建更新 SharePoint 外部列表中的业务数据*Updater*方法。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-an-updater-method"></a>若要创建 Updater 方法

1. 在 BDC 设计器中，选择实体。

2. 在菜单栏上依次选择**视图** > **其他 Windows** > **BDC 方法详细信息**。

    “BDC 方法详细信息”窗口将打开。 有关此窗口的详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**添加一个方法**列表中，选择**创建 Updater 方法**。

    Visual Studio 将以下元素添加到模型。 在 BDC 方法详细信息窗口中显示这些元素。

   - 名为的方法**更新**。

   - 方法的输入的参数。

   - 参数类型描述符。 默认情况下，Visual Studio 使用您定义的实体类型描述符为查找程序方法 (例如：请联系）。

   - 方法实例的方法。

     有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

   > [!NOTE]
   > 如果实体类型的标识符表示不会自动生成的数据库表中的字段，设置**Pre-updater 字段**属性设置为**True**。

4. 在中**解决方案资源管理器**，打开实体，已生成的服务代码文件的快捷菜单，然后选择**查看代码**。

    在中打开实体服务代码文件**代码编辑器**。 关于该文件的详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到要更新的数据的更新方法。 下面的示例更新 AdventureWorks 示例数据库中的联系人信息适用于 SQL Server。

   > [!NOTE]
   > 值替换为`ServerName`字段与服务器的名称。

    [!code-csharp[SP_BDC#5](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#5)]
    [!code-vb[SP_BDC#5](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#5)]

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
