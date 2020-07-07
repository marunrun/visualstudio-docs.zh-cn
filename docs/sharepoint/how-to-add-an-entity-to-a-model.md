---
title: 如何：向模型添加实体 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- EntityTool
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], entity
- Business Data Connectivity service [SharePoint development in Visual Studio], adding an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], entity
- BDC [SharePoint development in Visual Studio], adding an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b80f39494b98014a75d4265f228906be2ff45188
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016672"
---
# <a name="how-to-add-an-entity-to-a-model"></a>如何：向模型添加实体
  若要创建实体，请将 Visual Studio**工具箱**中的实体控件添加到业务数据连接（BDC）设计器。

### <a name="to-add-an-entity-to-the-model"></a>向模型添加实体

1. 创建 BDC 项目，或打开现有的 BDC 项目。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

2. 在 "**工具箱**" 的 " **BusinessDataCatalog** " 组中，将 "**实体**" 控件添加到设计器上。

     新实体将显示在设计器上。 Visual Studio 将一个 `<Entity>` 元素添加到项目中 BDC 模型文件的 XML 中。 有关实体元素特性的详细信息，请参阅[entity](/previous-versions/office/developer/sharepoint-2010/ee558325(v=office.14))。

3. 在设计器中，打开实体的快捷菜单，选择 "**添加**"，然后选择 "**标识符**"。

     实体上将显示一个新的标识符。

    > [!NOTE]
    > 您可以在 "**属性**" 窗口中更改实体的名称和标识符。

4. 在类中定义实体的字段。 您可以将新类添加到项目中，也可以使用通过使用其他工具（如对象关系设计器（O/R 设计器）创建的现有类。 下面的示例演示一个名为 Contact 的实体类。

     [!code-csharp[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs#1)]
     [!code-vb[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb#1)]

## <a name="see-also"></a>另请参阅
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
