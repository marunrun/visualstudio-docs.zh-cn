---
title: 如何：添加特定的 Finder 方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8fdd467f2b3a06398198f6fd8452c6a548bf0872
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431271"
---
# <a name="how-to-add-a-specific-finder-method"></a>如何：添加特定的 Finder 方法
  可以通过创建返回单个实体实例*特定的 Finder*方法。 在用户在业务数据 web 部件或外部列表中选择一个实体时，业务数据连接 (BDC) 服务将执行特定的 Finder 方法。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-specific-finder-method"></a>若要创建特定的 Finder 方法

1. 上**BDC 设计器**，选择实体。

    了解如何将实体添加到**BDC 设计器**在 Visual Studio 中，请参阅[如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上依次选择**视图** > **其他 Windows**， **BDC 方法详细信息**。

    **BDC 方法详细信息**窗口随即打开。 有关该窗口的详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**添加一个方法**列表中，选择**创建特定的 Finder 方法**。

    Visual Studio 将以下元素添加到模型。 这些元素出现在**BDC 方法详细信息**窗口。

   - 方法。

   - 方法的输入的参数。

   - 该方法是返回参数。

   - 每个参数类型描述符。

   - 方法实例的方法。

     有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 打开 Visual Studio**属性**窗口。

5. 将返回参数的类型描述符配置为实体类型描述符。 有关如何创建实体类型描述符的信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 您无需执行此步骤，如果为实体添加查找程序方法。 Visual Studio 使用查找程序方法中定义的类型描述符。

   > [!NOTE]
   > 如果实体类型的标识符字段表示自动生成的数据库表中的字段，设置**只读**属性的标识符字段**True**。

6. 在中**方法的详细信息**窗口中，选择方法实例的方法。

7. 在中**属性窗口**，请设置**返回参数名称**属性设置为该方法的返回参数的名称。 方法实例属性的详细信息，请参阅[MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282)。

8. 在中**解决方案资源管理器**，打开实体，已生成的服务代码文件的快捷菜单，然后选择**查看代码**。

    实体服务代码文件将在代码编辑器中打开。 有关实体服务代码文件的详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

9. 将代码添加到特定的 Finder 方法。 这段代码执行下列任务：

   - 从数据源中检索一条记录。

   - 向 BDC 服务返回的实体。

     下面的示例适用于 SQL Server 返回 AdventureWorks 示例数据库中的联系人。

     > [!NOTE]
     > 值替换为`ServerName`字段与服务器的名称。

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
