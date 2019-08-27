---
title: 如何：添加 Creator 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], Creator
- BDC [SharePoint development in Visual Studio], adding entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entity instances
- BDC [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Creator
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38312384c3e6ce51aa1b5b0b16df378286fc58b0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443579"
---
# <a name="how-to-add-a-creator-method"></a>如何：添加 Creator 方法
  创建者方法将新数据添加到的数据源的实体。 业务数据连接 (BDC) 服务调用此方法时用户选择**新项**按钮**功能区**的基于模型的列表。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-add-a-creator-method"></a>若要添加 Creator 方法

1. 上**BDC 设计器**，选择实体。

2. 在菜单栏上依次选择**视图** > **其他 Windows** >**BDC 方法详细信息**。

    **BDC 方法详细信息**窗口随即打开。 有关该窗口的详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**添加一个方法**列表中，选择**创建 Creator 方法**。

    Visual Studio 将以下元素添加到模型中，并且这些元素出现在**BDC 方法详细信息**窗口。

   - 一个名为方法**创建**。

   - 方法的输入的参数。

   - 该方法是返回参数。

   - 类型描述符的参数。

   - 方法实例的方法。

     有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 在中**解决方案资源管理器**，打开实体，已生成的服务代码文件的快捷菜单，然后选择**查看代码**。

    实体服务代码文件将在代码编辑器中打开。 有关实体服务代码文件的详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到将数据添加到数据源的创建者方法。 下面的示例适用于 SQL Server 将联系人添加到 AdventureWorks 示例数据库。

   > [!NOTE]
   > 值替换为`ServerName`字段与服务器的名称。

    [!code-csharp[SP_BDC#4](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#4)]
    [!code-vb[SP_BDC#4](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#4)]

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
