---
title: 如何：向方法添加参数 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb1a1c1e8f11ac6daa46f9fe1468a1ff3509e135
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72986236"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>如何：向方法添加参数
  使用参数将信息传递到方法或从方法返回信息。 所有方法都必须至少有一个参数。 有关如何设计参数来支持要创建的方法类型的详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 向方法添加参数时，Visual Studio 会将 Parameter 元素添加到项目中模型文件的 XML。 有关参数元素的特性的详细信息，请参阅[参数](/previous-versions/office/developer/sharepoint-2010/ee557705(v=office.14))。

### <a name="to-add-a-parameter-to-a-method"></a>向方法添加参数

1. 向实体添加方法。

2. 在菜单栏上，选择 "**查看** > **其他 Windows** > **BDC 方法详细信息**"。

     此时将打开 " **BDC 方法详细信息**" 窗口。 有关详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 " **BDC 方法详细信息**" 窗口中，展开方法的节点，然后展开 "**参数**" 节点。

4. 在 "**添加参数**" 列表中，选择 "**创建参数**"。

     新参数将出现在 "**参数**" 节点下。

5. 在菜单栏上，选择 "**查看** > **属性" 窗口**。

6. 在 "**属性**" 窗口中，将 "**名称**" 属性设置为任何有意义的名称。 例如，如果该方法将返回 customers，则可以将该方法命名为**GetCustomers**。

7. 在 " **BDC 方法详细信息**" 窗口中，打开为参数方向显示的列表，然后选择 " **In** **"、"输入**"、" **Out**" 或 " **Return**"。

     有关为要创建的类型方法选择哪个方向的详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

8. 修改参数的类型描述符。 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

## <a name="see-also"></a>请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
