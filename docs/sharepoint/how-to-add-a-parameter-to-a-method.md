---
title: 如何：将参数添加到方法 |Microsoft Docs
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
ms.openlocfilehash: a5b76e49285a629234557a973f6d4b45703f1cfd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967229"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>如何：将参数添加到方法
  若要将信息传递到方法或从方法返回的信息，请使用参数。 所有方法必须都具有至少一个参数。 有关如何设计用于支持你想要创建的方法的类型的参数的详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 在将参数添加到方法中，Visual Studio 将添加到你的项目中的模型文件的 XML 参数元素。 Parameter 元素的属性的详细信息，请参阅[参数](http://go.microsoft.com/fwlink/?LinkId=169284)。

### <a name="to-add-a-parameter-to-a-method"></a>向方法添加参数

1. 将方法添加到实体。

2. 在菜单栏上依次选择**视图** > **其他 Windows** > **BDC 方法详细信息**。

     **BDC 方法详细信息**窗口随即打开。 有关详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在中**BDC 方法详细信息**窗口中，展开该方法的节点，然后展开**参数**节点。

4. 在中**添加一个参数**列表中，选择**创建参数**。

     下一个新的参数会显示**参数**节点。

5. 在菜单栏上依次选择**视图** > **属性窗口**。

6. 在中**属性**窗口中，将**名称**属性设置为任何有意义的名称。 例如，如果该方法将返回客户，你可能会将该方法**GetCustomers**。

7. 在中**BDC 方法详细信息**窗口中，打开为参数的方向显示的列表，然后选择**中**， **InOut**，**出**，或**返回**。

     若要为你创建的类型方法选择哪个方向的详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

8. 修改该参数的类型描述符。 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

## <a name="see-also"></a>请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
